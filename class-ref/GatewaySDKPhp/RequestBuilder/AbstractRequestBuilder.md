---
layout: default
title: AppBundle\GatewaySDKPhp\RequestBuilder\AbstractRequestBuilder
parent: Class References
has_toc: true
nav_order: 1
---

# AbstractRequestBuilder
{: .no_toc }

Implements `AppBundle\GatewaySDKPhp\RequestBuilder\RequestBuilderInterface`
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
| protected | String | accessToken | Access token to be used in API |
| protected | Array | bodyParams | Request parameters |


## Methods

### `public withAccessToken(string $accessToken)`

*returns* AppBundle\GatewaySDKPhp\RequestBuilder\RequestBuilderInterface

Sets `accessToken`

### `protected validateParameters(array $requiredParams)`

*returns* self

Sets `bodyParams`

