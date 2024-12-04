---
title: Botpress Features
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
![](https://files.readme.io/95fa444-image.png)

## Overall Product Specifications

[block:parameters]
{
  "data": {
    "h-0": "Feature",
    "h-1": "Description",
    "0-0": "SDK",
    "0-1": "The utility functions that can be used as arguments in user custom code. You can find the NPM [here](https://www.npmjs.com/package/@botpress/sdk), and API documentation [here](https://botpress.com/docs/api/)",
    "1-0": "Security",
    "1-1": "<ul><li>Audit logs for all activities in your workspace</li><li>Encryption at rest and in transit</li><li>Rate limits & various HTTP-server limits</li><li>SSO - [talk to our sales representatives](https://botpress.com/contact-us)</li></ul>",
    "2-0": "CI/CD",
    "2-1": "One-click publish to production",
    "3-0": "Multi-Channel Support",
    "3-1": "Instantly deliver your bots on all the major messaging channels <br /><ul><li>Botpress Webchat</li><li>Facebook Messenger</li><li>Microsoft Teams</li><li>SMS via Twilio</li><li>WhatsApp</li><li>Line</li><li>Viber</li><li>Instagram</li><li>Coming Soon: Intercom, Webhook, Gmail, Rocketchat and more.</li></ul>",
    "4-0": "Botpress Webchat",
    "4-1": "<ul>**Create custom message widgets**<li>Create your own GUI messages using React</li><li>Customizable with CSS</li><br />**Flexibility for users**<li>Multiple simultaneous conversations with the same bot</li><li>Reset & delete conversation (for privacy purposes)</li><li>File-sharing using Shareable link</li><li>Hosted on AWS S3 or BPFS</li></ul>",
    "5-0": "Custom Chatbot Branding",
    "5-1": "[Rebrand the Botpress webchat interface](https://botpress.com/docs/cloud/webchat-customization/overview)",
    "6-0": "Community Support",
    "6-1": "<ul><li>[Botpress forum & community](https://discord.gg/botpress)</li><li>Intercom live support</li></ul>",
    "7-0": "Multilingual Support",
    "7-1": "<ul><li>Supported Languages: you can use Botpress to make bots in 100+ languages. However during the early preview of the new Botpress, only English is supported for natural language understanding.</li><li>Learn more about languages: [here](https://botpress.com/docs/cloud/getting-started/languages)</li></ul>",
    "8-0": "Conversational AI Management",
    "8-1": "<ul><li>Managed Natural Language Understanding (NLU) Engine - an industrial-grade native NLU engine, from domain specific natural language to structured data</li><li>**Intent classification** - understand the type of action or out of scope conveyed in the sentences and all its participating parts (e.g. book a flight, order dinner, buy a product, etc.)</li><li>**Entity extraction** - locate and classify named entities into predefined categories such as person names, organizations, locations, product SKUs, etc. Regex/pattern entities, List entities, Fuzzy matching, pre-built entities</li><li>**Slot tagging** - tag the words which carry meaning to the sentences (e.g. landing city, type of meal, etc.)</li><li>**Language identification** - determining the natural language that a document or part thereof is written in (e.g. English, French, etc.)</li><li>**Natural Language Understanding**: any number of languages within the same chatbot; the bot is able to detect the user's language and then answer in kind</li><li>**Spell checking** - check for misspellings and automatically fix the spelling mistakes so that the downstream NLU performs more accurately</li></ul>",
    "9-0": "Built-in Content Types",
    "9-1": "[Supported content types for each channel](https://botpress.com/docs/cloud/channels/overview/#supported-content-types)",
    "10-0": "Visual conversation / dialog management",
    "10-1": "Visual developer interface to create and management dialog states and topic <br /><ul><li>Low-code drag and drop user interface</li><li>Multiple visual flows and subflows with conditions divided by topics</li><li>Multi-turn and the ability to jump from a topic to another seamlessly</li><li>Topic management - process that enables data elements pertaining to a specific topic to be maintained within conversations (e.g. user name, SKU number, etc.)</li><li>Conversational detours - while the visual flows represent the \"happy paths\" that are desired by the conversation designers, detours are about automatically and gracefully handling exceptions</li><li>Template management - use pre-made templates to get started or find inspiration</li><li>Intelligent slot filling - prompting for missing form fields</li><li>Workflow management - group and reuse flows and subflows to embed and manage domain specific knowledge</li><li>Code autocompletion and user interface shortcuts</li></ul>",
    "11-0": "FAQ/Q&A",
    "11-1": "Create, manage, and centrally access the most frequently asked questions the users may have <br /><ul><li>Context management</li><li>Rich messages</li><li>Message \"alternatives\" - the bot doesn’t always say the same thing</li></ul>",
    "12-0": "Human in the Loop (HITL)",
    "12-1": "Straightforward integrations with leading third party HITL, including Salesforce, Zendesk, Servicenow, Oracle, Intercom, Genesis, Twilio Flex, Nuance and LiveAgent.",
    "13-0": "Analytics & continuous chatbot training",
    "13-1": "Dashboards and tools to capture and improve user engagement and chatbot accuracy <br /><ul><li>Misunderstood - capture everything the chatbot doesn't understand and use it to improve your chatbot or expand its capabilities</li><li>Engagement</li><li>Conversations</li><li>Interactions</li></ul>",
    "14-0": "Testing, debugging, and logging",
    "14-1": "End-to-end conversation emulation & testing <br />NLU testing <br />Debugging tools <br />Logging",
    "15-0": "Chatbot privacy",
    "15-1": "<ul><li>Sensitive data / conversation obfuscation</li><li>Variable time-based deletion</li><li>Selective data persistence</li></ul>",
    "16-0": "Javascript IDE",
    "16-1": "<ul><li>Easily integrate with your internal systems and any third parties</li><li>Actions & Hooks - create and edit actions within Botpress (e.g. call an API). Features typing and intelligent code completion</li><li>VS Code embedded in Botpress Studio</li></ul>",
    "17-0": "Terms and Conditions",
    "17-1": "[Terms and Conditions](https://botpress.com/company/terms)"
  },
  "cols": 2,
  "rows": 18,
  "align": [
    "left",
    "left"
  ]
}
[/block]


## Enterprise-Specific Features​

<Table>
  <Tr>
    <Td>**Feature**</Td>
    <Td>**Description**</Td>
  </Tr>
  <Tr>
    <Td>Enhanced Enterprise Security for Chatbot users</Td>
    <Td>Identity transmission - securely transmit the user identity to the webchat from the host web page</Td>
  </Tr>
  <Tr>
    <Td>Role-based access control (RBAC)</Td>
    <Td>
      RBAC - Users can be assigned roles, and permissions can be managed with regards to these roles in terms of giving
      users read and/or write access to specific features
    </Td>
  </Tr>
  <Tr>
    <Td>Single-Sign On (SSO)</Td>
    <Td>
      Seamlessly link Botpress to your identity provider, OAuth2 for Google, Github, Azure
      <br />
      Talk to sales for more information
    </Td>
  </Tr>
  <Tr>
    <Td>Scalability</Td>
    <Td>Botpress has you covered: your chatbot solution adapts instantaneously as your user base grows</Td>
  </Tr>
  <Tr>
    <Td>Monitoring</Td>
    <Td>
      Directly monitor messages left on your community plan
      <br />
      Set up alerts for messages and keep an eye on your monthly message traffic
    </Td>
  </Tr>
  <Tr>
    <Td>Enterprise Support</Td>
    <Td>
      Advanced Botpress technical support
      <br />
      Standard: EST business hours
      <br />
      Premium: 24/7
      <br />
      SLA
    </Td>
  </Tr>
  <Tr>
    <Td>Integrations</Td>
    <Td>For a full list of integrations check out our [integration hub](https://botpress.com/hub)</Td>
  </Tr>
  <Tr>
    <Td>Collaboration</Td>
    <Td>
      Real-time collaboration, with workspaces to organize both chatbots and developer work
      <br />
      Realtime collaborative interface (with lock management)
      <br />
      Workspaces - logical unit that groups up your conversational assistants based on the purpose of the chatbots or
      for something more granular such as for a specific task, etc.
    </Td>
  </Tr>
</Table>