---
title: Automatically open Webchat after a delay
excerpt: >-
  Open the Webchat widget after a user has browsed on a page for a defined
  period of time.
deprecated: false
hidden: false
metadata:
  robots: index
---
Proactively engaging users allows you to drive engagement to your Webchat widget. By automatically opening the chat widget after a user has spent a defined amount of time on a page, you can draw attention to the chat, encourage questions, and guide visitors toward additional resources or support.

In Botpress, you have the flexibility to configure a delayed auto-open for your Webchat widget. This involves using a JavaScript-based approach to open the widget after a specified period. It ensures that users have enough time to explore your page’s content before they are invited to engage in conversation if they need assistance.

# Important Considerations

## Strategic Delay

Determine an optimal amount of time for users to interact with the page before opening the chat. Too short a delay may be disruptive; too long may miss an opportunity to engage.

## User Experience

Make sure the pop-up appearance is smooth and unobtrusive, and consider whether to remind users they can close or minimize the widget if they prefer.

## Bot Configuration

Prepare your bot content, triggers, and conversation flow so that when the chat does open, users are greeted with a concise and welcoming message.

## Fallback & Accessibility

Ensure your implementation does not rely solely on user scripting (like JavaScript) and that the experience remains accessible for all users.

<br />

# Setup

```
<!DOCTYPE html>
<html>
<head>
  <title>My Webchat</title>
</head>
<body>
  <script src="https://cdn.botpress.cloud/webchat/v2/inject.js"></script>
  <script>
    // Wait for webchat to be ready
    window.botpress.on("webchat:ready", () => {
      // Set delay in milliseconds (e.g., 5000ms = 5 seconds)
      setTimeout(() => {
        window.botpress.open();
      }, 5000);
    });
  </script>
  
  <!-- Your bot initialization script -->
  <script>
    window.botpress.init({
      "botId": "your-bot-id",
      "clientId": "your-client-id", 
      "configuration": {
        "website": {},
        "email": {},
        "phone": {},
        "termsOfService": {},
        "privacyPolicy": {},
        "color": "#3B82F6",
        "variant": "solid",
        "themeMode": "light",
        "fontFamily": "inter",
        "radius": 1
      }
    });
  </script>
</body>
</html>

```