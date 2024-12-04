---
title: Autonomous Node
excerpt: >-
  The Autonomous node uses an LLM to determine when, and in what order, to
  execute the cards it contains.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The Autonomous Node allows you to create AI agents that make decisions, like what to say and which tools to call, based on the context available to them.

By providing clear instructions and integrating tools, you can use the Autonomous Node to quickly design flexible, performant conversations.

The Autonomous Node is designed to handle both decision-making and execution by understanding user inputs, responding with the right data, and leveraging the tools you make available to it.

## Key Features

1. LLM Decision-Driven

An Autonomous Node uses the capabilities of an LLM to make intelligent decisions instead of relying on hard-coded logic. This includes executing specific tools, calling functions, writing and executing custom code, and deciding on the direction of a conversations.

2. Toolset Integration

The Autonomous Node understands and utilizes the tools that you explicitly make available to it. For example, it can query knowledge bases, perform web searches, and execute workflow transitions.

3. Prompt Customization

By configuring an Autonomous Node with a persona and instructions, you can ensure that it behaves on-brand and within scope during conversations.

4. Autonomous Behaviour

An Autonomous Node can execute actions without manual intervention based on instructions and user input.

## Configuration

Ensuring your Autonomous Node's instructions are cogent and precise is the key to a performant AI agent. The prompt helps the agent understand its persona and guides its decision-making.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcW_BFE75vwUVOeS0vzhECNdBPYsoiQJVwA9NWGeW8eI_QGlNVGFXxVyG1tSeuQQxyT3Fnt3WGj-5m_rHyjn2yNfuKEjyYFi1y1dX4aCI3WpFoodTi27BjQk11ficYaDa6upnfNHX1d1GD6BB8_Pok5wJfY?key=tcM6xVfTehWnyG265C5blA)

### Instructions

Provide clear guidelines in this section. The more specific the instructions, the better the agent’s decision-making. Avoid using lengthy, convoluted descriptions with jargon and redundant terms.

Example: “You are a helpful assistant who always answers questions using the ‘knowledgeAgent.knowledgequery’ tool. If the user says ‘search,’ use the ‘browser.webSearch’ tool.”

### Allow Conversation

The Allow Conversation toggle enables the Autonomous Node to communicate with users directly. If turned off, the Node only processes commands and executes its internal logic without sending messages to users.

## Tool Calling

Based on the instructions you give it, an Autonomous Node is equipped with several tools it can call.

Each tool performs a specific action – understanding when and how to use these tools is critical for driving the Node’s decisions.

### Commonly-used Tools

* global.think: Allows the node to process or pause briefly.
* browser.webSearch: Enables the agent to search the web for answers.
* knowledgeAgent.knowledgequery: Queries an internal knowledge base for relevant information.
* clock.setReminder: Sets a reminder for future tasks or responses.
* workflow\.transition: Executes a workflow transition, moving from one part of the conversation to another based on user input.
* chat.sendText: Sends a text message to the user as a response.
* chat.waitForUserInput: Pauses execution and waits for further input from the user.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd3jgdaZY9mCCkRvE54JYgLYZ2_oTbM7KG1LONpL_xsOyZOMSxMUxPrks7LYLMhV0ckjcbOEdCzoKcnT7fs-SpHJuQb7biJdCB_UHnev4mwIVkodN4SleGARFqGXR_W_S1LsHbEaxJmScnKp5EYMb7b1To?key=tcM6xVfTehWnyG265C5blA)

By specifying which tool to use in response to user actions, you can control the flow and outcomes of the conversation.

For example, you can instruct the LLM to always perform certain actions when specific conditions are met: “When the user says ‘1’, use the ‘workflow\.transition’ tool to move to the next step.”

Or: “If the user asks a question, first try to answer it using the ‘knowledgeAgent.knowledgequery’ tool.”

## Example Workflow

Here is a step-by-step example of how the Autonomous Node might be configured and function during a conversation:

1. User Input

The user types a question about the company’s product.

2. Instruction Execution

The Autonomous Node follows the prompt and uses the knowledgeAgent.knowledgequery tool to search the internal knowledge base.

3. LLM Decision

If the knowledge base doesn’t have a satisfactory answer, the node may then use the browser.webSearch tool to search the web for additional information.

4. Send Message

Once the response is ready, the node uses chat.sendText to reply to the user with the relevant information.

5. Wait for Input

After responding, the node uses chat.waitForUserInput to await further queries or interaction from the user.

## Writing Instructions

As shown in the example above, clear instructions are vital to ensuring the Autonomous Node behaves correctly.

An LLM’s ability to make decisions is heavily influenced by the way the instructions are structured.

Here are 3 best practices for writing instructions for your Autonomous Node:

### Be specific

Instead of vague commands, use explicit language that guides the agent clearly.

Example: “If the user says ‘help’, send them a predefined list of support options using ‘chat.sendText’.”

### Define tool usage

Explicitly state which tool should be used under which circumstances.

Example: “Always use ‘knowledgeAgent.knowledgequery’ for answering product-related questions.”

### Guide the flow

Use clear transitions and steps to ensure the conversation flows in the right direction.

Example: “If the knowledge base cannot answer, transition to a search query using ‘browser.webSearch’.”

You can find more information at the following links:

* [Best practices for prompt engineering with the OpenAI API](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api)
* [Building Systems with the ChatGPT API](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/)
* [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/)

## Markdown Syntax

To create a structured prompt, we recommend using markdown syntax like headers, bullet points, and bold text.

This syntax helps the LLM recognize and respect the hierarchy of instructions, guiding it to differentiate between main sections, sub-instructions, and examples.

[More about Markdown Basic Syntax](https://www.markdownguide.org/basic-syntax/)

## Useful Prompts

This section contains a list of the most common examples and patterns that you can use to control the behaviour of the Autonomous Node.

### Focus on Internal Knowledge

To ensure the Autonomous Node differentiates between support questions and other types of inquiries, you can guide it in your prompt as follows:

**IMPORTANT General Process**

* `The knowledgeAgent.knowledgequery tool is to be used only for support-related questions and NOT for general features or price-related questions.`

* `The browser.websearch tool is to be used only for support questions, and it should not be used for general features or price-related questions.`

This prompt ensures the LLM will stick to using specific tools only in the context of support-related queries, maintaining control over the kind of information it retrieves.

### Transition to a Subflow

Sometimes, you want the bot to move out of the Autonomous Node into a sub-flow.

Let’s say that you want your bot to collect a user email, then look for more info about that email from other systems to enrich the associated contact information.

In that case, you might need the bot to move out of the Autonomous Node loop and into a workflow that contains other integrations you're using to enrich contact information.

`When the user wants more information about an email, go to the transition tool.`

This instruction tells the node to invoke the workflow\.transition tool whenever the user asks for more details about emails, directing the conversation flow accordingly.

### Filling a Variable and Performing an Action

For scenarios where you want the node to both capture input and trigger an action simultaneously, you can prompt it as such:

`When the user wants more information about an email, go to the transition tool and fill in the "email" variable with the email the user is asking about.`

Here, you guide the Autonomous Node to not only trigger the transition but also to extract and store the user’s email in a variable, enabling dynamic behavior later in the conversation.

### Manipulating the Response Based on a Condition

Sometimes, you’ll want the node to perform additional logic based on conditions. Here’s an example prompt related to providing video links:

`If the users selects “1” then say something like “thank you”, then use the transition tool.`

This prompt helps the node understand the expected structure of a video link and how to modify it when the user asks to refer to a specific point in the video.

### Dynamically Generated Video Links

You can further clarify the prompt by providing an actual example of how the system should behave when responding to a user request for video links:

`**Video Link Example:**`

`If the user is asking for a video link, the link to the video is provided below. To direct them to a specific second, append the "t" parameter with the time you want to reference. For example, to link to the 15-second mark, it should look like this: "t=15":`

`"""{{workflow.contentLinks}}"""`

This gives the node clear guidance on how to dynamically generate video links with specific timestamps, ensuring consistent and user-friendly responses.

## Troubleshooting & Diagnosis

The Botpress Studio offers a suite of tools you can use to understand how your Autonomous Node is behaving, why it made certain decisions, and how you can course correct when it's not behaving as expected.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcTPS0_bodYzbTHkkwE0vVBGG-0mRNDCt6GIhSnzrDYoQCOHm2OF90hfjkqtSpI1i_deBFlMfw8TZTxPEsVLECmGE1CtUGeuSAJNfe60sfP2lSVqtXJRTTANrQLxxRA-2zImpdx5r9TqeOWRGnIvJLdhodL?key=tcM6xVfTehWnyG265C5blA)

### Using the Inspect Window

The "Inspect" window surfaces information about the Autonomous Node's process, reasoning, and functions. In it, you'll see:

* What instructions the node is prioritizing
* How it interprets your prompt
* Whether it is adhering to the constraints and instructions you provided

If you notice that the node isn’t responding correctly or seems to ignore certain instructions, inspecting will reveal whether it has misunderstood the prompt or failed to execute a specific tool.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdZdWnjNPsaGcbXWCNqoksqspOkKKswr3y8V-mc_xuNz7stAtfdXBisTbbwYeZwUDpOsfHbP3SwduJgvcDSbn1W4BLM9w6Di8JFCG7dGnwKoRvGe0aiSO5e3rIvdeeieWtMd8Bocehf2pw6sYeEpMBujsY0?key=tcM6xVfTehWnyG265C5blA)

The Tools section displays all available tools that the Autonomous Node has access to. Each time you add a new card or make a change in the node configuration, the Tools list is updated.

* Ensure that the tools listed match what you expect to be available in the node’s decision-making process.
* Ensure that the tool names are spelled correctly in your prompt to ensure the node can correctly execute the specified action.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGugnCTJCAGcwPf6RDoevJ_eS-6v0VFSzWy8rhTCFK5RlTTjkDMGuQk--qZ4FbPg5LbAMMzzSJh2mlXLUShyOg-a5q6NjvBTcWa1Y_6WIQhaOh9syL-XcklW6GpnyJixSO1SvzBUtJa1pC_zAc1l9D2WGh?key=tcM6xVfTehWnyG265C5blA)

The Autonomous Node typically tries to execute all instructions within one or two iterations. The number of iterations depends on the complexity of the prompt and how the Node analyzes it.

For more complex tasks, the node might take multiple iterations to gather data, make decisions, or fetch external information.

By reviewing the Iterations tab , you can understand:

* How many iterations were required for the node to reach its final decision
* What caused the node to take multiple steps (e.g., fetching additional data from tools like knowledgeAgent.knowledgequery or browser.webSearch)
* Why a particular outcome was achieved

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe2l1awCb4v2G3CM67G01E7ZhArQ6n-mFT-KgrFnVhc1FVw4rV2AIptxwu7OWAkN2RDDdA_8Zz7DxKLOFT7B0xX7kUUgSOmBKBzB0II75I3l-tfa5dIKc8ptkPr_eXJ5ex7hXuE2ik-zsUEz-IW9T7ujVRo?key=tcM6xVfTehWnyG265C5blA)

The Autonomous Node might not be following all of your prompt, executing part of the prompt instead of all of it, or calling the “workflowQueue” without calling the “workflowExecuteAll” tools.

### Choosing the Right Model

Less performant LLMs may struggle with the complexity of operations typically executed by the Autonomous Node.

For this reason, we recommend using a highly performant model to power Autonomous Nodes, roughly equivalent to a model like Open AI's GPT-4o.

A smaller LLM might result in parts of the prompt being truncated, specifically the definition wrapper that Botpress adds to ensure the LLM understands how the cards function, or what parameters are required.

### LLMz

Always make sure you are using the latest stable version of LLMz. This is the autonomous engine that directs the Autonomous Node to work.

It also contains bug fixes, making the prompts more agnostic to variance between LLMs.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdoefd_OKvJOHII-GLIhrD8e1C_qyq_6y0MhcKlWMTp6mV0uuugIxj2Ugkrty-INTJgz3uDfXK-ZWFPLOSri0948S6ZXy0Bkw-A-xmsDYmfHgLJ7Fp-HfOCp4fYoTGucMV1YWfLzsWMvFcd7MMHIJgmXUup?key=tcM6xVfTehWnyG265C5blA)

### Troubleshooting Code Creation

Let’s say an Autonomous Node is generating code but isn’t following the prompt correctly. Here’s how you might troubleshoot:

1. Inspect: Check what instructions the node is following. Is it correctly understanding the request for code generation?
2. Tools: Verify that the node has access to the necessary tools (e.g., code generation tools or knowledge base query tools). Ensure the prompt references these tools explicitly.
3. Iterations: Look at the iterations tab to see how the node reached the point of generating the code. Did it take one or multiple steps? Did it query a knowledge base first, or did it try to generate code immediately?

If the bot is failing to generate code properly:

* Ensure the tool being used for code generation is correctly referenced in the prompt.
* Adjust the instructions so the node is guided to use specific steps, such as first retrieving relevant knowledge before attempting code generation.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeX0OzEAKxFkaH0wSSmROQWUEYqymGQ82zkA8Mm6Kv0CyEqMNI3dAjJUQFnyTgBKLtvYczGv-LNNxelnYS7p3TO9dEUaawdlZlgFhjgG3fMGGX7tWp09PuHDmyufCoXqGM6tFg-iXnhkJAjQ5it_-HF-Ejn?key=tcM6xVfTehWnyG265C5blA)

## Example Instructions

\*\*IMPORTANT: Query Knowledge Base is to be used only for support questions related explicitly to student courses, and NOT for general features or pricing inquiries.

\*\*Role Description:

You are an AI-powered troubleshooting agent named XYZ Assistant’, focused on providing support related to professional courses offered by XYZ LMS. Your primary goal is to handle student inquiries efficiently by retrieving accurate information from the knowledge base and answering questions clearly.

\*\*Tone and Language:

* Maintain a courteous, professional, and helpful demeanor at all times.
* Use language that is clear, concise, and appropriate for students and professionals in finance and investment.
* Ensure user data is handled securely and confidentially, adhering to all relevant data protection policies.
* Utilize information solely from **LMS Knowledge Base**.
* Personalize interactions to enhance user engagement and satisfaction.
* Reflect **XYZ branding** throughout the conversation, ensuring clarity and professionalism.
* Avoid providing answers outside the knowledge base or surfing the internet for information.
* If the user expresses frustration, acknowledge their concern and reassure them that you are here to help.

\*\*Interaction Flow and Instructions

1. Greeting and Initial Query

* Start with a friendly and professional greeting.
* Encourage users to ask questions about course content, support materials, or other course-related concerns.

2. Information Retrieval and Issue Resolution

* Utilize the ‘Query Knowledge Base’ tool to find accurate answers to student inquiries.
* Provide clear, concise, and helpful responses to resolve the user's question.
* If the inquiry involves linking to a video, use the provided video link structure. To link to a specific moment in the video, append the "t" parameter for the desired time (e.g., for the 15-second mark, use "t=15").

3. Conclusion

* Once the issue is resolved, politely conclude the interaction and ask if there's anything else you can assist with.

\*\*Extra Instructions

\*Video Link Example

\-If the user is asking for a video link, the link to the video is provided below. To direct them to a specific second, append the "t" parameter with the time you want to reference. For example, to link to the 15-second mark, it should look like this: "t=15":

"""\{\{workflow\.contentLinks}}"""

\*Handling Edge Cases

If the user asks a general or unclear question, prompt them to provide more details so that you can offer a better solution.

## Prompt Breakdown

In the sample instructions above, the user has created an agent that answers questions from students about educational courses.

The above example is a guideline that can be amended for your needs, but this layout is what I have found to be the most effective structure so far.

Let’s break down the structure of these instructions:

### 1. Important Notice

\*\*IMPORTANT: Query Knowledge Base is to be used only for support questions related explicitly to student courses, and NOT for general features or pricing inquiries.

* Set boundaries on when and how the Query Knowledge Base tool should be used. Emphasizes that it's strictly for course-related support, not for general inquiries about features or pricing. This helps narrow down the bot’s scope, focusing its responses and enhancing relevance for users, and ensures that responses align with educational content.

### 2. Role Description

You are an AI-powered troubleshooting chatbot named XYZ Assistant’, focused on providing support related to professional courses offered by XYZ LMS. Your primary goal is to handle student inquiries efficiently by retrieving accurate information from the knowledge base and answering questions clearly.

* This defines the AI’s role as a support-oriented assistant, clearly outlining its primary objective to resolve course-related inquiries. With this, you can ensure that the assistant’s responses align with its intended purpose, managing user expectations and staying relevant to its domain (which, in this case, is XYZ LMS).

### 3. Tone and Language

* Maintain a courteous, professional, and helpful demeanor at all times.
* Use language that is clear, concise, and appropriate for students and professionals in finance and investment.
* Ensure user data is handled securely and confidentially, adhering to all relevant data protection policies.
* Utilize information solely from **LMS Knowledge Base**.
* Personalize interactions to enhance user engagement and satisfaction.
* Reflect **XYZ branding** throughout the conversation, ensuring clarity and professionalism.
* Avoid providing answers outside the knowledge base or surfing the internet for information.
* If the user expresses frustration, acknowledge their concern and reassure them that you are here to help.

This section provides guidance on the assistant’s demeanor, tone, and professionalism while maintaining secure, data-protective interactions. In this way, you establish a friendly and secure tone, aligning with your company's brand guidelines and user expectations for a supportive and professional assistant.

### 4. Interaction Flow and Instructions

#### Greeting and Initial Query

Start with a friendly and professional greeting.

Encourage users to ask questions about course content, support materials, or other course-related concerns.

* This instruction directs the assistant to begin with a warm, professional greeting and encourage users to ask specific questions about their course. It establishes an inviting entry point that enhances user engagement and helps the bot gather details for a better response.

#### Information Retrieval and Issue Resolution

* Utilize the ‘Query Knowledge Base’ tool to find accurate answers to student inquiries.
* Provide clear, concise, and helpful responses to resolve the user's question.
* If the inquiry involves linking to a video, use the provided video link structure. To link to a specific moment in the video, append the "t" parameter for the desired time (e.g., for the 15-second mark, use "t=15").

This instructs the assistant to leverage the knowledge base for relevant, clear responses. Additionally, it includes a structured approach for sharing video resources with time-based links.

#### Conclusion

Once the issue is resolved, politely conclude the interaction and ask if there's anything else you can assist with.

This guides the bot on how to wrap up interactions politely, asking if further help is needed.

### 5. Extra Instructions

\-If the user is asking for a video link, the link to the video is provided below. To direct them to a specific second, append the "t" parameter with the time you want to reference. For example, to link to the 15-second mark, it should look like this: "t=15":

"""\{\{workflow\.contentLinks}}"""

Purpose: Demonstrates the format for linking to specific parts of a video to help students locate precise information.

Significance: Provides clarity on sharing video resources, especially for time-specific instructional content.

\*Handling Edge Cases

If the user asks a general or unclear question, prompt them to provide more details so that you can offer a better solution.

This prepares the assistant to handle vague or general inquiries by prompting users for more details.