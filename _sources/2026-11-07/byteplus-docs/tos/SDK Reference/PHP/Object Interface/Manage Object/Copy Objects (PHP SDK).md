---
title: "Copy Objects (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Copy-objects-php-sdk"
---

This article describes sample code related to copying objects.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can copy objects through TosClient\- \> copyObject. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\CopyObjectInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    $input = new CopyObjectInput('bucket-test',  'key-test',  'src-bucket',  'src-key');
    // Set the ACL of the target object
    $input->setACL(Enum::ACLPublicRead);
    // Set the storage class of the target object
    $input->setStorageClass(Enum::StorageClassIa);
    // Set the metadata directive to overwrite the metadata of the target object during replication. Only when this parameter is set, the metadata of the target object can be overwritten. Otherwise, the metadata of the target object will be inherited directly from the source object.
    $input->setMetadataDirective(Enum::MetadataDirectiveReplace);
    // Set the user-defined metadata of the target object
    $input->setMeta(['aaa' => 'bbb', 'Chinese Key' => 'Chinese Value']);
    // Set the HTTP standard properties of the target object
    $input->setContentDisposition('test-disposition');
    $input->setExpires(time() + 3600);
    $input->setContentEncoding('test-encoding');
    $input->setContentLanguage('test-language');
    $input->setContentType('text/plain');
    
    $output = $client->copyObject($input);
    echo $output->getRequestId() . PHP_EOL;
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
