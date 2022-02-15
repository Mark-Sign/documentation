---
layout: default
title: Mobileid Identification Remove
parent: API Reference
has_toc: true
nav_order: 6
---

# Mobileid Identification Remove
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
      <td>/api/mobile/session/31c5b0b8-9534-3e0e-2126-9d25945efc4c</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/mobile/session/31c5b0b8-9534-3e0e-2126-9d25945efc4c</td>
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



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |



## Sample request

```
DELETE /en/api/mobile/session/31c5b0b8-9534-3e0e-2126-9d25945efc4c HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
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
  "message": "Request number is invalid"
}
```

## Implementation

### CURL

```
curl --location --request DELETE 'https://app.marksign.local/en/api/mobile/session/31c5b0b8-9534-3e0e-2126-9d25945efc4c' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidIdentificationRemoveRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/MobileidIdentificationRemoveRequestBuilder.html) as request builder.

```
/**
 * The sessionId is the value of 'token' found either
 * from the response of 'mobile id init auth' request
 * or from the response of 'initialize hash signing auth via mobile id' request
 * The following values are dummy.
 */
$sessionId = '98ead4e1-015b-4968-bdcd-03797d1a4bea';
$accessToken = '6102d227-0dcf-4ce3-ab8f-337385f09ee4';

$indentRemReq = (new MobileidIdentificationRemoveRequestBuilder)
  ->withSessionId($sessionId)
  ->withAccessToken($accessToken)
  ->createRequest();
$indentRemRes = $client->postRequest($indentRemReq);
$indentRemResArray = $indentRemRes->toArray(false);
var_dump($indentRemResArray);
```
