---
title: "Limited Download (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-php-sdk"
---

When downloading an object, you can specify one or more qualification conditions. If the qualification conditions are met, the download will be downloaded. If the conditions are not met, throwing an exception will not trigger the download behavior. The TOS service follows the HTTP specification and provides a variety of qualifications, including If\-Match, If\-Unmodified\-Since, and so on.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can specify qualifications when downloading through GetObjectInput\- \> setIfMatch. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\GetObjectInput;

$output = null;
try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    $input = new GetObjectInput('bucket-test',  'key-test');
    // Specify If-Match
    $input->setIfMatch('object etag');
    // Specify If-None-Match
    // $input->setIfNoneMatch('none object etag');
    // Specify If-Modified-Since, pass in the timestamp in seconds
    // $input->setIfModifiedSince(time() - 3600);
    // Specify If-Unmodified-Since, pass in the timestamp in seconds
    // $input->setIfUnmodifiedSince(time() + 3600);
    $output = $client->getObject($input);
    echo $output->getRequestId() . PHP_EOL;
    // Get object length
    echo $output->getContentLength() . PHP_EOL;
    // Get object Content-Type
    echo $output->getContentType() . PHP_EOL;
    // Get object ETag
    echo $output->getETag() . PHP_EOL;
    // Get object StorageClass
    echo $output->getStorageClass() . PHP_EOL;
    // Get object CRC64
    echo $output->getHashCrc64ecma() . PHP_EOL;
    // Get object user-defined metadata
    foreach ($output->getMeta() as $k => $v) {
        echo $k . '=' . $v . PHP_EOL;
    }
    // Read the string directly.
    echo $output->getContent()->getContents() . PHP_EOL;
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
} finally {
    if($output){
        $output->getContent()->close();
    }
}
```
