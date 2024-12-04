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

* A [Botpress Cloud account](https://sso.botpress.cloud) and a [Botpress Bot](https://botpress.com/docs/cloud/getting-started/create-and-publish-your-chatbot/)
* Make sure you've [published your Botpress bot](../docs/create-publish-your-chatbot#publishing-your-bot).

# Setting up the Webchat integration in Botpress

1. Go to the [Integration Hub](https://app.botpress.cloud/hub) in Botpress Cloud (if you don't have the integration installed yet).
2. Find and open the Webchat integration then click on the "Install to Bot" button, now go back to your bot.

# Setting up the Webchat

## Pre-configured Script

**Shareable URL**

You can share your chatbot with people that would like to quickly test your chatbot using the **Shareable Link**.

**Embedded Script**

This script will add the webchat to your website. You can copy the script and paste it in the `<body></body>` tag of your HTML page.\
This is the **recommended** way of adding the webchat to your website.

## Configurable Script

The configurable webchat code must be updated manually every time there is a change. We highly recommend using the **Pre-configured** version.

Copy the code from the **Configurable** tab and paste it in the `<body></body>` tag of your HTML page.

## Configurable Script Parameters

You can customize the webchat by changing/adding the values of the parameters in the script.

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        **Parameter**
      </th>

      <th style={{ textAlign: "left" }}>
        **Description**
      </th>

      <th style={{ textAlign: "left" }}>
        **Default value**
      </th>

      <th style={{ textAlign: "left" }}>
        **parameter type**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        `stylesheet`
      </td>

      <td style={{ textAlign: "left" }}>
        Provide a path to a stylesheet to customize the webchat
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `showConversationsButton`
      </td>

      <td style={{ textAlign: "left" }}>
        If false, will hide the conversation list pane
      </td>

      <td style={{ textAlign: "left" }}>
        `true`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `showTimestamp`
      </td>

      <td style={{ textAlign: "left" }}>
        If true, will display a timestamp under each messages
      </td>

      <td style={{ textAlign: "left" }}>
        `false`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `enableTranscriptDownload`
      </td>

      <td style={{ textAlign: "left" }}>
        Allows the user to download the conversation history
      </td>

      <td style={{ textAlign: "left" }}>
        `true`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `enableConversationDeletion`
      </td>

      <td style={{ textAlign: "left" }}>
        Allows the user to delete its conversation history
      </td>

      <td style={{ textAlign: "left" }}>
        `false`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `closeOnEscape`
      </td>

      <td style={{ textAlign: "left" }}>
        Close the webchat when pressing the Esc key
      </td>

      <td style={{ textAlign: "left" }}>
        `true`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `botName`
      </td>

      <td style={{ textAlign: "left" }}>
        Displays the bot name to the right of its avatar
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `composerPlaceholder`
      </td>

      <td style={{ textAlign: "left" }}>
        Allows to set a custom composer placeholder
      </td>

      <td style={{ textAlign: "left" }}>
        `'Reply to {botname}'`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `avatarUrl`
      </td>

      <td style={{ textAlign: "left" }}>
        Allow to specify a custom URL for the bot's avatar
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `locale`
      </td>

      <td style={{ textAlign: "left" }}>
        Force the display language of the webchat (en, fr, ar, ru, etc..) <br /> Defaults to the user's browser language if not set<br /> Set to 'browser' to force use the browser's language
      </td>

      <td style={{ textAlign: "left" }}>
        `'browser'`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `botConversationDescription`
      </td>

      <td style={{ textAlign: "left" }}>
        Small description written under the bot's name
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `hideWidget`
      </td>

      <td style={{ textAlign: "left" }}>
        When true, the widget button to open the chat is hidden
      </td>

      <td style={{ textAlign: "left" }}>
        `false`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `disableAnimations`
      </td>

      <td style={{ textAlign: "left" }}>
        Disable the slide in / out animations of the webchat
      </td>

      <td style={{ textAlign: "left" }}>
        `false`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `useSessionStorage`
      </td>

      <td style={{ textAlign: "left" }}>
        Use sessionStorage instead of localStorage, which means the session expires when tab is closed
      </td>

      <td style={{ textAlign: "left" }}>
        `false`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `containerWidth`
      </td>

      <td style={{ textAlign: "left" }}>
        Sends an event to the parent container with the width provided
      </td>

      <td style={{ textAlign: "left" }}>
        `360`
      </td>

      <td style={{ textAlign: "left" }}>
        string OR number
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `layoutWidth`
      </td>

      <td style={{ textAlign: "left" }}>
        Sets the width of the webchat
      </td>

      <td style={{ textAlign: "left" }}>
        `360`
      </td>

      <td style={{ textAlign: "left" }}>
        string OR number
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `enablePersistHistory`
      </td>

      <td style={{ textAlign: "left" }}>
        When enabled, sent messages are persisted to local storage (recall previous messages)
      </td>

      <td style={{ textAlign: "left" }}>
        `true`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `className`
      </td>

      <td style={{ textAlign: "left" }}>
        CSS class to be applied to iframe
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `disableNotificationSound`
      </td>

      <td style={{ textAlign: "left" }}>
        If true, chat will no longer play the notification sound for new messages.
      </td>

      <td style={{ textAlign: "left" }}>
        `false`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `googleMapsAPIKey`
      </td>

      <td style={{ textAlign: "left" }}>
        Google Maps API Key required to display the map. It will display a link to Google Maps otherwise.
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `website`
      </td>

      <td style={{ textAlign: "left" }}>
        Displays the bot's website in the conversation page
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `phoneNumber`
      </td>

      <td style={{ textAlign: "left" }}>
        Displays the bot's contact phone number in the conversation page
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `termsConditions`
      </td>

      <td style={{ textAlign: "left" }}>
        Displays the bot's terms of service in the conversation page
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `privacyPolicy`
      </td>

      <td style={{ textAlign: "left" }}>
        Displays the bot's privacy policy in the conversation page
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `emailAddress`
      </td>

      <td style={{ textAlign: "left" }}>
        Displays the bot's email address in the conversation page.
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `coverPictureUrl`
      </td>

      <td style={{ textAlign: "left" }}>
        Displays the bot's cover picture in the conversation page
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        string
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `showBotInfoPage`
      </td>

      <td style={{ textAlign: "left" }}>
        Enables the bot's information page in the webchat
      </td>

      <td style={{ textAlign: "left" }}>
        `false`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `showCloseButton`
      </td>

      <td style={{ textAlign: "left" }}>
        Display's the webchat close button when the webchat is opened
      </td>

      <td style={{ textAlign: "left" }}>
        `true`
      </td>

      <td style={{ textAlign: "left" }}>
        boolean
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `userData`
      </td>

      <td style={{ textAlign: "left" }}>
        Passes the user data to the bot
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        object
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        `customUser`
      </td>

      <td style={{ textAlign: "left" }}>
        Passes the custom user data to the bot
      </td>

      <td style={{ textAlign: "left" }}>
        `-`
      </td>

      <td style={{ textAlign: "left" }}>
        object
      </td>
    </tr>
  </tbody>
</Table>

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
