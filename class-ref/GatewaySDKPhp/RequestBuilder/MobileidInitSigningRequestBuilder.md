---
layout: default
title: MobileidInitSigningRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# MobileidInitSigningRequestBuilder
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/RequestBuilder/MobileidInitSigningRequestBuilder.php)

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
| protected | String | type | Document format. Possible values: pdf, adoc, bdoc, asice |
| protected | String | phone | Phone number |
| protected | String | message | Message to be displayed on phone screen |
| protected | String | messageFormat | Format of the message which is displayed on the phone screen. Possible values: GSM-7 (default), UCS-2. Max characters count for GSM-7 and UCS-2 is 40 and 20 characters respectively |
| protected | String | code | Personal code |
| protected | String | signaturePosition | Position of a visible signature in the document. Possible values: auto, left_top, left_bottom, right_top, right_bottom. default results in invisible signature |
| protected | String | signaturePage | Page of a visible signature (pdf annotation) in the pdf document. Possible values: first_page, last_page. Default: last_page |
| protected | Boolean | peps | Whether to check PEPs information |
| protected | Boolean | sanctions | Whether to check sanctions information |
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Files.html) | pdf | PDF files object |
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Files.html) | asice | ASICE files object |
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Files.html) | adoc | ADOC files object |
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Files.html) | bdoc | BDOC files object |


## Methods

### `public withType(string $type)`

*returns* self

Sets `type`

### `public withPhone(string $phone)`

*returns* self

Sets `phone`

### `public withMessage(string $message)`

*returns* self

Sets `message`

### `public withMessageFormat(string $messageFormat)`

*returns* self

Sets `messageFormat`

### `public withCode(string $code)`

*returns* self

Sets `code`

### `public withSignaturePosition(string $signaturePosition)`

*returns* self

Sets `signaturePosition`

### `public withSignaturePage(string $signaturePage)`

*returns* self

Sets `signaturePage`

### `public withPeps(bool $peps)`

*returns* self

Sets `peps`

### `public withSanctions(bool $sanctions)`

*returns* self

Sets `sanctions`

### `public withPdf(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files $pdf)`

*returns* self

Sets `pdf` object

### `public withAsice(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files $asice)`

*returns* self

Sets `asice` Object

### `public withAdoc(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files $adoc)`

*returns* self

Sets `adoc` object

### `public withBdoc(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files $bdoc)`

*returns* self

Sets `bdoc` object

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

