---
title: How to send custom events and messages from your web application.
deprecated: false
hidden: false
metadata:
  robots: index
---
With webchat initialized on your web application, you can send events to your Bot and programmatically send messages on behalf of the user.

## Sending custom events to your Bot

You can send custom events to your bot by calling `await indow.botpress.customEvent(customPayload)`in your code where `customPayload` is a JSON Object.

You can capture this custom event using the "Custom Trigger" Card in the botpress studio and access the payload using `event.payload`

<Image align="center" width="50% " src="https://files.readme.io/281272814120b69a4608d292a22088e976290e02f055143657ffbbb835bc756e-image.png" />

<br />

## Sending messages from your web application

You can send from your web application to your bot by calling `await window\.botpress.sendMessage('custom message')`