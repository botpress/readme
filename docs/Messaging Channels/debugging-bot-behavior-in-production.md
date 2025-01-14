---
title: Debugging Bot Behavior in Production
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/eab228a-image.png)

# Overview

There are a few different ways to debug your bot's behavior in production:

## Using the Conversations Tab (Simple)

The Conversations tab allows you to view the conversation history of your bot which is great for identifying problems. Check out [this page](../docs/see-your-bot-conversations) to learn more.

## Using Logs (Advanced)

If your bot is live and already has users it's recommended to duplicate the bot to debug its behavior. This will allow you to safely test and debug without affecting your live bot. To do this:

1. Export your bot by clicking the Botpress icon.
2. Select "Export" and save the exported file.
3. Go to [app.botpress.cloud](https://app.botpress.cloud) and log in or create an account.
4. Create a new bot within the platform.
5. Click the Botpress icon and select "Import from file".
6. Select the exported file and wait for the import.

### Using Text as Breakpoints in a Conversation

You can add Text Cards at different stages of the conversation to isolate problems:

1. Insert Text Cards in various parts of the conversation.
2. Deploy the bot to production and engage with it.
3. Observe where the conversation deviates from the expected behavior using the text cards as indicators.

### Using `console.log` in Logs

For more detailed debugging, utilize `console.log` statements in the logs:

1. Add Execute Code cards containing `console.log('message')` statements.
2. Replace `'message'` with relevant information or variables like `workflow.userName`.
3. Deploy the bot to production and trigger conversations.
4. Check the [Logs](../docs/admin-logs) tab to analyze the flow of the conversation and gather more information about the bot's behavior.
