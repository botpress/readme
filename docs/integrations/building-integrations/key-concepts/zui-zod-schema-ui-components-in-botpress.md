---
title: ZUI - Zod schema UI components in Botpress [BETA]
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
ZUI allows builders to write schemas as code, and have bot builders to input data using corresponding inputs straight from the Botpress Studio. It is highly integrated with the Botpress Studio, and allows you to make selectors that request Botpress resources such as users, bots, intents, messages, workflows, etc.

For instance, if you want to have a user select from a list, you can have `z.enum(["first value","second value", "third value"...])`.

For example, a schema like this : 

<Image align="center" width="200px" src="https://files.readme.io/96b5589-image.png" />

Would allow you to have this as an input in a workflow:

<Image align="center" width="200px" src="https://files.readme.io/c3f7d28-image.png" />

<br />

In an integration you can import zui like this:

`import { z } from "@botpress/sdk";`

And use intellisense in your code editor to see the implemented methods.

<br />

## List of Types

**variable**

* Parameters: `type`, `params`
* Type Options: `any`, `string`, `number`, `boolean`, `object`, `pattern`, `date`, `array`, `target`, `time`, `enum` 
* (You can use any one of these like this : `z.string()`)

**conversation**

* Parameters: `params`

**user**

* Parameters: `params`

**message**

* Parameters: `params`

**agent**

* Parameters: `params`

**event**

* Parameters: `params`

**table**

* Parameters: `params`

**tablerow**

* Parameters: `params`

**intent**

* Parameters: `params`

**datasource**

* Parameters: `horizontal`

**knowledgebase**

* Parameters: `horizontal`

You can find the current list of zui components here [https://github.com/botpress/packages/blob/9b43dcd96f1fd7d059ee4dd0f4749f5b8bfd0dba/zui/src/z/extensions.ts](https://github.com/botpress/packages/blob/9b43dcd96f1fd7d059ee4dd0f4749f5b8bfd0dba/zui/src/z/extensions.ts) .

<br />

## Current support

Current implementation in Studio:

* Integrations configuration 
* Integration actions input
* Workflow Inputs using Botpress Schemas - Basic types like string, array, object, boolean
