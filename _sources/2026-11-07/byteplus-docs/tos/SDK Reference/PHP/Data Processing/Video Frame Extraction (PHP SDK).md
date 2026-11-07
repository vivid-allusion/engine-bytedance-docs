---
title: "Video Frame Extraction (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-framing-php-sdk"
---

The video frame capture function enables extraction of a single frame from a video stream at a specified time and resizes it to an image of the designated dimensions. This document describes how to perform video frame extraction using the TOS PHP SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 30,000 ms and download the resulting image to the local system.

```php
<?php

require_once __DIR__  .  '/autoload.php';

use Tos\TosClient;
use Tos\Exception\TosClientException;
use Tos\Exception\TosServerException;
use Tos\Model\HeadObjectInput;
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
    
    $input->setProcess('video/snapshot,t_30000');
    
    $output = $client->getObject($input);
    echo $output->getRequestId() . PHP_EOL;
   
    echo $output->getContent()->getContents() . PHP_EOL;
    $output->getContent()->close();
    
    
} catch (TosClientException $ex) {
    echo $ex->getMessage() . PHP_EOL;
} catch (TosServerException $ex) {
    echo $ex->getRequestId() . PHP_EOL;
    echo $ex->getStatusCode() . PHP_EOL;
    echo $ex->getErrorCode() . PHP_EOL;
} finally {
    if($output){
        $output->getContent()->close();
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to video frame extraction, please refer to [Video Frame Extraction](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).
