---
layout: default
title: Remove Identification Session
parent: Mobile-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 7
---

# Remove session initialized by mobile id
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API destroys the session initialed by authentication or signing processes via mobile id.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path (Locale: LT)</td>
      <td>/api/mobile/session/{sessionId}</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/mobile/session/{sessionId}</td>
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
| sessionId | Mandatory | String | Token that is being sent as a response of from the response of [Initialize authentication via mobile id](/api-references/mobileId/apiMobileidInitAuth.html#successful-response) request or [Initialize signing via mobile id](/api-references/mobileId/apiMobileidInitSigning.html#successful-response) request or [Initialize hash signing via mobile id](/api-references/mobileId/apiMobileidInitHashSigning.html#successful-response) request |

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

DELETE /en/api/mobile/session/320a35af-19c9-eecd-5f7e-8725393bd955 HTTP/1.1
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

curl --location --request DELETE 'https://app.marksign.local/en/api/mobile/session/320a35af-19c9-eecd-5f7e-8725393bd955' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidIdentificationRemoveRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/MobileidIdentificationRemoveRequestBuilder.html) as request builder.

```

/**
 * The sessionId is the value of 'token' found either
 * from the response of 'Initialize authentication via mobile id' request
 * or 'Initialize signing via mobile id' request
 * or 'Initialize hash signing via mobile id' request
 * The following is a dummy to use as example.
 */
$sessionId = '98ead4e1-015b-4968-bdcd-03797d1a4bea';

$indentRemReq = (new MobileidIdentificationRemoveRequestBuilder)
  ->withSessionId($sessionId)
  ->createRequest();
$indentRemRes = $client->postRequest($indentRemReq);
$indentRemResArray = $indentRemRes->toArray();
var_dump($indentRemResArray);

```