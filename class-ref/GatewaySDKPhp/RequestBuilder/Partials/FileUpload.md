---
layout: default
title: FileUpload
parent: Class References
has_toc: true
nav_order: 1
---

# FileUpload
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
| protected | String | filename | Name of the file, will be set to 'filename' in request body |
| protected | String | name | Name of the file, will be set to 'name' in request body |
| protected | String | content | Generally base64 encoded content of file |
| protected | String | digest | Digest of the file |
| protected | String | callbackUrl | Callback URL, will be set to 'callbackUrl' in request body |


## Methods

### `public getFilename()`

*returns* self


### `public setFilename(string $filename)`

*returns* self


### `public getName()`

*returns* self


### `public setName(string $name)`

*returns* self


### `public getContent()`

*returns* self


### `public setContent(string $content)`

*returns* self


### `public getCallbackUrl()`

*returns* self


### `public setCallbackUrl(string $callbackUrl)`

*returns* self


### `public getDigest()`

*returns* self


### `public setDigest(string $digest)`

*returns* self


