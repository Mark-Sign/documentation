---
layout: default
title: Temporary document signing link generation
parent: Iframe APIs
grand_parent: API Reference
has_toc: true
nav_order: 1
---

# Temporary document signing link generation
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

Short description

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path</td>
      <td>/api/document/generate-temporary-signing-link.json</td>
    </tr>
    <tr>
      <td>Method</td>
      <td>POST</td>
    </tr>
    <tr>
      <td>Request Body Schema</td>
      <td>application/json</td>
    </tr>
  </tbody>
</table>

## Request body parameter description

| Key                          | Requirement        | Type                  | Description                                                                                                                                  |
|:-----------------------------|:-------------------|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| access_token                 | Mandatory          | String                | API Access Token                                                                                                                             |
| document_id                  | Mandatory          | String                | Document UUID                                                                                                                                | 
| file                         | Optional           | Object                | {"filename": "string","content": "string"}                                                                                                   |
| callback_url                 | Mandatory          | String                | Callback URL                                                                                                                                 |
| expire_after                 | Optional           | Integer               | Expiration period in minutes (default value is 30)                                                                                           |
| delete_document_after        | Optional           | Integer               | Document removal period in minutes (should not be less than expire_after value)                                                              |
| signers                      | Optional           | Array of objects      | { "name": "string", "surname": "string", "signature_type": "string", "phone_number": "string", "personal_code": "string", "email": "string"} |
| language                     | Optional           | String                | User interface language ('lt' or 'en')                                                                                                       |



## Response body parameter description

### Successful response

| Key                    | Type   | Description                              |
|:-----------------------|:-------|:-----------------------------------------|
| status                 | String | Status of the request, `ok` in this case |
| temporary_signing_link | String | Temporary document signing link |
| valid_until            | String | Expiration time |

### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |


## Sample request

```
POST /api/document/generate-temporary-signing-link.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
    "access_token": "d7aaXNN5wodRH3514RuhkMqYUTRnd4o07IYliG8fxQicLfldCBmbZXV5",
    "document_id": "8c1b611f-ddcb-11ec-a74f-84c5a60a22fb",
    "file": {
        "filename": "string",
        "content": "string"
    },
    "callback_url": "string",
    "expire_after": 0,
    "delete_document_after": 0,
    "signers": [
        {}
    ],
    "language": "string"
}
```

## Sample response

### Sample success response

```
{
    "status": "ok",
    "temporary_signing_link": "https://app.marksign.lt/user/document/b3c0ba4c-1b5c-4131-0521-1e5dd0398677/b3c0ba4c-1b5c-4131-0521-1e5dd0398677",
    "valid_until": "1334216865"
}
```

### Sample failed response

```
{
    "status": "error",
    "message": "message text"
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/api/document/generate-temporary-signing-link.json 
--header 'Content-Type: application/json' 
--data-raw '{
  "access_token": "d7aaXNN5wodRH3514RuhkMqYUTRnd4o07IYliG8fxQicLfldCBmbZXV5",
    "document_id": "8c1b611f-ddcb-11ec-a74f-84c5a60a22fb",
    "file": {
        "filename": "string",
        "content": "string"
    },
    "callback_url": "string",
    "expire_after": 0,
    "delete_document_after": 0,
    "signers": [
        {}
    ],
    "language": "string"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\IframeTempSigningLinkGenerationRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/IframeTempSigningLinkGenerationRequestBuilder.html) as request builder.

```
/**
 * The document uuid that was found from "Document upload" request.
 * The following is a dummy to use as example.
 */

$linkGenerationReq = (new IframeTempSigningLinkGenerationRequestBuilder)
  ->withDocumentId('8c1b611f-ddcb-11ec-a74f-84c5a60a22fb')
  ->withCallbackUrl('string of url')
  ->withExpireAfter(30)
  ->withLanguage('en')
  ->createRequest();
$linkGenerationRes = $client->postRequest($linkGenerationReq);
$linkGenerationResArray = $linkGenerationRes->toArray();
var_dump($linkGenerationResArray);
```
