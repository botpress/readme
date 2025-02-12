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

<br />

## Video Demonstration

Here is a video demonstration on how to build a custom chatbot for Wix. Towards the end of the tutorial, around the 18th-minute mark, we go over how adding the Botpress Webchat in Wix.

<br />

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=rG7dguRDFIA" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FrG7dguRDFIA%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DrG7dguRDFIA%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FrG7dguRDFIA%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=rG7dguRDFIA" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## Testing the Integration

1. Publish your Wix website and navigate to your live Wix website.
2. You should see the Botpress Web Chat widget on the bottom right corner of your website.

## Embedding the Botpress Web Chat in a HTML div

1. Log in to your [**Wix**](https://www.wix.com) dashboard and click on **Edit Site** on the top right of the dashboard.
2. While in the Studio Editor, click on the **Add Elements** button from the left sidebar.
3. Scroll until you see **Embed Code**. Click on it and click on **Embed HTML**.
4. Place and modify the length/width of the HTML div wherever/however you'd like.
5. Afterwards, place the following code under **Add your code here (HTTPS only)**. Replace the "botId" and "clientId" with your values:

```Text HTML
<div id="webchat-container" style="position: relative; width: 100%; height: 100%;">
  <script src="https://cdn.botpress.cloud/webchat/v2.2/inject.js"></script>
  <script>
    window.botpress.on("webchat:ready", () => {
      window.botpress.open();
    });

    window.botpress.init({
      "botId": "YOUR_BOT_ID",
      "configuration": {
        "botName": "Mr. Botpress Bot",
        "botAvatar": "https://cdn.prod.website-files.com/637e5037f3ef83b76dcfc8f9/65b02372899b558fa6d650b8_Pricing%20Changes.webp",
        "website": {},
        "email": {},
        "phone": {},
        "termsOfService": {},
        "privacyPolicy": {},
        "color": "#3bf5a1",
        "variant": "solid",
        "themeMode": "light",
        "fontFamily": "inter",
        "radius": 1
      },
      "clientId": "YOUR_CLIENT_ID"
    });
  </script>
  <style>
    #webchat-container {
      position: relative;
      width: 100%;
      height: 100%;
    }
    .bpFab {
      display: none;
    }
    .bpWebchat {
      position: absolute !important;
      top: 0 !important;
      left: 0 !important;
      right: 0 !important;
      bottom: 0 !important;
      width: 100% !important;
      height: 100% !important;
    }
  </style>
</div>
```

6. **Note:** See [Here](https://botpress.com/docs/webchat-client) for a guide on finding your Botpress clientId. Your Botpress botId can be found in the url of your studio or the **Webchat** tab. For example, while getting your clientId from the **Webchat** tab in the left sidebar of the workspace dashboard, you will notice your url look something like this: [https://app.botpress.cloud/workspaces/THIS\_IS\_YOUR\_WORKSPACE\_ID/bots/THIS\_IS\_YOUR\_BOT\_ID/webchat/v2/general](https://app.botpress.cloud/workspaces/THIS_IS_YOUR_WORKSPACE_ID/bots/THIS_IS_YOUR_BOT_ID/webchat/v2/general).\
   Grab the part after "bots/" that corresponds to the "THIS\_IS\_YOUR\_BOT\_ID" section and paste that in the HTML code from above!
7. This is what it should look like in the end: (**Note:** Modify the code in the "configuration" section within "window\.botpress.init" to configure your bot's name, avatar, color, font, etc...).

   ![](https://files.readme.io/8836ec224a7f54381271a70db6b64ab879418b01639ced4434e88304f5fcbc95-image.png)

## Embedding the Botpress Web Chat in a Website div

1. Log in to your [**Wix**](https://www.wix.com) dashboard and click on **Edit Site** on the top right of the dashboard.
2. While in the Studio Editor, click on the **Add Elements** button from the left sidebar.
3. Scroll until you see **Embed Code**. Click on it and click on **Embed a site**.
4. Head over to your Botpress dashboard and click on **Webchat** in the left sidebar. Please make sure you are editing the Webchat of the correct bot by checking the title of the dropdown.

   ![](https://files.readme.io/0f53b0bd1f190d499d3d04e586b0de3267f0c9e772c41b16a304464488376f7e-image.png)
5. From there, head over to **Share** tab and copy the **Shareable Link**.
6. Go back to Wix and paste the link under "What's the website address?" and click **Apply**.

   Your embed should look like this (see screenshot below). **Note:** The name of the bot, the image, and the color scheme of the buttons comes from the changes you've made in the **Theme** tab of the Webchat.

   ![](https://files.readme.io/c012ca365436b2410245f9f2e9b0d35f98ad013ee400548ad29ffac34a4e61ef-image.png)

   <br />