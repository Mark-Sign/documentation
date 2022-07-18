---
layout: default
title: Remove Identification Session
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 7
---

# Remove Identification Session
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API destroys the session initialed by authentication or signing processes via smart id.

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
| sessionId | Mandatory | String | Token that is being sent as a response of from the response of [Initialize authentication via smart id](/api-references/smartId/apiSmartidInitAuth.html#successful-response) request or [Initialize signing via smart id](/api-references/smartId/apiSmartidInitSigning.html#successful-response) request or [Initialize hash signing via smart id](/api-references/smartId/apiSmartidInitHashSigning.html#successful-response) request |

## Request body parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | API Access Token |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |



### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |



## Sample request

```

DELETE /en/api/smartid/session/1c5cd62c-bbf7-779e-3fb4-bad3433ad83f HTTP/1.1
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

curl --location --request DELETE 'https://app.marksign.local/en/api/smartid/session/1c5cd62c-bbf7-779e-3fb4-bad3433ad83f' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidIdentificationRemoveRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/SmartidIdentificationRemoveRequestBuilder.html) as request builder.

```

/**
 * The sessionId is the value of 'token' found either
 * from the response of 'initialize authentication via smart id' request
 * or from the response of 'initialize hash signing authentication via smart id' request
 * The following is a dummy to use as example.
 */
$sessionId = '1c5cd62c-bbf7-779e-3fb4-bad3433ad83f';

$indentRemReq = (new SmartidIdentificationRemoveRequestBuilder)
  ->withSessionId($sessionId)
  ->createRequest();
$indentRemRes = $client->postRequest($indentRemReq);
$indentRemResArray = $indentRemRes->toArray();
var_dump($indentRemResArray);

```
