---
layout: default
title: Smartid Signing Status
parent: Smart-ID APIs
has_toc: true
nav_order: 2
---

# Smartid Signing Status
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
      <td>/smartid/sign/status/{token}.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/sign/status/{token}.json</td>
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
POST /en/smartid/sign/status/19f1c829-63f2-eb7f-b473-8bb481298dc2.json HTTP/1.1
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
curl --location --request POST 'https://app.marksign.local/en/smartid/sign/status/19f1c829-63f2-eb7f-b473-8bb481298dc2.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidSigningProcessStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidSigningProcessStatusRequestBuilder.html) as request builder.

```
/**
 * The token was found from the response of 'initialize authentication via smart id' request.
 * The following is a dummy to use as example.
 */
$token = '40a77456-8b15-4818-2df2-034376f6c6f5';

$signProcStatReq = (new SmartidSigningProcessStatusRequestBuilder)
  ->withToken($token)
  ->createRequest();
$signProcStatRes = $client->postRequest($signProcStatReq);
$signProcStatResArray = $signProcStatRes->toArray(false);
var_dump($signProcStatResArray);
```
