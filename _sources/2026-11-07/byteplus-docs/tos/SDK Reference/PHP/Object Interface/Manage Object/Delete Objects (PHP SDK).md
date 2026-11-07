---
title: "Delete Objects (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-objects-php-sdk"
---

This article describes sample code for deleting individual objects and deleting objects in bulk.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can delete individual objects and delete objects in batches through TosClient\- \> deleteObject and TosClient\- \> deleteMultiObjects, respectively. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\DeleteObjectInput;
use Tos\Model\DeleteMultiObjectsInput;
use Tos\Model\ObjectTobeDeleted;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
     
    // Delete a single object.
    $input = new DeleteObjectInput('bucket-test', 'key-test');
    $output = $client->deleteObject($input);
   
    echo $output->getRequestId() . PHP_EOL;

 
    // Batch delete objects
    $objects = [];
    $objects[] = new ObjectTobeDeleted('key-test1');
    $objects[] = new ObjectTobeDeleted('key-test2');
    $input = new DeleteMultiObjectsInput('bucket-test');
    $input->setObjects($objects);
    $output = $client->deleteMultiObjects($input);
    echo $output->getRequestId() . PHP_EOL;
    
    // Get successful deletion result.
    echo 'delete succeed:' . PHP_EOL;
    foreach ($output->getDeleted() as $deleted) {
        echo $deleted->getKey() . PHP_EOL;
    }
    // Failed to retrieve deletion results.
    echo 'delete error:' . PHP_EOL;
    foreach ($output->getError() as $error) {
        echo $error->getKey() . PHP_EOL;
        echo $error->getCode() . PHP_EOL;
    }
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
