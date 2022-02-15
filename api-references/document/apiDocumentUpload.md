---
layout: default
title: Document Upload
parent: Document APIs
has_toc: true
nav_order: 0
---

# Document Upload
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
      <td>Path (Locale: LT)</td>
      <td>/api/document/upload.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/document/upload.json</td>
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

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | Description |
| access | Mandatory | String | Description |
| file | Mandatory | Array of Objects | Description |
| signers | Mandatory | Object | Description |

### Request file object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| filename | Mandatory | String | Description |
| content | Mandatory | String | Description |

### Request signers object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| name | Mandatory | String | Description |
| surname | Mandatory | String | Description |
| email | Mandatory | String | Description |
| noEmail | Mandatory | Boolean | Description |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| document | Array of Objects | Description |
| signers | Object | Description |

### Response document object description

| Key | Type | Description |
| :--- | :--- | :--- |
| uuid | String | Description |

### Response signers object description

| Key | Type | Description |
| :--- | :--- | :--- |
| name | String | Description |
| surname | String | Description |
| invitationUrl | String | Description |



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |
| error_code | Integer | Description |



## Sample request

```
POST /en/api/document/upload.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae",
  "access": "private",
  "file": {
    "filename": "demo.pdf",
    "content": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0aCA3Ny..........RzdHJlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo="
  },
  "signers": [
    {
      "name": "Tex",
      "surname": "Ryta",
      "email": "tex.ryta@domain.com",
      "noEmail": false
    },
    {
      "name": "John",
      "surname": "Quil",
      "email": "john.quil@domain.com",
      "noEmail": false
    }
  ]
}
```

Please note that some json values have been truncated in the previous example.

## Sample response

### Sample success response

```
{
  "status": "ok",
  "document": {
    "uuid": "cff827fc-e70e-167c-4ae5-d388b1b5c264"
  },
  "signers": [
    {
      "name": "Tex",
      "surname": "Ryta",
      "invitationUrl": "https://app.marksign.local/en/user/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/signer/aa7ba4a1-d93e-b31c-81bf-a885cf952f45"
    },
    {
      "name": "John",
      "surname": "Quil",
      "invitationUrl": "https://app.marksign.local/en/user/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/signer/5244fc01-af77-319f-66e2-fbc8ba344520"
    }
  ]
}
```

### Sample failed response

```
{
  "status": "error",
  "message": "Invalid file type. Allowed file types: pdf, adoc, asice, bdoc",
  "error_code": 0
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/en/api/document/upload.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae",
  "access": "private",
  "file": {
    "filename": "demo.pdf",
    "content": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0aCA3Ny..........RzdHJlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo="
  },
  "signers": [
    {
      "name": "Tex",
      "surname": "Ryta",
      "email": "tex.ryta@domain.com",
      "noEmail": false
    },
    {
      "name": "John",
      "surname": "Quil",
      "email": "john.quil@domain.com",
      "noEmail": false
    }
  ]
}'
```

Please note that some json values have been truncated in the previous example.

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentUploadRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/DocumentUploadRequestBuilder.html) as request builder.

```
/**
 * The uuid of document from response ($uploadResArray['dpcument']['uuid'] in this example),
 * might need to be saved somewhere for future purposes.
 */
$uploadReq = (new DocumentUploadRequestBuilder)
  ->withAccess('private')
  ->withFile(
    (new FileUpload)->setFileName(basename($filePath))->setContent(base64_encode(file_get_contents($filePath)))
  )
  ->withSigners([
    (new Signer)->setName('Tex')->setSurName('Ryta')->setEmail('tex.ryta@domain.com')->setNoEmail(false),
    (new Signer)->setName('John')->setSurName('Quil')->setEmail('john.quil@domain.com')->setNoEmail(false),
  ])
  ->createRequest();
$uploadRes = $client->postRequest($uploadReq);
$uploadResArray = $uploadRes->toArray(false);
var_dump($uploadResArray);
```
