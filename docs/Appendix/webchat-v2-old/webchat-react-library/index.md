---
title: Webchat React Library
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
> 🚧 When using the react library, the configuration in the dashboard will not be used. You will need to configure the webchat using the React components.

 The Webchat React library is a set of React components that makes it easy to embed a webchat in any application or build a more advance version of the actual webchat. It is the building block for the Webchat UI.

Let's start simple, there are 3 main components to get started with the Webchat React library:

## Webchat

The `Webchat` component is the main component that will render the webchat. It must be wrapped in a `WebchatProvider` to work.

## useClient

The `useClient` hook is a custom hook that will create an instance of the `WebchatClient`. It requires a `clientId` prop that is a unique identifier for the client.

### WebchatProvider

The `WebchatProvider` component is a context provider that will provide the webchat with the necessary configuration. It requires a `client` prop that is an instance of the `WebchatClient`. The `WebchatProvider` must be provided for any Webchat component to work.

## Theme & Styles

The `WebchatProvider` component also accepts a `theme` prop which is an object that will style the webchat. Read the [extending Botpress themes](theming/extending-botpress-themes) to generate the `theme object` and `stylesheet`.

## What it looks like

```jsx /WebchatProvider/ /Webchat/ /useClient/
import "./style.css"
import theme from "./theme.json"

import { Webchat, WebchatProvider, useClient } from '@botpress/webchat'

const App = () => {
  const client = useClient({ clientId: '453254325-54325-435-345-345534253' })

  return (
    <WebchatProvider client={client} theme={theme}>
      <Webchat />
    </WebchatProvider>
  )
}
```

[Demo Example](https://stackblitz.com/github/botpress/documentation-examples/tree/master/examples/webchat-react-demo?embed=1\&hideNavigation=1\&view=both\&file=src%2FApp.tsx)

This is the simplest way to get started with the Webchat React library. After this, we'll get into more advanced topics like advance components, custom messages components, and more.

## Webchat Advance Components

The webchat offers 4 advanced components to help you build a more advanced version of the webchat. These components are:

### 1. [Message List](../docs/message-list-component)

### 2. [Fab](../docs/fab)

### 3. [Header](../docs/header)

### 4. [Composer](../docs/composer)
