---
layout: default
title: Generates a list of document signers
parent: Iframe APIs
grand_parent: API Reference
has_toc: true
nav_order: 2
---

# Generates a list of document signers
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
      <td>/api/document/{documentId}/signers.json</td>
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

| Key | Requirement | Type | Description   |
| :--- | :--- | :--- |:--------------|
| documentId | Mandatory | String | Document UUID |

## Request body parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | API Access Token |



## Response body parameter description

### Successful response

| Key                    | Type             | Description                              |
|:-----------------------|:-----------------|:-----------------------------------------|
| status                 | String           | Status of the request, `ok` in this case |
| signers | Array of Objects | Signers list                             |

### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |


## Sample request

```
POST /api/document/{documentId}/signers.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
    "access_token": "d7aaXNN5wodRH3514RuhkMqYUTRnd4o07IYliG8fxQicLfldCBmbZXV5",
    "document_id": "8c1b611f-ddcb-11ec-a74f-84c5a60a22fb"
}
```

## Sample response

### Sample success response

```
{
    "status": "ok",
    "signers": [
        {
            "name": "KIRIL",
            "surname": "MATOVIČ",
            "isSignatureValid": "true",
            "signStatus": "signed",
            "rejectionReason": "reason"
        }
    ]
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
curl --location --request POST 'https://app.marksign.local/api/document/{documentId}/signers.json
--header 'Content-Type: application/json' 
--data-raw '{
  "access_token": "d7aaXNN5wodRH3514RuhkMqYUTRnd4o07IYliG8fxQicLfldCBmbZXV5",
  "document_id": "8c1b611f-ddcb-11ec-a74f-84c5a60a22fb"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\IframeGeneratesDocumentSignersListRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/IframeGeneratesDocumentSignersListRequestBuilder.html) as request builder.

```
/**
 * The document uuid that was found from "Document upload" request.
 * The following is a dummy to use as example.
 */

$signersListReq = (new IframeGeneratesDocumentSignersListRequestBuilder)
  ->withDocumentId('8c1b611f-ddcb-11ec-a74f-84c5a60a22fb')
  ->createRequest();
$signersListRes = $client->postRequest($signersListReq);
$signersListResArray = $signersListRes->toArray();
var_dump($signersListResArray);
```
