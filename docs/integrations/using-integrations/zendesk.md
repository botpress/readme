---
title: Zendesk
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
![](https://files.readme.io/00252fb-image.png)

Turn Botpress chats into Zendesk tickets, with a handy link added to the conversation notes. A Zendesk agent can communicate directly with the user on the same conversation initially handled by the bot on any channels supported by Botpress (e.g. web chat, Whatsapp, Messenger, etc.)

# Getting Started

In this guide, we will demonstrate how to set up the Zendesk integration to facilitate live interactions through the bot.

[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2FKR87xwsh33Y%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DKR87xwsh33Y&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2FKR87xwsh33Y%2Fhqdefault.jpg&key=7788cb384c9f4d5dbbdbeffd9fe4b92f&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/watch?v=KR87xwsh33Y",
  "title": "How to Set Up Live Agent Handoff for Zendesk | Botpress",
  "favicon": "https://www.google.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/KR87xwsh33Y/hqdefault.jpg",
  "provider": "https://www.youtube.com/",
  "href": "https://www.youtube.com/watch?v=KR87xwsh33Y",
  "typeOfEmbed": "youtube"
}
[/block]


## Step 1: Add Zendesk Integration

Firstly, locate your bot's dashboard and click on the integrations tab. Use the search bar to find and select the Zendesk Integration. Once found, install this onto your bot.

## Step 2: Setting up Zendesk Integration

Switch to the Zendesk admin center, and find the Zendesk API menu. Ensure you have both password and token access enabled.

You will then need to create a distinct API token. Copy this for later use.

Return to your bot's dashboard. Here you will need to input your organizational subdomain, your consistent Zendesk account email, and the copied API token. Ensure to save this configuration and activate the newly installed integration.

## Step 3: User Info Accumulation

The bot will need the user's name and their email. This data will be saved to user variables.

Create a 'user.name' and a 'user.email' variable on the bottom-left variables panel. Make sure to select "User" as the scope. Confirmation of the information will be done using simple capture cards.

## Step 4: Enabling HITL Agent

From the "Agents" menu of the bot in Botpress Studio, click on the "HITL Agent" option, and then turn on the "Enable Agent" option.

This menu will allow you to configure options such as choosing Zendesk as the desired integration. Also, you have the capability to design an 'end_conversation' intent that permits the user to opt out of speaking to a live agent. To do so, pick a global intent from the dropdown, for instance "Cancel".

Most settings are default, you may choose to modify them to your preference.

## Step 5: Activating HITL

Add a new node to your bot in Botpress Studio and then insert a "Start HITL" card, which will trigger the bot into initiating a live agent.

The card will automatically summarize the conversation and provide a transcript for the live agent in the Zendesk menu.

## Step 6: Test the Configuration

Now that everything has been configured accordingly, publish your bot and open the Web Chat. 

> 📘 Note
> 
> This integration does not work in the emulator. Try it in other channels such as Web Chat.

<br />

# Cards

## Get Ticket

Retrieves details about a specific support ticket in Zendesk.

- **Input**:  
  - `Ticket ID`: The ID of the ticket from the ticket URL. <br/>(e.g., `https://companyname.zendesk.com/agent/tickets/1` for `Ticket ID` `1`).
- **Returns**: Real-time updates on the status and details of the ticket.

```javascript
// Return object example
{
  "ticket": {
    "id": 4,
    "subject": "Ticket Subject",
    "description": "Ticket Description",
    "priority": null,
    "status": "open",
    "tags": [],
    "requesterId": 11183521570160,
    "assigneeId": 11183526440284,
    "createdAt": "2023-11-08T18:27:49Z",
    "updatedAt": "2023-11-10T18:03:13Z"
  }
}
```

## Create Ticket

Creates a new support ticket in Zendesk.

- **Inputs**:
  - `Ticket subject`: Title of the ticket.
  - `Ticket comment`: Initial message for the support agent.
  - `Requester name`: Name of the user needing support.
  - `Requester email`: Email of the user needing support.
- **Returns**: Confirmation of ticket creation with details.

```javascript
// Return object example
{
  "ticket": {
    "id": 4,
    "subject": "Ticket Subject",
    "description": "Ticket Description",
    "priority": null,
    "status": "open",
    "tags": [],
    "requesterId": 11183511570160,
    "assigneeId": 11183521440284,
    "createdAt": "2023-11-08T18:27:49Z",
    "updatedAt": "2023-11-10T18:03:13Z"
  }
}

```

## Close Ticket

Closes the ticket of the provided Ticket ID in Zendesk.

- **Input**: 
  - `Ticket ID`: The ID of the ticket from the ticket URL. <br/>(e.g., `https://companyname.zendesk.com/agent/tickets/1` for `Ticket ID` `1`).
- **Optional**: `Closing Comment` for resolution summary or thanks.
- **Returns**: Confirmation that the ticket is closed with optional comment.

```javascript
// Return object example
{
  "ticket": {
    "id": 4,
    "subject": "Ticket Subject",
    "description": "Ticket Description",
    "priority": null,
    "status": "closed",
    "tags": [],
    "requesterId": 11183511570160,
    "assigneeId": 11183521440284,
    "createdAt": "2023-11-08T18:27:49Z",
    "updatedAt": "2023-11-10T18:03:13Z"
  }
}

```

## Get Ticket Conversation

Fetches the conversation ID of the provided Ticket ID in Zendesk.

- **Input**: 
  - `Ticket ID`: The ID of the ticket from the ticket URL. <br/>(e.g., `https://companyname.zendesk.com/agent/tickets/1` for `Ticket ID` `1`).
- **Returns**: Latest updates or responses from support agents on the ticket.

```javascript
// Return object example
{
  "conversationId": "5c9ea21d-3ce3-43fa-bd33-3fb7312f88b5",
  "tags": {"zendesk:id": "4", "zendesk:requesterId": "11232621609372"}
}

```

## Find Customer (WIP)

Finds a customer in Zendesk based on the provided search query.

- **Input**: 
  - `Search Query`: You can search by name, email, or phone number of the customer.
- **Returns**: A list of matching customers and their details.

```javascript
// Return object example
{
  "customers": [
    {
      "id": 11183521570160,
      "name": "Customer Name",
      "email": "Customer Email",
      "phone": "Customer Phone",
      "createdAt": "2023-11-08T18:27:49Z",
      "updatedAt": "2023-11-10T18:03:13Z"
    }
  ]
}

```

## List Agents (WIP)

Provides a list of available support agents in Zendesk. 

- **Input**: 
  - `Is Online`: Select this option to filter the list of agents by online status.
- **Returns**: List of agents, optionally filtered by online status.

```javascript
// Return object example
{
  "agents": [
    {
      "id": 11183521570160,
      "name": "Agent Name",
      "email": "Agent Email",
      "phone": "Agent Phone",
      "createdAt": "2023-11-08T18:27:49Z",
      "updatedAt": "2023-11-10T18:03:13Z"
    }
  ]
}

```

## Set Conversation Requester (WIP)

Changes the requester of a ticket conversation in Zendesk.

- **Inputs**:
  - `Conversation ID`: Get this from the `Get Ticket Conversation` card.
  - `Requester ID`: Get this from the requester's profile URL in Zendesk (e.g., `https://companyname.zendesk.com/agent/users/1` for `Requester ID` `1`).
- **Returns**: None. Does not return anything.

## Trigger - Assigned Ticket

This trigger is fired when a ticket is assigned to an agent. This can be used to notify the agent that they have a new ticket to work on.

## Trigger - Ticket Solved

This trigger is fired when a ticket is marked as solved. This can be used to notify the user that their issue has been resolved.

> 📘 Note
> 
> You can add a message after these triggers to send a notification to the agent. For example, you can use the `Send Message`card to send a message to the agent.