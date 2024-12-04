---
title: Invalid Action Payload
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
# About this Issue

This Issue arises when a Bot supplies an Action **input data** that does not conform to the **format expected** by the Integration. For example, the `addReaction` action for the Slack Integration expects the `messageId` input variable to be of type `string`. If your Bot supplies a value that is not a string (e.g. an object, number, etc), the `addReaction` Action will fail.

# Resolution

Make sure data provided via **SuperText inputs** is conform to the expected schema of the Action you are using. You can view required input fields and their formats in the [Integration Hub](https://app.botpress.dev/hub?_gl=1*1k0igll*_ga*NTIzNDQ0OTIwLjE3MTYzODQ4NzM.*_ga_HKHSWES9V9*MTcxNzY5NDgxMy41OS4xLjE3MTc3MDcwODUuMC4wLjA.).