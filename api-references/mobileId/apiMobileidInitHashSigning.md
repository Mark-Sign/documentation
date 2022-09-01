---
layout: default
title: Initialize Hash Signing
parent: Mobile-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 6
---

# Initialize hash signing via mobile id
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API initializes hash signing with qualified electronic signature stored on SIM card.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path (Locale: LT)</td>
      <td>/mobile/sign/hash.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/mobile/sign/hash.json</td>
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
| phone | Mandatory | String | Mobile phone number for which authentication is being initialized |
| code | Mandatory | String | Personal code related to the phone number |
| hash_algorithm | Mandatory | String | SHA256 or SHA512 |
| country | Mandatory | String | Signer's country code: LT, EE |
| message | Optional | String | Message to be displayed on the phone screen. |


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

POST /en/mobile/sign/hash.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "hash": "5fef901dc387c585fb470ec7887e204a23d8e16434ec94940019951bd02ffe44",
  "phone": "+37269000366",
  "hash_algorithm": "SHA256",
  "country": "EE",
  "message": "any message",
  "code": "60001017705"
}

```

## Sample response

### Sample success response

```

{
  "status": "ok",
  "token": "320a35af-19c9-eecd-5f7e-8725393bd955",
  "control_code": "3555"
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

curl --location --request POST 'https://app.marksign.local/en/mobile/sign/hash.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "hash": "5fef901dc387c585fb470ec7887e204a23d8e16434ec94940019951bd02ffe44",
  "phone": "+37269000366",
  "hash_algorithm": "SHA256",
  "country": "EE",
  "message": "any message",
  "code": "60001017705"
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidInitHashSigningRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/MobileidInitHashSigningRequestBuilder.html) as request builder.

```

/**
 * The token in response ($hashSignInitResArray['token'] in this example),
 * might need to be saved for future purposes.
 */
$filePath = __DIR__ . '/demo.pdf';

$hashSignInitReq = (new MobileidInitHashSigningRequestBuilder)
  ->withHash(hash('sha256', file_get_contents($filePath)))
  ->withHashAlgorithm('SHA256')
  ->withCountry('EE')
  ->withPhone('+37269000366')
  ->withCode('60001017705')
  ->withMessage('Dummy')
  ->createRequest();
$hashSignInitRes = $client->postRequest($hashSignInitReq);
$hashSignInitResArray = $hashSignInitRes->toArray();
var_dump($hashSignInitResArray);

```
