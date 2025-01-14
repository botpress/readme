---
title: Secrets
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
Secrets can be defined and managed within the integration definition. The secrets property is an array of secret names that are expected to be provided when configuring the integration. These secret names serve as identifiers for the secrets and are used to retrieve their values when needed.

# Example - Secrets

```javascript
import { IntegrationDefinition } from '@botpress/sdk'

export default new IntegrationDefinition({
  // Other integration properties...
  secrets: ['api_key', 'token', 'password'],
})
```

In this example, the secrets property is an array that contains three secret names: **api\_key**, **token**, and **password**. When configuring the integration, the user will be prompted to provide values for these secrets.

To access the values of the secrets within the integration code, the **ctx.secrets** object can be used. The **ctx.secrets** object provides a secure way to retrieve the values of the secrets by their names. Here's an example:

```javascript
const integration = {
  // ...
  actions: {
    myAction: async (ctx) => {
      const apiKey = ctx.secrets.api_key
      const token = ctx.secrets.token
      const password = ctx.secrets.password

      // Use the secrets in the integration logic...
    },
  },
  // ...
}
```

Your secret values will be asked when executing **bp deploy** using the CLI to deploy your integration, you can also pre-define these values when deploying with **bp deploy --secrets MYSECRET1NAME=MYSECRET1VALUE --secrets MYSECRET1NAME=MYSECRET2VALUE**
