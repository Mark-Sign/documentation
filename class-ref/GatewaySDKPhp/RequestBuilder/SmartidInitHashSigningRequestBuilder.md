---
layout: default
title: SmartidInitHashSigningRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# SmartidInitHashSigningRequestBuilder
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
| protected | String | hash | Sets the hash to ssign |
| protected | String | hashAlgorithm | Hash algorithm. Possible values: SHA256 or SHA512 |
| protected | String | country | Signer's country code: LT, EE |
| protected | String | message | Message to be displayed on phone screen |
| protected | String | code | Personal code |
| protected | String | certificateLevel | Requested SK Smart-ID certificate level. Possible values: QSCD, QUALIFIED. Defaults to QSCD |


## Methods

### `public withHash(string $hash)`

*returns* self

Sets `hash`

### `public withHashAlgorithm(string $hashAlgorithm)`

*returns* self

Sets `hashAlgorithm`

### `public withCountry(string $country)`

*returns* self

Sets `country`

### `public withMessage(string $message)`

*returns* self

Sets `message`

### `public withCode(string $code)`

*returns* self

Sets `code`

### `public withCertificateLevel(string $certificateLevel)`

*returns* self

Sets `certificate_level`

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/documentation/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

