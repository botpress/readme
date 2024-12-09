---
title: Getting Started
deprecated: false
hidden: true
metadata:
  robots: index
next:
  pages:
    - slug: how-to-style-your-webchat
      title: How to style your Webchat
      type: basic
---
The Embedded Webchat allows you to integrate chatbot functionality directly into your web application. It supports message handling, event subscriptions, and customization, enabling a dynamic user experience within the browser.

## Setup

The simplest way to get started with Webchat for your web application is by embedding a couple of script tags into your HTML. Follow the steps below:

1. Open your bot in the **Botpress Workspace**.
2. Navigate to the **Webchat** tab in your bot’s dashboard.
3. Click **Advanced Settings**.
4. Copy the provided Embed Code.

<Image align="center" width="90% " src="https://files.readme.io/820dc883bb2d56b0668729c2b17b7584ea4916e6b38b0826ae1fe24f34ca3ec7-image.png" />

5. Paste the copied code into your HTML:
   ```html index.html
   <!DOCTYPE html>
   <html>
   <head>
     <title>My Webchat</title>
   </head>
   <body>
     <!-- Other content -->
     <script src="https://cdn.botpress.cloud/webchat/v2/inject.js"></script>
     <script src="https://mediafiles.botpress.cloud/52345432-5432543-5435-435545434/webchat/v2/config.js"></script>
   </body>
   </html>
   ```

<br />

## Setup Webchat as a component in your web application.

Webchat can also be set up as part of your web application to give it a more unique look and feel. To do this:

* Follow steps 1 to 4 from above to get the embed code scripts.
* Instead of adding the scripts directly to your HTML body, open the src link in the second script and copy the code snippet. It should look like this:
  ```javascript
  window.botpress.init({
    "botId": "d3aea06d-0f04-4701-bec3-b457caf79902",
    "configuration": {
      "website": {},
      "email": {},
      "phone": {},
      "termsOfService": {},
      "privacyPolicy": {},
      "color": "#3B82F6",
      "variant": "solid",
      "themeMode": "light",
      "fontFamily": "inter",
      "radius": 1
    },
    "clientId": "0e772c62-e321-46b5-a9fb-a88c5104e067"
  });
  ```
* Add the following HTML wherever you want the Webchat component to appear in your web application and replace the `window.botpress.init` call in the iframe with the snippet you copied from the src link of the second script.
  ```html
  <div class="webchat" style="height: 600px; width: 400px;">
    <iframe
      style="height: 100%; width: 100%; border: none;"
      srcdoc='
      <!doctype html>
      <html lang="en">
        <head></head>
        <body>
          <script src="https://cdn.botpress.cloud/webchat/v2.2/inject.js"></script>
          <script defer>
            window.botpress.on("webchat:ready", (conversationId) => {
              botpress.open();
            });

            <!-- REPLACE THE CONTENT BELOW WITH THE JAVASCRIPT CODE YOU COPIED EARILER -->
            window.botpress.init({
              "botId": "d3aea06d-0f04-4701-bec3-b457caf79902",
              "configuration": {
                "website": {},
                "email": {},
                "phone": {},
                "termsOfService": {},
                "privacyPolicy": {},
                "color": "#3B82F6",
                "variant": "solid",
                "themeMode": "light",
                "fontFamily": "inter",
                "radius": 1
              },
              "clientId": "0e772c62-e321-46b5-a9fb-a88c5104e067"
            });
            <!-- REPLACE THE CONTENT ABOVE -->

          </script>
        </body>
      </html>'
    ></iframe>
  </div>
  ```
* Update the styles of the parent div to your requirements.
* **Note**: To have your webchat take up the full screen update the above code as follows:
  ```html
  <div class="webchat" style="height: 100vh; width: 100vw;">
    ... 
  </div>
  ```