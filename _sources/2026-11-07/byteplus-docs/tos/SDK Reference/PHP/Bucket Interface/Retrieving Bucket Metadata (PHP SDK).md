---
title: "Retrieving Bucket Metadata (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-metadata-php-sdk"
---

A bucket is a container for storing objects. This article presents example code for retrieving bucket metadata.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

You can obtain bucket metadata using the TosClient\-\>headBucket API. This API also allows you to verify whether a bucket exists. Sample code is as follows:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\HeadBucketInput;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new HeadBucketInput('bucket-test');
    $output = $client->headBucket($input);

    echo $output->getRequestId() . PHP_EOL;
    echo $output->getRegion() . PHP_EOL;
    echo $output->getStorageClass() . PHP_EOL;
    echo $output->getAzRedundancyType() . PHP_EOL;
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    if($ex->getStatusCode() === 404){
        echo 'bucket does not exist' . PHP_EOL;
    }
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
}
```
