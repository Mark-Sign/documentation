---
layout: default
title: Initialize Signing
parent: Mobile-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 3
---

# Initialize Signing
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
  "token": "e287226b-662b-013b-02cd-ede81a4013ec",
  "control_code": "2049"
}
```

### Sample failed response

```
{
  "status": "ok",
  "token": "1aa8b210-3695-dc7b-bf2e-480e4e6127c8",
  "control_code": "3291"
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

$initSignReq = (new MobileidInitSigningRequestBuilder)
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
