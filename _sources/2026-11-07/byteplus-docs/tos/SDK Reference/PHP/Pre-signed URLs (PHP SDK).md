---
title: "Pre-signed URLs (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Presigned-url-php-sdk"
---

You can generate a pre\-signed URL using TosClient\-\>preSignedURL, and then use the generated pre\-signed URL to directly send HTTP or HTTPS requests to access TOS services, enabling operations such as uploading and downloading objects.

<span id=".5L2_55So6aKE562-5ZCNLXVybC3kuIrkvKDlr7nosaE="></span>
## Uploading Objects Using Pre\-Signed URLs

When uploading an object using a pre\-signed URL, you must specify the request method as `Enum::HttpMethodPut`. The following is sample code:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use GuzzleHttp\Client;
use Tos\TosClient;
use Tos\Model\PreSignedURLInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    
    $input = new PreSignedURLInput(Enum::HttpMethodPut,  'bucket-test',  'key-test');
    $input->setExpires(3600);
    $output = $client->preSignedURL($input);
    echo $output->getSignedUrl() . PHP_EOL;
    echo var_export($output->getSignedHeader()) . PHP_EOL;
    
    $httpClient = new Client(
        [
            'timeout' => 10,
            'allow_redirects' => false,
            'http_errors' => false,
        ]
    );
    
    $output = $httpClient->put($output->getSignedUrl(), ['headers' => $output->getSignedHeader(), 'body' => 'hello world']);
    echo $output->getStatusCode() . PHP_EOL;
    $output->getBody()->close();

} catch (\RuntimeException $ex) {
    echo $ex->getMessage() . PHP_EOL;
}
```


<span id=".5L2_55So6aKE562-5ZCNLXVybC3kuIvovb3lr7nosaE="></span>
## Downloading Objects Using Pre\-Signed URLs

When downloading an object using a pre\-signed URL, you must specify the request method as `Enum::HttpMethodGet`. The following is sample code:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use GuzzleHttp\Client;
use Tos\TosClient;
use Tos\Model\PreSignedURLInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    
    $input = new PreSignedURLInput(Enum::HttpMethodGet,  'bucket-test',  'key-test');
    $input->setExpires(3600);
    $output = $client->preSignedURL($input);
    echo $output->getSignedUrl() . PHP_EOL;
    echo var_export($output->getSignedHeader()) . PHP_EOL;
    
    $httpClient = new Client(
        [
            'timeout' => 10,
            'allow_redirects' => false,
            'http_errors' => false,
        ]
    );
    
    $output = $httpClient->get($output->getSignedUrl(), ['headers' => $output->getSignedHeader(), 'stream' => true]);
    echo $output->getStatusCode() . PHP_EOL;
    echo $output->getBody()->getContents() . PHP_EOL;
    $output->getBody()->close();

} catch (\RuntimeException $ex) {
    echo $ex->getMessage() . PHP_EOL;
}
```


<span id=".55Sf5oiQ5Zu-54mH6L2s56CBLeinhumikeaIquW4p-eahOmihOetvuWQjS11cmw="></span>
## Generate Pre\-Signed URLs for Image Transcoding and Video Frame Extraction

When downloading an object using a pre\-signed URL, you can additionally include the `x-tos-process` parameter in the request, which indicates that image transcoding or video frame extraction will be performed. The following is sample code:

```php
<?php

require_once __DIR__  .  '/autoload.php';

use GuzzleHttp\Client;
use Tos\TosClient;
use Tos\Model\PreSignedURLInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    
    $input = new PreSignedURLInput(Enum::HttpMethodGet,  'bucket-test',  'key-test');
    $input->setExpires(3600);
    $input->setQuery([
        'x-tos-process' => 'image/info'
    ]);
    $output = $client->preSignedURL($input);
    echo $output->getSignedUrl() . PHP_EOL; 

} catch (\RuntimeException $ex) {
    echo $ex->getMessage() . PHP_EOL;
}
```
