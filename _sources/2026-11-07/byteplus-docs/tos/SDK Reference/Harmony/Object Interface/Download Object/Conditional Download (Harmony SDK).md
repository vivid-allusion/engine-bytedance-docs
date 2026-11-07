---
title: "Conditional Download (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-with-qualifications-harmony-sdk"
---

If you wish to set constraints when downloading an object—such as specifying the object's ETag or modification time—you can use the conditional download feature provided by the TOS Harmony SDK. The object will only be downloaded if its information meets the conditions you have specified. This article describes how to download objects under specified conditions.

<span id="fb16e5dc"></span>
## Precautions


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application performs many concurrent downloads of the same object, your access speed will be limited by TOS bandwidth and regional restrictions. It is recommended that you utilize CDN products to enhance performance while simultaneously reducing your costs. For detailed information on accessing TOS via CDN, please refer to [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).

* Different conditions can be combined; for example, both If\-Modified\-Since and If\-Unmodified\-Since can be present simultaneously, and both If\-Match and If\-None\-Match can also coexist.

* You can obtain the Etag information of an object by using the **headObject** interface of the TOS Harmony SDK.


<span id="5b8339e2"></span>
## Specification of Limiting Conditions


|Parameters |Description |
|---|---|
|If\-Match |The object is returned only if the incoming `ETag` matches the object's `ETag`; otherwise, a `412 Precondition Failed` response is returned. |
|If\-None\-Match |The object is returned only if the incoming `ETag` does not match the object's `ETag`; otherwise, `304 Not Modified` is returned. |
|If\-Modified\-Since |The object is returned only if it has been modified since the specified time; otherwise, `304 Not Modified` is returned. |
|If\-Unmodified\-Since |The object is returned only if it has not been modified since the specified time; otherwise, `412 Precondition Failed` is returned. |


<span id="534ef829"></span>
## Sample Code

The following code restricts downloads to objects that have been modified since 2024\-02\-22 18:33:00.

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
  const bucketName = 'node-sdk-test-bucket'; 
  const objectName = 'example_dir/example.txt'; 
 
  const date = new Date('2024-02-22 18:33:00');

  try {
  
    const res = await client.getObject({
      Bucket: bucketName,
      Key: objectName,
      IfModifiedSince: date,
    });

 
    res.Content.close();
  } catch (error) {
    if (error instanceof TosServerError) {
   
      if (error.StatusCode === 304) {
        console.log('Object not modify, Request ID:', error.RequestId);
      } else {
        handleError(error as Error);
      }
    }
  }

  try {

    const res = await client.getObject({
      Bucket: bucketName,
      Key: objectName,
      IfUnmodifiedSince: date,
    });
    res.Content.close();
  } catch (error) {
    if (error instanceof TosServerError) {
   
      if (error.StatusCode === 412) {
        console.log('Object modify, Request ID:', error.RequestId);
      } else {
        handleError(error as Error);
      }
    }
  }
}
main();
```


<span id="b7c82173"></span>
## **Relevant Documentation**

For API documentation on downloading objects, refer to [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
