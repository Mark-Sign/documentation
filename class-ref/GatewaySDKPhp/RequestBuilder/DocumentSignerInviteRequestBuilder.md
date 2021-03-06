---
layout: default
title: DocumentSignerInviteRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# DocumentSignerInviteRequestBuilder
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/RequestBuilder/DocumentSignerInviteRequestBuilder.php)

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

| Visibility | Type | Name | Description |
| :--- | :--- | :--- | :--- |
| protected | String | documentId | UUID of the document |
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Signer`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Signer.html) | signer | Signer to be set in request |


## Methods

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

### `public withDocumentId(string $documentId)`

*returns* self

Sets `documentId`, UUID of the document

### `public withSigner(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Signer $signer)`

*returns* self

Sets `signer` for request
