---
title: Telegram
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
![](https://files.readme.io/f0b7533-image.png)

<Embed url="https://www.youtube.com/watch?v=w0-UGm4mu74" title="How to Connect your Chatbot to Telegram" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/w0-UGm4mu74/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=w0-UGm4mu74" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252Fw0-UGm4mu74%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253Dw0-UGm4mu74%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252Fw0-UGm4mu74%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

# Prerequisites

* A Telegram account and a Telegram bot
* A [Botpress Cloud account](https://sso.botpress.cloud) and a [Botpress Bot](https://botpress.com/docs/cloud/getting-started/create-and-publish-your-chatbot/)

## Create a Bot

To create a bot on Telegram, use Telegram's BotFather. The BotFather will ask you for a name and username, then generate an authorization token for your new bot

The name of your bot is displayed in contact details and elsewhere

The Username is a short name to be used in mentions and t.me links. Usernames are 5-32 characters long and are case insensitive but may only include Latin characters, numbers, and underscores. Your bot's username must end in `bot`, such as `tetris_bot` or `TetrisBot`

<br />

# Setting up the Telegram integration in Botpress

1. Go to the [Integration Hub](https://app.botpress.cloud/hub) in Botpress Cloud (if you don't have the integration installed yet).
2. Find and open the Telegram integration then click on the "Install to Bot" button, now go back to your bot settings.

The Telegram integration has the following settings:

* **Enabled**: Whether Botpress will communicate with Telegram
* **Webhook URL**: The URL for receiving data in Botpress
* **Bot Token**: The token of your Telegram bot

<br />

# Setting up Telegram

## Generate an Authorization Token

When you create a Telegram bot, BotFather will automatically generate a token. The token is a string that is required to authorize the bot and send requests to the Bot API. Keep your token secure and store it safely; anyone can use it to control your bot

If your existing token is compromised or you lost it for some reason, use the `/token` command to generate a new one

## Bot Token

Copy your Telegram bot token and paste it into the **Bot Token** channel configuration and click **Save**.

That's it, you may now start chatting with your bot on Telegram!

<br />

# Tips

* To get the Telegram conversation ID, you can read the following variable:\
  `{{ event.tags.conversation["telegram:id"] }}`.

* To get the Telegram user ID, you can read the following variable:\
  `{{ event.tags.user["telegram:id"] }}`.

* To get the Telegram message ID, you can read the following variable:\
  `{{ event.tags.message["telegram:id"] }}`.
