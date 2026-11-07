---
title: "Append Upload (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-php-sdk"
---

Append upload can achieve the function of appending data content to the same object. This article describes sample code for append uploads.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

When appending uploads, the size limits for objects are described as follows:


* The size of each additional upload cannot be less than 128KiB, and the size of the appended object cannot be greater than 5GiB.

* For objects created by append upload, a normal upload operation occurs, the object is overwritten and the object type changes.

* Objects created with normal uploads do not support append uploads.

* Objects created by append upload do not support copying.

* If your bucket is in a state where multi\-version functionality is enabled or suspended, or if the bucket type is low\-frequency storage, you cannot create objects by append upload.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can add upload through TosClient\- \> appendObject. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\AppendObjectInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    // Upload string
    $content = 'hello world'
    $input = new AppendObjectInput('bucket-test', 'key-test');
    // Set object ACL, only valid for the first append upload
    $input->setACL(Enum::ACLPublicRead);
    // Set object StorageClass, only valid for the first append upload
    $input->setStorageClass(Enum::StorageClassStandard);
    // Set object custom metadata, only valid for the first append upload
    $input->setMeta(['aaa' => 'bbb', 'Chinese Key' => 'Chinese Value']);
    // Set object Content-Type, only valid for the first append upload
    $input->setContentType('text/plain');
    
    // The size of each incrementally uploaded data cannot be smaller than 128 KB. Here, a long string is constructed in memory.
    $content = '';
    for ($i = 0; $i < 20000; $i++) {
        $content .= uniqid();
    }
    $input->setContent($content);
    
    $output = $client->appendObject($input);
    echo $output->getRequestId() . PHP_EOL;
    
    // The starting position for the next additional upload.
    $nextAppendOffset = $output->getNextAppendOffset();
    
    $input->setOffset($nextAppendOffset);
    $content2 = '';
    for ($i = 0; $i < 20000; $i++) {
        $content2 .= uniqid();
    }
    $input->setContent($content2);
    
    $output = $client->appendObject($input);
    echo $output->getRequestId() . PHP_EOL;
    echo $output->getNextAppendOffset() . PHP_EOL;
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
