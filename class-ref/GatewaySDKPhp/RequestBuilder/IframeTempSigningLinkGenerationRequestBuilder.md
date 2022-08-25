---
layout: default
title: IframeTempSigningLinkGenerationRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# IframeTempSigningLinkGenerationRequestBuilder
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/RequestBuilder/IframeTempSigningLinkGenerationRequestBuilder.php)

{: .no_toc }

Extends `AppBundle\GatewaySDKPhp\RequestBuilder\AbstractRequestBuilder` <br><br> Trait `AppBundle\GatewaySDKPhp\RequestBuilder\Traits\TraitBuildParameters`
{: .fw-300 .fs-6 }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Properties

| Visibility  | Type                                                                                                                              | Name                | Description                                                                     |
|:------------|:----------------------------------------------------------------------------------------------------------------------------------|:--------------------|:--------------------------------------------------------------------------------|
| protected   | String                                                                                                                            | documentId          | UUID of the document                                                            |
| protected   | String                                                                                                                            | callbackUrl         | Callback URL                                                                    |
| protected   | Integer                                                                                                                           | expireAfter         | Expiration period in minutes (default value is 30)                              |
| protected   | Integer                                                                                                                           | deleteDocumentAfter | Document removal period in minutes (should not be less than expire_after value) |
| protected   | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\FileUpload`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/FileUpload.html)  | file                | File object                                                                     |
| protected   | Array of [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Signer`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Signer.html) | signers             | Array of signers object                                                         |
| protected   | String                                                                                                                            | language            | User interface language ('lt' or 'en')                                          |


## Methods

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

### `public withDocumentId(string $documentId)`

*returns* self

Sets `documentId`, UUID of the document

### `public withFile(FileUpload $file)`

*returns* self

Sets `file`

### `public withCallbackUrl(string $callbackUrl)`

*returns* self

Sets callback url

### `public withExpireAfter(int $expireAfter)`

*returns* self

Sets expires after

### `public withDeleteDocumentAfter(int $deleteDocumentAfter)`

*returns* self

Sets Document removal period in minutes

### `public withSigners(array $signers)`

*returns* self

Sets `signers` for request
