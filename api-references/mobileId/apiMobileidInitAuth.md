---
layout: default
title: Mobileid Init Auth
parent: Mobile-ID APIs
has_toc: true
nav_order: 0
---

# Mobileid Init Auth
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
| access_token | Mandatory | String | Description |
| phone | Mandatory | String | Description |
| code | Mandatory | String | Description |
| language | Mandatory | String | Description |
| message | Mandatory | String | Description |
| message_format | Mandatory | String | Description |
| peps | Mandatory | Boolean | Description |
| sanctions | Mandatory | Boolean | Description |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| certificate | Array of Objects | Description |
| code | String | Description |
| token | String | Description |
| control_code | String | Description |

### Response certificate object description

| Key | Type | Description |
| :--- | :--- | :--- |
| name | String | Description |
| subject | Array of Objects | Description |
| issuer | Array of Objects | Description |
| valid_from | String | Description |
| valid_to | String | Description |
| value | String | Description |

### Response subject object description

| Key | Type | Description |
| :--- | :--- | :--- |
| country | String | Description |
| organisation | NULL | Description |
| organisation_unit | NULL | Description |
| common_name | String | Description |
| surname | String | Description |
| name | String | Description |
| serial_number | String | Description |

### Response issuer object description

| Key | Type | Description |
| :--- | :--- | :--- |
| country | String | Description |
| organisation | String | Description |
| common_name | String | Description |



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |
| error_code | Integer | Description |



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
$initAuthResArray = $initAuthRes->toArray(false);
var_dump($initAuthResArray);

```
