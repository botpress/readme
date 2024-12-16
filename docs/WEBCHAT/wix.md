---
title: Wix
excerpt: Embedding the Web Chat in a Wix website
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/5a373f6-image.png)

# Prerequisites

1. A [**Wix**](https://www.wix.com) website with the ability to add custom scripts. This will require a paid plan. Checkout [**Wix Pricing**](https://www.wix.com/upgrade/website) for more information.
2. A [**Domain**](https://support.wix.com/en/article/connecting-a-domain-to-the-wix-name-servers) connected to your Wix website for the Custom Code to work. 
3. A [**Botpress**](https://sso.botpress.cloud) account with an active bot.

<br />

# Getting the Botpress Web Chat Script

1. Log in to your [**Botpress**](https://sso.botpress.cloud) account and navigate to your bot's **Integrations** tab.
2. Click on the **Webchat** Integration and copy the **Embedded** script from the **Pre-configured** tab.

<br />

# Adding the Botpress Web Chat Script in Wix

![](https://files.readme.io/f2494ca-image.png)

<br />

1. Log in to your [**Wix**](https://www.wix.com) dashboard and go to **Settings** from the left sidebar.
2. Scroll down to **Advanced Settings** and click on **Custom Code**.
3. Click on **+ Add Code** in **Body - Start** and paste the **Embedded** script you copied in the previous step.
4. Ensure you apply the code to **All pages** and load the code **Once** at the **Body - end** tag and click **Apply**.

## Testing the Integration

1. Publish your Wix website and navigate to your live Wix website.
2. You should see the Botpress Web Chat widget on the bottom right corner of your website.
