---
title: Channels
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
In the context of chatbot integrations, **channels** represent the different types of communication mediums within the integrated platform.

These might correspond to different features offered by the platform such as group chats, direct messages, threads, etc. Each of these communication mediums has a corresponding **channel** in the integration.

In the case of the Telegram integration code provided, a **channel** named **group** is defined. This is used to send messages to specific group channels within the Telegram system.

Each **channel** defined in the integration must be supported by the chatbot, as it's through these channels that the bot will send and receive messages.

Here's how it works:

# Defining Channels

The channels that an integration supports are defined in the **channels** object. Each key within this object corresponds to a supported channel.

In our Telegram example, we've defined a single channel, **group**, to send messages to a group chat in Telegram.

<br />

# Message Types

Each channel has a **messages** property, which is used to specify the types of messages that can be sent and received through that channel. Currently, we've implemented only **text** messages, but this can be expanded to include other message types as needed.

<br />

# Default Messages

The **defaults** object, which is part of the SDK, specifies the default types of messages that the integration should support. For a comprehensive integration, it's highly recommended to implement support for all the message types defined in the **defaults** object.

This ensures that the integration can handle the full range of interactions that the chatbot might need to support.

For example, in a Slack integration, you could define channels such as **channel**, **direct message**, and **thread**. Each of these would correspond to a different type of interaction in Slack - messages within a channel, direct messages between users, and threaded conversations, respectively.

Keep in mind that the channels and message types you define will depend on the features provided by the platform you're integrating with. The goal is to map the platform's features to corresponding channels and message types within the chatbot integration, thus ensuring seamless interaction between the chatbot and the platform.

<br />

# Example - Channels

```javascript
const integration = {
  // ...
  channels: {
    group: {
      messages: {
        text: {
          defaults: {
            title: 'Default title',
            body: 'Default body',
          },
          factory: ({ title, body }) => {
            return { title, body }
          },
        },
      },
    },
  },
  // ...
}
```

In this example, the **channels** object contains a **group** object that represents a **group chat** on Telegram.

Inside the **group** object, there's a **messages** object that lists the types of messages that this channel can handle, in this case, text messages.

Each message type has a **default** object and a **factory function**. The default object specifies the default values for this message type, which can be used when the specific message doesn't provide these fields.

The **factory function** is a function that takes an object with properties for this message type and returns a new object that will be used as the actual message.

Again, the exact structure of the channel object can vary based on the platform you're integrating with. Always refer to the platform's API documentation to understand how channels should be implemented.
