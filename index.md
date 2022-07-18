---
layout: default
title: Home
nav_order: 1
---

# Mark Sign Gateway PHP Client

Mark Sign Gateway PHP Client is given as open source PHP Client, allowing you to tweak its functionality to fit your specific needs.
This library simplifies the integration in PHP applications by encapsulating all Gateway API calls and responses in PHP objects.
This guide describes how to use our solution to upload, sign , validate and download documents. In only just few steps, you'll be able to use our Signature solution.

## Execution Flow
We have two types of system, one is Mobile ID & Another one is Smart ID.
We can use any of them for doing all of our tasks.
For each type of works, we use RequestBuilder Class for preparing our request
& then post that request using Client Class for collecting result. For simplicity, we will use Smart ID in all of our examples.
But you can use same type of examples for Mobile ID too.

## Getting started

### Installation
You can install it in your project using different ways.
1. From your php command line console run
```
composer require mark-sign/gateway-sdk-php
```
2. Or, alternatively you Download or clone repository
from this link https://github.com/Mark-Sign/gateway-sdk-php and run
```
composer install
```

### Initialize Library
To begin using this package, initialize the Client class with an access token( provided by mark sign which is used for authorization )
and a logger interface for logging detail about different server requests. The monolog logger is used in the following example.

```
use AppBundle\GatewaySDKPhp\Client;
use Monolog\Handler\StreamHandler;
use Monolog\Logger;

$accessToken = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';
$logger = new Logger('dev', [new StreamHandler('log_file_name')]);

$client = new Client($accessToken, $logger);
```

### Initialize Authentication
For doing any further operations, we need unique token from server which will be used as unique identifier for us.
We can collect this token by initializing authentication process.
For initiating authentication process, we will instantiate a `SmartidInitAuthRequestBuilder` object, will set all the necessary body parameters access_token, code, country & will call `createRequest` method.
Then we will post this request using our previously initiating `$client` object. It will return us our required token & all other information like status, control code.

Sample Code Example:
```
$initializeAuthReq = (new SmartidInitAuthRequestBuilder)
  ->withCode('50001018865')
  ->withCountry('LT')
  ->withMessage('any message')
  ->withPeps(true)
  ->withsanctions(true)
  ->createRequest();
$authResponse = $client->postRequest($initializeAuthReq);
```

We can also convert this json response to array using `$responseArray = $response->toArray();`
& can collect token like below example

```
$responseArray = $authResponse->toArray();
$token = $responseArray['token'];
```

[More detail about this end point](/api-references/smartId/apiSmartidInitAuth.html)

### Upload Document
After that, we need to initiate a request builder using DocumentUploadRequestBuilder class,
we should pass required body parameters with it & then we will create a request for uploading document.

Sample Code Example:
```
use AppBundle\GatewaySDKPhp\RequestBuilder\DocumentUploadRequestBuilder;
use AppBundle\GatewaySDKPhp\RequestBuilder\Partials\FileUpload;
use AppBundle\GatewaySDKPhp\RequestBuilder\Partials\Signer;

$filePath = __DIR__ . "demo.pdf";

$requestBuilder = (new DocumentUploadRequestBuilder)
    ->withAccessToken(ACCESS_TOKEN)
    ->withAccess('public')
    ->withFile(
        (new FileUpload)->setFileName(basename($filePath))->setContent(base64_encode(file_get_contents($filePath)))
    )
    ->withSigners([
        (new Signer)->setName('Tex')->setSurName('Ryta')->setEmail('tex.ryta@domain.com')->setNoEmail(false),
        (new Signer)->setName('John')->setSurName('Quil')->setEmail('john.quil@domain.com')->setNoEmail(false),
    ])
    ->createRequest();
```

Then we will post request using $client & pass this $requestBuilder as a parameter like previous endpoint.
It will return us a json response with success or error messages.

```
$response = $client->postRequest($requestBuilder);
```
[More Detail about this endpoint](/api-references/document/apiDocumentUpload.html)

### Sign Document
Next we can try to sign our document quite easily. Here we have defined another RequestBuilder
for initialize signing a document named SmartidInitSigningRequestBuilder.
We will use this class for starting signing process. We will create a request & post it using Client like all other endpoint.

Sample Code Example:
```
$filePath = __DIR__ . '/demo.pdf';

$initializeSignReq = (new SmartidInitSigningRequestBuilder)
  ->withType('pdf')
  ->withCountry('LT')
  ->withMessage('any message')
  ->withCode('50001018865')
  ->withSignaturePosition('auto')
  ->withSignaturePage('last_page')
  ->withCertificateLevel('QUALIFIED')
  ->withPeps(true)
  ->withsanctions(true)
  ->withPdf(
    (new Files)->setFiles([
      (new FileUpload)->setName(basename($filePath))->setContent(base64_encode(file_get_contents($filePath)))
    ])
  )
  ->createRequest();
$signingResponse = $client->postRequest($initializeSignReq);
```

Although we have a lot of options which we can define, but only few of them are mandatory like
access_token, type, country & actual file.
Using our system, you can sign different types of document (pdf, asice, adoc etc)

[More Detail about this endpoint](/api-references/smartId/apiSmartidInitSigning.html)

### Validate Document
After signing a document, you may want to validate it. Using this endpoint, you can do it in no time. We have kept all the process same for each endpoint.
So you need to create a RequestBuilder using DocumentValidationRequestBuilder, then will create a request using it & will post request using client.

Sample Code Example:
```
$documentId = 'c66cf14e-f763-9757-3b83-e5e28126a6df';

$validationReq = (new DocumentValidationRequestBuilder)
  ->withDocumentId($documentId)
  ->createRequest();
$validationRes = $client->postRequest($validationReq);
```
You will get the unique document id when you will upload document & this is the only mandatory field for this request.

[More Detail about this endpoint](/api-references/document/apiDocumentValidation.html)

### Download Document
After completing all of these processes, you can download your document for preserving it locally & this endpoint will help you for doing it.
Again you need to initiate a RequestBuilder named DocumentDownloadRequestBuilder, then create a request using it
& at last, post that request using Client object.

Sample Code Example:
```
$downloadReq = (new DocumentDownloadRequestBuilder)
  ->withDocumentId($documentId)
  ->createRequest();

$downloadRes = $client->postRequest($downloadReq);
```

## Want to know more
We have shown the common flow of execution from our endpoint list. There are many more options which can be useful for you. Please check below list too.
1. You can also remove document, invite signer, can check status.
Please [check here](/api-references/document/) for more details about all of these endpoints.
2. If you specifically want to know about mobile ID related endpoint, then [click here](/api-references/mobileId/)
3. If you need any other options for smart ID, then [click here](/api-references/smartId/)








