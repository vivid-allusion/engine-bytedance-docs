---
title: "Scope Download (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-php-sdk"
---

Range downloads can be used to download part of the data in an object, and large object downloads can be achieved using this feature. The principle is to split the original object into multiple shardings and download them in sequence, and generate complete data on the target side (e.g. the local file system).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

According to the HTTP Range request header specification, the specified range interval during range download satisfies the left\-closed and right\-closed rule starting from 0, such as bytes = 0\-1, which represents the first and second bytes of the downloaded object, totaling two bytes.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The example code downloaded from the scope is as follows:

```php
<?php

// Assuming the use of composer for installation.
require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\HeadObjectInput;
use Tos\Model\GetObjectInput;

$file = null;
$output = null;
try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        // Get access key from environment variables.
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);

    // Get object metadata
    $headObjectOutput = $client->headObject(new HeadObjectInput('bucket-test', 'key-test'));
    echo $headObjectOutput->getRequestId() . PHP_EOL;

    // Assuming the large file is split into 20MB portions.
    $partSize = intval(5 * 1024 * 1024);
    // Split the range of downloaded files by object size.
    $objectSize = $headObjectOutput->getContentLength();
    $partCount = intval($objectSize / $partSize);
    if ($objectSize % $partSize !== 0) {
        $partCount++;
    }

    // Assuming the downloaded large file path is local_big_file_path.
    $localBigFilePath = 'local_big_file_path';

    $file = fopen($localBigFilePath, 'w');
    // Download each shard sequentially through range download and write it to a local file.
    for ($i = 0; $i < $partCount; $i++) {
        $input = new GetObjectInput('bucket-test', 'key-test');
        // Set the starting position of the download object
        $input->setRangeStart($i * $partSize);
        // Note the range of values for RangeEnd
        if ($i === $partCount - 1) {
            // Handling the last fragment.
            $input->setRangeEnd($objectSize - 1);
        } else {
            $input->setRangeEnd(($i + 1) * $partSize - 1);
        }
        // Set the starting position for writing to a local file, usually the same as RangeStart.
        fseek($file, $partSize * $i, 0);
        $output = $client->getObject($input);
        echo $headObjectOutput->getRequestId() . PHP_EOL;

        while ($buf = $output->getContent()->read(65536)) {
            fwrite($file, $buf, strlen($buf));
        }
        $output->getContent()->close();
        echo sprintf('get object by range %d succeed', $i) . PHP_EOL;
    }
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

    if ($output) {
        $output->getContent()->close();
    }
}
```
