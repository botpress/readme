---
title: Upsert File
excerpt: >-
  Creates or updates a file using the `key` parameter as unique identifier.
  Updating a file will erase the existing content of the file. Upload the file
  content by sending it in a PUT request to the `uploadUrl` returned in the
  response.
api:
  file: botpress-api.json
  operationId: upsertFile
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
To associate a file with a knowledge base, you must use these tags:

```json json
{
  ...yourTags,
  source: 'knowledge-base',
  kbId: 'kb-2f0a7ea639',
}
```

You can get the kbId from the URL on the Knowledge Base you want to upsert the file to. For example:

![](https://files.readme.io/4ae6897-image.png)

in the above image, the kbId would be kb-2f0a7ba679.
