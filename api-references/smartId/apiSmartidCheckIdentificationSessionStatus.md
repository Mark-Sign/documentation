---
layout: default
title: Check Identification Session Status
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 2
---

# Check identification session status
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API chceks status of smart id identification session using token.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path (Locale: LT)</td>
      <td>/smartid/status/{token}.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/status/{token}.json</td>
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
| token | Mandatory | String | Token that is being sent as a response of [Initialize authentication via smart id](/documentation/api-references/smartId/apiSmartidInitAuth.html#successful-response) |

## Request body parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | API Access Token |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the authentication session |
| country | String | Country code |
| certificate | Object | Certificate information of the provided person |
| code | String | Provided person code |
| token | String | Unique session token used in the request |
| control_code | String | Verification code |
| name | String | Person name |
| surname | String | Person surname |
| sanctions_data | Object | Sanction informatiion |
| peps_data | Object | PEPs information |


### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |
| error_code | Integer | Unique code for the error |

## Sample request

```

POST /en/smartid/status/1c5cd62c-bbf7-779e-3fb4-bad3433ad83f.json HTTP/1.1
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
  "certificate": {
    "name": "\/C=LT\/CN=SURNAME,NAME\/SN=SURNAME\/GN=NAME\/serialNumber=PNOLT-30303039914",
    "subject": {
      "country": "LT",
      "organisation": null,
      "organisation_unit": null,
      "common_name": "SURNAME,NAME",
      "surname": "SURNAME",
      "name": "TEN",
      "serial_number": "PNOLT-30303039914"
    },
    "issuer": {
      "country": "EE",
      "organisation": "AS Sertifitseerimiskeskus",
      "common_name": "TEST of EID-SK 2016"
    },
    "valid_from": "2021-09-17",
    "valid_to": "2024-09-17",
    "value": "TUlJSUZqQ0NCZjZnQXd..........xPak02Mk5rLzlRPT0="
  },
  "code": "30303039914",
  "country": "LT",
  "name": "NAME",
  "surname": "SURNAME",
  "token": "1c5cd62c-bbf7-779e-3fb4-bad3433ad83f",
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

curl --location --request POST 'https://app.marksign.local/en/smartid/status/1c5cd62c-bbf7-779e-3fb4-bad3433ad83f.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidIdentificationStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidIdentificationStatusRequestBuilder.html) as request builder.

```

/**
 * The token can be found from the response of 'Initialize authentication via smart id' request.
 * The following is a dummy to use as example.
 */
$token = '1c5cd62c-bbf7-779e-3fb4-bad3433ad83f';

$identStatusReq = (new SmartidIdentificationStatusRequestBuilder)
  ->withToken($token)
  ->createRequest();
$identStatusRes = $client->postRequest($identStatusReq);
$identStatusResArray = $identStatusRes->toArray();
var_dump($identStatusResArray);

```
