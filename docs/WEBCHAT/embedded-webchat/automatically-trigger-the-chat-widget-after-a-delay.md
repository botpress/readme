---
title: Automatically Trigger the Chat Widget After a Delay
deprecated: false
hidden: false
metadata:
  robots: index
---
The HTML code provided ensures that your bot automatically appears on your website, preloaded as if a user had clicked on it, after a 5-second delay.

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Webchat</title>
</head>
<body>
  <script src="https://cdn.botpress.cloud/webchat/v2/inject.js"></script>
  <script>
    // Wait for webchat to be ready
    window.botpress.on("webchat:ready", () => {
      // Set delay in milliseconds (e.g., 5000ms = 5 seconds)
      setTimeout(() => {
        window.botpress.open();
      }, 5000);
    });
  </script>
  
  <!-- Your bot initialization script -->
  <script>
    window.botpress.init({
      "botId": "PUT-YOUR-BOT-ID",
      "clientId": "PUT-YOUR-CLIENT-ID", 
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
      }
    });
  </script>
</body>
</html>
```