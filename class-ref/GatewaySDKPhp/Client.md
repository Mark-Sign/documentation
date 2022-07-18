---
layout: default
title: Client
parent: Class References
has_toc: true
nav_order: 1
---

# Client
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/Client.php)

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
| private | String | accessToken | API access token |
| private | [`AppBundle\GatewaySDKPhp\ConnectorInterface`](/class-ref/GatewaySDKPhp/ConnectorInterface.html) | connector | Connector that will be used to request API |
| private | `Psr\Log\LoggerInterface` | logger | PSR compatible logger |


## Methods

### `public __construct(string $accessToken, Psr\Log\LoggerInterface $logger, string $locale)`

*returns* void

Constructs the object

### `public getRequestBuilder(string $apiName)`

*returns* void


### `public getSignDocumentSmartIdRequestBuilder()`

*returns* AppBundle\GatewaySDKPhp\RequestBuilder\SignDocumentSmartIdRequestBuilder


### `public postRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* void

Makes API request through `connector`

### `private getConnector()`

*returns* AppBundle\GatewaySDKPhp\ConnectorInterface


### `private hydrateRequestBuilder(AppBundle\GatewaySDKPhp\RequestBuilder\RequestBuilderInterface $requestBuilder)`

*returns* void


