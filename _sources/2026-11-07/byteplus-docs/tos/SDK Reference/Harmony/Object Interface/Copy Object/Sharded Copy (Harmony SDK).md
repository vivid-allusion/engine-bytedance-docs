---
title: "Sharded Copy (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multipart-copy-harmony-sdk"
---

When the object size exceeds 5 GiB, the uploadPartCopy operation must be used to perform multipart copy.

<span id="4587537d"></span>
## Precautions


* File copying does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id="4b2083f5"></span>
## Shard Copy Procedure


1. Initialize the multipart copy task using createMultipartUpload.

2. Perform multipart copy using uploadPartCopy.

3. Merge parts using completeMultipartUpload.


<span id="4d7e976c"></span>
## Sample Code

The following code demonstrates how to use createMultipartUpload, uploadPartCopy, and completeMultipartUpload to perform a multipart copy of the source\-test object from the harmonyos\-sdk\-test\-bucket to the harmonyos\-sdk\-copy\-bucket, and assigns the copied object the name copy\-test.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

function handleError(error) {
  if (error instanceof TosClientError) {
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
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
    let res = await client.createMultipartUpload({
      Bucket: dstBucket,
      Key: dstObject,
    })
    console.log('create part: ', res.UploadId)
    const res2 = await client.headObject({
      Bucket: srcBucket,
      Key: srcObject,
    })

    console.log('srcObject content-length', res2.ContentLength);
    const totalSize = res2.ContentLength;
    const partSize = 5 * 1024 * 1024;
    let offset = 0;
    let partNumber = 1;
    const partsInfo: UploadedPart[] = [];
    while (offset < totalSize) {
      
      const uploadResult = await client.uploadPartCopy({
        Bucket: dstBucket,
        Key: dstObject,
        PartNumber: partNumber,
        UploadID: res.UploadId,
        SrcBucket: srcBucket,
        SrcKey: srcObject,
        CopySourceRangeStart: offset,
        CopySourceRangeEnd: offset + partSize - 1,
      });
      const eTag = uploadResult.ETag;
      console.log(`partNumber${partNumber} Etag:`, eTag);
      partsInfo.push(new UploadedPart(partNumber, eTag));
      partNumber++;
      offset += partSize;
    }

    const res3 = await client.completeMultipartUpload({
      Bucket: dstBucket,
      Key: dstObject,
      UploadID: res.UploadId,
      Parts: partsInfo,
    });
    console.log('result data:', res3.StatusCode);

 
    const headResult = await client.headObject({
      Bucket: dstBucket,
      Key: dstObject,
    });
    console.log('headResult: ', headResult.ContentLength);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="5d0e6918"></span>
## **Relevant Documentation**


* For API documentation on creating a multipart upload task, please refer to [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on part copy operations, refer to [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For API documentation on completing multipart uploads, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
