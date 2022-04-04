---
layout: default
title: MobileidInitAuthRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# MobileidInitAuthRequestBuilder
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
| protected | String | phone | Phone number |
| protected | String | code | Personal code |
| protected | String | language | Language for messages to be displayed phone screen (default: LIT, other: ENG, RUS, EST) |
| protected | String | message | Message to be displayed on phone screen |
| protected | String | messageFormat | Format of the message which is displayed on the phone screen. Possible values: GSM-7 (default), UCS-2. Max characters count for GSM-7 and UCS-2 is 40 and 20 characters respectively |
| protected | Boolean | peps | Whether to check PEPs information |
| protected | Boolean | sanctions | Whether to check sanctions information |


## Methods

### `public withPhone(string $phone)`

*returns* self

Sets `phone`

### `public withCode(string $code)`

*returns* self

Sets `code`

### `public withLanguage(string $language)`

*returns* self

Sets `language`

### `public withMessage(string $message)`

*returns* self

Sets `message`

### `public withMessageFormat(string $messageFormat)`

*returns* self

Sets `messageFormat`

### `public withPeps(bool $peps)`

*returns* self

Sets `peps`

### `public withSanctions(bool $sanctions)`

*returns* self

Sets `sanctions`

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/documentation/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

