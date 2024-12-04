---
title: Introduction
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
## Introduction[](https://botpress.com/docs/api-documentation/#introduction)

The Botpress API is a RESTful set of HTTP endpoints that allow you to create, deploy, and run chatbots on the [Botpress Cloud](https://botpress.com/).

It can be used to create and manage bots, handle conversations and messages, as well as to manage their content, users, and configuration.

The base URL of the Botpress Cloud API is: `https://api.botpress.cloud`

The API endpoints will expect the `Content-type: application/json` HTTP header to be present in the request and the request body (if any) to be in JSON format, and will send back the same header in the response and return a JSON response body as well.

## Using the Botpress Client[](https://botpress.com/docs/api-documentation/#using-the-botpress-client)

If you're using JavaScript or TypeScript, we recommend using our official [Botpress Client](https://www.npmjs.com/package/@botpress/client) to call our API, but if you're using another programming language or just want direct access to our REST API you can use this documentation as reference.

## Authentication[](https://botpress.com/docs/api-documentation/#authentication)

To authenticate with the Botpress Cloud API, you'll need to use one of the methods below to obtain an access token.

These tokens can be used as a Bearer token to call all the endpoints of the API, by passing the following HTTP header to the API endpoints:

```
Authorization: Bearer {ACCESS_TOKEN}
```

#### Identity Token

- Personal Access Token (PAT): Can be generated in the Profile Settings section of your [Botpress Cloud account](https://app.botpress.cloud/).
- Bot Token: This will be provided to the bot (once deployed) in the `BP_TOKEN` environment variable.
- Integration Token: This will be provided to the integration (once deployed) in the `BP_TOKEN` environment variable.

## Pagination[](https://botpress.com/docs/api-documentation/#pagination)

The "List" endpoints of our API will return paginated results based on the creation date of the resource, with a default limit of 20 results per page.

When the number of results exceeds the limit, the response body will include a `meta.nextToken` property that can be passed as a query string parameter (e.g. `endpoint?nextToken={nextToken}`) to retrieve the next page of results.

If there are no more results, the endpoint will not provide a `nextToken` value.

#### Example:

1. Call the `/v1/chat/conversations` endpoint to obtain the first page of results:

```json json
{  "conversations": [    (...)  ],  "meta": {    "nextToken": "wwNgQn6tWNR/IHhKGHv/sg9zcIAGsxOk0TfmM+DdmcWkBZrXYjVvcfSZIZSs4ppCr/g="  }}
```

1. Call the endpoint again but now passing the `nextToken` as a query string parameter, making sure the value is URL-encoded:

```
/v1/chat/conversations?nextToken=wwNgQn6tWNR%2FIHhKGHv%2Fsg9zcIAGsxOk0TfmM%2BDdmcWkBZrXYjVvcfSZIZSs4ppCr%2Fg%3D
```

1. Repeat until the response body doesn't provide a `nextToken` value anymore:

```
{  "conversations": [    (...)  ],  "meta": {}}
```

## Errors[](https://botpress.com/docs/api-documentation/#errors)

If an error occurs when calling an API endpoint, the response will return the appropriate HTTP status code as indicated below and the response body will be one of the following JSON objects indicating the nature of the error:

#### Unknown

```
 {  "type": "Unknown",  "description": "An unknown error occurred",  "status": 500}
```

#### Internal

```
 {  "type": "Internal",  "description": "An internal error occurred",  "status": 500}
```

#### Unauthorized

```
 {  "type": "Unauthorized",  "description": "The request requires to be authenticated.",  "status": 401}
```

#### Forbidden

```
 {  "type": "Forbidden",  "description": "The requested action can't be peform by this resource.",  "status": 403}
```

#### Payload Too Large

```
 {  "type": "PayloadTooLarge",  "description": "The request payload is too large.",  "status": 413}
```

#### Invalid Payload

```
 {  "type": "InvalidPayload",  "description": "The request payload is invalid.",  "status": 400}
```

#### Unsupported Media Type

```
 {  "type": "UnsupportedMediaType",  "description": "The request is invalid because the content-type is not supported.",  "status": 415}
```

#### Method Not Found

```
 {  "type": "MethodNotFound",  "description": "The requested method does not exist.",  "status": 405}
```

#### Resource Not Found

```
 {  "type": "ResourceNotFound",  "description": "The requested resource does not exist.",  "status": 404}
```

#### Invalid Json Schema

```
 {  "type": "InvalidJsonSchema",  "description": "The provided JSON schema is invalid.",  "status": 400}
```

#### Invalid Data Format

```
 {  "type": "InvalidDataFormat",  "description": "The provided data doesn't respect the provided JSON schema.",  "status": 400}
```

#### Invalid Identifier

```
 {  "type": "InvalidIdentifier",  "description": "The provided identifier is not valid. An identifier must start with a lowercase letter, be between 2 and 100 characters long and use only alphanumeric characters.",  "status": 400}
```

#### Relation Conflict

```
 {  "type": "RelationConflict",  "description": "The resource is related with a different resource that the one referenced in the request. This is usually caused when providing two resource identifiers that aren't linked together.",  "status": 409}
```

#### Reference Constraint

```
 {  "type": "ReferenceConstraint",  "description": "The resource cannot be deleted because it's referenced by another resource",  "status": 409}
```

#### Reference Not Found

```
 {  "type": "ReferenceNotFound",  "description": "The provided resource reference is missing. This is usually caused when providing an invalid id inside the payload of a request.",  "status": 400}
```

#### Invalid Query

```
 {  "type": "InvalidQuery",  "description": "The provided query is invalid. This is usually caused when providing an invalid parameter for querying a resource.",  "status": 400}
```

#### Runtime

```
 {  "type": "Runtime",  "description": "An error happened during the execution of a runtime (bot or integration).",  "status": 400}
```

#### Already Exists

```
 {  "type": "AlreadyExists",  "description": "The record attempted to be created already exists.",  "status": 409}
```

#### Rate Limited

```
 {  "type": "RateLimited",  "description": "The request has been rate limited.",  "status": 429}
```

#### Payment Required

```
 {  "type": "PaymentRequired",  "description": "A payment is required to perform this request.",  "status": 402}
```

#### Quota Exceeded

```
 {  "type": "QuotaExceeded",  "description": "The request exceeds the allowed quota. Quotas are a soft limit that can be increased.",  "status": 403}
```

#### Limit Exceeded

```
 {  "type": "LimitExceeded",  "description": "The request exceeds the allowed limit. Limits are a hard limit that cannot be increased.",  "status": 413}
```

#### Breaking Changes

```
 {  "type": "BreakingChanges",  "description": "Request payload contains breaking changes which is not allowed for this resource without a version increment.",  "status": 400}
```