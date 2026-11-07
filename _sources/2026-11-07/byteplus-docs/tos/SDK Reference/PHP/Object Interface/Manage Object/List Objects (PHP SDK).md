---
title: "List Objects (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-php-sdk"
---

This article describes sample code that enumerates objects and multiversion objects.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can enumerate objects and enumerate multi\-version objects through TosClient\- \> listObjects and TosClient\- \> listObjectVersions, respectively. The example code is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\ListObjectsInput;
use Tos\Model\ListObjectVersionsInput;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
     
    // List objects
    $input = new ListObjectsInput('bucket-test');
    // Set the maximum number of objects to be returned in one list operation, maximum value is 1000
    $input->setMaxKeys(100);
    // Set the prefix of the objects to be listed
    $input->setPrefix('prefix');
    // Set the starting position of the objects to be listed
    $input->setMarker('');
    // Set the delimiter of the objects to be listed, always set to '/' when simulating listing directories.
    $input->setDelimiter('/');
    $output = $client->listObjects($input);
   
    echo $output->getRequestId() . PHP_EOL;
    // Get list of objects
    foreach ($output->getContents() as $content) {
        echo $content->getKey() . PHP_EOL;
        echo $content->getSize() . PHP_EOL;
        echo $content->getETag() . PHP_EOL;
    }
    // Get Common Prefix
    foreach ($output->getCommonPrefixes() as $commonPrefix) {
        echo $commonPrefix->getPrefix() . PHP_EOL;
    }
    
    // Get the starting position for the next enumeration.
    echo $output->getNextMarker() . PHP_EOL;
    
    // List multiple versions of objects
    $input = new ListObjectVersionsInput('bucket-test');
    // Set the starting position for listing multiple versions of objects
    $input->setKeyMarker('');
    $input->setVersionIDMarker('');
    // Set the delimiter for listing objects, which is fixed as '/'
    $input->setDelimiter('/');
    $output = $client->listObjectVersions($input);
    echo $output->getRequestId() . PHP_EOL;
    
    // Get a list of multiple version objects.
    foreach ($output->getVersions() as $version) {
        echo $version->getKey() . PHP_EOL;
        echo $version->getVersionID() . PHP_EOL;
        echo $version->getSize() . PHP_EOL;
        echo $version->getETag() . PHP_EOL;
    }
    
    // Get the list of delete markers.
    foreach ($output->getDeleteMarkers() as $deleteMarker) {
        echo $deleteMarker->getKey() . PHP_EOL;
        echo $deleteMarker->getVersionID() . PHP_EOL;
    }
    
    // Get Common Prefix
    foreach ($output->getCommonPrefixes() as $commonPrefix) {
        echo $commonPrefix->getPrefix() . PHP_EOL;
    }
    // Get the starting position for the next enumeration.
    echo $output->getNextKeyMarker() . PHP_EOL;
    echo $output->getNextVersionIDMarker() . PHP_EOL;
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
