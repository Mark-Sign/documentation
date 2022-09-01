---
layout: default
title: Initialize Hash Signing
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 5
---

# Initialize hash signing via smart id
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API initializes hash signing with qualified electronic signature via smart id.

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
| access_token | Mandatory | String | API Access Token |
| hash | Mandatory | String | Hash to sign |
| hash_algorithm | Mandatory | String | SHA256 or SHA512 |
| country | Mandatory | String | Signer's country code: LT, EE |
| message | Optional | String | Message to be displayed on the phone screen. |
| code | Mandatory | String | Personal code related to the phone number |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| token | String | Unique token to be used in future request |
| control_code | String | Verification code |

### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |
| error_code | Integer | Unique code for the error. Error codes are listed [here](/api-references/errorCodes.html) |

## Sample request

```

POST /en/smartid/sign/hash.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "hash": "b74970de7f4d8c26753a..........d17130930aa0dbb5f724c",
  "hash_algorithm": "SHA256",
  "country": "LT",
  "message": "any message",
  "code": "30303039914"
}

```

Please note that some json values have been truncated in the previous example.

## Sample response

### Sample success response

```

{
  "status": "ok",
  "token": "ea89b835-c585-3c3c-9ea8-0f1b6ed3e13d",
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
  "hash": "b74970de7f4d8c26753a..........d17130930aa0dbb5f724c",
  "hash_algorithm": "SHA256",
  "country": "LT",
  "message": "any message",
  "code": "30303039914"
}'

```

Please note that some json values have been truncated in the previous example.

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidInitHashSigningRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/SmartidInitHashSigningRequestBuilder.html) as request builder.

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
  ->withCode('30303039914')
  ->withMessage('any message')
  ->createRequest();
$hashSignInitRes = $client->postRequest($hashSignInitReq);
$hashSignInitResArray = $hashSignInitRes->toArray();
var_dump($hashSignInitResArray);

```
