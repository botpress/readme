---
title: Tags
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
Tags in chatbot integrations serve as unique identifiers or markers to associate specific data and information with users, conversations, or messages.

Tags can be used to extend the functionality of chatbot integrations and provide additional context to the data.

For example in the Slack Integration [Source Code](https://github.com/botpress/botpress/blob/master/integrations/slack/src/index.ts), we make use of tags extensively to map users, conversations, and messages between the chatbot system and the Slack system.

The particular tag used is **slack:id**, which is applied to the user, conversation, and message instances within the chatbot.

Here's how it works:

# User Tags

User tags are used to identify users in the system uniquely. The tag named **slack:id** is applied to each user, associating the user's unique ID within Slack with the user instance in the chatbot system.

This allows the integration to seamlessly map and interact with the corresponding user in Slack.

<br />

# Conversation Tags

Like user tags, conversation tags help in distinguishing and identifying unique conversations.

The **slack:id** tag is attached to each conversation, linking the conversation within the chatbot system to its corresponding conversation in Slack.

<br />

# Message Tags

Message tags are employed to keep track of individual messages within a conversation. In the Slack integration code, the **slack:id** tag is used to mark messages with the timestamp ('ts') of the message in Slack, enabling the chatbot system to associate messages between the two platforms.

By using tags in this way, the integration is able to identify and map users, conversations, and messages between the chatbot system and Slack, allowing it to manage interactions smoothly across platforms.

Just to remind you, the value you choose for your tag will depend on the integration you're building.

For instance, in our example, we used **slack:id** because we're integrating with **Slack**. If you were integrating with **Telegram**, you might use **telegram:id** instead.

For instance, in the Telegram integration, we added a tag named **id** to the users, conversations, and messages. These tags facilitate the identification of these entities within the Telegram system.

<br />

# Example - Tags

Here's a sample code snippet that illustrates this:

```javascript
const integration = {
  // ...
  tags: {
    user: ['id'],
    conversation: ['id'],
    message: ['id'],
  },
  // ...
}
```

In this example, the **tags** object contains three categories: **user**, **conversation**, and **message**. Each category has been tagged with **id**, which serves as an identifier in the Telegram system.

The **id** is a unique attribute for each category, allowing the system to track individual users, conversations, and messages. When developing your integration, you'll use similar tags to keep track of your entities based on the platform's requirements.

Keep in mind that the nature and number of tags might vary depending on the platform you're integrating with. It's important to understand the platform's data structures and to define your tags accordingly.
