---
layout: default
title: AppBundle\GatewaySDKPhp\Client
parent: Class References
has_toc: true
nav_order: 1
---

# AppBundle\GatewaySDKPhp\Client
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
| private |  | apiKey |  |
| private |  | connector |  |
| private |  | logger |  |


## Methods

### `public __construct(string $apiKey, Psr\Log\LoggerInterface $logger)`

*returns* void

A short description

### `public getRequestBuilder(string $apiName)`

*returns* void

A short description

### `public getSignDocumentSmartIdRequestBuilder()`

*returns* AppBundle\GatewaySDKPhp\RequestBuilder\SignDocumentSmartIdRequestBuilder

A short description

### `public postRequest(AppBundle\GatewaySDKPhp\Model\RequestInterface $request)`

*returns* AppBundle\GatewaySDKPhp\Model\ResponseInterface

A short description

### `private getConnector()`

*returns* AppBundle\GatewaySDKPhp\ConnectorInterface

A short description

### `private hydrateRequestBuilder(AppBundle\GatewaySDKPhp\RequestBuilder\RequestBuilderInterface $requestBuilder)`

*returns* void

A short description

