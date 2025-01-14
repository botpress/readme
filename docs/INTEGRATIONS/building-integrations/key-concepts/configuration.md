---
title: Configuration
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
When it comes to chatbot integrations, the **configuration** component plays a pivotal role. It's used to define the schema of the integration's settings and handles the validation of the provided configuration data.

It also serves as a secure place to store sensitive data such as API keys, access tokens, or other secrets that the chatbot needs to interact with the platform.

Here's a detailed explanation of each part:

# Defining Configuration Schema

The configuration schema is a blueprint that outlines the necessary parameters for the chatbot integration to function properly.

This includes parameters like API keys, access tokens, server URLs, etc., depending on the requirements of the specific platform being integrated.

The schema is defined in the **configuration** object, where each key corresponds to a configuration parameter.

Each parameter must specify a **type**, such as **string**, **number**, **boolean**, etc.\
Some parameters might be marked as **required** if they are necessary for the integration to function.

<br />

# Validation

Once the configuration schema is defined, it serves as a validation rule set for the integration. Whenever an attempt is made to add or update the integration's configuration, the provided configuration is checked against the schema.

This validation ensures that all required parameters are present and that they are of the correct type. If the validation fails, the integration should provide a meaningful error message indicating what was missing or incorrect.

<br />

# Storing Sensitive Information

The **configuration** object can store sensitive data like API keys, tokens, and other platform-specific credentials. This data is provided by the user when adding the integration to their bot.

This sensitive data is essential for the chatbot to authenticate with the platform and perform actions on behalf of the user. It's important to ensure that this data is securely handled and stored to maintain the security of the user's information and the integrity of the integration.

In essence, the configuration is an essential part of any chatbot integration. It dictates what information is necessary for the integration to function, validates the provided information, and securely stores important data.

Understanding how to define and work with the configuration is key to developing successful chatbot integrations.

<br />

# Example - Configuration Fields

```javascript
const integration = {
  // ...
  configuration: {
    fields: [
      {
        name: 'api_key',
        type: 'string',
        description: 'API key for the platform',
        secret: true, // This field indicates that this is sensitive data
        required: true, // This field should be provided by the user
      },
      {
        name: 'token',
        type: 'string',
        description: 'Token for interacting with the platform API',
        secret: true,
        required: true,
      },
    ],
  },
  // ...
}
```

In this example, the **configuration** object contains a field array that includes two objects.

Each object represents a single **configuration** field that the user must provide when setting up the integration.

1. The **name** field is the identifier for the configuration field.
2. The **type** field indicates the expected data type of the **configuration** field's value.
3. The **description** field provides the user with a brief explanation of the purpose of the configuration field.
4. The **secret** field is a boolean flag that, when set to true, indicates that the field is sensitive and should be treated as such (e.g., not being displayed in plaintext in the user interface).
5. The **required** field indicates whether or not this field must be provided for the integration to function.

These are general guidelines; the exact configuration schema may vary based on the requirements of the platform you're integrating with. Be sure to refer to the specific platform's API documentation to understand which fields are needed and how they should be treated.
