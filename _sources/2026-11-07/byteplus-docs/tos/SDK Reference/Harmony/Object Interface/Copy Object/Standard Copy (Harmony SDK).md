---
title: "Standard Copy (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Simple-copy-harmony-sdk"
---

The copyObject operation enables copying objects between buckets within the same region, as well as copying objects within the same bucket. When copying, you can specify new metadata or retain the metadata of the source object.

<span id="e5930708"></span>
## Precautions


* Copying files does not support cross\-region bucket\-to\-bucket copying.

* When copying objects, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you may retain all metadata (default setting) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id="4d2ff2de"></span>
## Sample Code

The following code demonstrates how to use the copyObject method to copy the source\-test object from the harmonyos\-sdk\-test\-bucket bucket to the harmonyos\-sdk\-copy\-bucket bucket, and name the copied object copy\-test.

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
    const srcBucket = 'harmonyos-sdk-test-bucket'; 
    const srcObject = 'source-test'; 
    const dstBucket = 'harmonyos-sdk-copy-bucket'; 
    const dstObject = 'copy-test'; 

    const res = await client.copyObject({
      Bucket: srcBucket,
      Key: dstObject,
      SrcBucket: srcBucket,
      SrcKey: srcObject,
      MetadataDirective: MetadataDirectiveType.MetadataDirectiveCopy,
    });
    console.log('copy result', res.ETag);
   
    const headResult = await client.headObject({
      Bucket: dstBucket,
      Key: dstObject,
    });
    console.log('headResult', headResult);

    const res2 = await client.copyObject({
      Bucket: dstBucket,
      Key: dstObject,
      SrcBucket: srcBucket,
      SrcKey: srcObject,
      MetadataDirective: MetadataDirectiveType.MetadataDirectiveReplace,
 
      SrcVersionID: StorageClassType.StorageClassIa,

      ACL: ACLType.ACLPrivate,
    });
    console.log('copy result', res2.ETag);

    const headResult2 = await client.headObject({
      Bucket: dstBucket,
      Key: dstObject,
    });
    console.log('headResult', headResult2);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="9645893d"></span>
## **Relevant Documentation**

For API documentation on standard copy operations, refer to [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
