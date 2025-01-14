---
title: Event
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
Events represent interactions or changes of state within the external platform that may not directly involve a message exchange in a conversation. These could include a variety of activities such as when a user opens the chat in WhatsApp, when a new issue is created in Linear, a member joining a group in Telegram, and so on.

These events may still be of importance to your chatbot and may be used to trigger specific flows or actions in response.

The **events** section of your integration is where you define how your chatbot handles these non-conversational events. The methods for implementing these handlers will depend on the APIs and capabilities provided by the external platform.

# Example - Events

Here's a general outline of what event handling might look like in your integration:

```javascript
const integration = {
  // ...

  events: {
    'issue.created': async (ctx, event) => {
      // An event handler for when a new issue is created in Linear
      // The event parameter contains information about the event
      // Use this to update your bot's state, trigger flows, etc.
    },

    'chat.opened': async (ctx, event) => {
      // An event handler for when a chat is opened in WhatsApp
      // The event parameter contains information about the event
      // Use this to update your bot's state, trigger flows, etc.
    },

    // Add more event handlers as needed
  },

  // ...
}
```

In the above example, the **issue.created** and **chat.opened** events represent hypothetical events for the Linear and WhatsApp platforms.

Your task as a developer is to understand what events are available on the external platform you're integrating with, and then implement handlers for the events that are relevant to your chatbot.
