---
title: Production Logs
excerpt: Admin Logs
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/61eb6ff-image.png)

To add logging to your Botpress chatbot, you can follow these steps:

* Open your Botpress studio and select a Flow.
* Add a new Execute Code Card to your flow by selecting it from the Toolbox and dragging it to the appropriate location.
* Inside the Execute Code Card, add the following code:

```typescript
console.log("Some text");
```

* Save your changes and publish your chatbot to the cloud.
* Navigate to your cloud dashboard and select your published chatbot.
* Open the Chat tab in the menu and start a conversation with your chatbot.
* Once you have completed the conversation, switch to the Logs tab to view the logs generated by your chatbot.

The `console.log()` function is used to log information to the Botpress logs.

You can customize this message to include any information that you need to log, such as user input or API responses.

By adding logging to your chatbot, you can get a better understanding of how your bot is behaving and identify any issues that need to be addressed.

This can help you to create a more effective and reliable chatbot that provides a better experience for your users.
