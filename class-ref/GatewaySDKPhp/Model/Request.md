---
layout: default
title: Request
parent: Class References
has_toc: true
nav_order: 1
---

# Request
{: .no_toc }

Implements `AppBundle\GatewaySDKPhp\Model\RequestInterface`
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
| private | String | apiName | Name alias of API |
| private | Array | body | Request parameters |


## Methods

### `public setApiName(string $apiName)`

*returns* self


### `public getApiName()`

*returns* string


### `public setBodyParameters(array $params)`

*returns* AppBundle\GatewaySDKPhp\Model\RequestInterface


### `public getBodyParameters()`

*returns* array


