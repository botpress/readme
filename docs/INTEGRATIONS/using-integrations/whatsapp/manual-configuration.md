---
title: Manual Configuration
excerpt: >-
  For more complex use cases, you can use your own Meta app with our
  integration. This configuration is optional, and most builders should use the
  simple one-click-install setup wizard.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Optional: Manual Configuration

For more complex use cases, you can use your own Meta app with our integration.

## Prerequisites

* A [Meta developer app](https://developers.facebook.com/apps/create/). Check out [this article](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started#set-up-developer-assets) to learn more about the setup.

<Embed url="https://www.youtube.com/watch?v=LQd1iGJLj58" title="How to Connect your Chatbot to WhatsApp" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/LQd1iGJLj58/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=LQd1iGJLj58" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FLQd1iGJLj58%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DLQd1iGJLj58%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FLQd1iGJLj58%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

## Enable Manual Configuration

1. Go to the [Integration Hub](https://app.botpress.cloud/hub) in Botpress Cloud (if you don't have the integration installed yet).
2. Find and open the WhatsApp integration then click on the "Install to Bot" button, now go back to your bot.
3. Enable "Use Manual Configuration"

The WhatsApp integration will have the following settings:

### 1. Verify Token

The **Verify Token** is used by Meta to verify that you are the real owner of the provided webhook.\
You can generate any random alphanumeric string for this configuration. Paste it in your **Verify Token** channel configuration.

### 2. Phone Number ID

1. In your Meta App's left sidebar, expand the **WhatsApp** menu and select **Getting Started**
2. In the **Send and receive messages** section, beside the label **Phone Number ID** click **Copy** then paste it in the **Phone Number ID** field in Botpress

### 3. Client Secret

1. In your Meta App's left sidebar, expand the **Settings** menu and select **Basic**
2. In the **App Secret** field,  click **Show** then copy and paste it in the **Client Secret** field in Botpress

### 4. Access Token

The **Phone Number ID** and **Access Token** are used to send and receive messages to/from the WhatsApp API.

1. In your Meta App's left sidebar, expand the **WhatsApp** menu and select **Getting Started**
2. In the **Temporary access token** section, click **Copy** and then paste it in the **Access Token** field in Botpress

### 5. (Optional): Permanent Access Token

**Permanent Access Token** can be used to send and receive messages to/from the WhatsApp API without the need to refresh the token every 24 hours.

1. Navigate to [Business Settings](https://business.facebook.com/settings).
2. Choose the business account associated with your app.
3. Click on `Add` under `System Users`.
4. Enter a name for the system user, assign the `Admin` role, and click `Create System User`.
5. Click on `Create Asset` and select `Apps` from the asset type Tab.
6. Select your app and toggle `Manage App (full control)`.
7. Click `Generate New Token` and select `whatsapp_business_messaging` and `whatsapp_business_management` permission.
8. Copy and save your token.

> 📘 Fix for Unexpected Messaging Behavior
>
> Experiencing replies from the wrong numbers? **Disable** the advanced permission for `whatsapp_business_management`. This adjustment is crucial because advanced permissions can interfere with how messages are routed, leading to responses from multiple numbers instead of the intended one. Reverting to basic permission settings ensures messages are directed correctly, solving this issue.

## Finalizing Channel Configuration

The next step is to Enable the channel from the top of the screen and then copy the webhook URL from the button below the webhook URL.

In the last step, click **Save**.

Now we can go back to Step (3) & Step (4) in this [article](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started#set-up-developer-assets).

## Webhook Fields

#### We need to subscribe to the webhook fields below

* Messages: For the chat to work properly, you need to subscribe to the **messages** webhook field.
