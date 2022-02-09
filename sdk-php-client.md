---
layout: default
title: SDK php-client
has_toc: true
nav_order: 5
---

# php-client
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

The [PHP client](https://github.com/Mark-Sign/gateway-sdk-php/) helps to lighten the hassle of building all APIs from the scratch. It contains wrapper classes which will help the development of integration with the Mark-Sign APIs faster. This package complies with PSR-4 autoloading standard.

## Installation

Installation is pretty much stright forward with composer. To install, just run the following command:

```
composer require mark-sign/gateway-sdk-php
```

## Usage

To use the package, at first initialize the `AppBundle\GatewaySDKPhp\Client` class with APIKey and a logger insterface. In the following example [monolog logger](https://seldaek.github.io/monolog/) is used.

```
use AppBundle\GatewaySDKPhp\Client;
use Monolog\Handler\StreamHandler;
use Monolog\Logger;

$apiKey = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';
$logger = new Logger('dev', [new StreamHandler('log_file_name')]);

$client = new Client($apiKey, $logger);
```

Then, build a request builder object which will contain request body parameters. The final call to `createRequest()` method will return an object that implements `AppBundle\GatewaySDKPhp\Model\RequestInterface`. All the request builders under the `AppBundle\GatewaySDKPhp\RequestBuilder` namespace implements `AppBundle\GatewaySDKPhp\RequestBuilder\RequestBuilderInterface` which contains the declaration of `createRequest()` method, and hence, all the request builders will have their own implementation of `createRequest()` method.

In the following, `AppBundle\GatewaySDKPhp\RequestBuilder\DocumentUploadRequestBuilder` is used as request builder.

```
use AppBundle\GatewaySDKPhp\RequestBuilder\DocumentUploadRequestBuilder;

$filePath = __DIR__ . "demo.pdf";

$requestBuilder = (new DocumentUploadRequestBuilder)
    ->withAccessToken(ACCESS_TOKEN)
    ->withAccess('private')
    ->withFile(
        (new FileUpload)->setFileName(basename($filePath))->setContent(base64_encode(file_get_contents($filePath)))
    )
    ->withSigners([
        (new Signer)->setName('Tex')->setSurName('Ryta')->setEmail('tex.ryta@domain.com')->setNoEmail(false),
        (new Signer)->setName('John')->setSurName('Quil')->setEmail('john.quil@domain.com')->setNoEmail(false),
    ])
    ->createRequest();
```

And finally, pass the result of `createRequest()` method to the `Client`'s `postRequest()` method.

```
$response = $client->postRequest($requestBuilder);
$responseArray = $response->toArray(false);
```

And, that's it. API call has been done and by using `toArray()` on the response, we can convert the response to an array.
