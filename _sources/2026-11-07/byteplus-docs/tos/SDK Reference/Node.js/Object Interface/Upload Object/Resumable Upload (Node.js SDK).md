---
title: "Resumable Upload (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resumption-node-js-sdk"
---

When uploading an object to TOS using resumable upload, you can configure parameters such as part size, concurrency for uploading parts, client\-side rate limiting, and event callback functions. If a network error or program crash occurs during the upload process, the upload will resume from the last recorded checkpoint and continue with the remaining parts. You can also cancel the upload by calling the Cancel method on the cancelToken passed to the upload operation.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before uploading an object, you must have the `tos: PutObject` permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* When uploading an object, the object name must meet certain specifications. For details, see [Common Concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage. The internal partition stores object index data. In order to scale out the maximum throughput when uploading and downloading objects, and reduce the probability of hot partitions, please avoid using lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. If versioning is enabled in your bucket, the original object is preserved and a new version number is generated to identify the newly uploaded object.

* The SDK will record the uploaded status information in the `Checkpoint` file, so the program needs to have write permission to the `Checkpoint` file.

* When using resumable upload, upload progress information is recorded in a `Checkpoint` file. If a part fails to upload during the process, the upload resumes from the point recorded in the `Checkpoint` file on the next attempt. After the upload is complete, the `Checkpoint` file is deleted.

* If local files change during the upload process, all parts are re\-uploaded.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5LiK5Lyg5paH5Lu2"></span>
### Upload an object

The following code uploads an object using resumable upload.

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
    const objectName = 'example_dir/multipartExample';
    // The multipartExample file in the local example_dir folder.
    const filePath = './example_dir/multipartExample';

    const { data } = await client.uploadFile({
      bucket: bucketName,
      key: objectName,
      // Uploaded file path
      file: filePath,
      // Specify the part size during upload
      partSize: 5 * 1024 * 1024,
      // Number of concurrent part upload tasks
      taskNum: 5,
    });
    console.log('uploadFile result', data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="0e9b460a"></span>
### **Traverse a local folder and upload its contents to a bucket**

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import fsp from 'fs/promises';
import path from 'path';

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
    // Directory where the uploaded object is located
    const objectDirName = 'example_dir/';
    // Upload all files under the local example_dir folder
    const localDirPath = './example_dir/';
    const localDirAbsolutePath = path.resolve(localDirPath) + '/';

    async function walkDir(dirPath) {
      for (const dirent of await fsp.readdir(dirPath, { withFileTypes: true })) {
        const filePath = path.resolve(dirPath, dirent.name);
        if (dirent.isDirectory()) {
          walkDir(filePath);
          continue;
        }

        const { data } = await client.uploadFile({
          bucket: bucketName,
          key: objectDirName + filePath.slice(localDirAbsolutePath.length),
          // File path for upload
          file: filePath,
          // Specify part size for upload
          partSize: 5 * 1024 * 1024,
          // Number of concurrent part upload tasks
          taskNum: 5,
        });
        console.log(`uploadFile ${filePath} result: `, data);
      }
    }
    await walkDir(localDirPath);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="1b3f6301"></span>
### **Configure progress bar**

During resumable upload, the progress can be received through the `dataTransferStatusChange` parameter. The code example is as follows.

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
    const objectName = 'example_dir/multipartExample';
    // The multipartExample file in the local example_dir folder.
    const filePath = './example_dir/multipartExample';

    const { data } = await client.uploadFile({
      bucket: bucketName,
      key: objectName,
      // Uploaded file path
      file: filePath,
      // Specify the part size during upload
      partSize: 5 * 1024 * 1024,
      // Concurrent number of part upload tasks
      taskNum: 5,

      // Set up a callback function to monitor the upload progress through custom configuration.
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
    console.log('uploadFile result', data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="fb80a5c2"></span>
### **Configure event callbacks**

The following code is used to customize the resumable upload callback function.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { UploadEventType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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
    const objectName = 'example_dir/multipartExample';
    // The multipartExample file under the local example_dir folder.
    const filePath = './example_dir/multipartExample';

    const { data } = await client.uploadFile({
      bucket: bucketName,
      key: objectName,
      // File path for upload
      file: filePath,
      // Specify the part size during upload
      partSize: 5 * 1024 * 1024,
      // Number of concurrent part upload tasks
      taskNum: 5,
      // Event listener callback
      uploadEventChange: (event) => {
        switch (event.type) {
          case UploadEventType.createMultipartUploadSucceed: {
            console.log(`Upload to ${event.bucket} ${event.key} create multipart upload success, upload id:${event.uploadId}`);
            break;
          }
          case UploadEventType.createMultipartUploadFailed: {
            console.log(`Upload to ${event.bucket} ${event.key} create multipart upload fail, upload id:${event.uploadId}`);
            break;
          }
          case UploadEventType.uploadPartSucceed: {
            console.log(`Upload to${event.bucket} ${event.key} part success, UploadPartInfo:%o`, event.uploadPartInfo);
            break;
          }
          case UploadEventType.uploadPartAborted: {
            console.log(`Upload to ${event.bucket} ${event.key} part aborted, upload id:${event.uploadId}`);
            break;
          }
          case UploadEventType.uploadPartFailed: {
            console.log(`Upload to ${event.bucket} ${event.key} part fail, upload id:${event.uploadId}`);
            break;
          }
          case UploadEventType.completeMultipartUploadSucceed: {
            console.log(`Upload to ${event.bucket} ${event.key} success, upload id:${event.uploadId}`);
            break;
          }
          case UploadEventType.completeMultipartUploadFailed: {
            console.log(`Upload to ${event.bucket} ${event.key} fail, upload id:${event.uploadId}, err: %o`, event.err);
            break;
          }
        }
      },
    });

    console.log('uploadFile result', data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="6cef1ee2"></span>
### **Configure client\-side rate limiting**

During resumable upload, you can use the tos.RateLimiter interface on the client side to limit the bandwidth usage. The code is as follows:

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { createDefaultRateLimiter, DataTransferType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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
    const objectName = 'example_dir/multipartExample';
    // The multipartExample file under the local example_dir folder.
    const filePath = './example_dir/multipartExample';
    const rateLimit1M = 1024;

    const { data } = await client.uploadFile({
      bucket: bucketName,
      key: objectName,
      // File path for upload
      file: filePath,
      // Specify part size for upload
      partSize: 5 * 1024 * 1024,
      // Number of concurrent part upload tasks
      taskNum: 5,
      // Upload object and limit upload speed to 1M/s on the client side
      rateLimiter: createDefaultRateLimiter(rateLimit1M, rateLimit1M),
      // Set callback function to view upload progress in a custom way
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
    console.log('uploadFile result', data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Y-W5raI5py65Yi2"></span>
### Cancellation mechanism

The following code is used to cancel an ongoing resumable upload task.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { CancelToken, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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
    const objectName = 'example_dir/multipartExample';
    // The multipartExample file under the local example_dir folder
    const filePath = './example_dir/multipartExample';
    // Generate cancelTokenSource
    const cancelTokenSource = CancelToken.source();

    client.uploadFile({
      bucket: bucketName,
      key: objectName,
      // Uploaded file path
      file: filePath,
      // Specify the part size during upload
      partSize: 5 * 1024 * 1024,
      // Inject cancelToken
      cancelToken: cancelTokenSource.token,
    });

    // Cancel task after 1 second.
    setTimeout(() => {
      cancelTokenSource.cancel();
      console.log('cancel request');
    }, 1000);
  } catch (error) {
    handleError(error);
  }
}

main();
```
