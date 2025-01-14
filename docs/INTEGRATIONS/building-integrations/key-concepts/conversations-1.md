---
title: Conversations
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
Conversations are a crucial part of any chatbot integration. They define the ongoing dialogues between users and the bot across various channels. Proper mapping of conversations is essential to ensure seamless interactions and maintain context.

The two key aspects of handling conversations within an integration are:

# getOrCreateConversation

This function retrieves an existing conversation or creates a new one if the conversation doesn't already exist. Similar to user handling, it helps maintain the connection between an external channel and Botpress.

# createConversation

This function is responsible for creating a new conversation in Botpress. It typically accepts parameters that represent the conversation details and uses these details to establish a new conversation object in Botpress.

# Example - Telegram Integration

Let's consider a sample code snippet to illustrate these concepts in a Telegram integration:

```javascript
const integration = {
  // ...
  conversations: {
    getOrCreateConversation: async (ctx, telegramConversationId) => {
      // Check if the conversation exists in the Botpress system
      let conversation = await ctx.bp.conversations.getById(telegramConversationId)
      if (!conversation) {
        // If not, create a new conversation
        conversation = await integration.conversations.createConversation(ctx, telegramConversationId)
      }
      return conversation
    },
    createConversation: async (ctx, telegramConversationId) => {
      // Define conversation fields
      const conversationFields = {
        id: telegramConversationId,
        platform: 'telegram',
        // Other fields like 'userId' can be added as per the platform's conversation object
      }
      // Create conversation in the Botpress system
      const conversation = await ctx.bp.conversations.create(conversationFields)
      return conversation
    },
  },
  // ...
}
```

In this example, **getOrCreateConversation** and **createConversation** are defined inside the conversations object of the integration. Both functions utilize the context ctx and the telegramConversationId which is a unique identifier for the conversation on the Telegram platform.
