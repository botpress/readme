---
title: Moving Parts
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
The standard way to develop a chatbot on Botpress Cloud is to use the [Studio](https://studio.botpress.cloud). It is a low-code platform; that is, the Studio allows you to create chatbots by writing little code, or even none at all.

To please developers, Botpress Cloud also allows you to develop chatbots with code only. This set of features is called the developer side of Botpress Cloud or the developer experience (DX).

In addition to allowing the development of Chatbots, the developer experience also allows the creation of Integrations. Integrations are applications that allow Chatbots to communicate with external services as well as share/reuse certain features. The only way to develop integrations is to do it with code.

The developer experience is composed of the following parts:

* the [Public HTTP API](https://botpress.com/reference/introduction)
* the [TypeScript HTTP Client](https://npmjs.com/package/@botpress/client)
* the [TypeScript SDK](https://npmjs.com/package/@botpress/sdk)
* the [CLI](https://npmjs.com/package/@botpress/cli)

The public HTTP API of Botpress Cloud is already documented [here](https://botpress.io/docs/cloud/api).

The TypeScript HTTP Client, on the other hand, only exposes the API in an npm package to facilitate requests to the API in JavaScript and TypeScript. It contains all the types of requests and responses of the API.

To create a Chatbot or an Integration, you must call the [create-bot](https://botpress.com/docs/api/#bot-create-bot) or [create-integration](https://botpress.com/docs/api/#bot-create-integration) route of the API. The HTTP body of the request contains a `code` field. This is the JavaScript program of the Bot or Integration. This code is executed by Botpress Cloud. However, this field cannot contain any program, it must have a certain format and a certain behavior for Botpress Cloud to be able to execute it. This is where the SDK comes in.

The SDK is an npm package that is used and executed with the code of the Bot or Integration. It facilitates development by providing functions and classes that frame your development. It is theoretically possible to develop a Bot or an Integration without using the SDK, but this is strongly discouraged.

At the time of writing, all Bots and Integrations are hosted and executed by Botpress Cloud. This means that it is not possible to host a server on your side. For this reason, the use of the JavaScript language is mandatory. If your program is written in TypeScript, it must be transpiled and bundled before being sent to Botpress Cloud. This is where CLI comes in.

The CLI wears several hats. It allows you to interact with the public HTTP API of Botpress Cloud and to develop/deploy Bots and Integrations. Just like the SDK, it is theoretically possible to do without it but this is strongly discouraged.

Since the public HTTP API of Botpress Cloud is already documented and the TypeScript HTTP Client only exposes it in an npm package, the next sections of this document will focus on the SDK and the CLI.