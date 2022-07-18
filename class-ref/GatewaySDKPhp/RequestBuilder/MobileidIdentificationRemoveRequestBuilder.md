---
layout: default
title: MobileidIdentificationRemoveRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# MobileidIdentificationRemoveRequestBuilder
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/RequestBuilder/MobileidIdentificationRemoveRequestBuilder.php)

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
| protected | String | sessionId | Response token from initialize authentication or signing processes |


## Methods

### `public withSessionId(string $sessionId)`

*returns* self

Sets `sessionId`

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

