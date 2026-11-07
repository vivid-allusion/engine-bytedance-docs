---
title: "Normal Upload (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-php-sdk"
---

This article describes sample code for a normal upload object.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

Ordinary upload uses Psr\ Http\ Message\ StreamInterface as the data source of the object. You can implement ordinary upload through TosClient\- \> putObject. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\PutObjectInput;
use Tos\Model\Enum;

$file = null;
try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    // Upload string
    $content = 'hello world';
    $input = new PutObjectInput('bucket-test', 'key-test', $content);
    // Set object ACL
    $input->setACL(Enum::ACLPublicRead);
    // Set object StorageClass
    $input->setStorageClass(Enum::StorageClassStandard);
    // Set object custom metadata
    $input->setMeta(['aaa' => 'bbb', 'Chinese Key' => 'Chinese Value']);
    // Set object Content-Type
    $input->setContentType('text/plain');
    $output = $client->putObject($input);
    echo $output->getRequestId() . PHP_EOL;
    
    // Upload file stream
    $input->setKey('key-test2');
    // Assuming the local file path is local_file_path
    $file = fopen('local_file_path', 'r');
    $input->setContent($file);
    $output = $client->putObject($input);
    echo $output->getRequestId() . PHP_EOL;
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
} finally {
    if (is_resource($file)) {
        fclose($file);
    }
}
```
