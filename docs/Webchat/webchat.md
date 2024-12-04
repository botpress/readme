---
title: Webchat
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
![](https://files.readme.io/1538ac2-image.png)

The Webchat is a widget that you can add to your website to allow your users to interact with your chatbot. It's a great way to provide support to your users and answer their questions.

# Prerequisites

- A [Botpress Cloud account](https://sso.botpress.cloud) and a [Botpress Bot](https://botpress.com/docs/cloud/getting-started/create-and-publish-your-chatbot/)
- Make sure you've [published your Botpress bot](../docs/create-publish-your-chatbot#publishing-your-bot).

# Setting up the Webchat integration in Botpress

1. Go to the [Integration Hub](https://app.botpress.cloud/hub) in Botpress Cloud (if you don't have the integration installed yet).
2. Find and open the Webchat integration then click on the "Install to Bot" button, now go back to your bot.

# Setting up the Webchat

## Pre-configured Script

**Shareable URL**

You can share your chatbot with people that would like to quickly test your chatbot using the **Shareable Link**.

**Embedded Script**

This script will add the webchat to your website. You can copy the script and paste it in the `<body></body>` tag of your HTML page.  
This is the **recommended** way of adding the webchat to your website.

## Configurable Script

The configurable webchat code must be updated manually every time there is a change. We highly recommend using the **Pre-configured** version.

Copy the code from the **Configurable** tab and paste it in the `<body></body>` tag of your HTML page.

## Configurable Script Parameters

You can customize the webchat by changing/adding the values of the parameters in the script.

[block:parameters]
{
  "data": {
    "h-0": "**Parameter**",
    "h-1": "**Description**",
    "h-2": "**Default value**",
    "h-3": "**parameter type**",
    "0-0": "`stylesheet`",
    "0-1": "Provide a path to a stylesheet to customize the webchat",
    "0-2": "`-`",
    "0-3": "string",
    "1-0": "`showConversationsButton`",
    "1-1": "If false, will hide the conversation list pane",
    "1-2": "`true`",
    "1-3": "boolean",
    "2-0": "`showTimestamp`",
    "2-1": "If true, will display a timestamp under each messages",
    "2-2": "`false`",
    "2-3": "boolean",
    "3-0": "`enableTranscriptDownload`",
    "3-1": "Allows the user to download the conversation history",
    "3-2": "`true`",
    "3-3": "boolean",
    "4-0": "`enableConversationDeletion`",
    "4-1": "Allows the user to delete its conversation history",
    "4-2": "`false`",
    "4-3": "boolean",
    "5-0": "`closeOnEscape`",
    "5-1": "Close the webchat when pressing the Esc key",
    "5-2": "`true`",
    "5-3": "boolean",
    "6-0": "`botName`",
    "6-1": "Displays the bot name to the right of its avatar",
    "6-2": "`-`",
    "6-3": "string",
    "7-0": "`composerPlaceholder`",
    "7-1": "Allows to set a custom composer placeholder",
    "7-2": "`'Reply to {botname}'`",
    "7-3": "string",
    "8-0": "`avatarUrl`",
    "8-1": "Allow to specify a custom URL for the bot's avatar",
    "8-2": "`-`",
    "8-3": "string",
    "9-0": "`locale`",
    "9-1": "Force the display language of the webchat (en, fr, ar, ru, etc..) <br /> Defaults to the user's browser language if not set<br /> Set to 'browser' to force use the browser's language",
    "9-2": "`'browser'`",
    "9-3": "string",
    "10-0": "`botConversationDescription`",
    "10-1": "Small description written under the bot's name",
    "10-2": "`-`",
    "10-3": "string",
    "11-0": "`hideWidget`",
    "11-1": "When true, the widget button to open the chat is hidden",
    "11-2": "`false`",
    "11-3": "boolean",
    "12-0": "`disableAnimations`",
    "12-1": "Disable the slide in / out animations of the webchat",
    "12-2": "`false`",
    "12-3": "boolean",
    "13-0": "`useSessionStorage`",
    "13-1": "Use sessionStorage instead of localStorage, which means the session expires when tab is closed",
    "13-2": "`false`",
    "13-3": "boolean",
    "14-0": "`containerWidth`",
    "14-1": "Sends an event to the parent container with the width provided",
    "14-2": "`360`",
    "14-3": "string OR number",
    "15-0": "`layoutWidth`",
    "15-1": "Sets the width of the webchat",
    "15-2": "`360`",
    "15-3": "string OR number",
    "16-0": "`enablePersistHistory`",
    "16-1": "When enabled, sent messages are persisted to local storage (recall previous messages)",
    "16-2": "`true`",
    "16-3": "boolean",
    "17-0": "`className`",
    "17-1": "CSS class to be applied to iframe",
    "17-2": "`-`",
    "17-3": "string",
    "18-0": "`disableNotificationSound`",
    "18-1": "If true, chat will no longer play the notification sound for new messages.",
    "18-2": "`false`",
    "18-3": "boolean",
    "19-0": "`googleMapsAPIKey`",
    "19-1": "Google Maps API Key required to display the map. It will display a link to Google Maps otherwise.",
    "19-2": "`-`",
    "19-3": "string",
    "20-0": "`website`",
    "20-1": "Displays the bot's website in the conversation page",
    "20-2": "`-`",
    "20-3": "string",
    "21-0": "`phoneNumber`",
    "21-1": "Displays the bot's contact phone number in the conversation page",
    "21-2": "`-`",
    "21-3": "string",
    "22-0": "`termsConditions`",
    "22-1": "Displays the bot's terms of service in the conversation page",
    "22-2": "`-`",
    "22-3": "string",
    "23-0": "`privacyPolicy`",
    "23-1": "Displays the bot's privacy policy in the conversation page",
    "23-2": "`-`",
    "23-3": "string",
    "24-0": "`emailAddress`",
    "24-1": "Displays the bot's email address in the conversation page.",
    "24-2": "`-`",
    "24-3": "string",
    "25-0": "`coverPictureUrl`",
    "25-1": "Displays the bot's cover picture in the conversation page",
    "25-2": "`-`",
    "25-3": "string",
    "26-0": "`showBotInfoPage`",
    "26-1": "Enables the bot's information page in the webchat",
    "26-2": "`false`",
    "26-3": "boolean",
    "27-0": "`showCloseButton`",
    "27-1": "Display's the webchat close button when the webchat is opened",
    "27-2": "`true`",
    "27-3": "boolean",
    "28-0": "`userData`",
    "28-1": "Passes the user data to the bot",
    "28-2": "`-`",
    "28-3": "object",
    "29-0": "`customUser`",
    "29-1": "Passes the custom user data to the bot",
    "29-2": "`-`",
    "29-3": "object"
  },
  "cols": 4,
  "rows": 30,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


## Domain Whitelisting

> 💼 Team Plan
> 
> This feature is only available to Team plan subscribers.

The domain whitelisting feature ensures that only approved domains can host and utilize the chatbot. This enhances security and control, ensuring that your chatbot is only available on trusted websites.

### Configuring Allowed Origins

1. Navigate to the Webchat integration settings on your Dashboard
2. Expand the 'Advanced Settings' menu
3. To add a domain (or an allowed origin), type the domain name in the provided field. You can provide multiple allowed origins or whitelisted domains.

Make sure to save the configuration after you've indicated which domains you want to whitelist.

## Customizing/Controlling the Webchat

For more information on customizing the webchat, please refer to the [Webchat developer documentation](../docs/controlling-web-chat-using-javascript).