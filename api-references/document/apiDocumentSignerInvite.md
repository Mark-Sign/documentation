---
layout: default
title: Document Signer Invite
parent: Document APIs
grand_parent: API Reference
has_toc: true
nav_order: 3
---

# Document signer invite
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
      <td>/api/document/{documentId}/invite-signer.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/document/{documentId}/invite-signer.json</td>
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

## URL parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| documentId | Mandatory | String | Document UUID from response of ["Document upload"](/api-references/document/apiDocumentUpload.html#response-document-object-description) |

## Request body parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | API Access Token |
| signer | Mandatory | Object | Follow [Request signer object description](#request-signer-object-description) section |

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
| message | String | Brief status message |
| signers | Array of Objects | Follow [Response signers object description](#response-signers-object-description) |

### Response signers object description

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



## Sample request

```

POST /en/api/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/invite-signer.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae",
  "signer": {
    "name": "Joseph",
    "surname": "Ritter",
    "email": "joseph.ritter@domain.com",
    "successUrl": "http://example.com",
    "noEmail": false
  }
}

```

## Sample response

### Sample success response

```

{
  "status": "ok",
  "message": "Invited to sign",
  "signers": [
    {
      "name": "Joseph",
      "surname": "Ritter",
      "invitationUrl": "https://app.marksign.local/en/user/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/signer/3204fbf6-fd61-5e30-6299-fe02baed182b"
    }
  ]
}

```

### Sample failed response

```

{
  "status": "error",
  "message": "Document was not found"
}

```

## Implementation

### CURL

```

curl --location --request POST 'https://app.marksign.local/en/api/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/invite-signer.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae",
  "signer": {
    "name": "Joseph",
    "surname": "Ritter",
    "email": "joseph.ritter@domain.com",
    "successUrl": "http://example.com",
    "noEmail": false
  }
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentSignerInviteRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/DocumentSignerInviteRequestBuilder.html) as request builder.

```

/**
 * The document id that was found from "Document upload" request.
 * The following is a dummy to use as example.
 */
$documentId = 'c66cf14e-f763-9757-3b83-e5e28126a6df';

$signerInviteReq = (new DocumentSignerInviteRequestBuilder)
  ->withDocumentId($documentId)
  ->withSigner(
    (new Signer)->setName('Joseph')->setSurname('Ritter')->setEmail('joseph.ritter@domain.com')->setSuccessUrl('http://example.com')->setNoEmail(false)
  )
  ->createRequest();
$signerInviteRes = $client->postRequest($signerInviteReq);
$signerInviteResArray = $signerInviteRes->toArray();
var_dump($signerInviteResArray);

```
