---
title: "Listing Buckets (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-php-sdk"
---

A bucket is a container for storing objects. This article presents sample code for listing buckets.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

You can use TosClient\-\>listBuckets to list buckets. This interface lists buckets across all regions. The following is sample code:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $output = $client->listBuckets();
   
    echo $output->getRequestId() . PHP_EOL;
    foreach ($output->getBuckets() as $bucket) {
        echo $bucket->getName() . PHP_EOL;
        echo $bucket->getLocation() . PHP_EOL;
        echo $bucket->getCreationDate() . PHP_EOL;
    }
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
