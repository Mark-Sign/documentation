---
layout: default
title: ResponseInterface
parent: Class References
has_toc: true
nav_order: 1
---

# ResponseInterface
[view source](https://github.com/Mark-Sign/gateway-sdk-php/blob/master/src/Model/ResponseInterface.php)

{: .no_toc }



<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>


## Methods

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
