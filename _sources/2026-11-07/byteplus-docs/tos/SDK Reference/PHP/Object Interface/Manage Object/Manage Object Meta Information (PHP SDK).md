---
title: "Manage Object Meta Information (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-meta-information-php-sdk"
---

Object meta\-information is a description of an object's attributes, including HTTP headers and user\-defined metadata. This article describes sample code for setting up and getting object meta information.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can set and get object metadata through TosClient\- \> setObjectMeta and TosClient\- \> headObject, respectively. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\SetObjectMetaInput;
use Tos\Model\HeadObjectInput;
use Tos\Model\Enum;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
    
    // Set object metadata.
    $input = new SetObjectMetaInput('bucket-test',  'key-test');
    $input->setContentDisposition('test-disposition-new');
    // Set HTTP standard properties
    $expires = time() + 7200;
    $input->setExpires($expires);
    $input->setContentEncoding('test-encoding-new');
    $input->setContentLanguage('test-language-new');
    $input->setContentType('text/plain-new');
    // Set user-defined metadata.
    $input->setMeta(['aaa' => 'bbb', 'Chinese Key' => 'Chinese Value']);
    $output = $client->setObjectMeta($input);
    echo $output->getRequestId() . PHP_EOL;
    
    // Retrieve object metadata
    $output = $client->headObject(new HeadObjectInput('bucket-test',  'key-test'));
    echo $output->getRequestId() . PHP_EOL;
    // Retrieve HTTP standard attributes
    echo $output->getExpires() . PHP_EOL;
    echo $output->getContentEncoding() . PHP_EOL;
    echo $output->getContentLanguage() . PHP_EOL;
    echo $output->getContentType() . PHP_EOL;
    // Retrieve user-defined metadata
    foreach ($output->getMeta() as $k => $v) {
        echo $k . '=' . $v . PHP_EOL;
    }
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
