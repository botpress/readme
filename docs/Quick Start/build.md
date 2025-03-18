---
title: Quick Start
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

Let's start building!

# Step 1: Build your bot

## Create a new bot

1. Login to [Botpress Cloud](https://app.botpress.cloud).
2. Select **+ New bot** and choose a name for the bot (or randomly generate one).
3. Select **Open in** [Studio](https://botpress.com/docs/interface).
4. Start building!

> 📘 Workspaces
>
> In Botpress, each bot belongs to a <Glossary>Workspace</Glossary>. When you login for the first time, we create a default Workspace for you, but you can create others depending on your needs.
>
> To learn more about Workspaces, check out the [Workspace guide](tbc).

## Configure your bot's behaviour

In Botpress, you configure your bot's behavior using Workflows. A Workflow is a visual, drag-and-drop representation of the steps your bot follows when a user starts a new conversation.

> 📘 Custom Workflows
>
> Every bot comes with a few helpful default Workflows, but you can create custom Workflows to organize your project more easily. For more information, check out the [Workflows](tbc) page.

### Main Workflow

For now, let's take a look at the **Main** Workflow:

1. In Studio, select ![Workflows](https://files.readme.io/f71ca6c253bf9be22d54f9a436282c1dfd9b08296e058564badaab29be40b3c9-Screen_Shot_2025-03-17_at_14.30.48.png)**Workflows**  from the left navigation bar.
2. Select your **Main** Workflow. It should look something like this:

<Image align="center" src="https://files.readme.io/08eed5c2bec051bae8472a56d88ec73296b1deb7163cb9fb9f508ffb219541ec-Screen_Shot_2025-03-18_at_10.14.01.png" />

The **Main** Workflow contains the main logic for your bot. Each step your bot follows is represented by a Node.

By default, the **Main** Workflow contains:

* A <Glossary>Start Node</Glossary>
* An <Glossary>Autonomous Node</Glossary>
* An <Glossary>End Node</Glossary>

# Step 2: Deploy your bot

# Step 3: Monitor your bot