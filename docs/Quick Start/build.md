---
title: Create a Bot
excerpt: >-
  This quick start guide will help you build, deploy, and monitor your first
  bot.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
It's easy to build a bot with Botpress, even if you don't have a technical background. This guide will show you how to create a simple bot from start to finish. Your bot will:

* Use AI to respond to messages
* Follow custom instructions
* Have a unique, shareable link

# Step 1: Build your bot

## Add a new bot

1. Login to [Botpress Cloud](https://app.botpress.cloud).
2. Select **+ New bot** and choose a name for the bot (or randomly generate one).
3. Select **Open in** [Studio](https://botpress.com/docs/interface).
4. Start building!

> 📘 Workspaces
>
> In Botpress, each bot belongs to a <Glossary>Workspace</Glossary>. When you login for the first time, we create a default Workspace for you, but you can create others depending on your needs.
>
> To learn more about Workspaces, check out the [Workspace guide](tbc).

## Customize your bot's behaviour

In Botpress, you customize your bot's behavior using Workflows Every bot has a few helpful default Workflows, but you can create custom Workflows to organize your project more easily. For more information, check out the [Workflows](tbc) page.

For now, let's take a look at the **Main** workflow:

1. In Studio, select **Workflows**  from the left navigation bar.

## Test your bot

Regularly testing the kinds of conversations end users will have with your bot is a crucial part of the building process.

There is a chat emulator built in the studio with which you can test your bot. It represents what your visitors will experience when they speak with your bot. You can reset the conversation by clicking the three dots at the top and selecting **New conversation** or **start as a new user**. **New conversation** will only remove temporary variables and start a new conversation while **start as a new user** will remove any variable saved with the user, starting the entire conversation from scratch.

You can get additional information from the Event Debugger to understand why your bot generated a specific answer or took a certain action.

The Event Debugger includes all sorts of useful information: the dialogue engine's elected suggestion, nodes flowed through, and natural language intents or questions. You can also view the raw JSON Payload that contains all details if you need further data. Additionally, your bot's logs record all events in the **Logs** tab of the bottom panel.

# 2. Deploy your bot

# 3. Monitor your bot