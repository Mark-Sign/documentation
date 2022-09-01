---
layout: default
title: Initialize Only Signing
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 4
---

# Initialize only signing via smart id
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
      <td>/smartid/only-sign.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/only-sign.json</td>
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
| access_token | Mandatory | String | API Access Token |
| type | Mandatory | String | Type of the file to be signed. Possible values: pdf, adoc, bdoc, asice |
| country | Mandatory | String | Signer country code: LT, LV, EE |
| message | Optional | String | Message displayed on the phone screen |
| code | Mandatory | String | Personal code related to the phone number |
| signature_position | Optional | String | Position of a visible signature (pdf annotation) in the pdf document. Possible values: auto, left_top, left_bottom, right_top, right_bottom. Unset value is equal to invisible signature |
| signature_page | Optional | String | Page of a visible signature (pdf annotation) in the pdf document. Possible values: first_page, last_page. Default value is last_page |
| certificate_level | Optional | String | Requested SK Smart-ID certificate level. Possible values: QSCD, QUALIFIED. Defaults to QSCD |
| peps | Optional | Boolean | Whether to check PEPs information, default is `false` |
| sanctions | Optional | Boolean | Whether to check sanctions information, default is `false` |
| pdf | Any one of pdf/asice/adoc/bdoc is mandatory | Object | Follow [Request pdf/asice/adoc/bdoc object description](#request-pdfasiceadocbdoc-object-description) |

### Request pdf object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| files | Mandatory | Array of Objects | Follow [Request files object description](#request-files-object-description) |

### Request files object description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| name | Mandatory | String | Name of the file |
| content | Mandatory | String | Base64 encoded file content |
| digest | Optional | String | Digest of the file |

## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| token | String | Unique token to be used in future request |
| control_code | String | Verification code |


### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |
| error_code | Integer | Unique code for the error. Error codes are listed [here](/api-references/errorCodes.html) |

## Sample request

```

POST /en/smartid/only-sign.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "type": "pdf",
  "country": "LT",
  "message": "any message",
  "code": "30303039914",
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

curl --location --request POST 'https://app.marksign.local/en/smartid/only-sign.json' \
--header 'Content-Type: application/json'
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6",
  "type": "pdf",
  "country": "LT",
  "message": "any message",
  "code": "30303039914",
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

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidInitOnlySigningRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/SmartidInitSigningRequestBuilder.html) as request builder.

```

$filePath = __DIR__ . '/demo.pdf';

$initSignReq = (new SmartidInitOnlySigningRequestBuilder)
  ->withType('pdf')
  ->withCountry('LT')
  ->withMessage('any message')
  ->withCode('30303039914')
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
$initSignResArray = $response->toArray();
var_dump($initSignResArray);

```
