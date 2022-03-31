---
layout: default
title: Initialize Authentication
parent: Mobile-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 1
---

# Initialize authentication via mobile id
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API initializes authentication via mobile id and provides a token to use in other requests.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path (Locale: LT)</td>
      <td>/mobile/login.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/mobile/login.json</td>
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
| phone | Mandatory | String | Mobile phone number for which authentication is being initialized |
| code | Mandatory | String | Personal code related to the phone number |
| language | Optional | String | Language for messages displayed on the phone screen (default: LIT, other: ENG, RUS, EST) |
| message | Optional | String | Message to be displayed on the phone screen. |
| message_format | Optional | String | Format of the message which is displayed on the phone screen. Possible values: GSM-7 (default), UCS-2. Max characters count for GSM-7 and UCS-2 is 40 and 20 characters respectively. |
| peps | Optional | Boolean | Whether to check PEPs information, default is `false` |
| sanctions | Optional | Boolean | Whether to check sanctions information, default is `false` |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| certificate | Object | Certificate information of the provided phone number |
| code | String | Personal code provided in hte request |
| token | String | Unique token to be used in future request |
| control_code | String | Verification code |


### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |
| error_code | Integer | Unique code for the error |



## Sample request

```

POST /en/mobile/login.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "phone": "+37269000366",
  "code": "60001017705",
  "language": "ENG",
  "message": "any message",
  "message_format": "GSM-7",
  "peps": true,
  "sanctions": true
}

```

## Sample response

### Sample success response

```

{
  "status": "ok",
  "certificate": {
    "name": "/C=EE/CN=TESTNUMBER,TEN,60001017705/SN=TESTNUMBER/GN=TEN/serialNumber=PNOEE-60001017705",
    "subject": {
      "country": "EE",
      "organisation": null,
      "organisation_unit": null,
      "common_name": "TESTNUMBER,TEN,60001017705",
      "surname": "TESTNUMBER",
      "name": "TEN",
      "serial_number": "PNOEE-60001017705"
    },
    "issuer": {
      "country": "EE",
      "organisation": "AS Sertifitseerimiskeskus",
      "common_name": "TEST of ESTEID-SK 2015"
    },
    "valid_from": "2020-11-13",
    "valid_to": "2025-11-12",
    "value": "TUlJRnZEQ0NBNlNnQXdJQkFnSVFUNnM1QU1GN1VncGZybytaam..........QxdnNBWmVZRGlveURtejVEaVg5QUlPWUtkWVhxOGZRT2k3ND0="
  },
  "code": "60001017705",
  "token": "381ed84f-0851-ce1e-a048-fa1e13a53bba",
  "control_code": "6223"
}

```

Please note that some json values have been truncated in the previous example.

### Sample failed response

```

{
  "status": "error",
  "message": "Invalid parameter [message_format]: Invalid message format",
  "error_code": 40001
}

```

## Implementation

### CURL

```

curl --location --request POST 'https://app.marksign.local/en/mobile/login.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "phone": "+37269000366",
  "code": "60001017705",
  "language": "ENG",
  "message": "any message",
  "message_format": "GSM-7",
  "peps": true,
  "sanctions": true
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidInitAuthRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/MobileidInitAuthRequestBuilder.html) as request builder.

```

/**
 * The token in response ($initAuthResArray['token'] in this example),
 * might need to be saved for future purposes.
 */
$initAuthReq = (new MobileidInitAuthRequestBuilder)
  ->withPhone('+37269000366')
  ->withCode('60001017705')
  ->withLanguage('ENG')
  ->withMessage('Dummy')
  ->withMessageFormat('GSM-7')
  ->withPeps(true)
  ->withsanctions(true)
  ->createRequest();
$initAuthRes = $client->postRequest($initAuthReq);
$initAuthResArray = $initAuthRes->toArray();
var_dump($initAuthResArray);

```
