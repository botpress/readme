---
title: Webchat Client
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Webchat Client
  description: >-
    The JavaScript client for Botpress Webchat allows seamless interaction with
    the Webchat API from your web application, enabling message exchange and
    event subscriptions. To integrate, install the package, obtain your bot's
    Client ID, and add the provided code to initialize and use the client.
  keywords:
    - webchat client botpress
  robots: index
next:
  description: ''
---
The JavaScript client enables seamless interaction with the Webchat API directly from your web application. Specifically designed for browser environments, this client allows you to send and receive messages from the bot and subscribe to various events, such as incoming messages.

> 📘 This is for advanced use cases where you want to build your own front-end or listen to particular events.
> 
> We recommend most people start with the Embedded Webchat or React Components.

# Quickstart

## 1. Install the package

Install the necessary package from the npm public registry.

```javascript npm
npm install @botpress/webchat
```
```javascript pnpm
pnpm add @botpress/webchat
```
```javascript yarn
yarn add @botpress/webchat
```

## 2. Obtain the Client ID

To integrate Botpress Webchat Client into your application, you need to obtain your bot's Client ID, which uniquely identifies your bot and enables communication with the Webchat service. Follow these steps to retrieve it:

1. Open your bot in the Botpress Workspace
2. Navigate to the **Webchat** tab
3. Access **Advanced Settings**
4. Copy the **Client ID**

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c4b8059-Screenshot_2024-08-15_at_9.05.51_AM.png",
        "",
        "Botpress interface"
      ],
      "align": "center"
    }
  ]
}
[/block]


## 3. Add the code

```javascript index.js
import { getClient } from '@botpress/webchat'

//Add your Client ID here ⬇️
const clientId = "YOUR_CLIENT_ID";

const client = getClient({ clientId })

client.on("message", (message) => {
  console.log("Received message", message); // Messages from the bot
});

await client.connect(); // Initialize the client

await client.sendMessage("Hello, Botpress!"); // Send a message to the bot
```

***

# API Reference

The Webchat Client provides a set of properties and methods that allow you to manage conversations, send messages, and handle user sessions. 

These are the available properties and methods:

| Name                 | Description                                                                                                                     |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `mode`               | Defines the mode of the webchat client. `'messaging'` for standard chat, and `'pushpin'` for pinning messages or conversations. |
| `clientId`           | A unique identifier for the client, used to associate the client with a specific bot or session.                                |
| `apiUrl`             | The URL of the API that the webchat client will connect to.                                                                     |
| `userId`             | The unique identifier of the user, if available.                                                                                |
| `conversationId`     | The unique identifier of the current conversation, if available.                                                                |
| `on`                 | A method to listen for specific events emitted by the webchat client.                                                           |
| `connect`            | Connects the client to the server with optional user credentials and data.                                                      |
| `disconnect`         | Disconnects the client from the server.                                                                                         |
| `getUser`            | Retrieves the current user's information.                                                                                       |
| `updateUser`         | Updates the current user's information.                                                                                         |
| `sendMessage`        | Sends a text message to the current conversation.                                                                               |
| `sendFile`           | Sends a file to the current conversation and returns its details.                                                               |
| `sendEvent`          | Sends a custom event to the current conversation.                                                                               |
| `switchConversation` | Switches to a different conversation by its ID.                                                                                 |
| `conversationExists` | Checks if a conversation with the specified ID exists.                                                                          |
| `newConversation`    | Starts a new conversation.                                                                                                      |
| `listMessages`       | Retrieves a list of messages from the current conversation.                                                                     |

***

# Live Demo

[block:embed]
{
  "html": false,
  "url": "https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-client?embed=1&hideNavigation=1&view=both&file=src%2Fmain.ts",
  "title": "iframe",
  "provider": "stackblitz.com",
  "href": "https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-client?embed=1&hideNavigation=1&view=both&file=src%2Fmain.ts",
  "typeOfEmbed": "iframe",
  "height": "500px",
  "width": "100%",
  "iframe": true
}
[/block]