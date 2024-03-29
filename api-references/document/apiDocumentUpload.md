---
layout: default
title: Document Upload
parent: Document APIs
grand_parent: API Reference
has_toc: true
nav_order: 1
---

# Document upload
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
| access_token | Mandatory | String | API access token |
| access | Mandatory | String | Document access. Possible values: public, private |
| file | Mandatory | Object | Uploading file information. Follow [Request file object description](#request-file-object-description) section |
| signers | Mandatory | Array of Objects | Signers information. Follow [Request signers object description](#request-signers-object-description) section |

### Request file object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| filename | Mandatory | String | Name of the file |
| content | Mandatory | String | Base64 encoded content of the file |
| callbackUrl | Optional | String | Callback URL to send uuid after signing |

### Request signers object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| name | Mandatory | String | Signer's name |
| surname | Mandatory | String | Signer's surname |
| email | Mandatory | String | Signer's email |
| successUrl | Optional | String | Document upload success redirection URL |
| noEmail | Optional | Boolean | If `true` them email with invitation URL will not be sent to signer (default: `false`) |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| message | String | Status message |
| document | Object | Contains document info, like `uuid` which will be used in future requests Follow [Response document object description](#response-document-object-description) |
| signers | Array of Objects | Array containing signer objects that was provided in request along with other infos. Follow [Response signer object description](#response-signer-object-description) section |

### Response document object description

| Key | Type | Description |
| :--- | :--- | :--- |
| uuid | String | UUID of the uploaded document |

### Response signer object description

| Key | Type | Description |
| :--- | :--- | :--- |
| name | String | Signer's name |
| surname | String | Signer's surname |
| invitationUrl | String | URL to re-invite this signer. Non null value if `noEmail` is `false`, else `null` |


### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |
| error_code | Integer | Unique code for the error. Error codes are listed [here](/api-references/errorCodes.html) |


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

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentUploadRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/DocumentUploadRequestBuilder.html) as request builder.

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
$uploadResArray = $uploadRes->toArray();
var_dump($uploadResArray);

```
