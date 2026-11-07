---
title: "Resumable Download (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-download-node-js-sdk"
---

When downloading large files, you can use the `downloadFile`breakpoint to resume the download interface. Breakpoint continuation downloads use sharding downloads to write content to temporary files. If partial sharding succeeds and partial failure occurs, the information of successful download and failed sharding can be recorded and saved to the Checkpoint file. When downloading the same object again, only the failed sharding is downloaded. When all shards succeed, rename the temporary file to the official file and delete the checkpoint file.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before downloading an object, you must have `tos: GetObject`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* To open multiple versions of a bucket, you must have the `tos: GetObjectVersion`permission when downloading the specified version object. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* If an application downloads a large number of the same object at the same time, your access speed will be limited by TOS bandwidth and geography. It is recommended that you use CDN products to improve performance while also reducing your costs.

* The SDK will record the uploaded status information in the `Checkpoint`file, so the program needs to have write permission to the `Checkpoint`file.

* When using breakpoint to resume downloading, the progress information of the file download will be recorded in the `Checkpoint`file. If a sharding download fails during the download process, it will continue to download from the point recorded in the `Checkpoint`file when downloading again, so as to achieve the effect of breakpoint renewal. Once the download is complete, the `Checkpoint`file is deleted.

* If the file's ETag changes, Parts are lost, or modified during the download process, the file is downloaded again.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5pat54K557ut5Lyg5LiL6L29"></span>
### Breakpoint Resume Download

The following code is used to download a file using a breakpoint continuation method.

```javascript
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
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    // Downloaded file path
    const filePath = './example_dir/example.txt';
    await client.downloadFile({
      bucket: bucketName,
      key: objectName,
      // Downloaded file path
      filePath,
      // Number of concurrent tasks for segmented downloading
      taskNum: 5,
      // Specify the temporary file path for resumable downloads
      checkpoint: './example_dir/example.checkpoint',
    });

    const fileStat = await fsp.stat(filePath);
    console.log('fileSize: ', fileStat.size);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="cb1ac493"></span>
### **Configure progress bar**

When the breakpoint resumes the download, the download progress can be received through the `dataTransferStatusChange`parameter. The code example is as follows.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
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
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    // Downloaded file path
    const filePath = './example_dir/example.txt';
    await client.downloadFile({
      bucket: bucketName,
      key: objectName,
      // Downloaded file path
      filePath,
      // Specify the size of each part during download (10M)
      partSize: 10 * 1024 * 1024,
      // Number of concurrent part download tasks
      taskNum: 5,
      // Specify the temporary file path for resumable downloads
      checkpoint: './example_dir/example.checkpoint',
      // Set a custom callback function to monitor the download progress
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

    const fileStat = await fsp.stat(filePath);
    console.log('fileSize: ', fileStat.size);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="d1d8fedd"></span>
### **Configure event callback**

The following code is used to customize the breakpoint continuation download callback function.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, DownloadEventType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
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
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    // Downloaded file path
    const filePath = './example_dir/example.txt';
    await client.downloadFile({
      bucket: bucketName,
      key: objectName,
      // Downloaded file path
      filePath,
      // Specify the size of each part during download (10M)
      partSize: 10 * 1024 * 1024,
      // Number of concurrent part download tasks
      taskNum: 5,
      // Specify the temporary file path for resumable downloads
      checkpoint: './example_dir/example.checkpoint',
      // Set a callback function to view the download progress using a custom method
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
      // Event listener callback
      downloadEventChange: (event) => {
        switch (event.type) {
          case DownloadEventType.CreateTempFileSucceed: {
            console.log('Download File Create Temp File Success.');
            break;
          }
          case DownloadEventType.CreateTempFileFailed: {
            console.log('Download File Create Temp File Fail.');
            break;
          }
          case DownloadEventType.DownloadPartSucceed: {
            console.log(`Download ${event.bucket} ${event.key} part success, DownloadPartInfo:%o`, event.downloadPartInfo);
            break;
          }
          case DownloadEventType.DownloadPartAborted: {
            console.log(`Download ${event.bucket} ${event.key} part aborted.`);
            break;
          }
          case DownloadEventType.DownloadPartFailed: {
            console.log(`Download ${event.bucket} ${event.key} part fail, err:%o`, event.err);
            break;
          }
          case DownloadEventType.RenameTempFileSucceed: {
            console.log(`Download ${event.bucket} ${event.key} success.`);
            break;
          }
          case DownloadEventType.CreateTempFileFailed: {
            console.log(`Download ${event.bucket} ${event.key} fail, err:%o`, event.err);
            break;
          }
        }
      },
    });

    const fileStat = await fsp.stat(filePath);
    console.log('fileSize: ', fileStat.size);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="fe6e6469"></span>
### **Configure client side speed limit**

When the breakpoint resumes the download, the client side can use the `rateLimiter`parameter to limit the bandwidth occupied by the downloaded data. The code is as follows.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, createDefaultRateLimiter, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
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
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    // The downloaded file path.
    const filePath = './example_dir/example.txt';
    const rateLimit1M = 1024 * 1024;
    await client.downloadFile({
      bucket: bucketName,
      key: objectName,
      // Download file path
      filePath,
      // Specify the chunk size during download to be 10M
      partSize: 10 * 1024 * 1024,
      // Number of concurrent chunk download tasks
      taskNum: 5,
      // Specify the temporary file path for resumable downloads
      checkpoint: './example_dir/example.checkpoint',
      // Set callback function to view download progress through custom methods
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
      // Limit the download speed to 1M/s on the client side while downloading the object.
      rateLimiter: createDefaultRateLimiter(rateLimit1M, rateLimit1M),
    });

    const fileStat = await fsp.stat(filePath);
    console.log('fileSize: ', fileStat.size);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Y-W5raI5py65Yi2"></span>
### Cancellation mechanism

The following code is used to cancel the ongoing breakpoint continuation download task at runtime.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { DataTransferType, CancelToken, TosClient, TosClientError, TosServerError, isCancel } from '@volcengine/tos-sdk';
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
  // checkpoint file path
  const checkpointFilePath = './example_dir/example.checkpoint';

  try {
    const bucketName = 'node-sdk-test-bucket'; // Target bucket
    const objectName = 'example_dir/example.txt'; // Target object
    // Downloaded file path
    const filePath = './example_dir/example.txt';

    try {
      // Generate cancelTokenSource.
      const cancelTokenSource = CancelToken.source();
      // Cancel task after 1 second.
      setTimeout(() => {
        cancelTokenSource.cancel();
        console.log('cancel downloadFile');
      }, 1_000);

      await client.downloadFile({
        bucket: bucketName,
        key: objectName,
        // Downloaded file path
        filePath,
        // Specify the chunk size during download (1M)
        partSize: 1 * 1024 * 1024,
        // Number of concurrent chunk download tasks
        taskNum: 5,
        // Specify the temporary file path for resumable download
        checkpoint: './example_dir/example.checkpoint',
        // Set a custom callback function to monitor the download progress
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
        cancelToken: cancelTokenSource.token,
      });
    } catch (error) {
      if (!isCancel(error)) {
        throw error;
      }

      const checkpointFileContent = await fsp.readFile(checkpointFilePath, 'utf-8');
      console.log(`checkpoint file's content after cancel: `, checkpointFileContent);

      console.log('Continue to download');
      // You can resume downloading through the checkpoint file.
      await client.downloadFile({
        bucket: bucketName,
        key: objectName,
        // Downloaded file path
        filePath,
        // Specify the chunk size during download (1M)
        partSize: 1 * 1024 * 1024,
        // Number of concurrent chunk download tasks
        taskNum: 5,
        // Specify the temporary file path for resumable downloads
        checkpoint: './example_dir/example.checkpoint',
        // Set a custom callback function to monitor download progress
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

      const fileStat = await fsp.stat(filePath);
      console.log('fileSize: ', fileStat.size);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
