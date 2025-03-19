---
title: Quick Start
excerpt: Build, test, and deploy your first bot.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: 'Congratulations on building your first bot with Botpress! '
---
It's easy to build a bot with Botpress, even if you don't have a technical background. This guide will teach you to create a simple bot from start to finish. Your bot will:

* Display a custom greeting
* Use AI to respond to messages
* Follow specific instructions
* Have a unique, shareable link

> 📘 Keep learning!
>
> This guide is designed to teach a total beginner how to deploy their first bot. If you have more questions and want to get creative with bot-building, check out the[ Learn section](tbc) for detailed how-to guides.
>
> For detailed explanations of any of the concepts introduced on this page, check out our [Concepts](tbc) guide.

# Step 1: Build your bot

## Create a new bot

1. Login to [Botpress Cloud](https://app.botpress.cloud).
2. Select **+ New bot** and choose a name for the bot (or randomly generate one).
3. Select **Open in** [Studio](https://botpress.com/docs/interface).
4. Start building!

## Configure your bot's behavior

Let's add some custom behavior to your bot. In Botpress, you configure your bot's behavior using Workflows. A Workflow is a drag-and-drop canvas that represents the steps your bot follows during a conversation with a user.

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

This is a transition. When someone starts a conversation with your bot, it first executes the Start Node, then transitions to the Autonomous Node.

> 📘 TIp: Drag Nodes
>
> You can drag a Node to move it anywhere in your Workflow. Just select and hold the Node, then drag and release wherever you want to move it.
>
> Moving a Node doesn't affect your bot's behavior — it just helps keep your Workflow organized.

### Display a custom greeting

Let's create a new Node to add a custom greeting to your bot.

First, we need to create a new <Glossary>Standard Node</Glossary>:

1. Select and hold the **right edge** of the Start Node.
2. Drag outwards to create a new transition.
3. Release anywhere on the canvas. You'll see a list of Node types to choose from — select **Standard Node**.

You just created a new Node! Notice that because you dragged out from the edge of the Start Node, it automatically transitioned to the new Node:

<Image align="center" src="https://files.readme.io/36f337ad98b4d45ff0f0a24a3dc6b1e8f525a2fa6120013a7f67afb1c200db34-Screenshot_2025-03-18_at_3.33.18_PM.png" />

Next, let's add the greeting. To do this, we need to add a <Glossary>Card</Glossary> to the new Node:

1. In the new Node, select **Add Card**. This opens the Cards menu.
2. Select the **Text** Card.
3. In the **Message to send** field, enter a custom greeting. For this guide, we'll enter "Hello! I'm Teddy, the helpful bot!":

<Image align="center" src="https://files.readme.io/49ceb15c84e25ab38083ad13de261dcd02521046a1d1818dbc9038aa0df4f074-Screenshot_2025-03-19_at_9.33.40_AM.png" />

Now your bot has a custom greeting! Before wrapping up, let's connect the new Node to the Autonomous Node:

1. Select and hold the **right edge** of the new Node.
2. Drag outwards to create a new transition.
3. Release on the **left edge** of the Autonomous Node.

This creates a transition from the new Node to the Autonomous Node, so your bot continues the conversation after displaying the greeting:

<Image align="center" src="https://files.readme.io/c5c8820baf0c7c4823bf5fdb48e5218c1cfec1f87dc76b983ada2181587a8824-Screenshot_2025-03-18_at_4.39.44_PM.png" />

### Add custom instructions

Now that your bot has a greeting, let's add some custom instructions for when it's interacting with a user. From the Autonomous Node, open the **Instructions** section.

By default, this field contains a detailed list of natural language instructions for your bot. You can modify these, or start from scratch with your own instructions.

For now, let's just tell your bot its name. Erase everything in the **Instructions** section, and enter "You are Teddy, a helpful bot":

<Image align="center" src="https://files.readme.io/acd51c4db5dfd71ab17953f747e7e821353d5634acd63cfe1822e306f7fa329f-Screenshot_2025-03-18_at_5.00.27_PM.png" />

# Step 2: Test your bot

# Step 3: Deploy your bot