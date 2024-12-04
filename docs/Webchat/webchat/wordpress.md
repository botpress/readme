---
title: Wordpress
excerpt: Embedding the Web Chat in a Wordpress website
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/f13d67d-image.png)

# Prerequisites

1. A [**Wordpress**](https://wordpress.com) website with a **Business Plan** upgrade for accessing [**WPCode**](https://wordpress.com/plugins/insert-headers-and-footers) plugin to add custom scripts.
2. A [**Botpress**](https://sso.botpress.cloud) account with an active bot.

<br />

# Installing WPCode Plugin in Wordpress

![](https://files.readme.io/08e2904-image.png)

<br />

1. Log in to your [**Wordpress**](https://wordpress.com) dashboard.
2. Go to [**WPCode**](https://wordpress.com/plugins/insert-headers-and-footers) and click **Install and activate**.
3. Once activated, you'll notice a new menu item labeled **Code Snippets** on your WordPress dashboard's left-hand sidebar.

## Adding the Botpress Web Chat Script

![](https://files.readme.io/e94ad0e-image.png)

<br />

1. Log in to your [**Botpress**](https://sso.botpress.cloud) account and navigate to your bot's **Integrations** tab.
2. Click on the **Webchat** tile and copy the **Embedded** script from the **Pre-configured** tab.
3. In the WPCode dashboard, navigate to the **Code Snippets** menu item and click **Headers and Footers**.
4. Paste the **Embedded** script in the **Body** section and click **Save Changes**.

## Testing the Integration

![](https://files.readme.io/8f740e9-image.png)

<br />

1. Navigate to your Wordpress website and refresh the page.
2. You should see the Botpress Web Chat widget on the bottom right corner of your website.
