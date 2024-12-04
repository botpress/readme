---
title: Generate Conditions using AI
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
![](https://files.readme.io/4d91065-image.png)

[Expressions](..docs/transition#expression) are steps in the conversation where the flow may transition to another node based on a condition.

The actual condition is a Javascript expression (that must return true for the transition to happen) but with our Generative AI you don't need to write code at all, you can turn plain language instructions like "if the user has already provided their email" or "if today is Wednesday" and even complex requests to external services like "saves new task to Trello" into working expressions that consider your variables and bot settings.

## How to do it

1. Create an Expression card
2. Write your condition in plain language
3. The condition will be generated automatically. You can edit and refine it to your needs if you want.

## Tips

> 📘 Info
>
> Create good descriptions for your workflow variables and table columns because they are taken into consideration by the AI when generating the expressions and [Code](..docs/generate-code-using-ai).
