---
title: Files API
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
The Files API allows you to upload, download, and manage files and searchable documents for your bots and integrations in Botpress Cloud.

Files can be in any text or binary format, and documents (such as PDF, Microsoft Office, HTML, CSV, etc.) can be indexed to be used for semantic search in RAG (Retrieval Augmented Generation) implementations. Files are private by default but can be made publicly accessible through a permanent URL that's unique for each file.

<br />

# Getting Started

1. Get familiarized with the [API reference](../docs/api-documentation/#files) and the different API endpoints available

2. Review the [instructions on how to authenticate](../docs/api-documentation/#authentication) with the API.

<br />

# Examples

# Creating and uploading a file

## In an Execute Card in your bot

The following code snippet can be put in an Execute Card in your bot to create and upload a file that can be accessed by anyone with the file URL and that will be indexed for semantic search:

> Note: Make sure you have enabled the "Use the Botpress Client" setting in your bot's settings in Botpress Studio in order to have access to the `client` global variable, otherwise it will not be accessible and you'll get an error.

```javascript
const file = await client.uploadFile({
  key: 'optional_prefix/unique_file_name.txt', // Each file needs a unique key under your bot
  content: 'This is a test file',
})
```

Once the code above runs, the URL to download the file will be available in the `file.url` property.

By default the file URL returned will be temporary and change on each request to this endpoint, and will expire after a short period of time and thus should not be stored long-term, but if the file was created with a 'public\_content' access policy then this URL will be permanent and can be stored long-term.

### Uploading from an existing URL

Or if the file is already available in a URL and you want to download and then upload it to Botpress Cloud you can pass it in the `url` parameter instead of using the `content` parameter:

```javascript
const file = await client.uploadFile({
  key: 'unique_file_name.pdf', // Each file needs a unique key under your bot
  url: 'https://example.com/test.pdf', // This is the external URL where the file is currently located
})
```

### Uploading a binary file

If you are dealing with a binary file such as a PDF or Microsoft Office document you can also pass a `Buffer` object as the `content` parameter for the file:

```javascript
const buffer = // This must be a Buffer object containing the binary content of the file

const file = await client.uploadFile({
  key: 'unique_file_name.pdf', // Each file needs a unique key under your bot
  content: buffer,
})
```

<br />

## In a custom script using the Botpress Client

If you're using Javascript or TypeScript the easiest way to interact with the API is using the [Botpress Client](https://www.npmjs.com/package/@botpress/client). You can install the client package by using your favorite package manager:

```Text npm
npm install @botpress/client
```
```Text pnpm
pnpm install @botpress/client
```
```
yarn add @botpress/client
```

The Botpress Client will handle the authentication and other details for you, you just need to provide your Botpress PAT (Personal Access Token) to the client and the ID of the bot that the client will access. If your use-case requires accessing multiple bots, you can define as many client instances as needed (one for each bot).

You can use the following code snippet to create and upload a file in a custom script using the Botpress Client. Note that in the example below your Botpress PAT (Personal Access Token) and bot ID must be defined in the environment variables `BOTPRESS_PAT` and `BOTPRESS_BOT_ID` respectively.

```javascript
import { Client } from '@botpress/client'

const client = new Client({
  token: process.env.BOTPRESS_PAT,
  botId: process.env.BOTPRESS_BOT_ID,
})

const file = await client.uploadFile({
  key: 'optional_prefix/unique_file_name.txt',
  content: 'This is a test file',
})
```

<br />

## In a custom script using an HTTP client

If you can't use the Botpress Client (e.g. you can't install the package or you're working with a different programming language) you can also use any HTTP client to make requests to the API directly.

Please note that when calling the API directly, an HTTP request to the Botpress API (specifying the file size beforehand) will be needed to create the empty file first, and a separate HTTP request will be needed to upload the file content to the unique upload URL provided in the response of the first request.

Additionally, if you need to access the file URL right away a third request to the "Get File" API endpoint will be needed to get the URL of the file after it has been uploaded.

Here's an example on how to do this using the native `fetch()` function in Javascript/TypeScript, note that your Botpress PAT will need to be defined in the environment variable `BOTPRESS_PAT`:

```javascript
const fileContent = 'Here goes the content of your file'

const buffer = Buffer.from(fileContent)

// Step 1: Create the file in Botpress Cloud.
// Please note that specifying the file size (in raw bytes, not characters) is required when calling this endpoint.
const result = await fetch('https://api.botpress.cloud/v1/files', {
  method: 'PUT',
  headers: {
    'x-bot-id': 'YOUR_BOT_ID_GOES_HERE',
    'Content-Type': 'application/json',
    Authorization: `Bearer ${process.env.BOTPRESS_PAT}`,
  },
  body: JSON.stringify({
    key: 'unique_file_name.txt',
    size: buffer.byteLength,
  }),
})

const response = await result.json()

// Step 2: Upload the file content to the unique upload URL provided for the created file.
await fetch(response.file.uploadUrl, {
  method: 'PUT',
  body: buffer,
})

// The variable below will contain the URL to download the file content uploaded above. If the file was
// created with the 'public_content' access policy it will be a permanent URL that you can store long-term,
// otherwise it will contain a temporary pre-signed URL that expires after a short period of time.
// If you need to get a new URL, you can always use the `getFile` API endpoint.
const downloadUrl = response.file.url
```

<br />

## Adding tags to a file

You can add custom tags to a file by passing the `tags` parameter when it's created. Tags allow you to organize and classify files in any way you see fit, and can be specified as a filter when listing or searching files.

```javascript
const file = await client.uploadFile({
  key: 'test.txt',
  content: 'This is a test file',
  tags: {
    // Tags are optional but are useful for filtering files by a custom criteria you choose when using the "List Files" or "Search Files" API endpoints. You can change or remove the tags below based on your needs.
    category: 'Sales',
    knowledgeBaseName: 'Client Questions',
  },
})
```

<br />

## Creating a public file

By default all files are private and can only be accessed by the bot that created them. If you need to make a file publicly accessible by anyone you can assign the `public_content` access policy to the file:

```javascript
const file = await client.uploadFile({
  key: 'test.txt',
  content: 'This is a public file',
  accessPolicies: ['public_content'],
})
```

If you only want to allow all the integrations installed in the bot to access the file rather than making it fully public, you can just assign the `integrations` access policy instead:

```javascript
const file = await client.uploadFile({
  key: 'test.txt',
  content: 'This is a file that can be accessed by all integrations in a bot',
  accessPolicies: ['integrations'],
})
```

<br />

## Creating an indexed file

If you need to index a file for semantic search you can use the `index` parameter when creating the file.

```javascript
const file = await client.uploadFile({
  key: 'test.txt',
  content: 'This is a test file',
  index: true,
})
```

<br />

#### Supported file formats

The following file formats are supported for indexing:

| Format   | File Extension | MIME Type       |
| -------- | -------------- | --------------- |
| PDF      | .pdf           | application/pdf |
| HTML     | .html          | text/html       |
| Text     | .txt           | text/plain      |
| Markdown | .md            | text/markdown   |

### Notes on indexing:

* The file it will initially have a status of "indexing\_pending" and will be indexed asynchronously. The time it takes to index the file will depend on the file size and the current load on the system.
* You can check the status of the file by calling the [Get File](../docs/api-documentation/#get-file) endpoint and checking that the `file.status` property has changed to "indexing\_completed".
* If the indexing failed the status will be set to "indexing\_failed" and the reason of the failure will be available in the `failedStatusReason` property of the file.

<br />

## Getting the file's metadata

To get the details of a file you can use the [Get File](../docs/api-documentation/#get-file) API endpoint.

You can also use this endpoint to retrieve a new temporary pre-signed URL to download a file if the previous pre-signed URL has already expired.

```Text Using the Botpress Client
 const file = await client.getFile('YOUR_FILE_ID')
```
```Text Calling the API directly
const result = await fetch('https://api.botpress.cloud/v1/files/YOUR_FILE_ID', {
  method: 'GET',
  headers: {
    'x-bot-id': 'YOUR_BOT_ID_GOES_HERE',
    Authorization: `Bearer ${process.env.BOTPRESS_PAT}`,
  },
})
 
const response = await result.json()
const file = response.file
```

<br />

## Listing existing files of a bot

To list all the files of a bot you can use the [List Files](../docs/api-documentation/#list-files) API endpoint.

```Text Using the Botpress Client
const res = await client.listFiles()
const files = res.data.files
```
```Text Calling the API directly
const result = await fetch('https://api.botpress.cloud/v1/files', {
  method: 'GET',
  headers: {
    'x-bot-id': 'YOUR_BOT_ID_GOES_HERE',
    Authorization: `Bearer ${process.env.BOTPRESS_PAT}`,
  },
})
 
const response = await result.json()
const files = response.files
```

### Filtering by tags

If you need to filter files by tags, you can just pass the `tags` parameter which should be an object with key-value pairs of tags a file must have in order to be returned. Tag filtering works in an "AND" fashion, so only the files that have all the specified tags will be returned.

```Text Using the Botpress Client
const res = await client.listFiles({
  tags: {
    category: 'Sales',
  },
})
```
```Text Calling the API Directly
const tags = {
  category: 'Sales',
}
 
const result = await fetch('https://api.botpress.cloud/v1/files?tags=' + encodeURIComponent(JSON.stringify(tags)), {
  method: 'GET',
  headers: {
    'x-bot-id': 'YOUR_BOT_ID_GOES_HERE',
    Authorization: `Bearer ${process.env.BOTPRESS_PAT}`,
  },
})
```

> 📘 Calling the API Directly
>
> If you're making the HTTP request directly to the API please note that you'll need to pass the tags parameter as a JSON-serialized, URL-encoded string (the Botpress Client handles this automatically for you).

### Pagination

The [List Files](../docs/api-documentation/#list-files) API endpoint will return by default the 20 most recent files your bot has. If you need to list older files you can use the `nextToken` property returned in the API response to retrieve the next page (if any) of files. The `nextToken` will be included for each page if there are files remaining to be listed.

For example:

```javascript
let res = await client.listFiles()
const files = res.data.files

// You can put this in a loop to retrieve all the files if needed.
if (res.data.nextToken) {
  res = await client.listFiles({ nextToken: res.data.nextToken })
  files.push(...res.data.files)
}
```

<br />

## Updating the file metadata

Only the tags and access policies of a file can be updated.

Here's an example of how to update the access policies and tags of a file using the Botpress Client:

```Text Using the Botpress Client
await client.updateFile({
  id: 'YOUR_FILE_ID',
  accessPolicies: ['integrations'], // This value will replace the existing access policies of the file.
  tags: {
    // This acts as a "patch" or partial update, so only the tags specified here will be updated, the rest will remain unchanged. If you need to delete an existing tag, you can set it to a `null` value.
    category: 'Support', // This tag will be updated.
    knowledgeBaseName: null, // This tag will be deleted.
    subcategory: 'Technical', // This tag will be added.
    // Any other tags not specified here will remain unchanged.
  },
})
```
```Text Calling the API Directly
await fetch(
  'https://api.botpress.cloud/v1/files/YOUR_FILE_ID',
  {
    method: 'PUT',
    headers: {
      'x-bot-id': 'YOUR_BOT_ID_GOES_HERE',
      Authorization: `Bearer ${process.env.BOTPRESS_PAT}`,
    },
    body: {
      accessPolicies: ['integrations'], // This value will replace the existing access policies of the file.
      tags: {
        // This acts as a "patch" or partial update, so only the tags specified here will be updated, the rest will remain unchanged. If you need to delete an existing tag, you can set it to a `null` value.
        category: 'Support', // This tag will be updated.
        knowledgeBaseName: null, // This tag will be deleted.
        subcategory: 'Technical', // This tag will be added.
        // Any other tags not specified here will remain unchanged.
      },
    },
  }
)
```

### Updating file content

If you need to update the content of a file, you can create a new file with the updated content and then delete the old file. The file ID will change in this case.

<br />

## Deleting a file

To delete a file you can use the "Delete File" API endpoint.

```Text Using the Botpress Client
await client.deleteFile('YOUR_FILE_ID')
```
```Text Calling the API Directly
await fetch('https://api.botpress.cloud/v1/files/YOUR_FILE_ID', {
  method: 'DELETE',
  headers: {
    'x-bot-id': 'YOUR_BOT_ID_GOES_HERE',
    Authorization: `Bearer ${process.env.BOTPRESS_PAT}`,
  },
})
```

<br />

## Searching files

To run a semantic search on your bot's files you can use the [Search Files](/api-documentation/#search-files) API endpoint. This is particularly useful for RAG (Retrieval Augmented Generation) implementations.

```Text Using the Botpress Client
const res = await client.searchFiles({
  query: 'what are the most popular products of your company?', // This is the natural language query (e.g. a user's question) to be used for running a semantic search on the files of the bot.
  contextDepth: 1, // Optional (default: 0), allows you prepend and append the surrounding context to each matching passage in the search results
  tags: {
    // Optional, allows you to only search files that match the specified tags. Useful if you only want to search a subset of the bot's files.
    category: 'Support',
    subcategory: 'Technical',
  },
  limit: 30, // Default is 20, maximum is 50 results
})
 
const passages = res.data.passages
 
for (const passage of passages) {
  // You can use passage.content here to retrieve the content (including surrounding context, if any) of each matching passage
}
```
```Text Calling the API Directly
const params = new URLSearchParams({
  query: 'what are the most popular products of your company?',
  tags: JSON.stringify({
    category: 'Support',
    subcategory: 'Technical',
  }),
})
 
const result = await fetch('https://api.botpress.cloud/v1/files/search?' + params.toString(), {
  method: 'GET',
  headers: {
    'x-bot-id': 'YOUR_BOT_ID_GOES_HERE',
    Authorization: `Bearer ${process.env.BOTPRESS_PAT}`,
  },
})
 
const response = await result.json()
const passages = response.passages
```

You can check the [API reference](/api-documentation/#search-files) for more details on the properties available for each passage object returned in the response.

### Using the search results for RAG

You can use the search results to provide relevant information to a chatbot for generating a response to a user's question.

Here's an example of a simple RAG (Retrieval Augmented Generation) implementation that shows how you can use the ChatGPT large language model (through the OpenAI API) and the search results provided by our API to answer a user's question:

```javascript
import OpenAI from 'openai' // You'll need to install this package first using your favorite package manager

const openai = new OpenAI({ apiKey: 'YOUR_OPENAI_API_KEY' })) // Change this for your own OpenAI API key

const userQuestion = 'Which are the most popular products of your company?' // This will come from the user's input

const res = await client.searchFiles({
  query: userQuestion,
  contextDepth: 1, // This number can be increased to pass more context to the model for each matching passage
})

const relevantInformation = res.data.passages.map(passage => passage.content).join("\n\n----------\n\n")

const answer = await openai.chat.completions.create({
    model: 'gpt-3.5-turbo', //  This can be changed for any other OpenAI model available here: https://platform.openai.com/docs/models
    messages: [
        {
            role: 'system',
            // You can change the text below to include any additional instructions to the model
            content: "You are a helpful assistant that answers the user's question based only on the relevant information you are provided along with the question.",
        },
        {
            role: 'user',
            content: `## RELEVANT INFORMATION: \n\n ${relevantInformation}\n\n` +
                     `## ANSWER THE FOLLOWING USER'S QUESTION: \n\n ${userQuestion}`,
        },
    ],
})
```

<br />

# Security

## Access Policies

A file can have a list of special access policies:

* `public_content`: Unauthenticated users can read contents (but not metadata) of the file through a unique permanent URL provided by the API for each file. Without this policy the file URL returned by the API will be temporary and will expire after a short period of time.
* `integrations`: Grants read, search, list access to all integrations of the bot that owns the file.

<br />

## Permissions

| Principal                                            | Permissions                                                                                                               |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Public (unauthenticated/unauthorized users)          | Can only download files that have the `public_content` access policy.                                                     |
| Bot                                                  | Owns and manages its files with full permissions to access and manage them, regardless of the user that created the file. |
| Integration                                          | Has all permissions on the files that were created by that integration for the bot they are installed on.                 |
| Viewer workspace member                              | Can read, search, and list all files for the bot, regardless of creator, but cannot create or delete files.               |
| Developer, Manager or Administrator workspace member | Has all permissions on the bot's files, regardless of creator.                                                            |
| Billing Manager workspace member                     | No permissions on files.                                                                                                  |

> 📘 Note
>
> The [List Files](../docs/api-documentation/#list-files) API endpoint will filter out files that are not accessible to the user calling that API endpoint.

<br />

# Pricing

There are two types of storage: File Storage and Vector DB Storage. All files count toward your workspace's File Storage usage. Indexed files also count toward your workspace's Vector DB Storage usage.

For full details on pricing please check our [Pricing page](https://botpress.com/pricing).

<br />

# Quotas/Limits

* Maximum file size: 100 MB
* Rate limits: [same as all other endpoints](../docs/preventing-abuse) of our public API
* Tags
  * As defined in the [Limits and Quotas of Botpress Cloud](../docs/limits-and-quotas-of-botpress-cloud)
* Search
  * Query: 1 KB maximum
  * Maximum number of results: 50
