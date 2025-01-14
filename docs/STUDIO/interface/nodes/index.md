---
title: Nodes
excerpt: The primary unit of conversational logic in your agent.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Nodes are the primary units of conversational logic of your agent. A node generally executes an action or a set of actions and transitions to another node or flow. You can think of a node as a step in a conversation.

A single node can have multiple content types, instructions, and transitions. When there aren't any more transitions, the conversation ends.

# Types of Nodes

## Standard Node

The Standard node is a versatile building block in your bot's workflow. It allows you to add both instructions and transitions to your flow, and it can be used to represent a variety of steps in the conversation with the user.

You can add instructions to the Standard node to define what the bot should do at that point in the conversation, such as sending a message or asking the user for input. You can also add transitions to the Standard node to specify the conditions under which the conversation should proceed to the next node.

Standard nodes can be connected to other nodes within the same workflow using transitions, allowing you to create complex conversation flows that adapt to the user's input and actions. They are essential building blocks for creating conversational AI experiences that are engaging and useful for your users.

## Autonomous Node

The Autonomous node uses an LLM to determine when, and in what order, to execute the cards it contains. Based on the context of the conversation, as well as a set of instructions provided by the builder, Autonomous nodes manage conversation flows and decide what actions to perform.

Autonomous Nodes can be created by right-clicking in the studio and selecting "Autonomous Node" from the dropdown menu.

## Start Node

The Start Node is a specialized Entry Node that is only available in the main flow of a Botpress bot. It serves as the starting point for the conversation and can only execute transitions to other standard nodes.

## Entry Node

Every workflow in your bot, except the main flow, starts with an Entry node. The Entry node is the starting point for each individual workflow and can only execute transitions to other standard nodes within that workflow. It is used to define the entry point for the workflow and the initial conditions that must be met for the workflow to start executing.

## Exit Node

Similar to the Entry node, every workflow in your bot, except the main flow, should end with an Exit node. The Exit node is the final node in a workflow and can only receive transitions from other standard nodes within that workflow. It is used to define the exit point for the workflow and specify the conditions that must be met for the workflow to end. The Exit node typically contains cleanup or finalization logic, such as sending a message to the user or updating a database, before the workflow is completed.

## End Node

The End Node is a unique node in your bot's Main Flow. Its purpose is to clear the conversation session and reset the bot to its initial state once it is reached. When the End Node is executed, it will erase all variables and user data associated with the conversation and set the cursor back to the beginning of the Main Flow.

The End Node is typically used when you want to reset the conversation with the user and start a new session from scratch. It is particularly useful for bots that handle sensitive or personal information, where it is important to ensure that previous session data is not accessible to subsequent users.

Note that the End Node is only available in the Main Flow of your bot and cannot be used in other workflows.
