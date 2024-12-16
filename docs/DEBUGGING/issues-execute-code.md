---
title: Execute Code
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# About this issue

This issue arises when an **unhandled exception** is thrown by JavaScript code in an **Execute Code** card, triggering the **Error flow** for your bot. You can inspect the [Logs](../docs/admin-logs) to see details about the exception.

# Resolution

You can wrap your code in a [`try..catch`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) statement and handle the exception. This will ensure the Error flow is not triggered.