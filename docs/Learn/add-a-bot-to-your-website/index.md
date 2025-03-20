---
title: How to add a bot to your website
excerpt: Use Webchat to embed a bot on your website.
deprecated: false
hidden: false
metadata:
  robots: index
---
Botpress makes it easy to embed a bot on your website using [Webchat](). If you self-host your website, just follow the instructions on this page.

> 📘 Website builders
>
> If you use a website-building tool like [Wordpress](), [Wix](https://botpress-docs.readme.io/v1.5/docs/wix-1#/) or [Webflow](), see the other pages in this section for instructions on how to add your bot.

> 🧩 Low-code
>
> This guide requires basic knowledge of:
>
> * HTML

# Step 1: Get your embed code

To embed a bot a bot on your website, you need the bot's Webchat embed code. You can get the embed code from either the Studio or the Dashboard.

## From the Studio

1. Select **Share** in the upper-right corner.
2. Select **Configure**, then copy the `script` tags:

<Image align="center" src="https://files.readme.io/fde8fb684e105e7dc3e04994924e40e5d2832cc3e1c5ca74efad7ce70fcbde4d-Screen_Shot_2025-03-20_at_10.16.22.png" />

## From the Dashboard

1. Open your bot's Workspace. In the left navigation bar, find the bot you want to embed.
2. Select **Webchat**, then open the **Share** tab.
3. Copy the **Embed code**:

<Image align="center" src="https://files.readme.io/fea6f348f871ea1e244d12f9b447f8c792da55e09064eebad83570d1666fa552-Screen_Shot_2025-03-20_at_10.45.28.png" />

# Step 2: Add to your website

Next, add the Webchat embed code to the `head` section of your website's HTML. For example:

```html index.html
<!DOCTYPE html>
<html>
<head>
  <script src="https://cdn.botpress.cloud/webchat/v2.3/inject.js"></script>
  <script src="https://files.bpcontent.cloud/2025/03/18/14/20250318141028-30WRMG85.js"></script>
</head>
<body>
  <!-- Website content -->
</body>
</html>
```

> ✅ Done!
>
> Your bot is now live on your website.

# Next steps

Now that your bot is live, try [styling]() it to match the rest of your website.