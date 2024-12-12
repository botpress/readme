---
title: Build
excerpt: Planning your bot project, setting goals, and testing your conversations.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Creating a chatbot with Botpress is a simple and intuitive process that can be accomplished by both technical and non-technical users. With a few straightforward steps, you can quickly set up an AI agent or chatbot.

## Creating a bot

1. Log in to [Botpress Cloud](https://app.botpress.cloud)
2. Click **+ New bot** and enter the Studio
3. Get creative.

In Botpress, each bot belongs to a <Glossary>Workspace</Glossary>. When you connect to Botpress Cloud for the first time, a default Workspace will be automatically created for you.

<br />

## Bot templates

Templates are pre-configured projects that contain predefined conversational flows, Knowledge Bases, and responses.

They serve as a starting point for building bots and can be customized to suit specific use cases. Botpress provides a collection of built-in templates that cover various scenarios and use cases, like customer support, sales, or an easy setup wizard.

These templates can be used as-is or modified according to the specific requirements of your chatbot.

### Using bot templates

When you enter Botpress Studio after creating a new bot, you'll be prompted to select from a Template or start building from scratch.

To access templates on an existing bot:

* In Botpress Studio, click on the Botpress icon located at the top-left corner, and select **Explore Bot Templates**.
* Choose the template you would like to use.

> 🚧 Warning: Overriding Template
>
> If you override an existing bot with a bot template, all the previous content and configurations of your bot will be erased and replaced with the new template.

<br />

## Testing your bot

Regularly testing the kinds of conversations end users will have with your bot is a crucial part of the building process.

There is a chat emulator built in the studio with which you can test your bot. It represents what your visitors will experience when they speak with your bot. You can reset the conversation by clicking the three dots at the top and selecting **New conversation** or **start as a new user**. **New conversation** will only remove temporary variables and start a new conversation while **start as a new user** will remove any variable saved with the user, starting the entire conversation from scratch.

You can get additional information from the Event Debugger to understand why your bot generated a specific answer or took a certain action.

The Event Debugger includes all sorts of useful information: the dialogue engine's elected suggestion, nodes flowed through, and natural language intents or questions. You can also view the raw JSON Payload that contains all details if you need further data. Additionally, your bot's logs record all events in the **Logs** tab of the bottom panel.