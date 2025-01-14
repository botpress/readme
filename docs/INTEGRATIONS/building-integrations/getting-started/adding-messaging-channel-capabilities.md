---
title: Adding Messaging Channel Capabilities
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
You can use an integration to add any messaging channel to your bot, such as Line, Facebook Messenger, or Instagram.

In this tutorial, we'll extend your existing integration to send and receive text messages to Telegram. We'll also create a bot to test it out. You can follow the instructions below or follow along the video.

<Embed url="https://www.youtube.com/embed/Z6LAwWq1gOM" title="Adding Channels functionality" favicon="https://www.youtube.com/favicon.ico" image="https://i.ytimg.com/vi/Z6LAwWq1gOM/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/embed/Z6LAwWq1gOM" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FZ6LAwWq1gOM%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DZ6LAwWq1gOM%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FZ6LAwWq1gOM%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22640%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

# Modify the Integration Definition

First, let's add the necessary configuration to your existing your integration definition, so your users will be able to use Telegram to connect to their own channel.

## Step 1: Add Telegram Configuration

Add the following configuration schema to you `integration.definition.ts`:

```ts
// integration.definition.ts
import { IntegrationDefinition, z } from '@botpress/sdk' // import the zod library like this

export default new IntegrationDefinition({
  // ...existing properties
  configuration: {
    schema: z.object({
      botToken: z.string(), // users of your integration will provide this token to connect to their Telegram bot
    }),
  },
  // ...existing properties
})
```

The configuration schema is used to validate the integration's configuration and ask users to provide information when adding the integration to their bot. In this case, we are adding a `botToken` which will store the Telegram Bot API token.

## Step 2: Define Telegram Channels and Tags

Next update the `channels` and `user` properties to support Telegram-specific functionality:

```ts
// integration.definition.ts
export default new IntegrationDefinition({
  // ...existing properties
  channels: {
    group: {
      // messages: messages.defaults,  // use this to support all message types supported in Botpress Studio
      messages: {
        text: messages.defaults.text, // For our example, we'll specify text messages only
      },
      message: {
        tags: {
          id: {}, // Add this line to tag messages
        },
      },
      conversation: {
        tags: {
          id: {}, // Add this line to tag conversations
        },
      },
    },
  },
  user: {
    tags: {
      id: {}, // Add this line to tag users
    },
  },
  // ...existing properties
})
```

The `channels` property defines the communication channels your integration supports. Here, we define a `group` channel to send messages to a specific group in Telegram. The `messages` property, on the other hand, defines the message types that this channel support. We set it to `messages.defaults.text`, for it to support `text` messages in the Botpress Studio. Tags are used to identify users, conversations, and messages within the Telegram system.

<br />

# Add the Integration Logic

Now that we've handled all the definitions, let's handle the logic that allows messages to flow to / from Botpress and Telegram.\
We'll use the Telegraf library to manage calls to the Telegram API.

Let's install it:

```bash
npm i telegraf
```

## Step 3: Register and Unregister Webhooks

Update your `src/index.ts` to manage the lifecycle of the integration:

```ts
// src/index.ts
import { Telegraf } from 'telegraf'
import { Integration, RuntimeError } from '@botpress/sdk' // import the RuntimeError class

export default new Integration({
  // ...existing properties
  register: async ({ webhookUrl, ctx }) => {
    const telegraf = new Telegraf(ctx.configuration.botToken)
    try {
      await telegraf.telegram.setWebhook(webhookUrl)
    } catch (error) {
      throw new RuntimeError(
        'Configuration Error! The Telegram bot token is not set. Please set it in your bot integration configuration.'
      )
    }
  },
  unregister: async ({ ctx }) => {
    const telegraf = new Telegraf(ctx.configuration.botToken)
    await telegraf.telegram.deleteWebhook({ drop_pending_updates: true })
  },
  // ...existing properties
})
```

The `register` function sets up the webhook for Telegram when the integration is added to a bot. The `unregister` function removes the webhook when the integration is removed from a bot. These functions also validate the configuration.

If the configuration is invalid, a `RuntimeError` is thrown, which will be displayed to the user in the Bot's Integration configuration page.

## Step 4: Handle Incoming Messages

Add the handler function to process incoming messages from Telegram:

```ts
// src/index.ts
export default new Integration({
  // ...existing properties
  handler: async ({ req, client }) => {
    const data = JSON.parse(req.body)

    const conversationId = data?.message?.chat?.id
    const userId = data?.message?.from?.id
    const messageId = data?.message?.message_id

    if (!conversationId || !userId || !messageId) {
      return {
        status: 400,
        body: "Handler didn't receive a valid message",
      }
    }

    const { conversation } = await client.getOrCreateConversation({
      channel: 'group',
      tags: { 'id': `${conversationId}` },
    })

    const { user } = await client.getOrCreateUser({
      tags: { 'id': `${userId}` },
    })

    await client.createMessage({
      tags: { 'id': `${messageId}` },
      type: 'text',
      userId: user.id,
      conversationId: conversation.id,
      payload: { text: data.message.text },
    })
  },
  // ...existing properties
})
```

The `handler` function processes incoming requests from Telegram. It extracts the conversation ID, user ID, and message ID, then creates or retrieves the conversation, user, and message using the client parameter. Finally, it creates a message in the conversation, which will be sent to the bot as an incoming message from Telegram.

## Step 5: Send Messages to Telegram

Implement the `text` message type in the `group` channel:

```ts
// src/index.ts
export default new Integration({
  // ...existing properties
  channels: {
    group: {
      messages: {
        text: async ({ payload, ctx, conversation, ack }) => {
          const client = new Telegraf(ctx.configuration.botToken)
          const message = await client.telegram.sendMessage(conversation.tags['id']!, payload.text)
          await ack({ tags: { 'id': `${message.message_id}` } })
        },
      },
    },
  },
  // ...existing properties
})
```

The `channels` object implements the `group` channel we defined earlier. The `text` message type sends a text message to the specified Telegram group. This function is called every time the bot sends a text message to the `group` channel.

<br />

# Try it Out

Before trying it out, make sure you either run `npm run deploy` or `npm run start` to deploy the changes to your Botpress Cloud workspace.

1. Send a message to [the BotFather](https://telegram.me/BotFather) on Telegram and create a new bot. It will provide you with a token.
2. Go to [your Botpress Cloud workspace](https://app.botpress.cloud/workspaces/).
3. Click your bot's name.
4. Click on "Integrations" in the sidebar.
5. Click your integration name.
6. Add your Telegram Bot API token in the configuration in the input.
7. Make sure the integration is enabled.
8. Hit "Save".
9. Open your bot in Telegram and chat with it!

Congratulations! You've just added Telegram chat capabilities to your bot. Now, you can use this integration in any bot that you create in this workspace.

Next up, we'll add action cards and external triggers to your integration.
