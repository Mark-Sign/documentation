---
layout: default
title: Smartid Init Signing
parent: Smart-ID APIs
has_toc: true
nav_order: 3
---

# Smartid Init Signing
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
      <td>/smartid/sign.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/sign.json</td>
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
| country | Mandatory | String | Description |
| message | Mandatory | String | Description |
| code | Mandatory | String | Description |
| signature_position | Mandatory | String | Description |
| signature_page | Mandatory | String | Description |
| certificate_level | Mandatory | String | Description |
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
| message | String | Description |
| error_code | Integer | Description |



## Sample request

```
POST /en/smartid/sign.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "type": "pdf",
  "country": "LT",
  "message": "any message",
  "code": "50001018865",
  "signature_position": "auto",
  "signature_page": "last_page",
  "certificate_level": "QUALIFIED",
  "peps": true,
  "sanctions": true,
  "pdf": {
    "files": [
      {
        "name": "demo.pdf",
        "content": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0aCA3Ny..........RzdHJlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo="
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
  "token": "dcfda816-f9ce-d69f-94eb-a5ed87d50606",
  "control_code": "9269"
}
```

### Sample failed response

```
{
  "status": "error",
  "message": "Invalid parameter [type]: Invalid type",
  "error_code": 40001
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/en/smartid/sign.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "type": "pdf",
  "country": "LT",
  "message": "any message",
  "code": "50001018865",
  "signature_position": "auto",
  "signature_page": "last_page",
  "certificate_level": "QUALIFIED",
  "peps": true,
  "sanctions": true,
  "pdf": {
    "files": [
      {
        "name": "demo.pdf",
        "content": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL0xlbmd0aCA3Ny..........RzdHJlYW0KZW5kb2JqCnN0YXJ0eHJlZgo1MDg5MwolJUVPRgo="
      }
    ]
  }
}'
```

Please note that some json values have been truncated in the previous example.

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidInitSigningRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidInitSigningRequestBuilder.html) as request builder.

```
$filePath = __DIR__ . '/demo.pdf';

$initSignReq = (new SmartidInitSigningRequestBuilder)
  ->withType('pdf')
  ->withCountry('LT')
  ->withMessage('any message')
  ->withCode('50001018865')
  ->withSignaturePosition('auto')
  ->withSignaturePage('last_page')
  ->withCertificateLevel('QUALIFIED')
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
