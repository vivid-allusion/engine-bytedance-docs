---
title: "Managing Real-Time Logs (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-real-time-logs-node-js-sdk"
---

TOS supports log analysis capabilities to retrieve and analyze access logs generated during your visit to TOS through the log service. With the TOS Go SDK, you can configure the log analysis function.

<span id=".6K6-572u5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Set up real\-time log configuration rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To use the log analysis feature, you need to have the log service enabled and authorized TOS to access the BytePlus log service TLS.</div>


* <div data-tips="true" data-tips-type="warning">After enabling the log analysis function, the log service will automatically create log items and topics to store the relevant logs of the TOS.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the live log configuration rules for the bucket.

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
    // Scene 2: Redirecting requests based on rules.
    const { requestId: putRealTimeLogRequestId } = await client.putBucketRealTimeLog({
      bucket: bucketName,
      realTimeLogConfiguration: {
        // Configuration of TLS Role
        Role: 'TOSLogTLSRole',
        // Configuration of TLS
        AccessLogConfiguration: {
          UseServiceTopic: true,
          TLSProjectID: 'TLSProjectID',
          TLSTopicID: 'TLSTopicID',
        },
      },
    });
    console.log('putBucketRealTimeLog Request ID: ', putRealTimeLogRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Get real\-time log configuration rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the live log configuration rules for a bucket, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the live log configuration rules for the bucket.

```go
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
    const { data, requestId: getRealTimeLogRequestId } = await client.getBucketRealTimeLog({
      bucket: bucketName,
    });
    console.log('getBucketRealTimeLog Request ID: ', getRealTimeLogRequestId);
    // View TLS log configuration.
    console.log('getBucketRealTimeLog Role', data.RealTimeLogConfiguration.Role);
    console.log('getBucketRealTimeLog TLSTopicID', data.RealTimeLogConfiguration.AccessLogConfiguration.TLSTopicID);
    console.log('getBucketRealTimeLog TLSProjectID', data.RealTimeLogConfiguration.AccessLogConfiguration.TLSProjectID);
    console.log('getBucketRealTimeLog UseServiceTopic', data.RealTimeLogConfiguration.AccessLogConfiguration.UseServiceTopic);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Delete live log configuration rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To remove a live log configuration rule for a bucket, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code deletes the live log configuration rule for the bucket.

```go
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
    const { requestId: deleteRealTimeLogRequestId } = await client.deleteBucketRealTimeLog({
      bucket: bucketName,
    });
    console.log('deleteBucketRealTimeLog Request ID: ', deleteRealTimeLogRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```
