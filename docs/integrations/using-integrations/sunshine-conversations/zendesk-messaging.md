---
title: Zendesk Messaging
excerpt: >-
  **Zendesk** acquired **Sunshine Conversations** and integrated it with their
  products, so it is possible to use also this integration to connect
  **Botpress** to **Zendesk Messaging **
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/6c03467-image.png)

<br />

# Prerequisites

- A [Zendesk Support Professional plan account](https://www.zendesk.com.br/pricing/support) with Zendesk Messaging enabled to the desired channels
- A [Botpress Cloud account](https://sso.botpress.cloud) and a [Botpress Bot](https://botpress.com/docs/cloud/getting-started/create-and-publish-your-chatbot/)

# Setting up the Sunshine Conversations integration in Botpress

1. Go to the [Integration Hub](https://app.botpress.cloud/hub) in Botpress Cloud (if you don't have the integration installed yet).
2. Find and open the Sunshine Conversations integration then click on the "Install to Bot" button, now go back to your bot settings.

The Sunshine Conversations integration has the following settings:

- **Enabled**: Whether Botpress will communicate with this channel
- **Webhook URL**: The URL for receiving data in Botpress (Copy this)
- **App Id**: The App Id of your Zendesk Conversation API Credentials
- **Key Id**: The Key Id of your Zendesk Conversation API Credentials
- **Key Secret**: The Key Secret of your Zendesk Conversation API Credentials
- **Webhook Secret**: The Webhook Secret of your Zendesk Conversation Integration Webhook

![](https://files.readme.io/2db5af00e37419217754e57db2fc1298a76e02be869639df446a7030574b342c-image.png)

<br />

# Setting up Zendesk Messaging

## Configure the Webhook

1. Open your Zendesk Admin Center.

   ![](https://files.readme.io/8afd375ec346818145acd9c2507c07fd4c6240cac7ab685c33dfd4c300f86154-image.png)
2. Click on **Apps and Integrations** and **Conversations Integrations**

   ![](https://files.readme.io/78bd0b1a02f131561509bc14e200c547a2ac96f892d54135cdd1fa231689baaf-image.png)
3. Give any name and put the **webhook URL** that you copied from Botpress.

   ![](https://files.readme.io/5234889a672d4f9867c17f1106257f22e5776a0e45df3a8f73b5af1963722ba3-image.png)
4. Also select **Conversation message** and **Postbacks** on **Webhook subscriptions**.
5. Click on **Save** on the bottom right corner.
6. Copy the **Shared Secret** and past on the Botpress Integration Configuration page at **Webhook Secret**

   ![](https://files.readme.io/ba2cd16a9ac0a82b3801dd8ae20a1f873b0ddf9a49c530c92e826e3fa39aea04-image.png)

   ![](https://files.readme.io/01dc560081680593182e258f8fc20f146dca7a06b5ea8fd43300a027260ca8bc-image.png)

<br />

## Configure the API Credentials

1. Click on **Apps and Integrations** view and **Conversation API**

   ![](https://files.readme.io/ed50f2a0574b20ce5bb7b2520a877aeeaeff6494a8a5a14460cdd0d17c9abee3-image.png)
2. Click on **Create API key** and give it any name, then **Next**.
3. Copy **App Id**, **Key ID**, **Secret key** and put them on the associated field on the integration configuration.

   ![](https://files.readme.io/fc96ee0c391eb6a41fdebc1c74168f96a085b7eabdaca5a4ef0dda05acf97a6c-image.png)

   ![](https://files.readme.io/949669a73a53e300e885642b75d999063781148d238eb47904ab174e6c8915cc-image.png)

## Save Configuration

Channel configuration is complete, you can now click **Save**

That's it, you may now start chatting with your bot on any channel from Zendesk Channels!

OBS: Please ensure that you enabled Zendesk Messaging for the required Zendesk Channel.