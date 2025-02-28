---
title: Advanced Starter Template
deprecated: false
hidden: false
metadata:
  robots: index
---
## Import Guide

Follow the instructions for downloading and importing the bot template on the Botpress Growth Team's Github! Link to the intructions found [here!!](https://github.com/botpress/growth/tree/master/advanced-starter-bot-template)

## Overview

This comprehensive template covers the core features and capabilities of Botpress, serving as both a learning resource and a foundation for your chatbot projects.

Whether you are new to Botpress or looking to explore our features, this template provides practical, real-world examples you can learn from and adapt to your needs. Follow along with our youtube tutorial below for a detailed walkthrough of all the features.

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=-N4OoKg_w4I" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252F-N4OoKg_w4I%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253D-N4OoKg_w4I%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252F-N4OoKg_w4I%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=-N4OoKg_w4I" providerUrl="https://www.youtube.com/" providerName="YouTube" />

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