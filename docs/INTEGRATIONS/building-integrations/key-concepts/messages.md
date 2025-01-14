---
title: Messages
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
Messages are the fundamental building blocks of any conversation. They carry the content that is exchanged between users and the bot during a conversation. In the context of a chatbot integration, understanding and properly handling messages is essential for maintaining a coherent dialogue.

In your integration, the messages object plays a critical role in managing the communication flow between the chatbot and the external platform. It provides methods for sending, receiving, and processing messages.\
Here are key methods typically found under the messages object:

# sendMessage

This function is responsible for sending a message from the bot to the external platform.

<br />

# processIncomingMessage

This function is responsible for processing incoming messages from the external platform, making them understandable by Botpress.

<br />

# processOutgoingMessage

This function takes care of converting the outgoing message from Botpress into a format that can be understood by the external platform.\
Here's a basic example of how these functions might look in a Telegram integration:

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

In this example, each method accepts the context **ctx**, which is used for storing and retrieving application-level data. **sendMessage** also accepts a **conversationId** and a **message**, **processIncomingMessage** accepts an **incomingMessage**, and **processOutgoingMessage** accepts an **outgoingMessage**.
