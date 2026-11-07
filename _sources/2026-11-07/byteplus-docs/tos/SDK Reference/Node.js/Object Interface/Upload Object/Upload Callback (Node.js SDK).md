---
title: "Upload Callback (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback-node-js-sdk"
---

Upload callback means that the client side carries the callback (Callback) parameter when the request is made. After the upload is completed, the server level sends a synchronized POST callback request to the third\-party app server specified in CallBack. After the server confirms acceptance and returns the result, all the results are returned to the client side.

<span id="9b4cf5b9"></span>
## Sample code

<span id="d5de9160"></span>
### Normal upload realizes upload callback

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

function handleError(error) {
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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const callbackUrl = '*** Provide your callback url ***';
    const objectKey = '*** Provide your object key ***';

    // Set upload callback parameters
    // The callback parameter can be set according to the requirement
    const callback = `
    {
      "callbackUrl" : "${callbackUrl}", 
      "callbackBody" : ${'"{\\"bucket\\": ${bucket}, \\"object\\": ${object}, \\"key1\\": ${x:key1}}"'}, 
      "callbackBodyType" : "application/json"                
    }`;
    // Configure related variable parameters.
    const callbackVar = `
    {
      "x:key1" : "ceshi"
    }`;
    const { requestId: putObjectRequestId } = await client.putObject({
      bucket: bucketName,
      key: objectKey,
      body: Buffer.from('object content'),
      callback: Buffer.from(callback).toString('base64'),
      callbackVar: Buffer.from(callbackVar).toString('base64'),
    });
    console.log('putObject Request ID: ', putObjectRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="04b3c44f"></span>
### Shard upload to achieve upload callback

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import fsp from 'fs/promises';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

function handleError(error) {
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
    // The multipartExample file in the local example_dir folder.
    const filePath = './example_dir/multipartExample';
    const callbackUrl = '*** Provide your callback url ***';
    const objectKey = '*** Provide your object key ***';

    // Set upload callback parameters
    // The callback parameters can be set according to the requirements.
    const callback = `
    {
      "callbackUrl" : "${callbackUrl}", 
      "callbackBody" : ${'"{\\"bucket\\": ${bucket}, \\"object\\": ${object}, \\"key1\\": ${x:key1}}"'}, 
      "callbackBodyType" : "application/json"                
    }`;
    // Configure related variable parameters.
    const callbackVar = `
    {
      "x:key1" : "ceshi"
    }`;
    // Get Upload Task ID
    const {
      data: { UploadId },
    } = await client.createMultipartUpload({
      bucket: bucketName,
      key: objectKey,
    });
    console.log('UploadId', UploadId);

    // Get local file information and prepare for segmentation
    const stats = await fsp.stat(filePath);
    // Total file size
    const totalSize = stats.size;

    let offset = 0;
    let partNumber = 1;
    const partsInfo = [];
    // Specify chunk size during upload.
    const partSize = 5 * 1024 * 1024;

    while (offset < totalSize) {
      const uploadResult = await client.uploadPartFromFile({
        bucket: bucketName,
        key: objectKey,
        filePath,
        partNumber,
        uploadId: UploadId,
        offset,
        partSize,
      });
      const eTag = uploadResult.data.ETag;
      console.log(`partNumber${partNumber} Etag:`, eTag);
      partsInfo.push({
        partNumber,
        eTag,
      });
      partNumber++;
      offset += partSize;
    }

    console.log('parts information', partsInfo);

    // Complete chunked upload.
    const { data, requestId: completeMultipartUploadRequestId } = await client.completeMultipartUpload({
      bucket: bucketName,
      key: objectKey,
      uploadId: UploadId,
      parts: partsInfo,
      callback: Buffer.from(callback).toString('base64'),
      callbackVar: Buffer.from(callbackVar).toString('base64'),
    });

    console.log('completeMultipartUpload Request ID: ', completeMultipartUploadRequestId);
    console.log('result data:', data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


&nbsp;
