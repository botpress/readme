---
title: React App
excerpt: Embedding the Web Chat in a React App
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/07cbb53-image.png)

<br />

You can use the web chat in a React app by creating a component that will add the web chat to your app.

# Prerequisites

* A React app
* A bot deployed on Botpress Cloud

```jsx
import React, { useEffect } from 'react'

const Chatbot = () => {
  useEffect(() => {
    const script = document.createElement('script')
    script.src = 'https://cdn.botpress.cloud/webchat/v1/inject.js'
    script.async = true
    document.body.appendChild(script)

    script.onload = () => {
      window.botpressWebChat.init({
        botId: '<botID>',
        hostUrl: 'https://cdn.botpress.cloud/webchat/v1',
        messagingUrl: 'https://messaging.botpress.cloud',
        clientId: '<clientID>',
      })
    }
  }, [])

  return <div id="webchat" />
}

export default Chatbot
```

You can then add the component to your app.

```jsx
import React from 'react'
import Chatbot from './Chatbot'

const App = () => {
  return (
    <div>
      <Chatbot />
    </div>
  )
}

export default App
```