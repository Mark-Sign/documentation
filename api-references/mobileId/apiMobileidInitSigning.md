---
layout: default
title: Initialize Signing
parent: Mobile-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 3
---

# Initialize signing via mobile id
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API initializes document signing/identification with qualified electronic signature stored on SIM card.

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
| access_token | Mandatory | String | API Access Token |
| type | Mandatory | String | Type of the file to be signed. Possible values: pdf, adoc, bdoc, asice |
| phone | Mandatory | String | Phone number of the signer |
| message | Optional | String | Message displayed on the phone screen |
| message_format | Optional | String | Format of the message which is displayed on the phone screen. Possible values: GSM-7 (default), UCS-2. Max characters count for GSM-7 and UCS-2 is 40 and 20 characters respectively |
| code | Mandatory | String | Personal code related to the phone number |
| signature_position | Optional | String | Position of a visible signature (pdf annotation) in the pdf document. Possible values: auto, left_top, left_bottom, right_top, right_bottom. Unset value is equal to invisible signature |
| signature_page | Optional | String | Page of a visible signature (pdf annotation) in the pdf document. Possible values: first_page, last_page. Default value is last_page |
| peps | Optional | Boolean | Whether to check PEPs information, default is `false` |
| sanctions | Optional | Boolean | Whether to check sanctions information, default is `false` |
| pdf | Any one of pdf/asice/adoc/bdoc is mandatory | Object | Follow [Request pdf/asice/adoc/bdoc object description](#request-pdfasiceadocbdoc-object-description) |
| asice | Any one of pdf/asice/adoc/bdoc is mandatory | Object | Follow [Request pdf/asice/adoc/bdoc object description](#request-pdfasiceadocbdoc-object-description) |
| adoc | Any one of pdf/asice/adoc/bdoc is mandatory | Object | Follow [Request pdf/asice/adoc/bdoc object description](#request-pdfasiceadocbdoc-object-description) |
| bdoc | Any one of pdf/asice/adoc/bdoc is mandatory | Object | Follow [Request pdf/asice/adoc/bdoc object description](#request-pdfasiceadocbdoc-object-description) |

### Request pdf/asice/adoc/bdoc object description

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
  "status": "error",
  "message": "Invalid parameter [type]: Invalid type",
  "error_code": 40001
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

To use the php-client, please follow the installation and basic usage [here](/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\MobileidInitSigningRequestBuilder`](/class-ref/GatewaySDKPhp/RequestBuilder/MobileidInitSigningRequestBuilder.html) as request builder.

```
/**
 * The token in response ($initSignResArray['token'] in this example),
 * might need to be saved for future purposes.
 */
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
$initSignResArray = $initSignRes->toArray();
var_dump($initSignResArray);

```
