---
layout: default
title: Smartid Init Hash Signing
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 4
---

# Smartid Init Hash Signing
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
      <td>/smartid/sign/hash.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/sign/hash.json</td>
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
| hash | Mandatory | String | Description |
| hash_algorithm | Mandatory | String | Description |
| country | Mandatory | String | Description |
| message | Mandatory | String | Description |
| code | Mandatory | String | Description |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| token | String | Description |
| control_code | String | Description |



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |
| error_code | Integer | Description |



## Sample request

```
POST /en/smartid/sign/hash.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "hash": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0aCA3Ny..........RzdHJlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo=",
  "hash_algorithm": "SHA256",
  "country": "LT",
  "message": "any message",
  "code": "50001018865"
}
```

Please note that some json values have been truncated in the previous example.

## Sample response

### Sample success response

```
{
  "status": "ok",
  "token": "c2d86cd3-ee0e-d5d2-2307-91ec420a06d0",
  "control_code": "9403"
}
```

### Sample failed response

```
{
  "status": "error",
  "message": "Invalid parameter [country]: This value is not valid.",
  "error_code": 40001
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/en/smartid/sign/hash.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "hash": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0aCA3Ny..........RzdHJlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo=",
  "hash_algorithm": "SHA256",
  "country": "LT",
  "message": "any message",
  "code": "50001018865"
}'
```

Please note that some json values have been truncated in the previous example.

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidInitHashSigningRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidInitHashSigningRequestBuilder.html) as request builder.

```
/**
 * The token in response ($hashSignInitResArray['token'] in this example),
 * might need to be saved for future purposes.
 */
$filePath = __DIR__ . '/demo.pdf';

$hashSignInitReq = (new SmartidInitHashSigningRequestBuilder)
  ->withHash(hash('sha256', file_get_contents($filePath)))
  ->withHashAlgorithm('SHA256')
  ->withCountry('LT')
  ->withCode('50001018865')
  ->withMessage('any message')
  ->createRequest();
$hashSignInitRes = $client->postRequest($hashSignInitReq);
$hashSignInitResArray = $hashSignInitRes->toArray(false);
var_dump($hashSignInitResArray);
```
