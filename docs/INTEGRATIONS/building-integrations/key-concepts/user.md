---
title: User
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
Users are essential components of chatbot integrations. They represent the individuals interacting with your bot via the integration platform.

It's crucial to correctly establish the mapping between the integration's users and the users in Botpress.

The two key parts involved in user handling within the integration are:

# getOrCreateUser

This function is used to retrieve an existing user or create a new one if the user doesn't already exist. It's a handy way to ensure that the user you're interacting with is always represented in your system. This function typically takes in an identifier from the incoming message and fetches or creates a corresponding user in Botpress.

<br />

# createUser

This function is responsible for creating a new user. It typically accepts parameters that represent the user's details, and then uses these details to create a user object in Botpress.

<br />

# Example - Slack Integration

Here's a sample code snippet showing how these parts could be implemented in a **Slack** integration:

```javascript
createUser: async ({ client, tags, ctx }) => {
  const userId = tags['slack:id']

  if (!userId) {
    return
  }

  const slack = new WebClient(ctx.configuration.botToken)
  const member = await slack.users.info({ user: userId })

  if (!member.user?.id) {
    return
  }

  const { user } = await client.getOrCreateUser({ tags: { 'slack:id': `${member.user?.id}` } })

  return {
    body: JSON.stringify({ user: { id: user.id } }),
    headers: {},
    statusCode: 200,
  }
}
```

<br />

# Messages

Messages are the fundamental building blocks of any conversation. They carry the content that is exchanged between users and the bot during a conversation. In the context of a chatbot integration, understanding and properly handling messages is essential for maintaining a coherent dialogue.\
In your integration, the messages object plays a critical role in managing the communication flow between the chatbot and the external platform. It provides methods for sending, receiving, and processing messages.

Here are key methods typically found under the messages object:

<br />

# sendMessage

This function is responsible for sending a message from the bot to the external platform.

<br />

# processIncomingMessage

This function is responsible for processing incoming messages from the external platform, making them understandable by Botpress.

<br />

# processOutgoingMessage

This function takes care of converting the outgoing message from Botpress into a format that can be understood by the external platform.

<br />

# Example - Telegram

Here's a basic example of how these functions might look in a **Telegram** integration:

```javascript
const integration = {
  // ...
  messages: {
    sendMessage: async (ctx, conversationId, message) => {
      // Implement logic to send message to the external platform
      // using its API
    },
    processIncomingMessage: async (ctx, incomingMessage) => {
      // Implement logic to convert incoming message from external platform
      // into Botpress understandable format
    },
    processOutgoingMessage: async (ctx, outgoingMessage) => {
      // Implement logic to convert outgoing message from Botpress
      // into the format understood by the external platform
    },
  },
  // ...
}
```

In this example, each method accepts the context **ctx**, which is used for storing and retrieving application-level data.

**sendMessage** also accepts a **conversationId** and a **message**,\
**processIncomingMessage** accepts an **incomingMessage**, and **processOutgoingMessage** accepts an **outgoingMessage**.
