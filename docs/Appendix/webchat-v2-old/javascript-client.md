---
title: Javascript Client
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The Javascript client gives you the ability to interact with the Webchat API from your web application. This client is designed to be used in the browser.

The Webchat client can be used to send and receive messages from the bot. It can also be used to subscribe to events such as new messages.

```ts
import { getClient } from '@botpress/webchat'

const client = getClient({ clientId: '5234523-543254-35342-52345' })

client.on("message", (message) => {
  console.log("Received message", message); // Messages from the bot
});

await client.connect();

await client.sendMessage("Hello, Botpress!"); // Send a message to the bot
```

[Demo Example](https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-client?embed=1\&hideNavigation=1\&view=both\&file=src%2Fmain.ts)
