---
title: Use Your Own LLM
excerpt: Botpress LLM Interfaces allows you to bring your own LLM for use in your bot.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This guide outlines how to integrate your own Large Language Model (LLM) with Botpress, enabling you to manage privacy, security, and have full control over your AI outputs.

# Using Your Own LLM

## Why Bring Your Own LLM?

Botpress Studio offers an adaptable and powerful platform for building, deploying, and managing AI agents and chatbots. While Botpress provides a suite of pre-integrated language models, you may have specific needs that call for a more customized approach. Bringing your own (LLM) can enhance your solution’s capabilities, allowing you to leverage specialized models tailored to your unique requirements, domain expertise, or compliance needs.

### Tailored Performance and Domain Expertise

Integrating your LLM into Botpress Studio allows you to use models fine-tuned on industry-specific data, enhancing the relevance and quality of responses. This is particularly valuable for industries like finance, healthcare, legal, or customer service, where general-purpose models may not understand the nuanced terminology or context.

### Full Control Over Model Behavior

By bringing your own LLM, you gain complete control over the model’s training data, parameters, and behavior. This flexibility enables you to optimize for specific outputs, ensure the language used aligns with your brand voice, and adjust to any special handling requirements.

### Enhanced Privacy and Security

In industries with strict data privacy regulations, such as GDPR or HIPAA, maintaining control over your LLM can help ensure compliance. With your own LLM, you have greater control over data handling, access, and storage, minimizing risks associated with third-party models and data leaks.

### Cost Efficiency and Scalability

Depending on your scale and use case, managing your LLM can lead to significant cost savings. By optimizing your model’s architecture and usage, you can better control computational costs and resource allocation, particularly when compared to the potentially high API costs of third-party services.

### Integration with Existing AI Pipelines

For organizations already investing in AI infrastructure, integrating their own LLM with Botpress Studio can seamlessly extend their current pipelines. This approach reduces redundancy, leverages existing models and datasets, and aligns with in-house development workflows.

### Experimentation and Customization

Bringing your own LLM provides the freedom to experiment with new architectures, training techniques, and optimization strategies. This freedom is essential for innovation, allowing you to test what works best for your specific application without being limited by the constraints of externally managed models.

### Performance Optimization and Fine-Tuning

In Botpress Studio, you can fine-tune your LLM’s performance based on real-world interactions. This iterative process of adjusting and retraining the model can lead to superior outcomes, as your LLM evolves to meet the changing needs of your users.

### Differentiation and Competitive Advantage

Owning and customizing your LLM allows you to differentiate your product from competitors using standard models. A unique LLM strategy can become a key value proposition, offering enhanced user experiences or capabilities that are not easily replicated.

> 💳 For LLM providers
>
> If you're interested in monetizing your own LLM by making it available for use on Botpress, [contact us.](https://botpress.com/contact-us)

## Instructions

There are three steps to use your own LLM: creating and configuring an integration, adding the LLM invocation logic, and selecting the LLM in the Botpress Studio.

<br />

### 1. Create and configure an integration

Start by [creating an integration](doc:getting-started-1). Once you've done that, you must [install **llm interface**](https://botpress.com/docs/how-to-install-botpress-packages) and adjust the integration definition using the `.extend()` method.

```javascript integration.definition.ts
import { z, IntegrationDefinition } from "@botpress/sdk";
import llm from './bp_modules/llm'

export default new IntegrationDefinition({
  // ... other configuration properties
  name: "my-llm",
  entities: {
    modelRef: {
      schema: z.object({
        id: z.string(),
      }),
    },
  },
})
.extend(llm, ({ modelRef }) => ({
  modelRef,
}));

```

In the above example, lines 14 - 16 were added. Once you are done with that, it's time to implement the LLM logic!

### 2. Add the LLM invocation logic

When you use the `llm interfaces`, you must implement two actions: `generateContent` and `listModels`. These actions define the core functionality of your LLM integration. 

**The listModels method**

Whenever a user chooses an LLM model in the Botpress Studio, all listModels actions are invoked on installed integrations to list all available models. 

Should you wish to act as an LLM provider for Botpress and have users pay for tokens through Botpress, you can use the costPer1MTokens to charge users for using your LLM. For all other use cases, the costPer1MTokens should be set to 0, and billing handled by yourself.  

**The generateContent method**

This method, whos input is a standard input for invoking a create chat completion, must convert the format to a format compatible with your llm, invoke your LLM via api or a client library, and convert the format back to the Botpress format. You can see a working example [here](https://github.com/botpress/botpress/blob/master/integrations/anthropic/src/actions/generate-content.ts). For the format types, we suggest using IntelliSense to guide you.

```javascript index.ts
export default new bp.Integration({
  register: async () => {},
  unregister: async () => {},
  actions: {
    generateContent: async ({input}) => {
      // Implement your own logic for generating content using your LLM
      const result = await myLLM.generateText(input);
      return { result };
    },
    listLanguageModels: async () => {
      // Implement your own logic for listing available models
      const models = [
        {
          id: "model1",
          name: "My LLM 1",
          description: "A highly accurate LLM",
          tags: ["recommended", "vision"],
          input: {
            costPer1MTokens: 1,
            maxTokens: 200_000,
          },
          output: {
            costPer1MTokens: 12,
            maxTokens: 4096,
          },
        },
        {
          id: "model2",
          name: "My LLM 2",
          description: "A more cost-effective LLM",
          tags: ["low-cost"],
          input: {
            costPer1MTokens: 1,
            maxTokens: 200_000,
          },
          output: {
            costPer1MTokens: 12,
            maxTokens: 4096,
          },
        },
      ];
      return { models };
    },
  },
  channels: {},
  handler: async () => {},
})
```

Once you are done with the above, simply deploy the integration, and install it to a bot you'd like to try it on.

### 3. Select your LLM in Botpress Studio

Now you can choose your LLM when configuring AI-related tasks. It will show up in the LLM selectors in the Botpress Studio. 

In the above example, **My LLM 1** and **My LLM 2** appear with the corresponding tags.

<Image align="center" width="200px" src="https://files.readme.io/6311471c2d53aa45e62cec732ec1a0b1a2961bc87c06fbfcdbe4bdc9fa5680d0-Screenshot_2024-08-30_at_9.44.34_AM.png" />

By integrating your own LLM with Botpress, you gain full control over AI outputs, privacy, and security, while also opening up potential monetization opportunities. Follow the outlined steps to configure your integration, implement the LLM logic, and seamlessly deploy it in Botpress Studio for a customized AI experience.

<br />

# Having difficulties with LLM Interfaces?

Contact us at [llm-help@botpress.com](mailto:llm-help@botpress.com) with as much details as possible about your company and your use case.
