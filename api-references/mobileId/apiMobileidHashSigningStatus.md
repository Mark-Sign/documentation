---
layout: default
title: Hash Signing Status
parent: Mobile-ID APIs
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

This API checks the status of the hash signing process initialized by [Initialize hash signing via mobile id](/documentation/api-references/mobileId/apiMobileidInitHashSigning.html#initialize-hash-signing-via-mobile-id) request.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path (Locale: LT)</td>
      <td>/mobile/sign-hash/status/{token}.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/mobile/sign-hash/status/{token}.json</td>
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
| token | Mandatory | String | Token that is being sent as a response of [Initialize hash signing via mobile id](/documentation/api-references/mobileId/apiMobileidInitHashSigning.html#successful-response) |

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
| message | String | Brief message about what is wrong |
| error_code | Integer | Unique code for the error |


## Sample request

```

POST /en/mobile/sign-hash/status/320a35af-19c9-eecd-5f7e-8725393bd955.json HTTP/1.1
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
  "signature_value": "2lbblqYAovd88pXDVK5FeC2d3hBd4xSoNII21doSIE17UZ+ZpSB9dpi/DqVhTziKrVYZysw5J0gqCEA4tji/Dw=="
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

curl --location --request POST 'https://app.marksign.local/en/mobile/sign-hash/status/320a35af-19c9-eecd-5f7e-8725393bd955.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidHashSigningProcessStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/MobileidHashSigningProcessStatusRequestBuilder.html) as request builder.

```

/**
 * The hashSignToken was found from the response of 'Initialize hash signing via mobile id' request.
 * The following is a dummy to use as example.
 */
$hashSignToken = 'e654322d-9c20-4630-bc26-16e11d8243ff';

$hashSignStatReq = (new MobileidHashSigningProcessStatusRequestBuilder)
  ->withToken($hashSignToken)
  ->createRequest();
$hashSignStatReq = $client->postRequest($hashSignStatReq);
$hashSignStatReqArray = $hashSignStatReq->toArray(false);
var_dump($hashSignStatReqArray);

```
