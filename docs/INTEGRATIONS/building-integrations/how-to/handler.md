---
title: Handler
excerpt: Handler Function Documentation
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Introduction

The handler function is a critical part of your Botpress integration. It acts as a processing and distribution point for any information, packets, messages, or payloads coming from the integration point (such as Slack, Messenger, WhatsApp, etc.). 

The handler function serves several key roles:

1. **Message processing**: It processes incoming messages and transforms them into a format Botpress understands.

2. **Event firing**: It is where events get fired.

3. **Verification**: It processes the verification requirements.

In essence, the handler function ensures that data from external platforms is appropriately processed and directed to perform its intended functions within your Botpress chatbot.

<br />

# Sample Handler Function Implementation - GitHub

Below is a sample handler function implemented for GitHub integration:

```javascript
import { verify as verifyWebhook } from '@octokit/webhooks-methods'
import type { WebhookEvent } from '@octokit/webhooks-types'

import { GITHUB_SIGNATURE_HEADER } from './const'
import { fireIssueOpened } from './events/issue-opened'
import { firePullRequestCommentCreated } from './events/pull-request-comment-created'
import { firePullRequesMerged } from './events/pull-request-merged'
import { firePullRequestOpened } from './events/pull-request-opened'
import {
  isIssueOpenedEvent,
  isPingEvent,
  isPullRequestCommentCreatedEvent,
  isPullRequestMergedEvent,
  isPullRequestOpenedEvent,
} from './misc/guards'

import * as botpress from '.botpress'

export const handler: botpress.IntegrationProps['handler'] = async ({ req, client, ctx }) => {
  const signature = req.headers[GITHUB_SIGNATURE_HEADER]
  const { body } = req
  if (!(body && signature)) {
    return console.warn('Body or signature is missing')
  }

  const { state } = await client.getState({
    type: 'integration',
    name: 'configuration',
    id: ctx.integrationId,
  })

  if (!(await verifyWebhook(state.payload.webhookSecret, body, signature))) {
    return console.warn('Invalid webhook secret', state.payload.webhookSecret, signature)
  }

  const rawEvent: WebhookEvent = JSON.parse(body)
  if (isPingEvent(rawEvent)) {
    return
  }

  const event: WebhookEvent = rawEvent

  // ============ EVENTS ==============
  if (isPullRequestOpenedEvent(event)) {
    return firePullRequestOpened({ githubEvent: event, client })
  } else if (isPullRequestMergedEvent(event)) {
    return firePullRequesMerged({ githubEvent: event, client })
  } else if (isIssueOpenedEvent(event)) {
    return fireIssueOpened({ githubEvent: event, client })
  }

  // ============ MESSAGES ==============
  if (isPullRequestCommentCreatedEvent(event)) {
    return firePullRequestCommentCreated({ githubEvent: event, client })
  }

  console.warn('Unsupported github event')
}
```

In this sample, the handler function is responsible for tasks like verifying the incoming webhook request, determining the type of event, firing the appropriate event or processing messages, and logging warnings for unsupported events. This illustrates how the handler function acts as a crucial node in the communication between an external service (GitHub, in this case) and the Botpress chatbot.

<br />

# Sample Handler Function Implementation - Slack

Below is a sample handler function implemented for Slack integration:

```javascript
import type { GenericMessageEvent, ReactionAddedEvent } from '@slack/bolt'

import { executeMessageReceived } from './events/message-received'
import { executeReactionAdded } from './events/reaction-added'
import {
  isInteractiveRequest,
  onOAuth,
  parseInteractiveBody,
  respondInteractive,
  getUserAndConversation,
  getConfig,
} from './misc/utils'

import * as botpress from '.botpress'

export const handler: botpress.IntegrationProps['handler'] = async ({ req, ctx, client }) => {
  if (req.path.startsWith('/oauth')) {
    return onOAuth()
  }

  if (!req.body) {
    console.warn('Handler received an empty body')
    return
  }

  const { botUserId } = await getConfig(client, ctx)

  if (isInteractiveRequest(req)) {
    const body = parseInteractiveBody(req)
    const actionValue = await respondInteractive(body)

    if (body.type !== 'block_actions') {
      throw Error(`Interaction type ${body.type} is not supported yet`)
    }

    await client.createMessage({
      tags: { ts: body.message.ts },
      type: 'text',
      payload: { text: actionValue },
      ...(await getUserAndConversation({ slackUserId: body.user.id, slackChannelId: body.channel.id }, client)),
    })

    return
  }

  const data = JSON.parse(req.body)

  if (data.type === 'url_verification') {
    console.info('Handler received request of type url_verification')
    return {
      body: JSON.stringify({ challenge: data.challenge }),
    }
  }

  const event: ReactionAddedEvent | GenericMessageEvent = data.event
  console.info(`Handler received request of type ${data.event.type}`)

  switch (event.type) {
    case 'message':
      return executeMessageReceived({ slackEvent: event, client })

    case 'reaction_added':
      if (event.user !== botUserId) {
        return executeReactionAdded({ slackEvent: event, client })
      }

      return

    default:
      return
  }
}
```

In this handler function implementation, it handles a variety of tasks like OAuth requests, parsing and responding to interactive requests, handling different types of events ('message' and 'reaction\_added'), as well as dealing with a 'url\_verification' type event. It demonstrates the handler's ability to manage diverse tasks and flow control in the context of a Slack integration.
