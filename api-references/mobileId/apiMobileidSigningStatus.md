---
layout: default
title: Mobileid Signing Status
parent: API Reference
has_toc: true
nav_order: 2
---

# Mobileid Signing Status
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
      <td>/mobile/sign/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/mobile/sign/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json</td>
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



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |
| error_code | Integer | Description |



## Sample request

```
POST /en/mobile/sign/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json HTTP/1.1
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
curl --location --request POST 'https://app.marksign.local/en/mobile/sign/status/15dd492c-8fc7-11ad-cad7-24bcde0b0254.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidSigningProcessStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/MobileidSigningProcessStatusRequestBuilder.html) as request builder.

```
/**
 * The token was found from the response of 'mobile id init auth' request.
 * The following values are dummy.
 */
$token = '40a77456-8b15-4818-2df2-034376f6c6f5';
$accessToken = '6102d227-0dcf-4ce3-ab8f-337385f09ee4';

$signProcStatReq = (new MobileidSigningProcessStatusRequestBuilder)
  ->withToken($responseArray['token'])
  ->withAccessToken($accessToken)
  ->createRequest();
$signProcStatRes = $client->postRequest($signProcStatReq);
$signProcStatResArray = $signProcStatRes->toArray(false);
var_dump($signProcStatResArray);
```
