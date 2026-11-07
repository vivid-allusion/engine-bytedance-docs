---
title: "Quick Start Guide (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-php-sdk"
---

This chapter describes how to perform common operations using the TOS PHP SDK, such as creating buckets, uploading, downloading, deleting objects, and more.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before sending HTTP or HTTPS requests to TOS, you must first create a TOS client (that is, instantiate a TosClient). For detailed instructions, see [Client Initialization](https://docs.byteplus.com/docs/tos/Initializing-the-client-side-php-sdk).

<span id=".5a6i5oi356uv6YCa55So56S65L6L"></span>
## General Client Example

After completing an API operation using TosClient, the absence of any exceptions indicates that the operation was successful. If an exception is thrown, the operation has failed; in this case, detailed error information should be obtained from [SDK custom exceptions](https://docs.byteplus.com/docs/tos/Exception-handling-php-sdk#sdk-%E8%87%AA%E5%AE%9A%E4%B9%89%E5%BC%82%E5%B8%B8). The following code demonstrates the general usage of TosClient.

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\PutObjectInput;

$region = 'your region';
$endpoint = 'your endpoint';
$ak = getenv('TOS_ACCESS_KEY'); 
$sk = getenv('TOS_SECRET_KEY'); 
$bucket = 'bucket-test';
$key = 'key-test';
$data = 'hello world';

try {
    $client = new TosClient([
        'region' => $region,
        'endpoint' => $endpoint,
        'ak' => $ak,
        'sk' => $sk,
    ]);
       
    $input = new PutObjectInput($bucket, $key, $data);
    $output = $client->putObject($input);
    echo 'put object succeed, request id: ' . $output->getRequestId() . PHP_EOL;
    echo $output->getETag() . PHP_EOL;
    echo $output->getHashCrc64ecma() . PHP_EOL;
} catch (TosClientException $ex) {
    echo 'put object failed, message: ' . $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo 'put object failed, code: ' . $ex->getErrorCode() . PHP_EOL;
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getMessage() . PHP_EOL;
} catch (\Exception $ex) {
    echo 'put object unexpected exception, message: ' . $ex->getMessage() . PHP_EOL;
}
```


<span id=".5Yib5bu65qG2"></span>
## Create Bucket

A bucket in TOS serves as the global namespace, functioning as a data container and the root directory of the file system, and is capable of storing multiple objects. The following code demonstrates how to create a new bucket.

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\CreateBucketInput;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new CreateBucketInput('bucket-test');
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


<span id=".5LiK5Lyg5a-56LGh"></span>
## Uploads an object.

The following code demonstrates how to upload an object to a TOS bucket.

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\PutObjectInput;

try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new PutObjectInput('bucket-test',  'key-test',  'hello world');
    $output = $client->putObject($input);

    echo $output->getRequestId() . PHP_EOL;
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```


<span id=".5LiL6L295a-56LGh"></span>
## Download Object

The following code demonstrates how to download a specified object from a TOS bucket and read its data.

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\GetObjectInput;

$output = null;
try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new GetObjectInput('bucket-test',  'key-test');
    $output = $client->getObject($input);

    echo $output->getRequestId() . PHP_EOL;
    echo $output->getContent().getContents(). PHP_EOL;
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
} finally {
    if ($output) {
        $output->getContent()->close();
    }
}
```


<span id=".5YiX5Li-5a-56LGh"></span>
## Enumeration of Objects

After completing a series of object upload operations, it may be necessary to review which objects are contained in the bucket. The following code demonstrates how to list objects in a specified bucket.

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\ListObjectsInput;

$output = null;
try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new ListObjectsInput('bucket-test');
    $output = $client->listObjects($input);

    echo $output->getRequestId() . PHP_EOL;
    foreach ($output->getContents() as $content) {
        echo $content->getKey() . PHP_EOL;
        echo $content->getETag() . PHP_EOL;
    }
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
} finally {
    if ($output) {
        $output->getContent()->close();
    }
}
```


<span id=".5Yig6Zmk5a-56LGh"></span>
## When you delete an object

The following code demonstrates how to delete a specified object.

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\DeleteObjectInput;

$output = null;
try {
    $client = new TosClient([
        'region' => 'your region',
        'endpoint' => 'your endpoint',
        'ak' => getenv('TOS_ACCESS_KEY'),
        'sk' => getenv('TOS_SECRET_KEY'),
    ]);
       
    $input = new DeleteObjectInput('bucket-test',  'key-test');
    $output = $client->deleteObject($input);

    echo $output->getRequestId() . PHP_EOL;
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
}
```
