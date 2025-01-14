---
title: States
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

States in Botpress provide a way to store and manage conversational context within a chatbot integration. They are used to remember the status of various conversations and users interacting with the bot, which helps create a more fluid and personalized user experience. State data can include details such as the current point in a conversation, the user's previous interactions, or any other information that needs to be stored temporarily for the ongoing conversation. This allows the bot to respond appropriately based on the context of the conversation.

The state is defined within the `states` object in your integration.

> 📘 States Concept
>
> You can find more about the [States Concept](../docs/states-1) here.

# State Definition

The state definition includes `type` and `schema`:

* `type`: It indicates the scope of the state. It could be 'integration' for global scope, 'conversation' for conversation-level scope or 'user' for user-level scope.

* `schema`: This uses the Zod library to define the structure and type of the state data. It represents the data that the state will hold.

<br />

# Examples

## Shopify Webhook ID State

Here's an example of state definition from a Shopify integration. This state holds a webhook ID that is created during the configuration of the integration and can be used later when the integration is disabled to remove the webhook:

```javascript
states = {
  configuration: {
    type: 'integration',
    schema: z.object({
      webhookId: z.string().optional()
    }),
  },
}
```

## LINE Reply Token State

In the case of a LINE integration, a "reply token" needs to be kept to use when replying back to the user. The state is defined at the conversation level:

```javascript
states: {
  conversation: {
    type: 'conversation',
    schema: z.object({
      replyToken: z.string(),
    }),
  },
},
```

These examples show how states can be used to store crucial data at different scopes for various purposes, enabling chatbot integrations to manage context and respond appropriately.

## GitHub Webhook Configuration State

In a GitHub integration, the state is defined at the integration level to store the webhook secret, the webhook ID, and the bot user ID. These pieces of data are important to establish and manage the integration with GitHub. The state can be defined as follows:

```javascript
states = {
  configuration: {
    type: 'integration',
    schema: z.object({
      webhookSecret: z.string().optional(),
      webhookId: z.number().optional(),
      botUserId: z.number().optional(),
    }),
  },
}
```
