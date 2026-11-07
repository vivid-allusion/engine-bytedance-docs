---
title: "Standard Upload (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-node-js-sdk"
---

A standard upload refers to the process of uploading a single object using the **putObject ** method. This method supports four types of input: string (character stream), bytes (byte stream), network stream, and local file.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before uploading an object, you must have the `tos: PutObject` permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* When uploading an object, the object name must meet certain specifications. For details, see [Common concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage, which stores object index data in internal partition. To scale out the maximum throughput when you upload and download objects and reduce the probability of hotspot partitions, please avoid lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. If versioning is enabled in your bucket, the original object is preserved and a new version number is generated to identify the newly uploaded object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5LiK5Lyg5a2X56ym5Liy"></span>
### Upload a string

The following sample code uploads a string as the `example.txt` object to the `example_dir` directory in TOS using the **putObject** API.

```javascript
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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    const objectName = 'example_dir/example.txt';
    // Upload object
    await client.putObject({
      bucket: bucketName,
      key: objectName,
      // Upload the string "Hello TOS" to the example.txt file in the specified example_dir directory.
      body: Buffer.from('Hello TOS'),
    });

    // Query the size of the recently uploaded object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    // object size: 9
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="ba8dd369"></span>
### **Upload a network stream**

The following sample code uploads a network stream as the `example.txt` object to the `example_dir` directory in TOS using the **putObject** API.

```JavaScript
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
    const objectName = 'example_dir/example.txt';
    // Get data from a network stream.
    const req = https.get('https://www.byteplus.com/en/');
    const res = await new Promise((resolve) => req.on('response', resolve));
    // Upload object
    await client.putObject({
      bucket: bucketName,
      key: objectName,
      body: res,
    });

    // Query the size of the just uploaded object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="e1b6faec"></span>
### **Upload a local file as a stream**

The following sample code uses the **putObject** API to upload a local file as a stream and save it as the `example.txt` object to the `example_dir` directory in TOS.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import fs from 'fs';

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
    const objectName = 'example_dir/example.txt';
    // Read local file data.
    const body = fs.createReadStream('./example.txt');
    // Upload object
    await client.putObject({
      bucket: bucketName,
      key: objectName,
      body,
    });

    // Query the size of the just uploaded object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5LuO5pys5Zyw5paH5Lu25LiK5Lyg"></span>
### Upload a local file directly

The following sample code uses the **putObjectFromFile** API to upload a local file directly as the `example.txt` object to the `example_dir` directory in TOS.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import fs from 'fs';

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
    const objectName = 'example_dir/example.txt';

    // Directly upload the file using the file path.
    await client.putObjectFromFile({
      bucket: bucketName,
      key: objectName,
      filePath: './example.txt',
    });

    // Query the size of the just uploaded object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="ea336f0c"></span>
### **Set object metadata when uploading**

The following sample code uses the **putObject** API to upload a string as the `example.txt` object to the `example_dir` directory. During the upload process, the storage type is set to Infrequent Access Storage, the access control list (ACL) is set to private, and the metadata of the uploaded object is set.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { ACLType, StorageClassType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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
    const objectName = 'example_dir/example.txt';
    // Upload object
    await client.putObject({
      bucket: bucketName,
      key: objectName,
      // Upload the string "Hello TOS" to the example.txt file in the specified example_dir directory
      body: Buffer.from('Hello TOS'),
      // Specify the storage class as Infrequent Access storage
      storageClass: StorageClassType.StorageClassIa,
      // Specify the object permission as private
      acl: ACLType.ACLPrivate,
      // User-defined metadata information
      meta: {
        key: 'value',
      },
    });

    // Query the size of the just uploaded object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log('object size:', data['content-length']);
    console.log('storage class:', data['x-tos-storage-class']);
    console.log('x-tos-meta-key:', data['x-tos-meta-key']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="cfe9fa2c"></span>
### **Configure progress bar**

When uploading, the upload progress can be processed through the `dataTransferStatusChange` parameter. The code example is as follows.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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
    const objectName = 'example_dir/example.txt';
    // Upload object
    await client.putObject({
      bucket: bucketName,
      key: objectName,
      // Upload the string "Hello TOS" to the example.txt file in the specified example_dir directory
      body: Buffer.from('Hello TOS'),
      // Set a custom callback function to view the upload progress
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

    // Query the size of the just uploaded object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="9f1ebf0a"></span>
### **Configure client\-side rate limiting**

When uploading objects, you can use the `rateLimiter` parameter on the client side to limit the bandwidth occupied by the uploaded data, as shown below.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, TosClient, TosClientError, TosServerError, createDefaultRateLimiter } from '@volcengine/tos-sdk';

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
    const objectName = 'example_dir/example.txt';
    const rateLimit1M = 1024 * 1024;
    // Upload object
    await client.putObject({
      bucket: bucketName,
      key: objectName,
      // Upload the string "Hello TOS" to the example.txt file in the specified example_dir directory
      body: Buffer.from('Hello TOS'),
      // Upload object and limit upload speed to 1M/s on the client side
      rateLimiter: createDefaultRateLimiter(rateLimit1M, rateLimit1M),
      // Set a custom callback function to monitor the upload progress
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

    // Query the size of the just uploaded object.
    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="5776c9a0"></span>
## **Related documentation**

For API documentation on uploading objects, see [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
