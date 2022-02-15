---
layout: default
title: Document Remove
parent: API Reference
has_toc: true
nav_order: 5
---

# Document Remove
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
      <td>/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/remove.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/remove.json</td>
    </tr>
    <tr>
      <td>Method</td>
      <td>DELETE</td>
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



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| data | Array of Objects | Description |

### Response data object description

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |



## Sample request

```
DELETE /en/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/remove.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae"
}
```

## Sample response

### Sample success response

```
{
  "status": "ok",
  "data": {
    "status": "ok",
    "message": "Document was successfully removed"
  }
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
curl --location --request DELETE 'https://app.marksign.local/en/api/document/7ecd1d16-ed31-195a-2dc4-51c53d2f18b0/remove.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentRemoveRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/DocumentRemoveRequestBuilder.html) as request builder.

```
/**
 * The document id that was found from document upload request.
 * The following values are dummy.
 */
$documentId = 'c66cf14e-f763-9757-3b83-e5e28126a6df';
$accessToken = '7298cc61-7184-4a06-a17f-5691a0970805';

$removeReq = (new DocumentRemoveRequestBuilder)
  ->withAccessToken($accessToken)
  ->withDocumentId($documentId)
  ->createRequest();
$removeRes = $client->postRequest($removeReq);
$removeResArray = $removeRes->toArray(false);
var_dump($removeResArray);
```
