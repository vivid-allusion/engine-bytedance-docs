---
title: "Range Download (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-node-js-sdk"
---

If you only need to retrieve part of the data in an object, you can use range download to download data within a specified range. This article describes range download.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before downloading an object, you must have `tos: GetObject`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* To open multiple versions of a bucket, you must have the `tos: GetObjectVersion`permission when downloading the specified version object. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* If an application downloads a large number of the same object at the same time, your access speed will be limited by TOS bandwidth and geography. It is recommended that you use CDN products to improve performance while also reducing your costs.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

**Specify Start/End Download Objects**

The following code specifies the partial data of the object in the Start/End download bucket.

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
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    // Return data.content as stream.
    const {
      data: { content },
    } = await client.getObjectV2({
      bucket: bucketName,
      key: objectName,
      rangeStart: 32,
      rangeEnd: 64,
    });

    // Get all the contents from the returned stream.
    let allContent = Buffer.from([]);
    for await (const chunk of content) {
      allContent = Buffer.concat([allContent, chunk]);
    }

    console.log('object size:', allContent.length);
    // If the object is a string of text, it can be parsed using toString.
    console.log('data string:', allContent.toString());
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="cee8d0c8"></span>
### **Configure progress bar**

When downloading, you can receive the download progress through the `dataTransferStatusChange`parameter. The code example is as follows.

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
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    // Return data.content as stream.
    const {
      data: { content },
    } = await client.getObjectV2({
      bucket: bucketName,
      key: objectName,
      rangeStart: 32,
      rangeEnd: 64,
      // Set up a callback function to view the download progress through a custom method.
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

    // Get all the contents from the returned stream.
    let allContent = Buffer.from([]);
    for await (const chunk of content) {
      allContent = Buffer.concat([allContent, chunk]);
    }

    console.log('object size:', allContent.length);
    // If the object is a string of text, it can be parsed using toString.
    console.log('data string:', allContent.toString());
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="fcc522d8"></span>
### **Configure client side speed limit**

When downloading an object, the client side can use the `rateLimiter`parameter to limit the bandwidth occupied by the downloaded data, as shown below.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, createDefaultRateLimiter, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    const rateLimit1M = 1024 * 1024;

    // Return data.content as stream.
    const {
      data: { content },
    } = await client.getObjectV2({
      bucket: bucketName,
      key: objectName,
      rangeStart: 32,
      rangeEnd: 64,
      // Set up a callback function to view the download progress through a custom method.
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
      // Download the object and limit the download speed to 1M/s on the client side.
      rateLimiter: createDefaultRateLimiter(rateLimit1M, rateLimit1M),
    });

    // Get all the contents from the returned stream.
    let allContent = Buffer.from([]);
    for await (const chunk of content) {
      allContent = Buffer.concat([allContent, chunk]);
    }

    console.log('object size:', allContent.length);
    // If the object is a string of text, it can be parsed using toString.
    console.log('data string:', allContent.toString());
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="62382451"></span>
## **Related documentation**

For API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
