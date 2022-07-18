---
layout: default
title: DocumentRemoveRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# DocumentRemoveRequestBuilder
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/RequestBuilder/DocumentRemoveRequestBuilder.php)

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


## Methods

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

### `public withDocumentId(string $documentId)`

*returns* self

Sets `documentId`, UUID of the document

