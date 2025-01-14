---
title: Definitions
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
In Botpress, definitions form the foundation of your integration and are crucial in ensuring smooth interaction between the bot and the desired platform, in this case Slack.

They hold essential components such as channels, actions, events, and configurations, among others. Each of these components needs to be clearly defined before being utilized in the integration.

# Example - Defining Slack Integration

Consider the following example where we define the Slack integration in Botpress:

```javascript
import { IntegrationDefinition } from '@botpress/sdk'
import { sentry as sentryHelpers } from '@botpress/sdk-addons'

import { INTEGRATION_NAME } from './src/const'
import { actions, events, configuration, channels, states, user } from './src/definitions'

export default new IntegrationDefinition({
  name: INTEGRATION_NAME,
  title: 'Slack',
  description: 'This integration allows your bot to interact with Slack.',
  version: '0.2.0',
  icon: 'icon.svg',
  readme: 'readme.md',
  configuration,
  states,
  channels,
  actions,
  events,
  secrets: sentryHelpers.COMMON_SECRET_NAMES,
  user,
})
```

In this code snippet, the **IntegrationDefinition** class from the Botpress SDK is used to create an instance representing the Slack integration.

Several components are defined:

1. **configuration**: defines the configuration schema of the integration, used for storing sensitive information such as API keys.
2. **states**: includes definitions of the different states that the bot can enter during a conversation.
3. **channels**: indicates which channels the integration supports.
4. **actions**: lists the actions that the bot can perform, such as adding a reaction.
5. **events**: covers non-conversational events, such as the creation of a new issue.
6. **user**: provides a mapping between the integration channel and Botpress.

Each component is imported from the **definitions** module, which contains separate files for each component.\
As a developer, it is crucial to ensure all the components needed for your integration are properly defined in the definitions module. Then they will be available for import in the main integration definition file.

Remember, the Botpress platform relies on these **definitions** to ensure the correct functioning of your integration, making them a pivotal part of your development process.

# Integration components

* **name**: The name of the integration. It can be a string or a constant representing the integration's unique identifier.

* **title**: The title or display name of the integration. It provides a human-readable name for the integration.

* **description**: A brief description of the integration, explaining its purpose and functionality.

* **version**: The version number of the integration. It helps track and manage updates to the integration over time.

* **icon**: The path or filename of the icon file associated with the integration. It represents the visual identity of the integration.

* **readme**: The path or filename of the README file for the integration. It typically provides detailed instructions, documentation, or guidelines for using the integration.

* **configuration**: The configuration schema for the integration. It defines the required parameters and their types that need to be provided when configuring the integration. This includes sensitive data such as API keys or access tokens.

* **states**: The definitions of different states that the bot can enter during a conversation. States help manage and maintain context throughout a conversation.

* **channels**: The channels supported by the integration. It defines the channels (e.g., Slack, Telegram, Facebook Messenger) that the bot can interact with through the integration.

* **actions**: The actions that the bot can perform through the integration. Actions represent specific tasks or behaviors that the bot can execute, such as sending a message, retrieving data, or performing external operations.

* **events**: The non-conversational events that the integration can handle. These events are triggered by external factors or actions and can be used to perform specific actions or respond to certain events.

* **secrets**: The names of the secrets required for the integration. Secrets are sensitive information, such as API keys or access tokens, that need to be securely stored and accessed within the integration.

* **user**: The mapping between the integration channel and Botpress. It defines how the user is identified or associated with the integration, allowing the integration to perform actions on behalf of the user.

Each of these properties plays a crucial role in defining and configuring the integration, enabling smooth interaction between the bot and the desired platform (in this case, Slack).
