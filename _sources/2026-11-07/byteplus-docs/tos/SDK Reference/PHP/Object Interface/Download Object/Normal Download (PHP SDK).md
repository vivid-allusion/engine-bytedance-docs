---
title: "Normal Download (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-php-sdk"
---

The normal download also uses Psr\ Http\ Message\ StreamInterface as the data source of the object. This article introduces the sample code of the normal download.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can get the data source of the downloaded object through TosClient\- \> getObject. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\GetObjectInput;
use GuzzleHttp\Psr7\Utils;

$output = null;
$file = null;
try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    // Download to memory
    $input = new GetObjectInput('bucket-test', 'key-test');
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
    $output->getContent()->close();
    
    // Download to local file.
    $file = fopen('local_file_path', 'w');
    $input = new GetObjectInput('bucket-test',  'key-test');
    $output = $client->getObject($input);
    echo $output->getRequestId() . PHP_EOL;
    // Stream writing to a local file.
    Utils::copyToStream(Utils::streamFor($output->getContent()), Utils::streamFor($file));
    
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
    if (is_resource($file)) {
        fclose($file);
    }
}
```
