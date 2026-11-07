---
title: "Delete Bucket (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-php-sdk"
---

This article presents example code for deleting a bucket.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* All objects in the storage bucket have been deleted.

* All shards with incomplete merges have been deleted.

* If multiple versions of an object exist, ensure that all versions have been deleted.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

You can delete a bucket using TosClient\-\>deleteBucket. The following is a sample code:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\DeleteBucketInput;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new DeleteBucketInput('bucket-test');
    $output = $client->deleteBucket($input);

    echo $output->getRequestId() . PHP_EOL;
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
