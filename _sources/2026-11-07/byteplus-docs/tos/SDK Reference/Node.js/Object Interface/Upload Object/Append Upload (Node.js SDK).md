---
title: "Append Upload (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-node-js-sdk"
---

The appendObject interface is used to append write objects. Append writing refers to appending content to the end of an uploaded object. This interface can only be used for objects of type Appendable. Objects created by direct upload and sharded upload are of type Normal.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You must have the `tos: PutObject`permission before appending an object, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* When uploading an object, the object name must meet certain specifications. For details, see [Common Concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage. The internal partition stores object index data. In order to scale out the maximum throughput when uploading and downloading objects, and reduce the probability of hotspot partitions, please avoid using lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. In the case of multiple versions of the bucket, the original object will be retained and a new version number will be generated to identify the newly uploaded object.

* The additional upload object does not support the Chunk\-Encoded request method. When you add the upload network stream, please iterate to obtain the data and then add the upload.


<span id=".6ZmQ5Yi26K-05piO"></span>
## Restriction statement

When using the appendObject interface, the size limits for objects are described as follows:


* The size of the appended object cannot be greater than 5GiB.

* The object created by appendObject is overridden and the object type is changed from Appendable to Normal. On the contrary, objects uploaded through putObject do not support append write operations.

* The object created by appendObject does not support copying.

* The appendObject interface cannot be used if the object type is low\-frequency storage or archive flashback storage.

* You cannot use the appendObject interface if your bucket is in a state where multiversion control is enabled or suspended.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id="d983345d"></span>
### **Append upload**

The following code is used to append the character stream to the target bucket.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import https from 'https';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    const objectName = 'append-example.txt';

    // First Addition
    const appendResult = await client.appendObject({
      bucket: bucketName,
      key: objectName,
      offset: 0,
      body: Buffer.from('your append object value.'),
    });
    console.log('appendResult', appendResult);

    // Upload additional streaming
    const req = https.get('https://www.byteplus.com/en/');
    const res = await new Promise((resolve) => req.on('response', resolve));
    await client.appendObject({
      bucket: bucketName,
      key: objectName,
      offset: appendResult.data.nextAppendOffset,
      body: res,
      contentLength: +res.headers['content-length'],
    });

    // The size of the query object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    // object size:
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

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

main();
```


<span id="95c8c850"></span>
### **Configure progress bar**

When adding upload, you can accept the upload progress through the `dataTransferStatusChange`parameter. The code example is as follows.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import https from 'https';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    const objectName = 'append-example.txt';
    const rateLimit1M = 1024 * 1024;

    // First installment
    const appendResult = await client.appendObject({
      bucket: bucketName,
      key: objectName,
      offset: 0,
      body: Buffer.from('your append object value.'),
    });
    console.log('appendResult', appendResult);

    // Upload additional network stream.
    const req = https.get('https://www.byteplus.com/en/');
    const res = await new Promise((resolve) => req.on('response', resolve));
    await client.appendObject({
      bucket: bucketName,
      key: objectName,
      offset: appendResult.data.nextAppendOffset,
      body: res,
      contentLength: +res.headers['content-length'],
      // Setting up a callback function to monitor upload progress through custom means.
      dataTransferStatusChange: (event) => {
        if (event.type === DataTransferType.Started) {
          console.log('Data Transfer Started');
        } else if (event.type === DataTransferType.Rw) {
          const percent = ((event.consumedBytes / event.totalBytes) * 100).toFixed(2);
          console.log(`Once Read:${event.rwOnceBytes},ConsumerBytes/TotalBytes: ${event.consumedBytes}/${event.totalBytes},${percent}%`);
        } else if (event.type === DataTransferType.Succeed) {
          const percent = ((event.consumedBytes / event.totalBytes) * 100).toFixed(2);
          console.log(`Data Transfer Succeed, ConsumerBytes/TotalBytes:${event.consumedBytes}/${event.totalBytes},${percent}%`);
        } else if (event.type === DataTransferType.Failed) {
          console.log('Data Transfer Failed');
        }
      },
    });

    // The size of the query object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    // object size:
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

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

main();
```


<span id="7c5ea139"></span>
### **Configure client side speed limit**

When adding an upload, you can use the `rateLimiter`parameter on the client side to limit the bandwidth occupied by the uploaded data. The code is as follows.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, createDefaultRateLimiter, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import https from 'https';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    const objectName = 'append-example.txt';
    const rateLimit1M = 1024 * 1024;

    // First addition.
    const appendResult = await client.appendObject({
      bucket: bucketName,
      key: objectName,
      offset: 0,
      body: Buffer.from('your append object value.'),
    });
    console.log('appendResult', appendResult);

    // Additional upload of network stream
    const req = https.get('https://www.byteplus.com/en/');
    const res = await new Promise((resolve) => req.on('response', resolve));
    await client.appendObject({
      bucket: bucketName,
      key: objectName,
      offset: appendResult.data.nextAppendOffset,
      body: res,
      contentLength: +res.headers['content-length'],
      // Set up a callback function to monitor the upload progress through custom means.
      dataTransferStatusChange: (event) => {
        if (event.type === DataTransferType.Started) {
          console.log('Data Transfer Started');
        } else if (event.type === DataTransferType.Rw) {
          const percent = ((event.consumedBytes / event.totalBytes) * 100).toFixed(2);
          console.log(`Once Read:${event.rwOnceBytes},ConsumerBytes/TotalBytes: ${event.consumedBytes}/${event.totalBytes},${percent}%`);
        } else if (event.type === DataTransferType.Succeed) {
          const percent = ((event.consumedBytes / event.totalBytes) * 100).toFixed(2);
          console.log(`Data Transfer Succeed, ConsumerBytes/TotalBytes:${event.consumedBytes}/${event.totalBytes},${percent}%`);
        } else if (event.type === DataTransferType.Failed) {
          console.log('Data Transfer Failed');
        }
      },
      // Limit the upload speed to 1M/s on the client side while uploading the object.
      rateLimiter: createDefaultRateLimiter(rateLimit1M, rateLimit1M),
    });

    // The size of the query object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    // object size:
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

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

main();
```


<span id="735894dd"></span>
## **Related documentation**

For additional uploaded API documentation, see [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
