---
title: Building a Custom Integration
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
# Introduction

Are you keen to leverage the powerful capabilities of Botpress combined with your favorite applications? You're in the right place. This step-by-step guide will take you through the procedure of crafting a customized integration in Botpress. Integrations like these can supercharge your business operations, streamlining tasks, automating workflows, and enhancing productivity. For instance, you could:

* Integrate your customer relationship management system to effectively manage users and conversations via Botpress.
* Connect your e-commerce platform to optimize order tracking, customer communication, and invoice processing via your bots.
* Use analytics tools to track bot performance and user engagement in real-time.

This guide will primarily focus on integrating with ClickUp, a highly-respected project management tool. By creating this integration, you can automate task assignments, boost team collaboration, and streamline project management in your organization. If you're ready to unlock a whole new level of productivity, let's dive in!

<br />

# Prerequisites

To follow this guide and build your own integration, ensure you have the following:

* A Botpress account
* A ClickUp account
* A code editor, such as Visual Studio Code or Sublime Text
* Node.js Package Manager (npm) installed. Please use Node version `18`. You can check your Node version by running `node --version` in your terminal.
* Ensure pnpm is installed and is on version 8. Check with `pnpm --version`. If not, install it following [these instructions](https://pnpm.io/installation).

## Setup

These steps should be done for every integration you create and are not specific to the ClickUp example.

1. `pnpm dlx @botpress/cli init`  - For Initialising the integrations template
2. select `integration` when prompted, and give it a name
3. `cd <integration-name>` - to go into the integration folder
4. `pnpm install @botpress/sdk @botpress/client zod axios` - sdk for botpress, client for clickup, zod for validation, axios for http requests
5. `pnpm install -D @botpress/cli typescript @types/node ts-node` - dev dependencies for botpress cli, typescript, node, ts-node
6. (recommended) initialize git and commit. This will help you track changes and revert if needed.
7. Add the following scripts to your package.json file:

```json
"scripts": {
    "version": "bp --version",
    "login": "bp login",
    "gen": "bp gen",
    "deploy": "bp deploy"
  },
```

## Writing the Integration

Building an integration with Botpress is a straightforward process. It involves setting up a few key files that define the integration's behavior and interactions. In this guide, we'll walk you through the process of creating an integration with ClickUp, a popular project management tool. 

There are two files you will work with.

* The main logic of your application lies in `index.ts`. This will be used to handle the creation of tasks, registration, and unregistration of the integration, webhook handling, and sending messages to ClickUp.
* The second important file is `integration.definition.ts`. This will be used to define the integration's name, version, configuration, events, actions, channels, messages, and user tags. This allows bot builders to have code completion within the Botpress Studio. 

### The Blueprint: integration.definition.ts

Every integration starts with a blueprint, a file that outlines the structure and behavior of the integration. In Botpress, this blueprint is the `integration.definition.ts` file. This file specifies the integration's name, version, configuration, events, actions, icon, channels, messages, and user tags. 

Let's take a look at the `integration.definition.ts` file for our ClickUp integration:

```ts
// Import necessary modules and definitions
import { IntegrationDefinition } from '@botpress/sdk'; // This imports the IntegrationDefinition class from Botpress SDK.
import z from 'zod'; // This imports zod, a library used for building schemas.

// Note: if you have issues related to the name of the integration, try importing it from another file.
const INTEGRATION_NAME = "clickup"

// This is where we define our integration using the IntegrationDefinition class.
export default new IntegrationDefinition({
    // The name and version of the integration are defined here.
    name: INTEGRATION_NAME, 
    version: '0.2.0',
    
    // This is where we define the configuration schema for our integration.
    configuration: {
        schema: z.object({
            apiKey: z.string(), // Defines that apiKey should be a string.
            teamId: z.string(), // Defines that teamId should be a string.
        })
    },
    
    // Events that our integration can handle are defined here.
    events: {
        taskCreated: {
            schema: z.object({id: z.string()}) // Defines the schema for taskCreated event.
        },
    },
    
    // Actions that our integration can perform are defined here.
    actions: {
        createTask: {
            input: {
                schema: z.object({
                  // Defines the input schema for creating a task.
                  listId: z.string(), 
                  name: z.string(), 
                  description: z.string().optional() // Description is optional.
                })
            },
            output: {
                schema: z.object({id: z.string()}) // Defines the output schema of creating a task.
            }
        }
    },
    
    // Specifies the icon of the integration.
    icon: 'icon.svg',
    
    // This is where we define channels and their messages, tags, etc.
    channels: {
        comment: {
            messages: {
                text: {
                    schema: z.object({text: z.string()}) // Defines the schema for text messages.
                }
            },
            message: {
                tags: {
                    id: {
                        title: "Message ID", // The title of the Message ID tag.
                        description: "Message ID from ClickUp", // Describes what the Message ID tag is.
                    }
                }
            },
            conversation: {
                tags: {
                    taskId: {
                        title: "Task ID", // The title of the Task ID tag.
                        description: "Task ID from ClickUp", // Describes what the Task ID tag is.
                    }
                }
            }
        }
    },
    
    // Defines the user tags for our integration.
    user: {
        tags: {
            id: {
                title: "User ID", // The title of the User ID tag.
                description: "User ID from ClickUp", // Describes what the User ID tag is.
            }
        }
    }
});
```

### The Engine: index.ts

The `index.ts` file is the engine of your integration. It contains the logic that drives the integration's behavior, handling tasks such as creating tasks, registering and unregistering the integration, handling webhooks, and sending messages to ClickUp.

Here's what the `index.ts` file looks like for our ClickUp integration:

```ts
// Importing necessary modules, classes, and types.
import { Integration } from ".botpress";
import { ClickUpClient } from "./client";
import { comment } from ".botpress/implementation/channels";

// Declaring and exporting the Integration instance with defined actions, register methods, handlers, and channels.
export default new Integration({
    // Declaring actions that the integration can perform.
    actions: {
        createTask: async({ ctx, input }) => { 
            // Initializing ClickUpClient with necessary configurations.
            const clickup = new ClickUpClient(ctx.configuration.apiKey, ctx.configuration.teamId)
            // Creating a task and returning its ID.
            const task = await clickup.createTask(input)
            return { id: task.id }
        }
    },
    // Declaring the register method to enable and save the integration.
    register: async ({ctx, logger, webhookUrl}) => { 
        logger.forBot().info('ClickUp integration enabled')
        const clickup = new ClickUpClient(ctx.configuration.apiKey, ctx.configuration.teamId)
        
        // Fetching the user and registering the webhook.
        await clickup.getUser()
        await setWebhook(clickup, webhookUrl)
    },
    // Declaring the unregister method to delete the integration (not disable).
    unregister: async () => { },
    // Declaring the handler to manage incoming events from ClickUp.
    handler: async ({ctx, req, client, logger}) => { 
        if (!req.body) return;
        const body = JSON.parse(req.body)

        // Processing taskCommentPosted events.
        if (body.event === "taskCommentPosted") {
            const clickup = new ClickUpClient(ctx.configuration.apiKey, ctx.configuration.teamId)
            const botUser = await clickup.getUser()

            // Processing history items from ClickUp.
            for (const historyItem of body.history_items) {
                if(botUser.id === historyItem.user.id) continue;
                
                // Creating or fetching users, conversations, and messages from Botpress.
                const { user } = await client.getOrCreateUser({ tags: {"id": historyItem.user.id.toString()} })
                const { conversation } = await client.getOrCreateConversation({ channel: "comment", tags: {"taskId": body.task_id.toString()} })
                const { message } = await client.getOrCreateMessage({
                    conversationId: conversation.id,
                    userId: user.id,
                    type: "text",
                    payload: { text: historyItem.comment.text_content },
                    tags: {"id": historyItem.comment.id.toString()}
                })

                logger.forBot().debug(`Received comment from ClickUp: ${message.payload.text}`)
            }
        }
    },
    // Declaring channels and their message handling logic.
    channels: {
        comment: {
            messages: {
                text: async ({ctx, conversation, ack, payload, logger}) => { 
                    // Sending a text message to ClickUp from Botpress.
                    const clickup = new ClickUpClient(ctx.configuration.apiKey, ctx.configuration.teamId)
                    const comment = await clickup.createComment({ text: payload.text, taskId: conversation.tags["clickupnew:taskId"]! })
                    
                    logger.forBot().debug(`Comment Logs: ${comment}`)
                    logger.forBot().debug(`Logs:${payload.text}`)
                    await ack({tags: {"clickupnew:id": comment.id.toString()}})
                }
            }
        }
    }
})

// Function to set webhook for the ClickUp events.
async function setWebhook(clickup: ClickUpClient, webhookUrl: string) {
    const webhooks = await clickup.listWebhooks()
  
    for (const webhook of webhooks) {
        if (webhook.endpoint === webhookUrl) {
            await clickup.updateWebhook({
              endpoint: webhookUrl,
              status: 'active',
              webhookId: webhook.id,
              events: ['taskCommentPosted', 'taskCreated']
            })
            return
        }
    }
    await clickup.createWebhook({ endpoint: webhookUrl, events: ['taskCommentPosted', 'taskCreated'] })
}
```

Notice we import a client.ts module. We'll cover that next.

### The Helper: client.ts

The `client.ts` file is an optional helper file that manages the interaction with the ClickUp API. It contains a set of predefined functions that handle requests and responses, making API calls more manageable and organized. If you are using an external library to handle your external service, you could call that from index.ts and skip this file.

```ts
// Importing necessary modules and defining the baseURL of the ClickUp API.
import axios, { AxiosInstance } from 'axios'
const baseURL = 'https://api.clickup.com/api/v2'

// Declaring the ClickUpClient class.
export class ClickUpClient {
  private axios: AxiosInstance  // Instance of Axios to make HTTP requests.

  // Constructor to initialize the ClickUpClient with token and teamId.
  constructor(private token: string, private teamId: string) {
    this.axios = axios.create({
      baseURL,  // Setting the base URL for the API.
      headers: { Authorization: this.token },  // Setting the Authorization header with the token.
    })
  }

  // Method to get user information.
  async getUser() {
    const { data } = await this.axios.get('/user')
    return data.user
  }

  // Method to list all the webhooks.
  async listWebhooks() {
    const { data } = await this.axios.get(`/team/${this.teamId}/webhook`)
    return data.webhooks
  }

  // Method to create a new webhook.
  async createWebhook(body: { endpoint: string, events: string[] }) {
    const { data } = await this.axios.post(`/team/${this.teamId}/webhook`, body)
    return data
  }

  // Method to update an existing webhook.
  async updateWebhook({ webhookId, ...body }: { webhookId: string, endpoint: string, events: string[]; status: 'active' }) {
    const { data } = await this.axios.put(`/webhook/${webhookId}`, body)
    return data
  }

  // Method to create a new comment on a task.
  async createComment({ taskId, text }: { taskId: string, text: string }) {
    const user = await this.getUser()
    const { data } = await this.axios.post(`/task/${taskId}/comment`, { comment_text: text, notify_all: false, assignee: user.id })
    return data
  }

  // Method to create a new task in a list.
  async createTask({ name, description, listId }: { listId: string; name: string, description?: string }) {
    const { data } = await this.axios.post(`/list/${listId}/task`, { name, description })
    return data
  }

  // Method to get information about a task.
  async getTask(taskId: string) {
    const { data } = await this.axios.get(`/task/${taskId}`)
    return data
  }
}
```

And that's it! You've now set up the main files required for a Botpress integration. With these files in place, you can start building out your integration's functionality and interactions. Happy coding!

## Important CLI Commands

* `pnpm dlx @botpress/cli build` - Use this to build the integration
* `pnpm run deploy` - Use this to deploy the integration. 
* `pnpm run deploy -y` - Use this to deploy the integration without confirmation.
* `pnpm dlx @botpress/cli login`  - Use this to login to your botpress account. You will need to generate a personal access token from your botpress account. Go to Admin Dashboard → Profile → Personal Access Token. Generate a new one and paste it in the CLI.

<br />

# Video Tutorials

Kickstart your journey by watching our comprehensive video series on building a ClickUp integration with Botpress. Our in-house experts walk you through the entire process, from the initial setup to handling outgoing messages.

***

## Part 1: Setup and Definitions

In the first part of this series, we delve deep into the process of laying the groundwork for a successful ClickUp-Botpress integration. Learn how to properly set up your environment, define your channels, messages, and tags, as well as generate the required code using the intuitive Botpress Command Line Interface (CLI).

<Embed url="https://www.youtube.com/embed/uXRQuBl1r2U?si=SgPFtY2WWTETTr0f" title="EP 01: Building Integrations" favicon="https://www.youtube.com/favicon.ico" image="https://i.ytimg.com/vi/uXRQuBl1r2U/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/embed/uXRQuBl1r2U?si=SgPFtY2WWTETTr0f" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FuXRQuBl1r2U%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DuXRQuBl1r2U%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FuXRQuBl1r2U%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

***

## Part 2: Setting Up Webhooks and Handling Messages

Join us in the second portion of our series as we delve deeper into the complexities of building an effective integration. Learn expert techniques on setting up webhooks, managing incoming messages from ClickUp, and priming your system for sending responses back to the platform.

<Embed url="https://www.youtube.com/embed/Q-wV112_rOw?si=HbeJOP7Iom8tZCww" title="EP 02: Continuing to build the ClickUp integration" favicon="https://www.youtube.com/favicon.ico" image="https://i.ytimg.com/vi/Q-wV112_rOw/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/embed/Q-wV112_rOw?si=HbeJOP7Iom8tZCww" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FQ-wV112_rOw%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DQ-wV112_rOw%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FQ-wV112_rOw%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

***

## Part 3: ClickUp Integration Final Build

In the concluding video of our three-part series, see how we tie everything together to finish building a seamless ClickUp integration. Gain insights on how to handle outgoing messages, create tasks, and set up listeners for events within ClickUp. This is an all-inclusive tutorial that offers a thorough exploration of building powerful integrations in Botpress.

<Embed url="https://www.youtube.com/embed/1D3aC_asXYA?si=hpFdcIYnWVKEkgbT" title="EP 03: Finishing the ClickUp integration" favicon="https://www.youtube.com/favicon.ico" image="https://i.ytimg.com/vi/1D3aC_asXYA/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/embed/1D3aC_asXYA?si=hpFdcIYnWVKEkgbT" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252F1D3aC_asXYA%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253D1D3aC_asXYA%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252F1D3aC_asXYA%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

So, that's basically it folks! Happy integration-building!
