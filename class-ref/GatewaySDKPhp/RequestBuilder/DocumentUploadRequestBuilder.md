---
layout: default
title: AppBundle\GatewaySDKPhp\RequestBuilder\DocumentUploadRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# DocumentUploadRequestBuilder
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
| protected | String | access | Document access. Possible values: public, private |
| protected | [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\FileUpload`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/Partials/FileUpload.html) | file | File for request |
| protected | Array of [`AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Signer`](/documentation/class-ref/GatewaySDKPhp/RequestBuilder/Partials/Signer.html) | signers | Signer's who will be invited to perform operations on the document |


## Methods

### `public createRequest()`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface

Creates and returns `AppBundle\GatewaySDKPhp\Model\RequestInterface` to be used with [`postRequest`](/documentation/class-ref/GatewaySDKPhp/ConnectorInterface.html#public-postrequestappbundlegatewaysdkphpmodelrequestinterface-request) method.

### `public withAccess(string $access)`

*returns* self

A short description

### `public withFile(AppBundle\GatewaySDKPhp\RequestBuilder\Partials\FileUpload $file)`

*returns* self

Sets `file` for request

### `public withSigners(array $signers)`

*returns* self

Sets `signers` array

