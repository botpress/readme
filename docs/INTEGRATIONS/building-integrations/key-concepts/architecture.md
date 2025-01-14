---
title: Architecture
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
# Introduction:

Start with a brief overview of Botpress, what it is used for, and the importance of understanding its architecture.\
In this documentation, we want to discuss the architecture of the integrations in Botpress. That should help you understand better how the integration works, and that should make it easier for you to develop it.

<br />

# Key Concepts:

Below are the main Key Concepts when developing an integration in Botpress

## 1. [Tags](../docs/tags)

These identify users, conversations, and messages in the external system (e.g., Slack). Each tag is assigned a unique identifier.

## 2. [Channels](../docs/channels)

Define which channels the integration supports. Channels can be group conversations, direct messages, or others, depending on the external system.

## 3. [Configuration](../docs/configuration)

This is where sensitive information, such as API keys and tokens, is stored. The configuration is used to validate the integration setup.

## 4. [User](../docs/user)

This refers to the mapping between the external system and Botpress. It defines how users are identified and created in the bot system.

## 5. [Conversation](../docs/conversation)

This refers to the dialogue happening between the external system, the user, and the bot. It holds the mapping between the conversation ID in the external system and the conversation ID in Botpress.

## 6. [Messages](../docs/messages)

These are payloads exchanged between the external system, the user, and the bot within a conversation. Messages contain information essential to map interactions between the systems and hold valuable data for the conversation designer.

## 7. [States](../docs/states)

The state is responsible for associating data with a user, a conversation, or in a global context to store important information that needs to be tracked.

## 8. [Actions](../docs/actions)

Actions are tasks that the integration can perform. These could be sending a message, adding a reaction, or any other function that the external system supports.

## 9. [Events](../docs/events)

These are non-conversational incidents that are triggered and captured by the system. For example, in Linear, an event could be when a new issue is created; in WhatsApp, it could be when someone opens the chat.

## 10. [Definitions](../docs/definitions)

Everything within the integration needs to be defined before use. This is done in the IntegrationDefinition class.

## 11. [Secrets](../docs/secrets)

Finally, Botpress securely handles sensitive information like API keys or tokens in the **Secrets** field of the **IntegrationDefinition** class. This field defines and manages the secrets needed by the integration, keeping them secure from potential security breaches.

<br />

# Architecture Overview:

A high-level diagram of Botpress's integration architecture is provided below:

## Message Flow Diagram

This flowchart describes the steps taken when a message is passed from a user to a bot, and the response is delivered back.

![](https://files.readme.io/ae304a3-image.png)

1.0 The external system (e.g., Slack) receives a message from the user.

* A user interacts with the bot through the external system.

  1.1 The external system calls the Botpress webhook and sends the respective information to the Botpress Handler.

* The external system triggers a webhook to pass the message to Botpress.

  2.0 The integration handler defined in the integration code is called.

* The Botpress Handler gets the message and triggers the appropriate integration handler.

  3.0 After the handler code is executed, the transformed information is sent to the platform API.

* The message is processed and translated into a format that Botpress can understand and then sent to the platform API.

  4.0 This information is then directed to the respective bot for processing.

* The Botpress platform directs the message to the appropriate bot for processing.

  5.0 After processing the message, the output is sent back to the Platform API.

* The bot generates a response which is then sent back to the Botpress platform.

  6.0 This output is transformed by the integration code into a format the external systems can understand.

* The response is translated back into a format that the external system can understand.

  7.0 The transformed message is sent to the External System.

* The response is sent back to the external system.

  7.1 The External System forwards the message to the user.

* Finally, the external system delivers the bot's response to the user.

## Event Flow Diagram

This flowchart describes the steps taken when an event is detected in the external system and how it's processed in Botpress.

![](https://files.readme.io/ce4be19-image.png)

1.0 The external system (e.g., Slack) matches an event/trigger conditions.

* An event or trigger condition is met in the external system.

  1.1 The external system calls the Botpress webhook and sends the respective information to the Botpress Handler.

* The external system triggers a webhook to inform Botpress about the event.

  2.0 The respective integration event defined in the integration code is called.

* The Botpress Handler gets the event information and triggers the appropriate event handler in the integration.

  3.0 After the event code is executed, the transformed information is sent to the platform API.

* The event information is processed and translated into a format that Botpress can understand and then sent to the platform API.

  4.0 The event is then sent to the bot for processing.

* The Botpress platform directs the event information to the appropriate bot for further processing.
