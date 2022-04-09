---
layout: default
title: Initialize Authentication
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 1
---

# Initialize authentication via smart id
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
      <td>/smartid/login.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/login.json</td>
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
| code | Mandatory | String | Personal code related to the phone number |
| country | Mandatory | String | Country related to person code: LT, LV, EE |
| message | Optional | String | Message to be displayed on the phone screen |
| peps | Optional | Boolean | Whether to check PEPs information, default is `false` |
| sanctions | Optional | Boolean | Whether to check sanctions information, default is `false` |



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
| error_code | Integer | Unique code for the error |


## Sample request

```

POST /en/smartid/login.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "code": "30303039914",
  "country": "LT",
  "message": "any message",
  "peps": true,
  "sanctions": true
}

```

## Sample response

### Sample success response

```

{
  "status": "ok",
  "token": "1c5cd62c-bbf7-779e-3fb4-bad3433ad83f",
  "control_code": "5210"
}

```

### Sample failed response

```

{
  "status": "error",
  "message": "Invalid parameter [country]: Invalid country code",
  "error_code": 40001
}

```

## Implementation

### CURL

```

curl --location --request POST 'https://app.marksign.local/en/smartid/login.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "code": "30303039914",
  "country": "LT",
  "message": "any message",
  "peps": true,
  "sanctions": true
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidInitAuthRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidInitAuthRequestBuilder.html) as request builder.

```

/**
 * The token in response ($initAuthResArray['token'] in this example),
 * might need to be saved for future purposes.
 */
$initAuthReq = (new SmartidInitAuthRequestBuilder)
  ->withCode('30303039914')
  ->withCountry('LT')
  ->withMessage('any message')
  ->withPeps(true)
  ->withsanctions(true)
  ->createRequest();
$initAuthRes = $client->postRequest($initAuthReq);
$initAuthResArray = $initAuthRes->toArray();
var_dump($initAuthResArray);

```
