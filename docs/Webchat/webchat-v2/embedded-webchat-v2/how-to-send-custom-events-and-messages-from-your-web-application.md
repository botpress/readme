---
title: How to send custom events and messages from your web app to webchat
deprecated: false
hidden: true
metadata:
  robots: index
next:
  pages:
    - slug: how-to-send-custom-events-from-the-webchat-to-your-web-application
      title: How to send custom events from the Webchat to your web application
      type: basic
---
With the webchat initialized on your web application, you can send custom events to your bot and programmatically send messages on behalf of the user.

## Sending Custom Events to Your Bot

You can send custom events to your bot by calling `await window.botpress.customEvent(customPayload)` in your code, where `customPayload` is a JSON object.

You can capture this custom event using the **“Custom Trigger”** card in Botpress Studio and access the payload via `event.payload`

<Image align="center" width="50% " src="https://files.readme.io/281272814120b69a4608d292a22088e976290e02f055143657ffbbb835bc756e-image.png" />

<br />

## Sending Messages from Your Web Application

To send messages directly to your bot from your web application, use the following method:

`await window\.botpress.sendMessage('custom message')`