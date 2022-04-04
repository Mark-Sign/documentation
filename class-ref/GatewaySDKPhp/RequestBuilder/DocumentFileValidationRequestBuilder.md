---
layout: default
title: DocumentFileValidationRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# DocumentFileValidationRequestBuilder
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/RequestBuilder/DocumentFileValidationRequestBuilder.php)

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
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\FileUpload`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/Partials/FileUpload.html) | file | File for request |

## Methods

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/documentation/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

### `public withFile(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\FileUpload $file)`

*returns* self

Sets `file` for request

