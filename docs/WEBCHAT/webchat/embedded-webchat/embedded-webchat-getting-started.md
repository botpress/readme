---
title: Getting started with Webchat
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
The Embedded Webchat allows you to integrate chatbot functionality directly into your web application. It supports message handling, event subscriptions, and customization, enabling a dynamic user experience within the browser.

# Quickstart

## 1. Obtain the embedded code

1. Open your bot in the Botpress Workspace.
2. Go to the **Webchat** tab in your bot's dashboard.
3. Click **Advanced Settings** to expand the section.
4. Copy the provided **Embed Code**.

<Image align="center" src="https://files.readme.io/a1f223e-Screenshot_2024-08-16_at_3.08.38_PM.png" />

## 2. Add the code

Paste the copied code to your HTML.

```html index.html
<!DOCTYPE html>
<html>
<head>
  <title>My Webchat</title>
</head>
<body>
  //...
  <script src="https://cdn.botpress.cloud/webchat/v2/inject.js"></script>
  <script src="https://mediafiles.botpress.cloud/52345432-5432543-5435-435545434/webchat/v2/config.js"></script>
</body>
</html>

```

***

# Styling

1. Open your bot in the Botpress Workspace.
2. Go to the Webchat Tab in your bot's dashboard.
3. Click **Styles** to expand the section.
4. Add your custom CSS. You can style the components using our pre-defined [CSS classes](https://botpress.com/docs/custom-css-reference)

<Image align="center" src="https://files.readme.io/673eb94-style.png" />

***

# Webchat controls

When you embed Botpress Webchat into your website, a `botpress` object becomes available on the global window object. This object provides various methods and properties that allow you to interact with the webchat, customize its behavior, and manage the user experience. 

### Properties

| Property        | Description                                                               |
| --------------- | ------------------------------------------------------------------------- |
| `initialized`   | Indicates whether the webchat has been initialized.                       |
| `version`       | The version of the Botpress Webchat.                                      |
| `messagingUrl`  | The URL used for messaging interactions with the bot.                     |
| `clientId`      | The unique client identifier for the webchat instance.                    |
| `fabIframe`     | The iframe element used for the floating action button (FAB).             |
| `fabId`         | The ID of the FAB element.                                                |
| `state`         | The current state of the webchat (e.g., "opened", "closed").              |
| `webchatIframe` | The iframe element used for the webchat interface.                        |
| `webchatId`     | The ID of the webchat element.                                            |
| `style`         | The URL of the stylesheet used by the webchat.                            |
| `configuration` | The configuration settings for the bot, such as bot name and description. |
| `user`          | Information about the current user interacting with the webchat.          |

### Methods

| Method        | Description                                                                                                                        |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `open`        | Opens the webchat interface.                                                                                                       |
| `close`       | Closes the webchat interface.                                                                                                      |
| `toggle`      | Toggles the webchat interface between opened and closed states.                                                                    |
| `init`        | Initializes the webchat with the specified properties.                                                                             |
| `config`      | Updates the webchat configuration.                                                                                                 |
| `sendEvent`   | Sends a custom event to the bot.                                                                                                   |
| `sendMessage` | Sends a message to the bot.                                                                                                        |
| `getUser`     | Retrieves the current user's information.                                                                                          |
| `updateUser`  | Updates the current user's information.                                                                                            |
| `on`          | Listens for specific events emitted by the webchat (e.g., `message received`). Full list of events can be found in the demo below. |

## Listen to events

The `on` method on the `botpress` object is used to register event listeners for various webchat events, allowing you to execute custom JavaScript code in response to those events. It takes two arguments: the event name (as a string) and a callback function that gets executed when the specified event occurs.

<Embed url="https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-embed-event?embed=1&hideNavigation=1&view=both&file=index.html" title="iframe" provider="stackblitz.com" href="https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-embed-event?embed=1&hideNavigation=1&view=both&file=index.html" typeOfEmbed="iframe" height="500px" width="100%" iframe="true" />

***

# Live Demo

<Embed url="https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-embed-controls?embed=1&hideNavigation=1&view=both&file=index.html&ajs_aid=%24device%3A190bbf803c1598-009fa1707e1dbe8-42272e3d-384000-190bbf803c1598" title="iframe" provider="stackblitz.com" href="https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-embed-controls?embed=1&hideNavigation=1&view=both&file=index.html&ajs_aid=%24device%3A190bbf803c1598-009fa1707e1dbe8-42272e3d-384000-190bbf803c1598" typeOfEmbed="iframe" height="500px" width="100%" iframe="true" />

<br />

### Markdown support

We use the react-markdown to display markdown in the front-end. You can find their documentation [here](https://github.com/remarkjs/react-markdown).

### Saving User Information

With the Embedded Webchat, you can send information to Botpress and use it in your Studio. Look [here](/docs/user-data) for more information.
