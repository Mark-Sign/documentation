---
layout: default
title: SmartidInitAuthRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# SmartidInitAuthRequestBuilder
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/RequestBuilder/SmartidInitAuthRequestBuilder.php)

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
| protected | String | code | Personal code |
| protected | String | country | Signer's country code: LT, EE |
| protected | String | message | Message to be displayed on phone screen |
| protected | Boolean | peps | Whether to check PEPs information |
| protected | Boolean | sanctions | Whether to check sanctions information |


## Methods

### `public withCode(string $code)`

*returns* self

Sets `code`

### `public withCountry(string $country)`

*returns* self

Sets `country`

### `public withMessage(string $message)`

*returns* self

Sets `message`

### `public withPeps(bool $peps)`

*returns* self

Sets `peps`

### `public withSanctions(bool $sanctions)`

*returns* self

Sets `sanctions`

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

