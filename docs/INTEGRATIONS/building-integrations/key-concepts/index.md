---
title: Key Concepts
excerpt: Overview
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Botpress Integration Documentation

The Botpress SDK provides a structured way for developers to create new integrations for their chatbots. In this documentation, we're using the [Slack integration class](https://github.com/botpress/botpress/blob/master/integrations/slack/src/index.ts) as a reference to illustrate the process.

<br />

# Key Concepts

## 1. [Tags](./tags.md)

These identify users, conversations, and messages in the external system (e.g., Slack). Each tag is assigned a unique identifier.

## 2. [Channels](./channels.md)

Define which channels the integration supports. Channels can be group conversations, direct messages, or others, depending on the external system.

## 3. [Configuration](./configuration.md)

This is where sensitive information, such as API keys and tokens, is stored. The configuration is used to validate the integration setup.

## 4. [User](./user.md)

This refers to the mapping between the external system and Botpress. It defines how users are identified and created in the bot system.

## 5. [Conversation](./conversation.md)

This refers to the dialogue happening between the external system, the user, and the bot. It holds the mapping between the conversation ID in the external system and the conversation ID in Botpress.

## 6. [Messages](./messages.md)

These are payloads exchanged between the external system, the user, and the bot within a conversation. Messages contain information essential to map interactions between the systems and hold valuable data for the conversation designer.

## 7. [States](./states.md)

The state is responsible for associating data with a user, a conversation, or in a global context to store important information that needs to be tracked.

## 8. [Actions](./actions.md)

Actions are tasks that the integration can perform. These could be sending a message, adding a reaction, or any other function that the external system supports.

## 9. [Events](./events.md)

These are non-conversational incidents that are triggered and captured by the system. For example, in Linear, an event could be when a new issue is created; in WhatsApp, it could be when someone opens the chat.

## 10. [Definition](./definition.md)

Everything within the integration needs to be defined before use. This is done in the IntegrationDefinition class.

## 11. [Secrets](./secrets.md)

Finally, Botpress securely handles sensitive information like API keys or tokens in the **Secrets** field of the **IntegrationDefinition** class. This field defines and manages the secrets needed by the integration, keeping them secure from potential security breaches.
