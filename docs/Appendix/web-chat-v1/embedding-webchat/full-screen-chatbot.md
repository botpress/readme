---
title: Full Screen Chatbot
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
![](https://files.readme.io/eb6cc5a-image.png)

You can Customize the Chatbot to be Full Screen by default using below CSS

```typescript
// Import the Botpress WebChat JavaScript file
<script src="https://cdn.botpress.cloud/webchat/v0/inject.js"></script>

// Initialize the Botpress WebChat with the required parameters
<script>
    window.botpressWebChat.init({
        // Replace <your-bot-id> and <your-client-id> with your actual bot and client IDs
        "botId": "<your-bot-id>",
        "clientId": "<your-client-id>",

        // Set the URL for the Botpress WebChat JavaScript file and the messaging server
        "hostUrl": "https://cdn.botpress.cloud/webchat/v0",
        "messagingUrl": "https://messaging.botpress.cloud",

        // Set the name of the bot that will be displayed in the WebChat interface
        "botName": "Test",

        // Set the width of the WebChat container and layout to 100% (Full Screen)
        "containerWidth": "100%25",
        "layoutWidth": "100%25",

        // Hide the widget and disable animations
        "hideWidget": true,
        "disableAnimations": true,
    });

    // Opens up the Chatbot by default
    // This lets users start chatting with the Chatbot without needing to click any buttons or menus.
    window.botpressWebChat.onEvent(
        function () {
            window.botpressWebChat.sendEvent({ type: "show" });
        },
        ["LIFECYCLE.LOADED"]
    );
</script>

```
