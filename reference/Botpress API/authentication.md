---
title: Authentication
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
To authenticate with the Botpress Cloud API, you'll need to use one of the methods below to obtain an access token.

These tokens can be used as a Bearer token to call all the endpoints of the API, by passing the following HTTP header to the API endpoints:

```
Authorization: Bearer {ACCESS_TOKEN}
```

#### Identity Token

* Personal Access Token (PAT): Can be generated in the Profile Settings section of your [Botpress Cloud account](https://app.botpress.cloud/profile/settings).
* Bot Token: This will be provided to the bot (once deployed) in the `BP_TOKEN` environment variable.
* Integration Token: This will be provided to the integration (once deployed) in the `BP_TOKEN` environment variable.
