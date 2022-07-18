---
layout: default
title: SmartidInitOnlySigningRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# SmartidInitOnlySigningRequestBuilder
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
| protected | String | type | Document format. Possible values: pdf |
| protected | String | country | Signer's country code: LT, EE |
| protected | String | message | Message to be displayed on phone screen |
| protected | String | code | Personal code |
| protected | String | signaturePosition | Position of a visible signature in the document. Possible values: auto, left_top, left_bottom, right_top, right_bottom. default results in invisible signature |
| protected | String | signaturePage | Page of a visible signature (pdf annotation) in the pdf document. Possible values: first_page, last_page. Default: last_page |
| protected | String | certificateLevel | Requested SK Smart-ID certificate level. Possible values: QSCD, QUALIFIED. Defaults to QSCD |
| protected | Boolean | peps | Whether to check PEPs information |
| protected | Boolean | sanctions | Whether to check sanctions information |
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files`](/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Files.html) | pdf | PDF files object |

## Methods

### `public withType(string $type)`

*returns* self

Sets `type`

### `public withCountry(string $country)`

*returns* self

Sets `country`

### `public withMessage(string $message)`

*returns* self

Sets `message`

### `public withCode(string $code)`

*returns* self

Sets `code`

### `public withSignaturePosition(string $signaturePosition)`

*returns* self

Sets `signaturePosition`

### `public withSignaturePage(string $signaturePage)`

*returns* self

Sets `signaturePage`

### `public withCertificateLevel(string $certificateLevel)`

*returns* self

Sets `certificate_level`

### `public withPeps(bool $peps)`

*returns* self

Sets `peps`

### `public withSanctions(bool $sanctions)`

*returns* self

Sets `sanctions`

### `public withPdf(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Files $pdf)`

*returns* self

Sets `pdf` object

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

