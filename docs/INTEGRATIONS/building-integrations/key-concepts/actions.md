---
title: Actions
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
Actions refer to the tasks that your chatbot can perform on a specific platform, beyond sending and receiving messages. They provide a way for your bot to interact with the channel, such as by adding a reaction to a message on Slack or initiating a conversation on Telegram. The methods for implementing these actions will depend on the capabilities provided by the external platform.

Actions are defined within the actions object of your integration and can be invoked from your conversation flows in Botpress using the actions service.

Here's how you might document the **addReaction** action for a Slack integration:

# addReaction

This action allows the bot to add a reaction (emoji) to a specific message in a Slack conversation. It can be used to acknowledge a user's message, show approval, or convey any other sentiment that can be represented by an emoji.\
In the implementation, this function should make a request to the Slack API to add the specified reaction to the message. The function accepts the context **ctx**, a **conversationId** and **messageId** to identify the message to react to, and a reaction parameter specifying the emoji to use.

Here's a simple example of what the addReaction action might look like in your Slack integration:

```javascript
const integration = {
  // ...
  actions: {
    addReaction: async (ctx, conversationId, messageId, reaction) => {
      // Retrieve the bot token and channel ID from the conversation context
      const token = ctx.config.botToken
      const channelId = ctx.mapping[conversationId]

      // Use the `reactions.add` method of the Slack API to add the reaction
      const result = await ctx.client.reactions.add({
        token,
        channel: channelId,
        name: reaction,
        timestamp: messageId,
      })

      if (!result.ok) {
        // Handle the error
      }
    },
  },
  // ...
}
```

In this example, **ctx.client.reactions.add** represents a call to the **reactions.add** method of the Slack API. The function needs to handle potential errors, such as if the specified reaction doesn't exist, the message is not found, or the bot doesn't have permission to add reactions.
