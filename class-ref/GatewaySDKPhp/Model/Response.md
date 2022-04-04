---
layout: default
title: Response
parent: Class References
has_toc: true
nav_order: 1
---

# Response
{: .no_toc }

Implements `AppBundle\GatewaySDKPhp\Model\ResponseInterface`
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
| private | `Symfony\Contracts\HttpClient\ResponseInterface` | response |  |


## Methods

### `public __construct(Symfony\Contracts\HttpClient\ResponseInterface $response)`

*returns* void

### `public getStatusCode()`

*returns* int

Gets response status code

### `public getContent()`

*returns* string

Gets content from response

### `public toArray()`

*returns* array

Converts the response to array

### `public getHeaders()`

*returns* array

Gets response headers

### `public getHeader(string $headerName)`

*returns* string

Gets response header by name

