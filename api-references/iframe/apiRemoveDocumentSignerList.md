---
layout: default
title: Removes a document signer
parent: Iframe APIs
grand_parent: API Reference
has_toc: true
nav_order: 3
---

# Removes a document signer
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
      <td>/api/document/{documentId}/remove-temporary-signer.json</td>
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

| Key                      | Requirement        | Type        | Description                           |
|:-------------------------|:-------------------|:------------|:--------------------------------------|
| access_token             | Mandatory          | String      | API Access Token                      |
| name                     | Optional           | String      | Signer's name                         |
| surname                  | Optional           | String      | Signer's surname                      |
| email                    | Optional           | String      | Signer's email                        |
| personal_code            | Optional           | String      | Signer's personal code                |



## Response body parameter description

### Successful response

| Key                    | Type             | Description                              |
|:-----------------------|:-----------------|:-----------------------------------------|
| status                 | String           | Status of the request, `ok` in this case |

### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |


## Sample request

```
POST /api/document/{documentId}/remove-temporary-signer.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
    "access_token": "d7aaXNN5wodRH3514RuhkMqYUTRnd4o07IYliG8fxQicLfldCBmbZXV5",
    "name": "Vardenis",
    "surname": "Pavardenis",
    "email": "vardas@pastas.lt",
    "personal_code": "31111111111"
}
```

## Sample response

### Sample success response

```
{
    "status": "ok"
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
curl --location --request POST 'https://app.marksign.local/api/document/{documentId}/remove-temporary-signer.json
--header 'Content-Type: application/json' 
--data-raw '{
  "access_token": "d7aaXNN5wodRH3514RuhkMqYUTRnd4o07IYliG8fxQicLfldCBmbZXV5",
  "name": "Vardenis",
  "surname": "Pavardenis",
  "email": "vardas@pastas.lt",
  "personal_code": "31111111111"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\IframeRemoveDocumentSignerRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/IframeRemoveDocumentSignerRequestBuilder.html) as request builder.

```
/**
 * The document uuid that was found from "Document upload" request.
 * The following is a dummy to use as example.
 */

$initReq = (new IframeRemoveDocumentSignerRequestBuilder)
  ->withDocumentId('8c1b611f-ddcb-11ec-a74f-84c5a60a22fb')
  ->withPersonalCode('31111111111')
  ->withName('Vardenis')
  ->withSurname('Pavardenis')
  ->withEmail('vardas@pastas.lt')
  ->createRequest();
$initRes = $client->postRequest($initReq);
$initResArray = $initRes->toArray();
var_dump($initResArray);
```
