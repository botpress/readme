---
title: Connect a live agent platform with Botpress
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: >-
    This document provides a step-by-step guide for setting up and implementing
    a Human-In-The-Loop (HITL) integration with Botpress, enabling seamless
    interaction between end-users and live agents by configuring the integration
    definition, implementing HITL logic, and handling message exchanges.
  keywords:
    - hitl
    - ' botpress'
    - ' live agent'
  robots: index
next:
  description: ''
---
This documentation will guide you through setting up and implementing a Human-In-The-Loop (HITL) integration with Botpress. By following these steps, you'll be able to connect your platform to Botpress, enabling seamless interaction between your end-users and live agents.

# How HITL Works in Botpress

In Botpress, the Human-In-The-Loop (HITL) functionality is powered by the HITL Agent. This agent consumes integrations that correctly implement the HITL interface, turning agent hand-off on and off.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a11417252c75c4771500955f4b4e6faff70b921c56efb9e292128189c2a57928-Screenshot_2024-09-16_at_10.45.05_AM.png",
        "",
        ""
      ],
      "align": "center",
      "sizing": "250px"
    }
  ]
}
[/block]


Here is an overview of the HITL workflow in Botpress:

- **When a conversation is escalated to a live agent:**
  1. A user is created on both Botpress and the third-party live chat platform. The link between the two users can be done on both sides, but we recommend doing it on Botpress's end using user [tags](#tags).
  2. A conversation is initiated on Botpress, and a corresponding ticket is created on the agent handoff platform. The link between the two conversations can be done on both sides, but we recommend doing it on Botpress's end using conversation [tags](#tags).

- **When the end user sends a message to a live agent:** The message is forwarded to the agent handoff platform through the "hitl" channel.

- **When the live agent sends a message to the end user:** The agent handoff platform calls the integration webhook, which then forwards the message to the end user.

This guide will teach you how to make your integration compatible with the HITL agent.

# Configuring the Integration Definition

After completing the steps in our [Quickstart Guide](https://botpress.com/docs/getting-started-1) and [installing the HITL interface](https://botpress.com/docs/how-to-install-botpress-packages), the next step is to enhance your integration definition to support HITL.

The following code snippet accomplishes the following:

1. Extends the HITL interface, making this integration compatible with HITL in Botpress.
2. Adds a HITL channel, which will be used to route messages between the end user and the live agent.
3. Enhances conversation and user tags with additional information, ensuring proper matching of users and conversations between Botpress and your platform.

```javascript integration.definition.ts
import { z, IntegrationDefinition, interfaces } from "@botpress/sdk";
import hitl from './bp_modules/hitl'

export default new IntegrationDefinition({
  name: "My HITL Integration",
  version: "0.0.1",
  readme: "hub.md",
  icon: "icon.svg",
  channels: {
    hitl: {
      title: "My HITL",
      messages: {},
      conversation: {
        tags: {
          ticketId: {
            // This is the ticket ID from your platform. It ensures that conversations are correctly matched between Botpress and your platform.
            title: "Ticket ID",
          },
          additionalData: {
            title: "You can pass additional data in the tags object.",
          },
        },
      },
    },
  },
  actions: {},
  user: {
    tags: {
      // This is the user ID from the live agent platform. It ensures that users are correctly matched between Botpress and live agent platform.
      agentHandoffPlatformUserId: {
        title: "Live Agent Platform User ID",
      },
    },
  },
  // Extend the HITL interface to implement HITL in your integration.
}).extend(hitl, () => ({}));

 
```

## Tags

Tags in this integration are customizable fields that can store any information relevant to a conversation or user. You can think of them as metadata. These tags are crucial for maintaining context and linking data between Botpress and your platform. While the examples provided focus on using IDs to match conversations and users, you can customize the tags to include any additional data that suits your needs.

# Implementing the HITL Logic

Now, let’s walk through the process of implementing the integration step by step. Start by adding the following code to `index.ts` to initialize the integration:

```javascript index.ts
import * as sdk from "@botpress/sdk";
import * as bp from ".botpress";

export default new bp.Integration({}); 
```

<br />

## 1. Add Register & Unregister Methods

These methods are part of the integration's lifecycle.

- **register:** This method is executed every time the integration configuration is saved. We use it to set a webhook that will be triggered when a live agent sends a message. If you manually set the webhook on the third-party platform, this step can be skipped.

- **unregister:** This method is executed when the integration is uninstalled. We use it to remove the Botpress webhook from the third-party platform. If the webhook was set manually, this step can be skipped.

```javascript index.ts
import * as sdk from "@botpress/sdk";
import * as bp from ".botpress";
import AgentHandoffPlatformClient from "./agent-handoff-client" 

export default new bp.Integration({
  register: async ({ webhookUrl }) => {
    // Set the webhook to be triggered when a live agent responds
    AgentHandoffPlatformClient.setWebhook(webhookUrl);
  },
  unregister: async ({ webhookUrl }) => {
    // Remove the webhook when the integration is uninstalled
    AgentHandoffPlatformClient.deleteWebhook(webhookUrl);
  }
});
```

The webhookUrl provided in the parameters points is unique to an bot integration installation. It's refreshed when an integration is installed/re-installed. There are three webhooks that you should implement in the handler method: handling agent messages, assign a conversation to an agent, and stopping HITL. If you can set up webhooks programmatically, this is the right place to do it.

## 2. Implement Actions

When extending the HITL interface, you need to implement a set of predefined methods, similar to how you implement methods when working with interfaces in TypeScript. Once these methods are correctly implemented, the integration can be used by the HITL Agent. These actions are automatically called by the HITL Agent and do not need to be triggered manually. You can rely on IntelliSense to guide you on the exact parameters provided to each action.

Here are the actions you need to implement:

- **createUser:** Creates a user in both Botpress and the third-party platform and maps them together. Then, the action returns the user ID of the created Botpress user. The mapping between the two users can be done on both sides, but we recommend doing it on Botpress's end using conversation [tags](#tags).

- **startHitl:** Creates a conversation in Botpress and a corresponding conversation (often called a ticket) on the third-party platform and maps them together. This action must return the ID of the created Botpress conversation. The mapping between the two conversations can be done on both sides, but we recommend doing it on Botpress's end using conversation [tags](#tags).

- **stopHitl:** Deletes a conversation on the third-party platform.

Here’s how you can implement these actions:

```javascript index.ts
// import a library to interact with the agent handoff platform
import AgentHandoffPlatformClient from "./agent-handoff-client" 

export default new bp.Integration({
  //...
  // Previously added code
  actions: {
    //...
    
    // create a user in both platforms
    createUser: async ({ client: botpressClient }) => {
      
      // Create a user on the agent handoff platform
      const userOnAgentPlatform = AgentHandoffPlatformClient.createUser();

      // Create a user on Botpress
      const { user: botpressUser } = await botpressClient.getOrCreateUser({
        tags: {
          // Link the Botpress user with the user on the agent handoff platform
          agentHandoffPlatformUserId: userOnAgentPlatform.id,
        },
      });

      return {
        userId: botpressUser.id, // always return the newly created botpress user id
      };
    },
    
    
    // create a conversation in both platforms
    startHitl: async ({ client: botpressClient, input }) => {
      const { user } = await botpressClient.getUser({
        // Retrieve the user ID created in the createUser action
        id: input.userId,
      });
      
      // These properties are provided from the "Escalate to a Human" action in the Studio
      const { title, description } = input;
			
      // Create a ticket on the agent handoff platform
      const ticket = AgentHandoffPlatformClient.createTicket({
        ticketTitle: title,
        ticketDescription: description,
      });

      // Create a conversation in Botpress
      const { conversation } = await botpressClient.getOrCreateConversation({
        channel: "hitl",
        tags: {
          // Link the ticket with the Botpress conversation
          ticketId: ticket.id,
        },
      });

      return {
        conversationId: conversation.id, // always return the newly created botpress conversation id
      };
    },
    
    
    // close the conversation in the agent handoff platform
    stopHitl: async ({ client: botpressClient, input }) => {
      const { conversation } = await botpressClient.getConversation({
        id: input.conversationId,
      });

      const ticketId = conversation.tags.ticketId;

      // Close the ticket on the agent handoff platform
      AgentHandoffPlatformClient.closeTicket({ ticketId });

      return {};
    },
    
    //...
  },
});
```

<br />

## 3. Send Messages from End User to Live Agent

To enable communication between the end user and the live agent, you'll need to add a special HITL channel that interacts with the third-party API.

```javascript
// index.ts

//...
export default new bp.Integration({
// Previously implemented code
  channels: {
    hitl: {
      messages: {
        // Send a message from the end user to the live agent
        text: async ({ client, conversation,  ...props }: bp.AnyMessageProps) => {
          const { text: userMessage } = props.payload;
					
          const externalUserId = payload.userId ? (await client.getUser({ id: payload.userId })).tags.externalId : "BOT";
          
          // Retrieve the ticket ID that was set in the startHitl action
          const ticketId = conversation.tags.ticketId;

          // Use the agent handoff platform's API to send the message
          AgentHandoffPlatformClient.sendMessage(ticketId, externalUserId, userMessage);
        },
        //...  you can add more message types if you want to support them
      },
    },
  },
});

 
```

We suggest starting with the text message type and adding more as needed. 

> 🚧 Watch out!
> 
> `payload.userId` is the user id of the chat-user as seen from the HITL conversation. `user.id` is the id of the bot. If you want the agent to know who he's talking to, you must use `payload.userId`.

## 4. Send Messages from Live Agent to End User

When a live agent responds, the live-agent platform needs to send a request to the integration's webhook URL. Upon receiving this request, a special **handler** method is triggered. Let's implement this method to forward the message to the end user.

```javascript index.ts
// ...
export default new bp.Integration({
  // ...previously implemented logic
  handler: async ({ req, client: botpressClient, ctx, logger }) => {
    const liveAgentEvent = JSON.parse(req.body);
    
    // Fetch the Botpress user based on the user ID from the third-party platform
    const { user } = await botpressClient.getOrCreateUser({
      tags: {
        agentHandoffPlatformUserId: liveAgentEvent.userId,
      },
    });

    // Fetch a conversation in Botpress associated with the ticket ID
    const { conversation } = await botpressClient.getOrCreateConversation({
      channel: 'hitl',
      tags: {
        ticketId: liveAgentEvent.ticketId,
      },
    });

    switch (liveAgentEvent.eventType) {
      case 'newMessage':
        // Send the received message from the live agent to the end user
        await botpressClient.createMessage({
          type: 'text',
          userId: user.id,
          conversationId: conversation.id,
          payload: { text: liveAgentEvent.message },
        });

        break;
    }
  },
});
```

In the above example, we don't check the route, or method, but we can do that with the `req` parameter of the handler, which returns an express.js-like request object. You can add `if` conditions to route different actions you'd like, such as assigning agents, or releasing the user back to the bot.

> 📘 Why do I keep seeing getOrCreate?
> 
> We don't actually want to create users or conversations at this point. Its simply a matter of the `get` methods not supporting finding by tags, while the `getOrCreate` methods do.

<br />

## 5. Inform Bot When HITL Started and Stopped

We need to emit two events to inform the bot about the status of the Human-In-The-Loop (HITL) process:

**hitlAssigned**: Tells the bot that the conversation has been successfully escalated to a live agent.  
**hitlStopped**: Tells the bot that the conversation with the live agent has ended.

```coffeescript index.ts
// index.ts

// ...

export default new bp.Integration({
  // ...previously implemented logic

  handler: async ({ req, client: botpressClient, ctx, logger }) => {
    const liveAgentEvent = JSON.parse(req.body);

    switch (liveAgentEvent.eventType) {
      case 'newMessage':
        // ...
        break;

      case 'ticketAssigned':
        // Emit an event to inform the bot that HITL has been assigned
        await botpressClient.createEvent({
          type: 'hitlAssigned',
          payload: {
            conversationId: conversation.id,
            userId: user.id,
          },
        });
        break;

      case 'ticketSolved':
        // Emit an event to inform the bot that HITL has been stopped
        await botpressClient.createEvent({
          type: 'hitlStopped',
          payload: {
            conversationId: conversation.id,
          },
        });
        break;
    }
  },
});

```

<br />

# Full Example

```
// index.ts

import * as sdk from "@botpress/sdk";
import * as bp from ".botpress";

// Replace with your actual platform client library
import AgentHandoffPlatformClient from "./agent-handoff-client";

// Initialize the integration
export default new bp.Integration({
  // Register method to set the webhook when configuration is saved
  register: async ({ webhookUrl }) => {
    // Set the webhook to be triggered when a live agent responds
    AgentHandoffPlatformClient.setWebhook(webhookUrl);
  },

  // Unregister method to remove the webhook when integration is uninstalled
  unregister: async ({ webhookUrl }) => {
    // Remove the webhook when the integration is uninstalled
    AgentHandoffPlatformClient.deleteWebhook(webhookUrl);
  },

  // Define the HITL actions
  actions: {
    // Create a user on both Botpress and the agent handoff platform
    createUser: async ({ client: botpressClient }) => {
      // Create a user on the agent handoff platform
      const userOnAgentPlatform = AgentHandoffPlatformClient.createUser();

      // Create a user on Botpress
      const { user: botpressUser } = await botpressClient.getOrCreateUser({
        tags: {
          // Link the Botpress user with the user on the agent handoff platform
          agentHandoffPlatformUserId: userOnAgentPlatform.id,
        },
      });

      return {
        userId: botpressUser.id,
      };
    },

    // Start a HITL session by creating a conversation on both platforms
    startHitl: async ({ client: botpressClient, input }) => {
      const { user } = await botpressClient.getUser({
        // Retrieve the user ID created in the createUser action
        id: input.userId,
      });

      // These properties are provided from the "Escalate to a Human" action in the Studio
      const { title, description } = input;

      // Create a ticket on the agent handoff platform
      const ticket = AgentHandoffPlatformClient.createTicket({
        ticketTitle: title,
        ticketDescription: description,
      });

      // Create a conversation in Botpress
      const { conversation } = await botpressClient.getOrCreateConversation({
        channel: "hitl",
        tags: {
          // Link the ticket with the Botpress conversation
          ticketId: ticket.id,
        },
      });

      return {
        conversationId: conversation.id,
      };
    },

    // Stop a HITL session by closing the conversation on the agent handoff platform
    stopHitl: async ({ client: botpressClient, input }) => {
      const { conversation } = await botpressClient.getConversation({
        id: input.conversationId,
      });

      const ticketId = conversation.tags.ticketId;

      // Close the ticket on the agent handoff platform
      AgentHandoffPlatformClient.closeTicket({ ticketId });

      return {};
    },
  },

  // Define the HITL channel to send messages from the end user to the live agent
  channels: {
    hitl: {
      messages: {
        // Send a message from the end user to the live agent
        text: async ({ client, payload }) => {
          const { text: userMessage, conversation, userId } = payload;

          // Retrieve the ticket ID that was set in the startHitl action
          const ticketId = conversation.tags.ticketId;

          // Use the agent handoff platform's API to send the message
          AgentHandoffPlatformClient.sendMessage(ticketId, userId, userMessage);
        },
      },
    },
  },

  // Handler to process messages sent from the live agent to the end user
  handler: async ({ req, client: botpressClient }) => {
    const liveAgentEvent = JSON.parse(req.body);

    // Fetch the Botpress user based on the user ID from the agent handoff platform
    const { user } = await botpressClient.getOrCreateUser({
      tags: {
        agentHandoffPlatformUserId: liveAgentEvent.userId,
      },
    });

    // Retrieve or create a conversation in Botpress associated with the ticket ID
    const { conversation } = await botpressClient.getOrCreateConversation({
      channel: "hitl",
      tags: {
        ticketId: liveAgentEvent.ticketId,
      },
    });

    switch (liveAgentEvent.eventType) {
      case "newMessage":
        // Send the received message from the live agent to the end user
        await botpressClient.createMessage({
          type: "text",
          userId: user.id,
          conversationId: conversation.id,
          payload: { text: liveAgentEvent.message },
        });
        break;

      case "ticketAssigned":
        // Emit an event to inform the bot that HITL has been assigned
        await botpressClient.createEvent({
          type: "hitlAssigned",
          payload: {
            conversationId: conversation.id,
            userId: user.id,
          },
        });
        break;

      case "ticketSolved":
        // Emit an event to inform the bot that HITL has been stopped
        await botpressClient.createEvent({
          type: "hitlStopped",
          payload: {
            conversationId: conversation.id,
          },
        });
        break;
    }
  },
});
```

<br />

# Production Example

For a production-grade implementation, you can refer to the Zendesk integration maintained by the Botpress team.  Check it out [here](https://github.com/botpress/botpress/tree/master/integrations/zendesk).

<br />

# Having difficulties with HITL Interfaces?

Contact us at [hitl-help@botpress.com](mailto:hitl-help@botpress.com) with as much details as possible about your company and your use case.