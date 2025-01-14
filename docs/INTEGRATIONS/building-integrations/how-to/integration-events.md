---
title: Integration Events
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
# Introduction

Integration Events in Botpress are mechanisms that capture various interactions or changes of state within an external platform, irrespective of whether they directly involve a conversation or message exchange. For example, a user opening the chat window on WhatsApp, creation of a new issue in Linear, a member joining a group in Telegram, among others, can be perceived as Integration Events.

These events can be instrumental for your chatbot, enabling it to trigger specific actions or flows in response. The area in your integration where you define the chatbot's reaction to these non-conversational events is referred to as the events section. The techniques you employ to set up these handlers largely depend on the APIs and capabilities that the external platform provides.

# Event Definition

An event definition is comprised of the event type and a schema. We utilize the Zod library for defining these schemas. More information about Zod can be found here.

## Example:

Here's an illustration of how to define a new order event for Shopify:

```javascript
import { IntegrationDefinitionProps } from '@botpress/sdk'
import z from 'zod'

import { INTEGRATION_NAME } from '../const'

export type NewOrderCreated = z.infer<typeof newOrderCreated.schema>

const newOrderCreated = {
  schema: z.object({
    type: z.literal(`${INTEGRATION_NAME}:newOrderCreated`).optional(),
    order_id: z.number(),
    shopName: z.string(),
    confirmation_number: z.string(),
    created_at: z.string(),
    currency: z.string().optional(),
    current_subtotal_price: z.string().optional(),
    current_total_discounts: z.string().optional(),
    current_total_price: z.string().optional(),
    current_total_tax: z.string().optional(),
    customer_locale: z.string().optional(),
    order_status_url: z.string().optional(),
    fullBody: z.object({}).passthrough(),
  }),
  ui: {},
}

export const events = {
  newOrderCreated,
} satisfies IntegrationDefinitionProps['events']
```

<br />

# Event Implementation

This refers to the actual code segment that contains the implementation of the action in the integration. The parameters that are passed to the implementation function include but are not limited to `ctx` (context), `input` (user-provided inputs in the fields defined in the UI section in the definition), `logger` (useful for logging information to the bot logs), and `client` (Botpress API Client).

## Example:

Here's an example of how you might implement the NewOrderCreated event in Shopify:

```javascript
import { Client, Context } from '@botpress/client'

export const fireNewOrderCreated = async ({
  req,
  client,
  ctx,
  logger,
}: {
  req: any
  client: Client
  ctx: Context
  logger: any
}) => {
  const shopifyEvent = JSON.parse(req.body)

  const payload = {
    order_id: shopifyEvent.id,
    shopName: ctx.configuration.shopName,
    confirmation_number: shopifyEvent.confirmation_number,
    created_at: shopifyEvent.created_at,
    currency: shopifyEvent.currency,
    current_subtotal_price: shopifyEvent.current_subtotal_price,
    current_total_discounts: shopifyEvent.current_total_discounts,
    current_total_price: shopifyEvent.current_total_price,
    current_total_tax: shopifyEvent.current_total_tax,
    customer_locale: shopifyEvent.customer_locale,
    order_status_url: shopifyEvent.order_status_url,
    fullBody: req,
  }

  await client.createEvent({
    type: 'newOrderCreated',
    payload,
  })
}
```

<br />

# Event Firing

In the handler, you can invoke the event just like any other function, and you can pass to it the required parameters.

## Example:

Here's an example of how to call the NewOrderCreated event in Shopify:

```javascript
import * as botpress from '.botpress'
import { fireNewOrderCreated } from './events/newOrderCreated'
export const handler: botpress.IntegrationProps['handler'] = async ({ req, client, ctx, logger }) => {
  if ((req.headers['x-shopify-topic'] = 'orders/create')) return fireNewOrderCreated({ req, client, ctx, logger })
}
```
