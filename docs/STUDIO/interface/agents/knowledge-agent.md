---
title: Knowledge Agent
excerpt: Retrieves information from the bot's knowledge base.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The Knowledge Agent is responsible for retrieving information from the bot’s knowledge bases, such as FAQs, documents, websites, or structured databases. This agent is essential for providing accurate and detailed answers to user queries.

# Configuration

## Answer Manually

When this option is enabled, your bot won't automatically provide answers in the conversation. The answers it generates will be saved to a dedicated variable which you can use manually in the conversation at a later point.

## Additional Context

This setting enables the bot to include extra contextual information when generating answers. By considering additional context, the Knowledge Agent can provide more accurate and relevant responses, especially in complex or nuanced scenarios.

## Model Strategy

The "Model Strategy" option allows you to choose how the Knowledge Agent selects and applies machine learning models to generate answers. Depending on your strategy, the agent can prioritize different models based on speed, accuracy, or specific use cases.

### Fastest Model

This is the model you designate as being the fastest, suited to your specific need. Generally, these are considered quicker, more performant, and less expensive models, and should be used when you anticipate simple queries.

### Best Model

This is the model you designate as being the most performant, suited to your specific need. Generally, this option should be used only when you anticipate that the additional performance of a more expensive model will be needed 

### Question Extractor Model

This is the model used to extract questions from a conversation. Generally, you should follow the above rules here: a faster model if you anticipate simple queries, and a more performant one if the questions you expect to receive will be complex.

## Chunks Count

This is the number of <Glossary>chunks</Glossary> that Botpress will elect to send from the Knowledge Base to a model to generate an answer. A larger number of chunks will send more information to the model, generally resulting in more accurate answers, with longer generation times and a higher token cost.

## Exposed Variables

The Knowledge Agent exposes two variables that you can use:

### Generated Response

```
{{turn.KnowledgeAgent.answer}}
```

### Response citations

```
{{turn.KnowledgeAgent.citations}}
```
