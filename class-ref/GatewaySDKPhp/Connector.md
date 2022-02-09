---
layout: default
title: AppBundle\GatewaySDKPhp\Connector
parent: Document
has_toc: true
nav_order: 1
---

# AppBundle\GatewaySDKPhp\Connector
{: .no_toc }

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
| private |  | apiUrl |  |
| private |  | client |  |
| private |  | logger |  |


## Methods

### `public __construct(Psr\Log\LoggerInterface $logger)`

*returns* void

A short description

### `public postRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public replaceURLParameters(string $url, AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* string

A short description

### `public postSignDocumentSmartIdRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postSignDocumentMobileIdRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postDocumentUploadRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postDocumentValidationRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postDocumentFileValidationRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postDocumentSignerInviteRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public getDocumentStatusCheckRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public getDocumentDownloadRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public deleteDocumentRemoveRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postMobileidInitAuthRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postMobileidIdentificationSessionStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postMobileidInitSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postMobileidSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postMobileidInitHashSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postMobileidHashSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public deleteMobileidIdentificationSessionRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postSmartidInitAuthRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postSmartidIdentificationSessionStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postSmartidInitSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postSmartidSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postSmartidInitHashSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public postSmartidHashSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `public deleteSmartidIdentificationSessionRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `private postClientRequest(string $method, string $apiPath, array $options)`

*returns* Symfony\Contracts\HttpClient\ResponseInterface

A short description

