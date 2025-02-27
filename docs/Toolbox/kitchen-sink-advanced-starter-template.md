---
title: Advanced Starter Template
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

This comprehensive template covers the core features and capabilities of Botpress, serving as both a learning resource and a foundation for your chatbot projects.

Whether you are new to Botpress or looking to explore our features, this template provides practical, real-world examples you can learn from and adapt to your needs. Follow along with our youtube tutorial below for a detailed walkthrough of all the features.

<Embed typeOfEmbed="youtube" url="" />

## Import Guide

<br />

## Core Functionalities

1. **Initial User Data Loading**
   * Capture platform-specific user data (Messenger ID, WhatsApp number, webchat data, etc...)
   * Handle different integration sources
   <br />
2. **Event Tracking**
   * Custom analytics platform integration
   * Support for Google Analytics, Mixpanel, and Segment
   * Botpress' built-in analytics Agent.
   <br />
3. **Proactive Greeting**
   * Bot-initiated conversations (embedded webchat and shareable link only)
   <br />
4. **Workflow Routing System**
   * Using a central routing node to route to other workflows.
   * Helps solve the question "How to transition outside of an autonomous node?"
   * Two routing options:
     1. Autonomous node-based routing (AI option)
     2. Button-based routing (non-AI option)
     <br />
5. **Requiring Information from the User to Send to an External Tool**
   * Required field collection (e.g. requiring a valid email)
   * External tool to send tickets or information to
   * Botpress table integration (to send information as rows)
   <br />
6. **Querying Knowledge Base and Saving Search Results**
   * Question and answer tracking
   * Prevent AI hallucinations by telling the user that no answer was found if the information does not exist within the knowledge base. This bot covers fallback handling for unanswered questions.
   * Track the exact chunk, knowledge base, and citation for where the information came from within your knowledge base.
   <br />
7. **Live Agent Handoff**
   * Assigning a ticket to a live agent, causing the conversation with the bot to be temporarily paused until the live agent is done solving the ticket.
   * The human can "talk through" the bot to the user.
   <br />
8. **CSAT (Customer Satisfaction) System**
   * End-of-conversation survey
   * Conversation summary generation and storage in Conversation Ratings Table
   <br />
9. **Table Search and Filtering**
   * Querying from a Botpress table to fetch row(s) based on user input parameters.
   <br />
10. **Management of Multiple Sub-Bots within a Single Bot for Multi-Client Purposes**
    * Client-specific knowledge base segmentation
    * Customer tag and identity management
    * Dynamic knowledge base selection
    * Multi-client support within a single bot instance