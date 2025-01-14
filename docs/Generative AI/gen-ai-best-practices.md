---
title: Best Practices
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
![](https://files.readme.io/1544f5b-image.png)

# Do's and Dont's

In general, the AI Task, Execute Code, and the transition don't know what is happening in the rest of the flow. Each is concerned only with itself. To get the best results with AI, these are the words to use and the words to stay away from:

## Do's - Use Effective phrasing:

* "What is the capital of France?"
* "Can you tell me about the history of the Great Wall of China?"
* "Please provide a definition of the word 'algorithm.'"
* Use absolutes, words like: “ignore”, “add”, “extract”, “use”, “store”, etc.

## Dont's - Use Ineffective phrasing:

* "Don't tell me the wrong answer."
* "I'm not interested in hearing your opinion."
* "You wouldn't happen to know what I'm talking about, would you?"
* Don't use hedge words like: “maybe”, “try”, "potentially", "avoid", etc.

<br />

# Personality, Tone, Language

You can set the personality, tone, and language of your bot using simple natural words.

## Personality

Words such as **act like**, **pretend**, and **sound like** can influence the AI to act like a celebrity or to sound like a person from specific profession can have a great effect on the users who use your bot.

For example, you can use **"Act like Kevin Hart"**

![](https://files.readme.io/d42362f-image.png)

Or **"Act like a Teacher"**

![](https://files.readme.io/4978e28-image.png)

## Tone

Phrases starting with **"use emojis"**, **"be extra friendly"** or **"be empathetic"** can influence the AI by showing emotions in its text.

For example, you can use **"sound like a loving mum who is fond of babies"**

We can also mix that with **"Use a lot of emojis"**

![](https://files.readme.io/f576d78-image.png)

## Language

You can also instruct your bot to answer or speak in a specific language using **"speak in"**, **"use language"** and **"answer using"**

![](https://files.readme.io/4be8a74-image.png)

<br />

# Input and Output

What words can we use to direct the AI to our inputs and outputs effectively? These are just guidelines, so feel free to be as creative as you want.

## Input Sample

We can use a phrase like **Taking the user's input into consideration**, and in the input, we can specify exactly what each input means.

For example - the AI Task Instruction could be:

```text
Taking the user's input into consideration, what is the typical budget for a family that consists of "No of Family Members" and lives in "Country & City Name" for those inputs?
```

And the AI Input will be:

```text
Country & City Name: {{workflow.fullAddress.country}} - {{workflow.fullAddress.city}}
No of Family Members: {{workflow.noOfPeople}}
```

We can also direct it to where it will find the information and in which variable like **in the variable**, and then mention the variable name.

For example - the AI Task Instruction could be:

```text
Give advice to the question in the variable userQuestion
```

And the AI Input will be:

```text
This is the question that needs advice {{workflow.userQuestion}}
```

## Output Sample

We can use words like **store** and **into** to direct it to store the extracted value into a specific variable.

For example - the AI Task Instruction could be:

```text
store it in variable whatDoYouThink
```

And the output will be stored in a Variable named **whatDoYouThink**

<br />

# Example - Preserving Context

To ensure that the AI knows the context and keeps it into its consideration, we will need to do a couple of things.

## Step 1: Saving context

For this step, we can use an Execute code to append everything related to the context to a string variable:

So every time the user says something, it is concatenated/append to what they said before

## Step 2: Pass it to AI Input

In the AI Task, we can pass that variable as an input, then direct the AI to consider it using a statement like **Take into consideration the user history.**

## The Result

In the end, we can ask multiple questions while making sure the AI takes into consideration the history of the conversation.

You can also pass the past answers from the AI and direct it to **Use new answers every time**. This way you can achieve AI Prompt Chaining.

<br />

# Limitations

## Token Limitation

The current limitation is 5000 characters, and we are working to increase it.

You can find more information here: [https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)

## Understanding Limitation

There are limitations to what the AI can understand, such as complex or nuanced language involving sarcasm, irony, or figurative expressions.

## Time Limitation

Since the AI is based on ChatGPT models, you must know that ChatGPT is not connected to the internet, and it can occasionally produce incorrect answers. It has limited knowledge of the world and events that happened after 2021 and may also occasionally produce harmful instructions or biased content.

You can find more information here: [https://help.openai.com/en/articles/6783457-chatgpt-general-faq](https://help.openai.com/en/articles/6783457-chatgpt-general-faq)

<br />

# Conclusion

Generally, it's best to avoid negative and vague language or ambiguous statements when using AI-related tasks. Instead, always try to be specific and direct, and use a language that is easy to understand.

It is better to use natural language; you can use a wide range of inputs, including commands and requests. AI doesn't have human emotions; it may not fully understand some complex or nuanced language, especially if it involves sarcasm, irony, or figurative expressions.
