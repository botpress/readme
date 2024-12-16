---
title: Adding Actions & Triggers to Botpress Studio
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
When you install an integration in your bot in Botpress Studio, you can add custom cards that run advanced JavaScript programs and triggers that listen for external events.

For this tutorial, we will add the capability for a bot to create a trackable URL that notifies the creator when it is used. You can follow the instructions below or follow along the video.

<Embed url="https://www.youtube.com/embed/5-vQGSOC2EE" title="Extending Botpress Studio - Actions and Triggers cards" favicon="https://www.youtube.com/favicon.ico" image="https://i.ytimg.com/vi/5-vQGSOC2EE/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/embed/5-vQGSOC2EE" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252F5-vQGSOC2EE%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253D5-vQGSOC2EE%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252F5-vQGSOC2EE%252Fhqdefault.jpg%26key%3D02466f963b9b4bb8845a05b53d3235d7%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22640%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

# Modify the Integration Definition

First, let's add the necessary configuration to your integration definition to enable the creation of trackable links and handle the trigger events.

## Step 1: Add Actions to Integration Definition

Add the following configuration schema to the `actions` property in your `integration.definition.ts`:

```ts
// integration.definition.ts
import { IntegrationDefinition, z } from '@botpress/sdk'; // make sure to add the z import

export default new IntegrationDefinition({
  // ...existing properties
  actions: {
    createTrackableLink: {
      title: 'Create Trackable Link',
      description: 'Takes a link as an input and returns a link that notifies the author when the link is clicked.',
      input: {
        schema: z.object({
          conversationId: z.string().describe('ID of the conversation'),
          originalLink: z.string().describe('URL of the link to be tracked'),
        }),
      },
      output: {
        schema: z.object({
          trackableLink: z.string().describe('URL of the trackable link'),
        })
      },
    }
  },
  // ...existing properties
});
```

The `actions` property defines the custom action `createTrackableLink` which takes a conversation ID and an original link as input, and returns a trackable link. 

## Step 2: Add Events to Integration Definition

Next, add the following configuration schema to the `events` property in your `integration.definition.ts`:

```ts
// integration.definition.ts
import { IntegrationDefinition, z } from '@botpress/sdk'; // make sure to add the z import

export default new IntegrationDefinition({
  // ...existing properties
  events: {
    clickedLink: {
      schema: z.object({
        conversationId: z.string().describe("ID of the conversation to notify the user"),
        originalLink: z.string(),
      })
    },
  },
  // ...existing properties
});
```

The `events` property defines the `clickedLink` event that is triggered when the trackable link is clicked.

<br />

# Add the Integration Logic

Now that we've defined the actions and triggers, let's implement the logic that creates the trackable link and handles the click event.

## Step 3: Implement Action Logic

Update your `src/index.ts` to handle the creation of trackable links:

```ts
// src/index.ts
import { Integration, z } from '@botpress/sdk'; // import the z import

export default new Integration({
    // ...existing properties
  actions: {
    createTrackableLink: async ({ input, ctx }) => {
      const { conversationId, originalLink } = input;
      const { webhookId } = ctx;
      const encodedInformation = btoa(JSON.stringify({ conversationId, originalLink }));
      const trackableLink = `https://webhook.botpress.cloud/${webhookId}?rd=${encodedInformation}`;

      return { trackableLink };
    },
  },
  // ...existing properties
});
```

This allows a user to add a "createTrackableLink" card in Botpress Studio, which takes a conversation ID and an original link as input. The output is saved to a variable, which contains the trackable link.\
We are using the btoa function to obfuscate the conversation ID and original link in the URL. We'll use in the next step to decode this information.

## Step 4: Implement Event Handler Logic

Next, add the handler code to your `src/index.ts` to handle the redirect:

```ts
// src/index.ts
import { Integration } from '@botpress/sdk';

export default new Integration({
  // ...existing properties
  handler: async ({ req, client }) => {
    // add this code to the handler function
    if (req.path === "" && req.method === "GET" && req.query.startsWith("rd=")) {
      const url = new URL(`https://example.com/?${req.query}`);
      const rd = url.searchParams.get("rd") ?? "";
      const decodedInformation = JSON.parse(atob(rd));
      const conversationId = decodedInformation.conversationId;
      const originalLink = decodedInformation.originalLink;

      // this reports back to the url creator that the link was clicked
      await client.createEvent({
        type: "clickedLink",
        payload: { conversationId, originalLink },
      });

      // this redirects the url-clicker to the original link
      return {
        status: 307,
        headers: { "content-type": "text/html" },
        body: `<http><head><meta http-equiv="Refresh" content="0; URL=${originalLink}" /></head></http>`,
      };
    }
    // ...existing logic
  },
  // ...existing properties
});
```

The handler function allows you to catch any http requests sent to the webhook URL and its sub paths. We use the if statement to catch relevant requests and allow other requests to be handled by other functions.\
The `createTrackableLink` action encodes the conversation ID and original link into a base64 string and creates a trackable link. The `handler` function decodes this information when the link is clicked, triggers the `clickedLink` event, and redirects the user to the original link.

<br />

# Create and Test the Action in Botpress Studio

Now, let's create and test the action in Botpress Studio.

## Step 5: Create the Action in Botpress Studio

1. **Create an Action:**
   * In Botpress Studio, create an action card.
   * Provide the URL as a string in the input and the current conversation ID like this: `"{{event.conversationId}}"`.
   * Save the output to a variable called `output`.
   * Create a text card with the text: `"This is the shareable URL: {{workflow.output.trackableLink}}"`.

2. **Create a Trigger:**
   * Right-click the workflow, click "Trigger", then select the `clickedLink` event.
   * In the created node, click it, then "Advanced settings", and put `{{event.payload.conversationId}}` in the conversation ID field.
   * Create a text card connected to the trigger node, and add `"A user has clicked your tracked link to {{event.payload.originalLink}}"`.

## Step 6: Test the Action and Trigger

To test the action and trigger, you must use a published bot outside the emulator:

1. **Publish the Bot:**
   * Ensure your bot is published and accessible.

2. **Test the Trackable Link:**
   * Interact with the bot to generate the trackable link.
   * Use the generated link.
   * Verify that the bot notifies the creator when the link is clicked.

Congratulations! You've successfully added and tested custom actions and triggers in Botpress Studio. Now, your bot can create trackable links and notify users when those links are clicked.