---
layout: default
title: Mobileid Init Signing
parent: API Reference
has_toc: true
nav_order: 3
---

# Mobileid Init Signing
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
      <td>/mobile/sign.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/mobile/sign.json</td>
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
| type | Mandatory | String | Description |
| phone | Mandatory | String | Description |
| message | Mandatory | String | Description |
| message_format | Mandatory | String | Description |
| code | Mandatory | String | Description |
| signature_position | Mandatory | String | Description |
| signature_page | Mandatory | String | Description |
| peps | Mandatory | Boolean | Description |
| sanctions | Mandatory | Boolean | Description |
| pdf | Mandatory | Array of Objects | Description |

### Request pdf object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| files | Mandatory | Object | Description |

### Request files object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| name | Mandatory | String | Description |
| content | Mandatory | String | Description |



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
| token | String | Description |
| control_code | String | Description |



## Sample request

```
POST /en/mobile/sign.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "type": "pdf",
  "phone": "+37269000366",
  "message": "any message",
  "message_format": "GSM-7",
  "code": "60001017705",
  "signature_position": "auto",
  "signature_page": "last_page",
  "peps": true,
  "sanctions": true,
  "pdf": {
    "files": [
      {
        "name": "Mark iD_PEP ir Sankcijų paslaugų teikimo sutartis NF.pdf",
        "content": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdG..........9QcmV2IDMxNDQ2MD4+CnN0YXJ0eHJlZgozNTk4ODIKJSVFT0YK"
      }
    ]
  }
}
```

Please note that some json values have been truncated in the previous example.

## Sample response

### Sample success response

```
{
  "status": "ok",
  "token": "3cf176a2-5229-6c07-e7d6-6a5fe042b46b",
  "control_code": "0668"
}
```

### Sample failed response

```
{
  "status": "ok",
  "token": "7e3cc964-7ea5-109c-ddf1-9a4f2f417b43",
  "control_code": "5973"
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/en/mobile/sign.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "type": "pdf",
  "phone": "+37269000366",
  "message": "any message",
  "message_format": "GSM-7",
  "code": "60001017705",
  "signature_position": "auto",
  "signature_page": "last_page",
  "peps": true,
  "sanctions": true,
  "pdf": {
    "files": [
      {
        "name": "Mark iD_PEP ir Sankcijų paslaugų teikimo sutartis NF.pdf",
        "content": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdG..........9QcmV2IDMxNDQ2MD4+CnN0YXJ0eHJlZgozNTk4ODIKJSVFT0YK"
      }
    ]
  }
}'
```

Please note that some json values have been truncated in the previous example.

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidInitSigningRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/MobileidInitSigningRequestBuilder.html) as request builder.

```
// The following values is dummy.
$accessToken = '6102d227-0dcf-4ce3-ab8f-337385f09ee4';

$filePath = __DIR__ . '/demo.pdf';

$initSignReq = (new MobileidInitSigningRequestBuilder)
  ->withAccessToken($accessToken)
  ->withType('pdf')
  ->withPhone('+37269000366')
  ->withMessage('Dummy')
  ->withMessageFormat('GSM-7')
  ->withCode('60001017705')
  ->withSignaturePosition('auto')
  ->withSignaturePage('last_page')
  ->withPeps(true)
  ->withsanctions(true)
  ->withPdf(
    (new Files)->setFiles([
      (new FileUpload)->setName(basename($filePath))->setContent(base64_encode(file_get_contents($filePath)))
    ])
  )
  ->createRequest();
$initSignRes = $client->postRequest($initSignReq);
$initSignResArray = $response->toArray(false);
var_dump($initSignResArray);
```
