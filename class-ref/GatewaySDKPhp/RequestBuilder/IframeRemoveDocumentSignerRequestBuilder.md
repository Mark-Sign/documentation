---
layout: default
title: IframeRemoveDocumentSignerRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# IframeRemoveDocumentSignerRequestBuilder
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

| Visibility  | Type        | Name         | Description            |
|:------------|:----------------------------------------------------------------------------------------------------------------------------------|:-------------|:--------------------------------------------------------------------------------|
| protected   | String     | documentId   | UUID of the document               |
| protected   | String      | name         | Signer's name                         |
| protected   | String      | surname      | Signer's surname                        |
| protected   | String      | email        | Signer's email |                                                     |
| protected   | String      | personalCode | Signer's personal code                                    |


## Methods

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

### `public withDocumentId(string $documentId)`

*returns* self

Sets `documentId`, UUID of the document

### `public withName(string $name)`

*returns* self

Sets Signer's name

### `public withSurname(string $surname)`

*returns* self

Sets Signer's surname

### `public withEmail(string $email)`

*returns* self

Sets Signer's email

### `public withPersonalCode(string $personalCode)`

*returns* self

Sets Signer's personal code
