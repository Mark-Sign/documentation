---
layout: default
title: Hash Signing Status
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 6
---

# Hash Signing Status
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API checks the status of the hash signing process initialized by [Initialize hash signing via smart id](/api-references/smartId/apiSmartidInitHashSigning.html#initialize-hash-signing-via-smart-id) request.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path (Locale: LT)</td>
      <td>/smartid/sign/hash/status/{token}.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/sign/hash/status/{token}.json</td>
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
| access_token | Mandatory | String | API Access Token |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| signature_value | String | Signature value |

### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Description |
| error_code | Integer | Description |

## Sample request

```

POST /en/smartid/sign/hash/status/ea89b835-c585-3c3c-9ea8-0f1b6ed3e13d.json HTTP/1.1
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
  "signature_value": "T2RKYUlGL1dxUUJjc3ZI..........TmFkQzY4OTU3dnNuYw=="
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

curl --location --request POST 'https://app.marksign.local/en/smartid/sign/hash/status/ea89b835-c585-3c3c-9ea8-0f1b6ed3e13d.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidHashSigningProcessStatusRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/SmartidHashSigningProcessStatusRequestBuilder.html) as request builder.

```

/**
 * The hashSignToken was found from the response of 'Initialize hash signing via smart id' request.
 * The following is a dummy to use as example.
 */
$hashSignToken = 'ea89b835-c585-3c3c-9ea8-0f1b6ed3e13d';

$hashSignStatReq = (new SmartidHashSigningProcessStatusRequestBuilder)
  ->withToken($hashSignToken)
  ->createRequest();
$hashSignStatRes = $client->postRequest($hashSignStatReq);
$hashSignStatResArray = $hashSignStatRes->toArray();
var_dump($hashSignStatResArray);

```
