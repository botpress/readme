---
title: Knowledge Base Optimization
excerpt: Automatically improve your bot's ability to respond to knowledge queries.
deprecated: false
hidden: false
metadata:
  robots: index
---
> 🚧 Early Beta
>
> The Knowledge Base Optimization feature is in beta and should not be used in production or critical workflows. We encourage testing in non-production environments and welcome your feedback to improve its stability and functionality.
>
> While in early beta, optimization is a manual process.
>
> Each optimization can cost up to 2x the total number of tokens present in each document and consumes a portion of your [AI Spend quota.](usage-2)
>
> Optimization uses your default "Best Model", configured through your LLM settings in the Studio.

You can use the Knowledge Base Optimization feature to improve your bot's ability to respond to questions with information contained in your knowledge base.

# How to use

## Install

Start by installing the Knowledge Base Optimizer integration from the integration hub.

[Link to integration](https://studio.botpress.cloud?exploreHub=1\&hubItemId=intver_01JEZ0DVQSVVFHKVK5V5XQE7KX)

<Image align="center" src="https://files.readme.io/a186e6f91fc798e1de45d7a8de46b944304850c37b8a931c73bad40231fa3552-Screenshot_2024-12-13_at_11.28.52_AM.png" />

## Optimize

After installing the integration, you can use the "Auto-optimize" feature that now appears on your knowledge bases.

<Image align="center" src="https://files.readme.io/0ce1bdd4989935671ddc0e702e4d6a283719c794c8b5beef5459d5d1838b7ee9-Screenshot_2024-12-13_at_11.34.29_AM.png" />

Optimizing improves your bot's ability to respond to queries with the information contained in your knowledge bases.

## Test

### Before optimizing

In the example below, the bot is unable to parse the user's question, and does not understand that the user is trying to query the information contained in the knowledge base.

<Image align="center" src="https://files.readme.io/82f20a25db6360dfa0251b69c96066e5fda7633ec253f52c6b2dd61742399343-Screenshot_2024-12-13_at_11.37.01_AM.png" />

### After optimizing

After optimizing the same example, the bot is able to take the same input and recognize that it is being asked a question that pertains to the information contained in its knowledge base.

<Image align="center" src="https://files.readme.io/0a2c1e947223ef085fb8af4acebbcbd594b41d0861ce0dc71a079be382063f7a-Screenshot_2024-12-13_at_11.43.27_AM.png" />

> 🚧 Early Beta
>
> The Knowledge Base Optimization feature is in beta and should not be used in production or critical workflows. We encourage testing in non-production environments and welcome your feedback to improve its stability and functionality.
>
> While in early beta, optimization is a manual process.
>
> Each optimization can cost up to 2x the total number of tokens present in each document and consumes a portion of your [AI Spend quota.](usage-2)
>
> Optimization uses your default "Best Model", configured through your LLM settings in the Studio.