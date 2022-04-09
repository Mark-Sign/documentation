---
layout: default
title: Signing Status
parent: Smart-ID APIs
grand_parent: API Reference
has_toc: true
nav_order: 4
---

# Signing status
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This API checks the status of the signing process initialized by [Initialize signing via smart id](/documentation/api-references/smartId/apiSmartidInitSigning.html#initialize-signing-via-smart-id) request.

## Endpoint

<table>
  <tbody>
    <tr>
      <td>Path (Locale: LT)</td>
      <td>/smartid/sign/status/{token}.json</td>
    </tr>
    <tr>
      <td>Path (Locale: EN)</td>
      <td>/en/smartid/sign/status/{token}.json</td>
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
| token | Mandatory | String | Token that is being sent as a response of [Initialize signing via smart id](/documentation/api-references/smartId/apiSmartidInitSigning.html#initialize-signing-via-smart-id) |

## Request body parameter description

| Key | Requirement | Type | Description |
| :--- | :--- | :--- | :--- |
| access_token | Mandatory | String | API Access Token |



## Response body parameter description

### Successful response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the signing process |
| signature_id | String | Unique ID of signature |
| file | Object | Follow [Response file object description](#response-file-object-description) section |
| person | ObJect | Follow [Response person object description](#response-person-object-description) section |
| sanctions_data | Object | Sanction information |
| peps_data | Object | PEPs information |

### Response file object description

| Key | Type | Description |
| :--- | :--- | :--- |
| name | String | Name of the file |
| content | String | Base64 encoded file content |
| digest | String | Digest string of the file |

### Response person object description

| Key | Type | Description |
| :--- | :--- | :--- |
| name | String | Name of the signer |
| surname | String | Surname of the signer |

### Failed response

| Key | Type | Description |
| :--- | :--- | :--- |
| status | String | Status of the request, `error` in this case |
| message | String | Brief message about what is wrong |
| error_code | Integer | Unique code for the error |


## Sample request

```

POST /en/smartid/sign/status/aec29dc7-bde3-8299-6dc6-00686318e538.json HTTP/1.1
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
  "signature_id": "IEBCLXycNwpDQ\/Orcts..........PN+FTv\/nhGn6u+E9z2KB+W4Aw",
  "file": {
    "name": "aec29dc7-bde3-8299-6dc6-00686318e538_signed.pdf",
    "content": "JVBERi0xLjUKJbXtrvsKNzYgMCBvYmoKPDwgL..........RhcnR4cmVmCjEzOTg1MwolJUVPRgo=",
    "digest": "a09f67cf3253cca105..........03e1e3fb3ee5db98c2f9"
  },
  "person": {
    "name": "NAME",
    "surname": "SURNAME"
  },
  "sanctions_data": [{
    "id": 17,
    "reference": "10131008196",
    "first_name": "Ali Barzan Ibrahim Hasan",
    "last_name": "AL-TIKRITI",
    "full_name": "",
    "date_of_birth": "18 Apr 1981",
    "place_of_birth": "Country",
    "aka": "Barzan Ibrahim Hasan al-Tikriti",
    "gender": "male",
    "document_number": "",
    "country_of_origin": "Country",
    "type_sdn_or_entity": "Individual",
    "name_of_the_list": "OFAC SDN (Specially Designated Nationals) List",
    "date_of_publication": "OFAC SDN List",
    "date_of_publication_of_the_list": "2020-09-23 07:28:28",
    "search_created_at": "2019-04-07T11:21:53Z",
    "associates": {
      "parent": "Name Surname"
    },
    "image_url": "http://www.eltiempo.com/archivo/documento/MAM-2761276.jpg",
    "date_of_death": "2020-09-23 07:28:28"
  }],
  "peps_data": [{
    "id": 1422,
    "reference": "10101007067-sHft2244Qt",
    "first_name": "Name",
    "last_name": "Surname",
    "full_name": "Name Surname",
    "political_position": "Lithuanian politician",
    "associates": {
      "parent": "Name Surname"
    },
    "aka": "Name Surname, Name Surname",
    "date_of_birth": "1972-07-20",
    "place_of_birth": "Lithuania",
    "gender": "male",
    "country_of_origin": "",
    "country_of_activity": "",
    "search_created_at": "2020-06-30 08:40:02",
    "date_of_death": "2020-06-30 08:40:02"
  }]
}

```

Please note that some json values have been truncated in the previous example.

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

curl --location --request POST 'https://app.marksign.local/en/smartid/sign/status/aec29dc7-bde3-8299-6dc6-00686318e538.json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "access_token": "52900c96-3f60-5307-3719-5948f0191da6"
}'

```

### Using php-client

To use the php-client, please follow the installation and basic usage [here](/documentation/sdk-php-client.html#usage), and use [`AppBundle\GatewaySDKPhp\RequestBuilder\SmartidSigningProcessStatusRequestBuilder`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/SmartidSigningProcessStatusRequestBuilder.html) as request builder.

```

/**
 * The token can be found from the response of 'Initialize signing via smart id' request.
 * The following is a dummy to use as example.
 */
$token = 'aec29dc7-bde3-8299-6dc6-00686318e538';

$signProcStatReq = (new SmartidSigningProcessStatusRequestBuilder)
  ->withToken($token)
  ->createRequest();
$signProcStatRes = $client->postRequest($signProcStatReq);
$signProcStatResArray = $signProcStatRes->toArray();
var_dump($signProcStatResArray);

```
