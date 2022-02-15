---
layout: default
title: Smartid Identification Remove
parent: Smart-ID APIs
has_toc: true
nav_order: 6
---

# Smartid Identification Remove
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
      <td>/api/smartid/session/{sessionId}</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/smartid/session/{sessionId}</td>
    </tr>
    <tr>
      <td>Method</td>
      <td>DELETE</td>
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
| sessionId | Mandatory | String | Description |

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



## Sample request

```
DELETE /en/api/smartid/session/c2d86cd3-ee0e-d5d2-2307-91ec420a06d0 HTTP/1.1
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
  "status": "ok"
}
```

### Sample failed response

```
{
  "status": "error",
  "message": "Request number is invalid"
}
```

## Implementation

### CURL

```
curl --location --request DELETE 'https://app.marksign.local/en/api/smartid/session/c2d86cd3-ee0e-d5d2-2307-91ec420a06d0' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidIdentificationRemoveRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidIdentificationRemoveRequestBuilder.html) as request builder.

```
/**
 * The sessionId is the value of 'token' found either
 * from the response of 'initialize authentication via smart id' request
 * or from the response of 'initialize hash signing authentication via smart id' request
 * The following is a dummy to use as example.
 */
$sessionId = '98ead4e1-015b-4968-bdcd-03797d1a4bea';

$indentRemReq = (new SmartidIdentificationRemoveRequestBuilder)
  ->withSessionId($sessionId)
  ->createRequest();
$indentRemRes = $client->postRequest($indentRemReq);
$indentRemResArray = $indentRemRes->toArray(false);
var_dump($indentRemResArray);
```
