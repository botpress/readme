---
title: Import & Export
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
You may want to import or export a bot for various reasons, such as:

- Sharing the bot with others - friends, clients, etc.
- Contributing the bot to the community
- Seeking help to fix issues
- Creating a backup of the bot
- Transferring the bot to a different workspace or account

And with Botpress Cloud, you can do that with just a few clicks!

# How to Export a Bot

On the left panel in your Botpress Studio, click the Botpress icon and select Import / Export. Then click Export as.

Studio will start preparing the export, which may take some time, depending on the amount of content in your tables and knowledge bases. When it is done, the download will start automatically.

> ❗️ Error
> 
> Bots ~3gb or larger cannot be exported!

The exported file will be a `.bpz` file (which is a special archive format for Botpress Cloud bots). It will have the name of your bot and the current date (for example: recipe-bot - 2023 Sep 06.bpz).

> 🚧 Warning
> 
> Do not attempt to extract the file or modify its content, otherwise you may not be able to import your bot again!

The exported file contains your whole bot, including:

- Bot information and settings
- Agents settings
- Knowledge bases - with sources (files are stored on our servers and only linked in the export to keep it small)
- Tables - with records
- Intents and entities
- Hooks
- Variables (workflow, user, bot, config) - names and default values
- Folders
- Workflows and nodes
- Cards - with content
- Transition lines

So you can rest assured that all of your data is included!

# How to Import a Bot

> ❗️ Error
> 
> Importing a bot will overwrite the current bot, including media, knowledge bases, documents and tables. Proceed with caution!

On the left panel in your Botpress Studio, click the Botpress icon and select Import / Export. Then click Import. Next, click "Select bot archive to upload" and the explorer window will open. Find the `.bpz` file you want to import on your computer and click Open.

You have now successfully imported your bot! Test it using the Emulator or publish it to make it available to your users.

> 👍 Good to know
> 
> You can import bots up to 120 MB!

> 📘 Restoring the Integrations
> 
> Remember to set up the desired integrations again in the Dashboard, so that it works on the channels exactly as it did before you exported it!

# Video tutorial

[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2FgaralsWay1U%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DgaralsWay1U&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2FgaralsWay1U%2Fhqdefault.jpg&key=02466f963b9b4bb8845a05b53d3235d7&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/embed/garalsWay1U?si=S9J8kk6WckEAmxaw",
  "title": "Import and Export",
  "favicon": "https://www.youtube.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/garalsWay1U/hqdefault.jpg",
  "provider": "https://www.youtube.com/",
  "href": "https://www.youtube.com/embed/garalsWay1U?si=S9J8kk6WckEAmxaw",
  "typeOfEmbed": "youtube"
}
[/block]