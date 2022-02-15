---
layout: default
title: Mobileid Hash Signing Status
parent: API Reference
has_toc: true
nav_order: 5
---

# Mobileid Hash Signing Status
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
      <td>/mobile/sign-hash/status/31c5b0b8-9534-3e0e-2126-9d25945efc4c.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/mobile/sign-hash/status/31c5b0b8-9534-3e0e-2126-9d25945efc4c.json</td>
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



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| signature_value | String | Description |



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |
| error_code | Integer | Description |



## Sample request

```
POST /en/mobile/sign-hash/status/31c5b0b8-9534-3e0e-2126-9d25945efc4c.json HTTP/1.1
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
  "status": "ok",
  "signature_value": "yFejaXcMw/AyhJjvWj+R/d8ucmXchpfMzWebW4OcRvMkkfTZxtwQQwZQI1NondeeytAYWJXdxmgEM40/qRu5aA=="
}
```

### Sample failed response

```
{
  "status": "error",
  "message": "Session for given token was not found",
  "error_code": 40402
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/en/mobile/sign-hash/status/31c5b0b8-9534-3e0e-2126-9d25945efc4c.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidHashSigningProcessStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/MobileidHashSigningProcessStatusRequestBuilder.html) as request builder.

```
/**
 * The hashSignToken was found from the response of 'initialize hash signing auth via mobile id' request.
 * The following values are dummy.
 */
$hashSignToken = 'e654322d-9c20-4630-bc26-16e11d8243ff';
$accessToken = '6102d227-0dcf-4ce3-ab8f-337385f09ee4';

$hashSignStatReq = (new MobileidHashSigningProcessStatusRequestBuilder)
  ->withToken($hashSignToken)
  ->withAccessToken($accessToken)
  ->createRequest();
$hashSignStatReq = $client->postRequest($hashSignStatReq);
$hashSignStatReqArray = $hashSignStatReq->toArray(false);
var_dump($hashSignStatReqArray);
```
