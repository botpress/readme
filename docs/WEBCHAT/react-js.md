---
title: React Components
deprecated: false
hidden: false
metadata:
  title: React Components
  description: |2-
      To integrate Botpress Webchat into your application, install the necessary
        packages, obtain your bot's Client ID, and add the provided code to your
        app, optionally configuring additional settings for a customized chat
        experience.
  keywords:
    - botpress webchat react
  robots: index
---
---
Botpress React components provide a flexible way to build and customize chatbot interfaces in React applications. They enable conversation management, user input handling, and event subscriptions for a seamless chat experience.
# Quickstart
## Install the packages
Install the necessary packages from the npm public registry.
```javascript npm
npm install @botpress/webchat @botpress/webchat-generator
```
```javascript pnpm
pnpm add @botpress/webchat @botpress/webchat-generator
```
```javascript yarn
yarn add @botpress/webchat @botpress/webchat-generator
```
## Obtain the Client ID
To integrate Botpress Webchat into your application, you need to obtain your bot's Client ID, which uniquely identifies your bot and enables communication with the Webchat service. Follow these steps to retrieve it:
1. Open Your Bot in Botpress Workspace
2. Navigate to the Webchat tab
3. Access Advanced Settings
4. Copy the Client ID
<img align="center" src="https://files.readme.io/c4b8059-Screenshot_2024-08-15_at_9.05.51_AM.png" />
## Add the code
Here’s a basic implementation example to get you started:
```jsx App.tsx
import { Webchat, WebchatProvider, Fab, getClient } from "@botpress/webchat";
import { buildTheme } from "@botpress/webchat-generator";
import { useState } from "react";
const { theme, style } = buildTheme({
  themeName: "prism",
  themeColor: "#634433",
});
//Add your Client ID here ⬇️
const clientId = "YOUR_CLIENT_ID";
export default function App() {
  const client = getClient({ clientId });
  const [isWebchatOpen, setIsWebchatOpen] = useState(false);
  const toggleWebchat = () => {
    setIsWebchatOpen((prevState) => !prevState);
  };
  return (
    <div style={{ width: "100vw", height: "100vh" }}>
      <style>{style}</style>
      <WebchatProvider
        theme={theme}
        client={client}
      >
        <Fab onClick={toggleWebchat} />
        <div
          style={{
            display: isWebchatOpen ? "block" : "none",
          }}
        >
          <Webchat />
        </div>
      </WebchatProvider>
    </div>
  );
}
```
## Optional: Configuration
You can enhance your Webchat experience by incorporating additional configuration options. Here's an example:
```jsx App.tsx
// ...
const config = {
  composerPlaceholder: "What would you like to know?",
  botName: "Customer service",
  botAvatar: "https://picsum.photos/200/300",
  botDescription:
    "Hi! 👋  Welcome to webchat this is some description talking about what it is. This might be a bit longer when expanded.",
  email: {
    title: "randomEmail@boptress.com",
    link: "mailto:randomEmail@boptress.com",
  },
  phone: {
    title: "555-555-5555",
    link: "tel:555-555-5555",
  },
  website: {
    title: "https://botpress.com",
    link: "https://botpress.com",
  },
  termsOfService: {
    title: "Terms of service",
    link: "https://botpress.com/terms",
  },
  privacyPolicy: {
    title: "Privacy policy",
    link: "https://botpress.com/privacy",
  },
};
export default function App() {
  // ...
  return (
    <div style={{ width: "100vw", height: "100vh" }}>
      <style>{style}</style>
      <WebchatProvider
        key={JSON.stringify(config)}
        theme={theme}
        //Add the configuration to the Webchat Provider ⬇️
        configuration={config}
        client={client}
      >
        <Fab onClick={toggleWebchat} />
        <div
          style={{
            display: isWebchatOpen ? "block" : "none",
          }}
        >
          <Webchat />
        </div>
      </WebchatProvider>
    </div>
  );
}
```
***
# Component References
## WebchatProvider
`WebchatProvider` is a necessary component in the Botpress Webchat SDK. It ensures that all webchat components function correctly by providing the essential context. All webchat components, such as `<Webchat />`, `<Fab />`, and others, must be placed inside the WebchatProvider to work properly.
```jsx App.tsx
// ...  
  <WebchatProvider client={client} theme={theme}>
      // All Webchat components go here
  </WebchatProvider>
// ...  
```
## FAB (Floating Action Button)
<br />
<img align="center" src="https://files.readme.io/61cf345-38b71ad-image.png" />
`FAB` component is a UI element designed to to open or toggle the visibility of the webchat interface.
```jsx App.tsx
import { Fab } from "@botpress/webchat";
// ...
<WebchatProvider client={client}>
  <Fab onClick={toggleWebchat} />
  {/* Other Webchat components */}
</WebchatProvider>
// ...
```
## WebChat
<br />
<img align="center" width="250px" src="https://files.readme.io/628a9b7-Screenshot_2024-08-19_at_3.28.07_PM.png" />
`WebChat` component serves as the main container for the chat interface. It provides a complete chat experience by rendering a header, a list of messages, and an input area where users can compose and send messages. 
Under the hood, the `Webchat` component is composed of several modular components that can be used separately for more customized layouts. 
```jsx App.tsx
import { Container, Header, MessageList, Composer, ComposerInput, ComposerButton, UploadButton, WebchatProvider } from '@botpress/webchat';
// Using Webchat directly:
<WebchatProvider client={client} theme={theme}>
  <Webchat />
</WebchatProvider>
// is equivalent to:
<WebchatProvider client={client} theme={theme}>
  <Container>
    <Header />
    <MessageList />
    <Composer>
      <ComposerInput />
      <ComposerButton />
    </Composer>
  </Container>
</WebchatProvider>
```
## Header
<img align="center" width="300px" src="https://files.readme.io/e0b68c4-Screenshot_2024-08-19_at_4.22.41_PM.png" />
`Header` component sits at the top of the Webchat, providing clear bot identification and quick access to functions like refreshing or closing the chat.
## MessageList
<img align="center" width="200px" src="https://files.readme.io/d9e5473-Screenshot_2024-08-19_at_4.33.19_PM.png" />
`MessageList` component displays the ongoing conversation between the user and the bot within the Botpress Webchat.
## Composer
`Composer` component functions as a container for the text input field and the send message button.
```jsx App.tsx
import {Composer, ComposerInput, ComposerButton } from '@botpress/webchat';
// ...
    <Composer>
      <ComposerInput />
      <ComposerButton />
    </Composer>
// ...
```