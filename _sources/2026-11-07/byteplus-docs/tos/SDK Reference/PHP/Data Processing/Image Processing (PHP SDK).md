---
title: "Image Processing (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Image-processing-php-sdk"
---

TOS supports processing of stored images, including operations such as image resizing, image cropping, image watermarking, and format conversion. This document describes how to perform basic image processing using the TOS PHP SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The original image must be in the JPG, PNG, BMP, GIF, WEBP, or TIFF format.

* The original image size must be 20 MB or smaller.

* The original image can have a width and height of up to 30,000 pixels, for a total of up to 250 million pixels. However, the width and height cannot exceed 4,096 pixels for the rotate operation.

* The resized image can have a width and height of up to 16,384 pixels, for a total of 16,777,216 pixels.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to set the image width to 100px and subsequently download the image to the local device.

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
    
    $input->setProcess('image/resize,w_100');
    
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

For a detailed introduction to image processing, please refer to [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2).
