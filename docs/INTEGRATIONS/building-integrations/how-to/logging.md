---
title: Logging
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
# Introduction

In Botpress Integrations, logging is an essential functionality used for error tracing, tracking down issues, debugging, and keeping track of the bot's actions. The `logger` object provided by Botpress offers this logging functionality, allowing you to log different severity levels of messages.

The `logger` is designed for developers or technical personnel dealing with bot integrations in Botpress. It has four methods, namely `info`, `warn`, `error`, and `debug`, each catering to different levels of logging severity.

<br />

# Using Logger

The integration logger is readily available in the properties received from the integration function, the same place where you have the `ctx` object.

```text
({ logger, ctx }) => {
  // ...
}
```

Example: Calling it in the Channel Integration\
Here is an example of using the logger within a channel integration:

```javascript
text: async ({ logger, payload, ctx, conversation, ack }) => {
  logger.forBot().debug(ctx);
  logger.forBot().debug(payload);
  logger.forBot().debug(conversation);
}
```

In the above example, `logger.forBot().debug()` is used to log the ctx, payload, and conversation objects. This can be particularly helpful when debugging your bot's interactions within this channel.

<br />

# logger Object

## forBot Function

This function returns an object that provides four methods for logging: `info`, `warn`, `error`, and `debug`. The intended use for this function is to log messages that the bot owner would want to see. For example, these messages could be related to actions performed by the bot, errors that occurred, or any information that might be useful for monitoring or debugging.

```javascript
logger.forBot()
```

## Info Method

Logs an informational message. This is useful for general information that you would like to log about the operations of your bot.

```javascript
logger.forBot().info(message, ...optionalParams)
```

## Warn Method

Logs a warning message. Use this method to log anything that might potentially cause a problem in your bot. This might include deprecations, bad practices, or approaching quota limits.

```javascript
logger.forBot().warn(message, ...optionalParams)
```

## Error Method

Logs an error message. When your bot encounters a problem that prevents it from operating normally, log it using this method. This will make it easier for you to find and fix problems in your bot.

```javascript
logger.forBot().error(message, ...optionalParams)
```

## Debug Method

Logs a debugging message. When you're trying to figure out why your bot is behaving in a certain way, or you're trying to find a bug, this method allows you to log additional details about the operations of your bot.

```javascript
logger.forBot().debug(message, ...optionalParams)
```

<br />

# Extra Data

Each of these methods optionally accepts multiple parameters. The first parameter is a message to log. Subsequent parameters are optional, and will be logged alongside the message. For example:

```javascript
logger.forBot().info('This is an informational message', { data: 'Some relevant data' })
```

This will log the message "This is an informational message" along with the additional data object `{ data: 'Some relevant data' }`.
