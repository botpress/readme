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
  description: 'Congratulations on building your first bot with Botpress! '
---
It's easy to build a bot with Botpress, even if you don't have a technical background. This guide will show you how to create a simple bot from start to finish. Your bot will:

* Display a custom greeting
* Use AI to respond to messages
* Follow specific instructions
* Have a unique, shareable link

> 📘 Keep learning!
>
> This guide is designed to teach a total beginner how to deploy their first bot. If you have more questions and want to get creative with bot-building, check out the[ Learn section](tbc) for detailed how-to guides.

# Step 1: Build your bot

## Create a new bot

1. Login to [Botpress Cloud](https://app.botpress.cloud).
2. Select **+ New bot** and choose a name for the bot (or randomly generate one).
3. Select **Open in** [Studio](https://botpress.com/docs/interface).
4. Start building!

## Configure your bot's behavior

Let's add some custom behavior to our bot. In Botpress, you configure your bot's behavior using Workflows. A Workflow is a visual, drag-and-drop representation of the steps your bot follows during a conversation with a user.

Each step in a Workflow is represented by a Node. Let's open the **Main** Workflow and take a look at its Nodes:

1. In Studio, select![Workflows](https://files.readme.io/f71ca6c253bf9be22d54f9a436282c1dfd9b08296e058564badaab29be40b3c9-Screen_Shot_2025-03-17_at_14.30.48.png)**Workflows**  from the left navigation bar.
2. Select your **Main** Workflow. It should look something like this:

<Image align="center" src="https://files.readme.io/08eed5c2bec051bae8472a56d88ec73296b1deb7163cb9fb9f508ffb219541ec-Screen_Shot_2025-03-18_at_10.14.01.png" />

The **Main** Workflow contains the main logic for your bot — it executes as soon as a user starts a new conversation. By default, the **Main** Workflow contains:

* A <Glossary>Start Node</Glossary>
* An <Glossary>Autonomous Node</Glossary>
* An <Glossary>End Node</Glossary>

Notice the path connecting the Start Node and the Autonomous Node:

<Image align="center" src="https://files.readme.io/50ce2e6c6a41d9d25c90a238a045ce7d1414dc0cab8d422c5a5296549b7f7ec6-Screenshot_2025-03-18_at_1.56.53_PM.png" />

This is a transition. When someone starts a conversation with your bot, it will first execute the Start Node, then transition to the Autonomous Node.

### Add a custom greeting

Let's create a new Node to add a custom greeting to our bot:

1. Click and hold the right edge of the Start Node. Then, drag outwards to create a new transition.
2. Release anywhere on the canvas. You will see a list of Node types to choose from — select **Standard Node**.

You just created a new Node! Notice that since you dragged out from the edge of the Start Node, it automatically transitions to the Start Node.

# Step 2: Deploy your bot

# Step 3: Monitor your bot