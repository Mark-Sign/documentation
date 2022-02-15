---
layout: default
title: Smartid Hash Signing Status
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 6
---

# Smartid Hash Signing Status
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
      <td>/smartid/sign/hash/status/{token}.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/sign/hash/status/{token}.json</td>
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
| token | Mandatory | String | Description |

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
| error_code | Integer | Description |



## Sample request

```
POST /en/smartid/sign/hash/status/c2d86cd3-ee0e-d5d2-2307-91ec420a06d0.json HTTP/1.1
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
  "status": "waiting"
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
curl --location --request POST 'https://app.marksign.local/en/smartid/sign/hash/status/c2d86cd3-ee0e-d5d2-2307-91ec420a06d0.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidHashSigningProcessStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidHashSigningProcessStatusRequestBuilder.html) as request builder.

```
/**
 * The hashSignToken was found from the response of 'initialize hash signing authentication via smart id' request.
 * The following is a dummy to use as example.
 */
$hashSignToken = 'e654322d-9c20-4630-bc26-16e11d8243ff';

$hashSignStatReq = (new SmartidHashSigningProcessStatusRequestBuilder)
  ->withToken($hashSignToken)
  ->createRequest();
$hashSignStatRes = $client->postRequest($hashSignStatReq);
$hashSignStatResArray = $hashSignStatRes->toArray(false);
var_dump($hashSignStatResArray);
```
