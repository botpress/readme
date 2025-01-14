---
title: Translator Agent
excerpt: Enables your bot to communicate in multiple languages.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The Translator Agent enables the bot to communicate in multiple languages by automatically translating text between different languages. This agent is crucial for bots that need to operate in a multilingual environment.

# Configuration

## Detect Initial User Language

When this option is enabled, the agent will automatically detect the language in which the user is communicating on the first incoming message it receives.

The message must be at least 3 <Glossary>tokens</Glossary> in order to be processed by the agent. Note that this process will automatically overwrite the language variable, even if you set that variable manually at the beginning of the conversation.  

## Detect Language Change

When this option is enabled, the agent will attempt to detect the user's language on ever <Glossary>conversation turn</Glossary>. This is particularly useful if you expect the user's language to switch throughout a single conversation.

If this option is disabled, the agent will only detect the user's language when it is designated as 'null'.

## Model

This is the model your agent will use to translate messages.

# Exposed Variables

The Translator Agent exposes one variable for use:

```
{{user.TranslatorAgent.language}}
```
