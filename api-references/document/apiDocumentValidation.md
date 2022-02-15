---
layout: default
title: Document Validation
parent: Document APIs
has_toc: true
nav_order: 1
---

# Document Validation
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
      <td>/api/v2/document/{documentId}/validation.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/api/v2/document/{documentId}/validation.json</td>
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
| documentId | Mandatory | String | Description |

## Request body parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | Description |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| data | Array of Objects | Description |

### Response data object description

| Key | Type | Description |
| :--- | :--- | :--- |
| simpleReport | Array of Objects | Description |
| diagnosticData | Array of Objects | Description |

### Response simpleReport object description

| Key | Type | Description |
| :--- | :--- | :--- |
| validationTime | Integer | Description |
| firstTimestampId | NULL | Description |
| documentFilename | String | Description |
| validSignaturesCount | Integer | Description |
| signatureIdList | Object | Description |
| timestampIdList | Object | Description |
| firstSignatureId | NULL | Description |
| signaturesCount | Integer | Description |
| jaxbModel | Array of Objects | Description |

### Response signatureIdList object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response timestampIdList object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response jaxbModel object description

| Key | Type | Description |
| :--- | :--- | :--- |
| validationPolicy | Array of Objects | Description |
| documentName | String | Description |
| validSignaturesCount | Integer | Description |
| signaturesCount | Integer | Description |
| containerType | NULL | Description |
| signatureOrTimestamp | Object | Description |
| semantic | Object | Description |
| validationTime | Integer | Description |

### Response validationPolicy object description

| Key | Type | Description |
| :--- | :--- | :--- |
| policyName | String | Description |
| policyDescription | String | Description |

### Response signatureOrTimestamp object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response semantic object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response diagnosticData object description

| Key | Type | Description |
| :--- | :--- | :--- |
| DocumentName | String | Description |
| ValidationDate | String | Description |
| Signatures | Object | Description |
| UsedCertificates | Object | Description |
| UsedRevocations | Object | Description |
| UsedTimestamps | Object | Description |
| OriginalDocuments | Object | Description |
| TrustedLists | Object | Description |

### Response Signatures object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response UsedCertificates object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response UsedRevocations object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response UsedTimestamps object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response OriginalDocuments object description

| Key | Type | Description |
| :--- | :--- | :--- |


### Response TrustedLists object description

| Key | Type | Description |
| :--- | :--- | :--- |




### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Description |
| message | String | Description |



## Sample request

```
POST /en/api/v2/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/validation.json HTTP/1.1
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
      "validationTime": 1644945539572,
      "firstTimestampId": null,
      "documentFilename": "XsZP49.pdf",
      "validSignaturesCount": 0,
      "signatureIdList": [],
      "timestampIdList": [],
      "firstSignatureId": null,
      "signaturesCount": 0,
      "jaxbModel": {
        "validationPolicy": {
          "policyName": "QES AdESQC TL based",
          "policyDescription": "Validate electronic signatures and indicates whether they are Advanced electronic Signatures (AdES), AdES supported by a Qualified Certificate (AdES/QC) or a\n\t\tQualified electronic Signature (QES). All certificates and their related chains supporting the signatures are validated against the EU Member State Trusted Lists (this includes\n\t\tsigner's certificate and certificates used to validate certificate validity status services - CRLs, OCSP, and time-stamps).\n\t"
        },
        "documentName": "XsZP49.pdf",
        "validSignaturesCount": 0,
        "signaturesCount": 0,
        "containerType": null,
        "signatureOrTimestamp": [],
        "semantic": [],
        "validationTime": 1644945539572
      }
    },
    "diagnosticData": {
      "DocumentName": "XsZP49.pdf",
      "ValidationDate": "2022-02-15T17:18:59",
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
curl --location --request POST 'https://app.marksign.local/en/api/v2/document/cff827fc-e70e-167c-4ae5-d388b1b5c264/validation.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "f4b79b72-7587-f417-41f8-2de5a7c87fae"
}'
```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\DocumentValidationRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/DocumentValidationRequestBuilder.html) as request builder.

```
/**
 * The document id that was found from document upload request.
 * The following is a dummy to use as example.
 */
$documentId = 'c66cf14e-f763-9757-3b83-e5e28126a6df';

$validationReq = (new DocumentValidationRequestBuilder)
  ->withDocumentId($documentId)
  ->createRequest();
$validationRes = $client->postRequest($validationReq);
$validationResArray = $validationRes->toArray(false);
var_dump($validationResArray);
```
