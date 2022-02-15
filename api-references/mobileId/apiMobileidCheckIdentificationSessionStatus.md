---
layout: default
title: Mobileid Check Identification Session Status
parent: API Reference
has_toc: true
nav_order: 1
---

# Mobileid Check Identification Session Status
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
      <td>/mobile/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/mobile/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json</td>
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
| country | String | Description |
| certificate | Array of Objects | Description |
| code | String | Description |
| name | String | Description |
| token | String | Description |
| control_code | String | Description |
| surname | String | Description |
| sanctions_data | Object | Description |
| peps_data | Object | Description |

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

### Response sanctions_data object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response peps_data object description

| Key | Type | Description |
| :--- | :--- | :--- |




### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |
| error_code | Integer | Description |



## Sample request

```
POST /en/mobile/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json HTTP/1.1
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
  "country": "EE",
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
    "value": "TUlJRnRUQ0NBNTJnQXdJQkFnSVFYb1VTQmJPQmJJZGZybytZNF..........FSNXFaRFc0aStyM2FkOG1hb1RoSDRIWjFrb2w2TmVVWEErQT09"
  },
  "code": "60001017705",
  "name": "TEN",
  "token": "15dd492c-8fc7-11ad-cad7-24bcde0b0254",
  "control_code": "1554",
  "surname": "TESTNUMBER",
  "sanctions_data": [],
  "peps_data": []
}
```

Please note that some json values have been truncated in the previous example.

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
curl --location --request POST 'https://app.marksign.local/en/mobile/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidIdentificationStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/MobileidIdentificationStatusRequestBuilder.html) as request builder.

```
/**
 * The token was found from the response of 'mobile id init auth' request.
 * The following values are dummy.
 */
$token = '40a77456-8b15-4818-2df2-034376f6c6f5';
$accessToken = '6102d227-0dcf-4ce3-ab8f-337385f09ee4';

$identStatusReq = (new MobileidIdentificationStatusRequestBuilder)
  ->withToken($token)
  ->withAccessToken($accessToken)
  ->createRequest();
$identStatusRes = $client->postRequest($identStatusReq);
$identStatusResArray = $identStatusRes->toArray(false);
var_dump($identStatusResArray);
```
