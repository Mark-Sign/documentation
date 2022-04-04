---
layout: default
title: Connector
parent: Class References
has_toc: true
nav_order: 1
---

# Connector
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/Connector.php)

{: .no_toc }

Implements `AppBundle\GatewaySDKPhp\ConnectorInterface`
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
| private | String | apiUrl | URL of the request |
| private | `Symfony\Component\HttpClient\HttpClient` | client | Holds client through which actual API requests are made |
| private | `Psr\Log\LoggerInterface` | logger | PSR compatible logger |


## Methods

### `public __construct(Psr\Log\LoggerInterface $logger)`

*returns* void


### `public postRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public replaceURLParameters(string $url, AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* string


### `public postSignDocumentSmartIdRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postSignDocumentMobileIdRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postDocumentUploadRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postDocumentValidationRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postDocumentFileValidationRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postDocumentSignerInviteRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public getDocumentStatusCheckRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public getDocumentDownloadRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public deleteDocumentRemoveRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postMobileidInitAuthRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postMobileidIdentificationSessionStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postMobileidInitSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postMobileidSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postMobileidInitHashSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postMobileidHashSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public deleteMobileidIdentificationSessionRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postSmartidInitAuthRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postSmartidIdentificationSessionStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postSmartidInitSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postSmartidSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postSmartidInitHashSignRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public postSmartidHashSigningStatusRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `public deleteSmartidIdentificationSessionRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface


### `private postClientRequest(string $method, string $apiPath, array $options)`

*returns* Symfony\Contracts\HttpClient\ResponseInterface

Performs API request and return response to caller method

