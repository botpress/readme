---
title: Events
excerpt: Custom actions based on different states and interactions in the conversation.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The cards in the Events category allow you to interact with your bot based on different states and interactions within the chat platform.

# What are Events?

Events represent interactions or changes of state within the chat platform. These might not directly involve a message exchange in a conversation, but they capture a variety of activities. For instance, it could be when a user opens the chat in WhatsApp, when a new issue is created in Linear, or a member joining a group in Telegram.

# Fixed Schedule

Fixed Schedule is a feature that allows you to schedule events to occur at specific times. This can be useful for sending reminders, notifications, or other time-sensitive messages to users. Here's how you can use the Fixed Schedule feature:

## Cron Expression

A cron expression is a string representing a schedule. It consists of five fields separated by spaces, each representing a different aspect of the schedule. The fields are as follows:

1. Minute (0 - 59)
2. Hour (0 - 23)
3. Day of the month (1 - 31)
4. Month (1 - 12)
5. Day of the week (0 - 7)

Here are some examples of cron expressions:

* `0 0 12 * * ?` - This expression triggers an event every day at 12:00 PM.
* `0 0 12 ? * MON-FRI` - This expression triggers an event every weekday at 12:00 PM.
* `0 0 12 1/1 * ? *` - This expression triggers an event every minute.

#### Preview Run

You can preview the next 10 runs of the cron expression by clicking on the "Preview Run" button. This will show you the next time the event will be triggered based on the cron expression.

You can use any website to visualize your cron expression. For example, check [https://crontab.guru/](https://crontab.guru/)

# Webchat Triggers

When you enable the webchat, you can access Webchat Triggers. These are specific types of events that you can use for your benefit. Here are the types of Webchat Triggers:

* Trigger:\
  Activated when a custom event is sent from the user's browser.

* Conversation Started:\
  Activated when the user opens the bot, useful for showing a welcome message before the user sends a message.

* Message In Channel:\
  Used to start a conversation or listen to events on external systems. For example, if there's a new lead in Salesforce, you can send a message to the sales team in Slack, or start the webchat when a visitor is on Page X.

## Using Triggers

To use a trigger, add it to the studio editor. Here's what you need to remember when using triggers:

* Conversation triggers can only be used once.
* You can add conditions for firing the trigger using the Edit Filter.
* To test your trigger, click 'Discover Events', choose the event you want to repeat, click 'save', then 'close'. Select it from the dropdown list named "Select an event to trigger". Now you can click "Trigger this event" to repeat the payload in the emulator.

> 🚧 Using Filters
>
> Please note: filters are evaluated from the first trigger card created to the last one created. Make sure your conditions are written in consequence.

## Advanced Options - Conversation ID

The conversation ID is a unique identifier for each conversation. It can be used to track the conversation history and context. You can use the conversation ID to send messages to a specific conversation or to store information about the conversation.

# Welcome Message

To make the bot send a welcome message, add a trigger to your flow, then choose the "Conversation Started" type. This would make the bot send a message even if the user didn't.

> 🚧 Welcome Message
>
> Welcome Messages can be tested only after publishing the chatbot and can be tested mainly from the web chat screen. Like in the shareable link, the chat from the chatbot dashboard or the embedded web chat component.

## Sending Custom Information

To send custom information from your website to the bot using the "trigger" type, you can use a simple code snippet like the one provided here. For example you can execute this code when a button on the webpage is clicked, sending a custom payload to the bot:

```javascript
window.botpressWebChat.sendPayload({
  type: 'trigger',
  payload: {
    myCustomProperty: 'hello',
  },
})
```

## Webchat Lifecycle and Events

Webchat lifecycle events are specific stages in the lifecycle of the bot's interaction with the user. These stages include when the bot is loaded, ready, when the UI is opened, closed, resized, or when the user is connected, among others.

These are specific stages in the lifecycle of the bot's interaction with the user:

| Event Name         | Description                                                          |
| ------------------ | -------------------------------------------------------------------- |
| `LIFECYCLE.LOADED` | Indicates the bot has been loaded.                                   |
| `LIFECYCLE.READY`  | Indicates the bot is ready for interaction.                          |
| `UI.OPENED`        | Indicates the chat user interface (UI) is opened.                    |
| `UI.CLOSED`        | Indicates the chat UI is closed.                                     |
| `UI.RESIZE`        | Triggered when the chat UI is resized. Useful in responsive designs. |
| `UI.SET-CLASS`     | Allows setting a specific class to the chat UI. Useful for styling.  |
| `CONFIG.SET`       | Triggered when a configuration setting is changed.                   |
| `MESSAGE.SENT`     | Indicates a message has been sent.                                   |
| `MESSAGE.RECEIVED` | Indicates a message has been received.                               |
| `MESSAGE.SELECTED` | Triggered when a message is selected.                                |
| `USER.CONNECTED`   | Indicates a user has connected.                                      |

> 👍 Tip
>
> Whether 'UI.RESIZE' and 'UI.SET-CLASS' are necessary depends on the specific needs of your bot interface and how you want to handle different UI events.

## Webchat Integration

To integrate the webchat into your website, you can include the Botpress webchat script in your HTML code and use the provided functions to control the bot's behavior based on user interactions.

Here's an example:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Triggers</title>
  </head>

  <body>
    <script src="https://cdn.botpress.cloud/webchat/v0/inject.js"></script>
    <script src="https://mediafiles.botpress.cloud/{botId}/webchat/config.js" defer></script>

    <button id="myButton">Click Me!</button>
    <script>
      function handleClick() {
        console.log('Button clicked!')
        window.botpressWebChat.sendPayload({
          type: 'trigger',
          payload: {
            myCustomProperty: 'hello',
          },
        })
      }

      const button = document.getElementById('myButton')
      button.addEventListener('click', handleClick)

      window.botpressWebChat.onEvent(
        function (event) {
          if (event.type === 'LIFECYCLE.LOADED') {
            window.botpressWebChat.sendEvent({ type: 'show' })
          }
        },
        ['LIFECYCLE.LOADED']
      )
    </script>
  </body>
</html>
```

In this example, when the user clicks on the button, the bot opens up and then sends a payload to the bot. You can customize this code based on your needs to create interactive experiences for your users.
