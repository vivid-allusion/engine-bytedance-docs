---
title: "Creating a Bucket (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-bucket-php-sdk"
---

A Bucket (桶) is the globally unique namespace in TOS, functioning as a data container for storing Object data. The name of a newly created bucket must be unique within TOS.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

You can create a new bucket using TosClient\-\>createBucket. The following is a sample code:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\CreateBucketInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new CreateBucketInput('bucket-test');
    $input->setACL(Enum::ACLPublicRead);
    $input->setAzRedundancy(Enum::AzRedundancySingleAz);
    $input->setStorageClass(Enum::StorageClassIa);
    $output = $client->createBucket($input);

    echo $output->getRequestId() . PHP_EOL;
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
