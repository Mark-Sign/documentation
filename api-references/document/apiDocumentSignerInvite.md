---
layout: default
title: Document Signer Invite
parent: API Reference
has_toc: true
nav_order: 2
---

# Document Signer Invite
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
      <td>/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/invite-signer.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/invite-signer.json</td>
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
| signer | Mandatory | Array of Objects | Description |

### Request signer object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| name | Mandatory | String | Description |
| surname | Mandatory | String | Description |
| email | Mandatory | String | Description |
| successUrl | Mandatory | String | Description |
| noEmail | Mandatory | Boolean | Description |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |
| signers | Object | Description |

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



## Sample request

```
POST /en/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/invite-signer.json HTTP/1.1
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
      "invitationUrl": "https://app.marksign.local/en/user/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/signer/73fcb66e-4531-327c-15d0-7f84299020a7"
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
curl --location --request POST 'https://app.marksign.local/en/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/invite-signer.json' \
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

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentSignerInviteRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/DocumentSignerInviteRequestBuilder.html) as request builder.

```
/**
 * The document id that was found from document upload request.
 * The following values are dummy.
 */
$documentId = 'c66cf14e-f763-9757-3b83-e5e28126a6df';
$accessToken = '7298cc61-7184-4a06-a17f-5691a0970805';

$signerInviteReq = (new DocumentSignerInviteRequestBuilder)
  ->withAccessToken($accessToken)
  ->withDocumentId($documentId)
  ->withSigner(
    (new Signer)->setName('Joseph')->setSurname('Ritter')->setEmail('joseph.ritter@domain.com')->setSuccessUrl('http://example.com')->setNoEmail(false)
  )
  ->createRequest();
$signerInviteRes = $client->postRequest($signerInviteReq);
$signerInviteResArray = $signerInviteRes->toArray(false);
var_dump($signerInviteResArray);
```
