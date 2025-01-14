---
title: SDK
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
# Installation

The SDK is an npm package that can be installed with the following command:

```
npm install @botpress/sdk # for npm
yarn add @botpress/sdk # for yarn
pnpm add @botpress/sdk # for pnpm
```

## Chatbot Development

The first step in developing a Bot with the SDK is to instantiate the Bot class as follows:

```ts
import { Bot } from "@botpress/sdk";

const bot = new Bot();

export default bot;
```

This is the minimal functional code that can be executed by Botpress as a Bot. It does absolutely nothing.

To add behavior to the Bot, you can register a message handler as follows:

```ts
bot.message("", async ({ message, client, ctx }) => {
  console.info("Received message", message);

  let responseText: string;
  if (message.payload.text === "/ping") {
    responseText = "Pong !";
  } else if (message.payload.text === "/order_pizza") {
    await orderPizza();
    responseText = "Pizza successfully ordered";
  } else {
    responseText = `Unknown command: ${message.payload.text} ...`;
  }

  await client.createMessage({
    conversationId: message.conversationId,
    userId: ctx.botId,
    tags: {},
    type: "text",
    payload: {
      text: responseText,
    },
  } satisfies CreateMessageBody<"text">);

  console.info("text message sent");
});
```

This handler will be called every time the Bot receives a message. It will then check the content of the message and send a response accordingly.

The Bot's constructor is what we call its definition. It contains information such as the Bot's configuration or the type of events the Bot can receive. The message handler, on the other hand, is part of the Bot's implementation. The Bot's definition restricts its implementation and influences intellisense during development.

The Bot's definition is described by the following fields:

* `tags`

  This field is used to specify the Tags used by the **Bot**.

  **Tags** are strings that allow to filter messages, conversations or users when querying the API.

* `states`

  This field is used to specify the **States** used by the **Bot**.

  **States** are used to persist data in between a **Bot**'s invocations.

  A **State** can be attached to a conversation, a user or can be global to the **Bot**.

  **States** have a schema, meaning that only the data that matches the schema can be persisted and retrieved.

* `integrations`

  This field is used to specify the **Integrations** installed in the **Bot**.

  **Integrations** are used to connect a **Bot** to external services.

  Disabled **Integrations** are not used by the ***Bot***. They can however be enabled later in the [CDM](https://app.Botpress.cloud) or through the [API](https://botpress.com/docs/api/).

  Setting an **Integration** in the **Bot**'s definition does two things:

  * it allows the **Integration** to call your **Bot** with events and messages.
  * it allows your **Bot** to call the **Integration** with actions.

* `configuration`

  This field is used to specify the schema of the **Configuration** provided to the **Bot** when it's called.

  The actual **Configuration** is provided by the user when deploying the **Bot**.

* `events`

  This field is used to specify the schema of the **Events** that can be sent to the **Bot** by **Integrations**.

  **Events** are just like messages, only they have a more general purpose, a custom schema and a wider use case.

* `recurringEvents`

  This field is used to specify **Recurring Events**.\
  **Recurring Events** are events that are sent to the **Bot** following a certain cron schedule.

Here's an example of a more complete Bot's definition:

```ts
const bot = new Bot({
  integrations: [
    {
      enabled: true,
      id: `${YOUR_INTEGRATION_ID}`,
      configuration: YOUR_INTEGRATION_CONFIGURATION,
    },
  ],
  configuration: {
    schema: {
      botName: z.string(),
    },
  },
  states: {
    profile: {
      type: "user",
      schema: {
        userName: z.string(),
      },
      expiry: 1000 * 60 * 60, // 1 hour
    },
  },
  tags: {
    users: ["inventoryAdmin"], // will allow to target users with the tag "inventoryAdmin"
  },
  events: {
    scheduledEvent: {
      schema: {},
    },
  },
  recurringEvents: {
    crawlInventory: {
      type: "scheduledEvent",
      payload: {},
      schedule: {
        cron: "*/5 * * * *", // crawl and sync inventory every 5 minutes
      },
    },
  },
});
```

In addition to the message handler, a Bot can also implement an event handler and an expired state handler as follows:

```ts
bot.event("scheduledEvent", async ({ event, client, ctx }) => {
  log.info("Received event", event);
});

bot.stateExpired("profile", async ({ state, client, ctx }) => {
  log.info("State expired", state);
});
```

## Integration Development

Integrations are developped in a similar fashion to Bots. The only difference is that there is 2 classes to instantiate: `IntegrationDefinition` and `Integration` wich stands for the Integration's implementation.

This means that a typical Integration's code would require at least 2 files. Here's an example:

```ts
// integration.definition.ts
import { IntegrationDefinition } from "@botpress/sdk";

export default new IntegrationDefinition({
  name: "myintegration",
  version: "0.1.0",
});

// integration.ts
import { Integration } from "@botpress/sdk";

export default new Integration({
  channels: {},
  actions: {},
  register: async ({ ctx }) => {
    console.info(`integration installed in bot ${ctx.botId}`);
  },
  unregister: async ({ ctx }) => {
    console.info(`integration uninstalled from bot ${ctx.botId}`);
  },
  handler: async ({ req }) => {
    console.info("received request from external service", req);
  },
});
```

The implementation code is actually the one that must be transpiled and bundled to run in Botpress Cloud, but the definition contains fields that are required when creating the Integration with the API. The reason why the definition and the implementation are separated might be obscure for now, but it will become clearer when introducing the CLI and the `generate` command.

Here's an example of a more complete Integration's definition with a proper implementation:

```ts
// integration.definition.ts
import * as sdk from "@botpress/sdk";
import { z } from "zod";

export default new sdk.IntegrationDefinition({
  name: "myintegration",
  version: "0.1.0",
  public: true,
  configuration: {
    schema: z.object({
      appId: z.string(),
      appSecret: z.string(),
    }),
  },
  channels: {
    channel: {
      messages: {
        text: sdk.messages.defaults.text,
        image: sdk.messages.defaults.image,
      },
      tags: {
        messages: ["id"],
        conversations: ["id"],
      },
    },
  },
  tags: {
    users: ["id"],
  },
  actions: {
    fetchInventory: {
      input: {
        schema: z.object({
          itemId: z.string(),
        }),
      },
      output: {
        schema: z.object({
          name: z.string(),
          price: z.number(),
        }),
      },
    },
  },
  events: {},
  states: {},
});

// integration.ts
import * as sdk from "@botpress/sdk";
import { ExternalService } from "@externalservice/client";

export default new sdk.Integration({
  register: async () => {},
  unregister: async () => {},
  actions: {
    fetchInventory: async (props) => {
      const { appId; appSecret } = props.ctx.configuration;
      const client = new ExternalService(appId, appSecret);
      const inventory = await client.fetchInventory(props.input.itemId);
      return {
        name: inventory.name,
        price: inventory.price,
      };
    },
  },
  channels: {
    channel: {
      messages: {
        text: async (props) => {
          const { appId; appSecret } = props.ctx.configuration;
          const client = new ExternalService(appId, appSecret);
          const convId = props.conversation.tags["myintegration:id"]
          await client.sendMessage(convId, { text: props.payload.text });
        },
        image: async (props) => {
          const { appId; appSecret } = props.ctx.configuration;
          const client = new ExternalService(appId, appSecret);
          const convId = props.conversation.tags["myintegration:id"]
          await client.sendImage(convId, { imageUrl: props.payload.imageUrl });
        },
      },
    },
  },
  handler: async ({ req, client }) => {
    if (!req.body) {
      log.warn("Handler received an empty body");
      return;
    }

    const activity: Activity = JSON.parse(req.body);
    log.info(`Handler received event of type ${activity.type}`);

    if (!activity.id) {
      return;
    }

    const convRef: Partial<ConversationReference> =
      TurnContext.getConversationReference(activity);

    switch (activity.type) {
      case "message":
        const { conversation } = await client.getOrCreateConversation({
          channel: "channel",
          tags: {
            [`${name}:id`]: activity.conversation.id,
          },
        });

        const { user } = await client.getOrCreateUser({
          tags: {
            [`${name}:id`]: activity.from.id,
          },
        });

        await client.createMessage({
          tags: { [`${name}:id`]: activity.id },
          type: "text",
          userId: user.id,
          conversationId: conversation.id,
          payload: { text: activity.text },
        });
        break;
      default:
        return;
    }
  },
});
```

The Integration's definition is described by the following fields:

* `name`

  The name of the Integration. It must be unique accross all Integrations.

* `version`

  The version of the Integration. It must be unique accross all versions of the same Integration.

  Currently, only the version `0.2.0` is allowed for public Integrations and `0.0.1` for private Integrations. This is a temporary limitation that will be lifted in a near future.

* `public`

  Whether the Integration is public or not. A public Integration can be installed by any Bot, while a private Integration can only be installed by Bots in the same workspace.

* `title`

  Display name of the Integration.

* `description`

  A description of the Integration.

* `icon`

  Path to an SVG file containing the Integration's icon. This path can either be absolute or relative to the Integration's working directory.

* `readme`

  Path to a Markdown file containing the Integration's documentation. This path can either be absolute or relative to the Integration's working directory.

* `tags`

  A list of tags that can be used to filter users when querying the API.

* `configuration`

  The configuration schema of the Integration. The actual configuration is provided by the bot when installing the Integration.

* `events`

  A map of events that can be emitted by the Integration. Events can be used to trigger handlers in the Bot.

* `actions`

  A map of actions that can be called by the Bot. Actions can be used to trigger handlers in the Integration. Actions are defined by their input and output schemas.

* `channels`

  A map of communication channels that can be used by the Bot send a message to the external service. Channels are defined by their messages types. The SDK provides a set of default messages types that can be used to send text, images, videos, etc.

* `states`

  Just like for Bots, Integrations can define states that can be used to store data. States are defined by their schema.

* `user`

  Allows the Integration to proactively create a user. This is usefull if the Integration needs to send a message to a user that has not yet interacted with the Bot.

The Integration's implementation must implement handlers for the defition's actions and channels as well as a handler for the external service's requests. The first two handlers are called by the Bot when an action or a message is triggered. The last handler is called by the external service when an event is triggered.
