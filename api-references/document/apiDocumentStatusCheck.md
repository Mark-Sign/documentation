---
layout: default
title: Document Status Check
parent: Document APIs
grand_parent: API Reference
has_toc: true
nav_order: 4
---

# Document status check
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
      <td>/api/document/{documentId}/check-status.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/document/{documentId}/check-status.json</td>
    </tr>
    <tr>
      <td>Method</td>
      <td>GET</td>
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
| documentId | Mandatory | String | Document UUID from response of ["Document upload"](/documentation/api-references/document/apiDocumentUpload.html#response-document-object-description) |

## Query parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | API Access Token |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| data | Object | For object description, follow [Response data object description](#response-data-object-description) |

### Response data object description

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| document_status | String | Status of the document |



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |



## Sample request

```

GET /en/api/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/check-status.json?access_token=f4b79b72-7587-f417-41f8-2de5a7c87fae HTTP/1.1
Host: app.marksign.local

```

## Sample response

### Sample success response

```

{
  "status": "ok",
  "data": {
    "status": "ok",
    "document_status": "saved"
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

curl --location --request GET 'https://app.marksign.local/en/api/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/check-status.json?access_token=f4b79b72-7587-f417-41f8-2de5a7c87fae'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentStatusCheckRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/DocumentStatusCheckRequestBuilder.html) as request builder.

```

/**
 * The document id that was found from "Document upload" request.
 * The following is a dummy to use as example.
 */
$documentId = 'c66cf14e-f763-9757-3b83-e5e28126a6df';

$statusCheckReq = (new DocumentStatusCheckRequestBuilder)
  ->withDocumentId($documentId)
  ->createRequest();
$statusCheckRes = $client->postRequest($statusCheckReq);
$statusCheckResArray = $response->toArray();
var_dump($statusCheckResArray);

```
