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

[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2Fw0-UGm4mu74%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3Dw0-UGm4mu74&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2Fw0-UGm4mu74%2Fhqdefault.jpg&key=7788cb384c9f4d5dbbdbeffd9fe4b92f&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/watch?v=w0-UGm4mu74",
  "title": "How to Connect your Chatbot to Telegram",
  "favicon": "https://www.google.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/w0-UGm4mu74/hqdefault.jpg",
  "provider": "youtube.com",
  "href": "https://www.youtube.com/watch?v=w0-UGm4mu74",
  "typeOfEmbed": "youtube"
}
[/block]


# Prerequisites

- A Telegram account and a Telegram bot
- A [Botpress Cloud account](https://sso.botpress.cloud) and a [Botpress Bot](https://botpress.com/docs/cloud/getting-started/create-and-publish-your-chatbot/)

## Create a Bot

To create a bot on Telegram, use Telegram's BotFather. The BotFather will ask you for a name and username, then generate an authorization token for your new bot

The name of your bot is displayed in contact details and elsewhere

The Username is a short name to be used in mentions and t.me links. Usernames are 5-32 characters long and are case insensitive but may only include Latin characters, numbers, and underscores. Your bot's username must end in `bot`, such as `tetris_bot` or `TetrisBot`

<br />

# Setting up the Telegram integration in Botpress

1. Go to the [Integration Hub](https://app.botpress.cloud/hub) in Botpress Cloud (if you don't have the integration installed yet).
2. Find and open the Telegram integration then click on the "Install to Bot" button, now go back to your bot settings.

The Telegram integration has the following settings:

- **Enabled**: Whether Botpress will communicate with Telegram
- **Webhook URL**: The URL for receiving data in Botpress
- **Bot Token**: The token of your Telegram bot

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

- To get the Telegram conversation ID, you can read the following variable:  
  `{{ event.tags.conversation["telegram:id"] }}`.

- To get the Telegram user ID, you can read the following variable:  
  `{{ event.tags.user["telegram:id"] }}`.

- To get the Telegram message ID, you can read the following variable:  
  `{{ event.tags.message["telegram:id"] }}`.