---
title: "Scoped Download (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Range-download-harmony-sdk"
---

If you only need to download part of the data from an object, you can use range download to download data within a specified range. This article explains how to specify a range to download data from an object.

<span id="230dc5b1"></span>
## Precautions


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object many times simultaneously, your access speed will be restricted by TOS bandwidth and regional limitations. It is recommended that you use CDN products to enhance performance while also reducing your costs. For detailed information on accessing TOS via CDN, please refer to [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).


<span id="12a9b611"></span>
## Sample Code

The following code is used to specify the Start and End positions for partial data of an object in the bucket.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

function handleError(error: Error) {
  if (error instanceof TosClientError) {
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket'; 
    const objectName = 'example_dir/example.txt'; 

    const res = await client.getObject({
      Bucket: bucketName,
      Key: objectName,
      RangeStart: 32,
      RangeEnd: 64,
    });

    const str = buffer.from(res.Content.read(100)).toString()
    res.Content.close();

    console.log('object size:', str.length);

    console.log('data string:', str);
  } catch (error) {
    handleError(error);
  }
}

main();
```
