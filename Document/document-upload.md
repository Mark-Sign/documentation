---
layout: default
title: Document Upload
parent: Document
has_toc: true
nav_exclude: true
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

This endpoint is for uploading document for further tasks like validating the document, inviting the signers, check the status of the document and downloading the document.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path</td>
      <td>/api/document/upload.json</td>
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
| access_token | Mandatory | String | API Access Token |
| access | Mandatory | String | Document access. Possible values: public, private |
| file | Mandatory | Object | File object that will be uploaded. Follow [Request file object description](#request-file-object-description) section |
| signers | Mandatory | Array of Objects | Array containing signer objects. Follow [Request signer object description](#request-signer-object-description) section |

### Request file object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| filename | Mandatory | String | Name of the file |
| content | Mandatory | String | Base64 encoded file content |
| callbackUrl | Optional | String | Callback URL to send uuid after signing |

### Request signer object description

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
| message | String | Status message |
| error_code | Integer | Unique code for the error. Error codes are listed [here](/api-references/errorCodes.html) |

## Sample request

```
POST /api/document/upload.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "access": "private",
  "file": {
    "filename": "demo.pdf",
    "content": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0a..............JlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo="
  },
  "signers": [{
    "name": "Tex",
    "surname": "Ryta",
    "email": "tex.ryta@domain.com",
    "noEmail": false
  }, {
    "name": "John",
    "surname": "Quil",
    "email": "john.quil@domain.com",
    "noEmail": false
  }]
}
```
## Sample response

### Sample success response

```
{
  "status": "ok",
  "document": {
    "uuid": "646b5202-a49c-b11f-6599-0035fb42d847"
  },
  "signers": [{
    "name": "Tex",
    "surname": "Ryta",
    "invitationUrl": "https://app.marksign.local/user/document/646b5202-a49c-b11f-6599-0035fb42d847/signer/625d0eb0-a0b9-44b3-c6e3-e74326cbaf10"
  }, {
    "name": "John",
    "surname": "Quil",
    "invitationUrl": "https://app.marksign.local/user/document/646b5202-a49c-b11f-6599-0035fb42d847/signer/a3afe745-6a33-5b80-5459-51143d7783ee"
  }]
}
```

### Sample failed response

```
{
  "status": "error",
  "message": "Invalid parameter [access]: Access must be private or public",
  "error_code": 40001
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/api/document/upload.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "access": "private",
  "file": {
    "filename": "demo.pdf",
    "content": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0a..............JlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo="
  },
  "signers": [{
    "name": "Tex",
    "surname": "Ryta",
    "email": "tex.ryta@domain.com",
    "noEmail": false
  }, {
    "name": "John",
    "surname": "Quil",
    "email": "john.quil@domain.com",
    "noEmail": false
  }]
}'
```

Please note that content has been truncated in the previous example.

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentUploadRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/DocumentUploadRequestBuilder.html) as request builder.

```
$apiKey = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';
$accessToken = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';

$client = new Client($apiKey, new Logger('dev', [new StreamHandler('log.txt')]));

$filePath = __DIR__ . "/demo.pdf";

$uploadRB = (new DocumentUploadRequestBuilder)
  ->withAccessToken($accessToken)
  ->withAccess('private')
  ->withFile(
      (new FileUpload)->setFileName(basename($filePath))->setContent(base64_encode(file_get_contents($filePath)))
  )
  ->withSigners([
    (new Signer)->setName('Tex')->setSurName('Ryta')->setEmail('tex.ryta@domain.com')->setNoEmail(false),
    (new Signer)->setName('John')->setSurName('Quil')->setEmail('john.quil@domain.com')->setNoEmail(false),
  ])
  ->createRequest();
$uploadRes = $client->postRequest($uploadRB);
$uploadResArray = $uploadRes->toArray(false);
```