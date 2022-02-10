---
layout: default
title: Document Validation
parent: Document
has_toc: true
nav_order: 2
---

# Document validation
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This endpoint is for validation checking of the document.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path</td>
      <td>/api/v2/document/{documentId}/validation.json</td>
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

| Key |  Requirement | Type | Description |
| :--- |  :--- | :--- | :--- |
| documentId |  Mandatory | String | Document UUID from response of ["Document upload"](/documentation/Document/document-upload.md) |

## Request body parameter description

| Key |  Requirement | Type | Description |
| :--- |  :--- | :--- | :--- |
| access_token |  Mandatory | String | API Access Token |

## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `ok` in this case |
| data | Object | Contains validation information |

### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Status message |
| error_code | Number | Unique code for the error |

## Sample request

```
POST /api/v2/document/1a7b6218-af7f-9dad-1b2e-566bcf903fcf/validation.json HTTP/1.1
Host: app.marksign.local
Content-Type: application/json

{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae"
}
```
## Sample response

### Sample success response

```
{
  "status": "ok",
  "data": {
    "simpleReport": {
      "firstTimestampId": null,
      "documentFilename": "ZKc7be.pdf",
      "validSignaturesCount": 0,
      "signaturesCount": 0,
      "firstSignatureId": null,
      "validationTime": 1644497720663,
      "signatureIdList": [],
      "timestampIdList": [],
      "jaxbModel": {
        "validationPolicy": {
          "policyName": "QES AdESQC TL based",
          "policyDescription": "Validate electronic signatures and indicates whether they are Advanced electronic Signatures (AdES), AdES supported by a Qualified Certificate (AdES/QC) or a\n\t\tQualified electronic Signature (QES). All certificates and their related chains supporting the signatures are validated against the EU Member State Trusted Lists (this includes\n\t\tsigner's certificate and certificates used to validate certificate validity status services - CRLs, OCSP, and time-stamps).\n\t"
        },
        "documentName": "ZKc7be.pdf",
        "validSignaturesCount": 0,
        "signaturesCount": 0,
        "containerType": null,
        "signatureOrTimestamp": [],
        "semantic": [],
        "validationTime": 1644497720663
      }
    },
    "diagnosticData": {
      "DocumentName": "ZKc7be.pdf",
      "ValidationDate": "2022-02-10T12:55:20",
      "Signatures": [],
      "UsedCertificates": [],
      "UsedRevocations": [],
      "UsedTimestamps": [],
      "OriginalDocuments": [],
      "TrustedLists": []
    }
  }
}
```

### Sample failed response

```
{
  "status": "error",
  "message": "Document was not found"
}
```

## Implementation

### CURL

```
curl --location --request POST 'https://app.marksign.local/api/v2/document/1a7b6218-af7f-9dad-1b2e-566bcf903fcf/validation.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.md), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentValidationRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/DocumentValidationRequestBuilder.md) as request builder.
And we have to use document uuid as `documentId` that can be found in the response in [this section](/documentation/Document/document-upload.md#using-php-client)

```
$apiKey = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';
$accessToken = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';

$client = new Client($apiKey, new Logger('dev', [new StreamHandler('log.txt')]));

$filePath = __DIR__ . "/demo.pdf";

$uploadRB = (new DocumentUploadRequestBuilder)
    ->withAccessToken($accessToken)
    ->withAccess('private')
    ->withFile(
        (new FileUpload)->setFileName(basename($filePath))->setContent(base64_encode(file_get_contents($filePath)))
    )
    ->withSigners([
        (new Signer)->setName('Tex')->setSurName('Ryta')->setEmail('tex.ryta@domain.com')->setNoEmail(true),
        (new Signer)->setName('John')->setSurName('Quil')->setEmail('john.quil@domain.com')->setNoEmail(true),
    ])
    ->createRequest();
$uploadRes = $client->postRequest($uploadRB);
$uploadResArray = $uploadRes->toArray(false);

$validationRB = (new DocumentValidationRequestBuilder)
    ->withDocumentId($uploadResArray['document']['uuid'])
    ->withAccessToken($accessToken)
    ->createRequest();
$validationRes = $client->postRequest($validationRB);
$validationResArray = $validationRes->toArray(false);
```