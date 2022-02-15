---
layout: default
title: Smartid Init Auth
parent: Smart-ID APIs
has_toc: true
nav_order: 
---

# Smartid Init Auth
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
| access_token | Mandatory | String | Description |
| code | Mandatory | String | Description |
| country | Mandatory | String | Description |
| message | Mandatory | String | Description |
| peps | Mandatory | Boolean | Description |
| sanctions | Mandatory | Boolean | Description |



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
POST /en/smartid/login.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "code": "50001018865",
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
  "token": "19f1c829-63f2-eb7f-b473-8bb481298dc2",
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
  "code": "50001018865",
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
  ->withCode('50001018865')
  ->withCountry('LT')
  ->withMessage('any message')
  ->withPeps(true)
  ->withsanctions(true)
  ->createRequest();
$initAuthRes = $client->postRequest($initAuthReq);
$initAuthResArray = $initAuthRes->toArray(false);
var_dump($initAuthResArray);
```
