---
title: "Managing Bucket Lifecycle (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-the-bucket-lifecycle-node-js-sdk"
---

You can use the lifecycle management function of TOS through the SDK to achieve the purpose of saving storage costs by expiring and deleting objects. When configuring a lifecycle rule, you can specify the object prefix or object tag on which the rule takes effect. If you specify both conditions, the object must satisfy all the conditions set before the lifecycle rule applies.

<span id=".6K6-572u55Sf5ZG95ZGo5pyf"></span>
## **Set lifecycle rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before you can set a lifecycle rule, you must have the <code>tos: PutLifecycleConfiguration</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">If a bucket has been configured with a lifecycle rule, performing this operation overrides the original configuration. If you need to append a lifecycle rule, use GetLifecycleConfigutation to get the current rule, append and write a new rule, and finally call PutLifecycleConfiguration to update the rule.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the lifecycle rules for a bucket.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, LifecycleStatusType } from '@volcengine/tos-sdk';

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
    const lifeCycleRule = {
      // Rule ID
      ID: 'rule1',
      // Specify the prefix to which the rule applies, matching the prefix
      Prefix: 'prefix-',
      // Rule status, indicating whether the rule is enabled
      Status: LifecycleStatusType.Enabled,
      // Object expiration time
      // Days: specify the number of days after which the object will expire
      // Date: specify the date on which the object will expire
      Expiration: {
        Days: 30,
      },
      // Object labels
      Tags: [
        {
          Key: 'key',
          Value: 'value',
        },
      ],
    };
    const { requestId: putLifecycleRequestId } = await client.putBucketLifecycle({
      bucket: bucketName,
      rules: [lifeCycleRule],
    });
    console.log('putBucketLifecycle Request ID: ', putLifecycleRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W55Sf5ZG95ZGo5pyf6YWN572u"></span>
## **Get lifecycle rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You must have the <code>tos: GetLifecycleConfiguration</code> permission before getting the bucket setup lifecycle rule. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information on lifecycle rules, see <a href="https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules">Setting lifecycle rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the lifecycle rules for a bucket.

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
    const { data, requestId: getLifecycleRequestId } = await client.getBucketLifecycle({
      bucket: bucketName,
    });
    console.log('getBucketLifecycle Request ID: ', getLifecycleRequestId);
    console.log('getBucketLifecycle Rules Length: ', data.Rules.length);
    for (const rule of data.Rules) {
      // Rule ID
      console.log('Rule ID:', rule.ID);
      // Rule Prefix, matching prefix for the specified rule
      console.log('Rule Prefix:', rule.Prefix);
      // Rule Status, indicating whether the rule is enabled
      console.log('Rule Status:', rule.Status);
      // Rule Transitions, describes when the storage type of an object is converted
      console.log('Rule Transitions:', rule.Transitions);
      // Expiration time for the object
      console.log('Rule Expiration:', rule.Expiration);
      // Non-current version storage type transition
      console.log('Rule NonCurrentVersionTransition:', rule.NonCurrentVersionTransition);
      // Non-current version object expiration
      console.log('Rule NoCurrentVersionExpiration:', rule.NoCurrentVersionExpiration);
      // Tags
      for (const tag of rule.Tags) {
        console.log('Rule Tag Key:', tag.Key);
        console.log('Rule Tag Value:', tag.Value);
      }
      // The maximum retention time for unfinished uploaded chunks.
      console.log('Rule AbortInCompleteMultipartUpload:', rule.AbortInCompleteMultipartUpload);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## **Delete lifecycle rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting a bucket lifecycle rule, you must have the <code>tos: PutLifecycleConfiguration</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete the bucket's lifecycle rule.

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
    const { requestId: deleteLifecycleRequestId } = await client.deleteBucketLifecycle({
      bucket: bucketName,
    });
    console.log('deleteBucketLifecycle Request ID: ', deleteLifecycleRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information on lifecycle rules, please refer to [Setting lifecycle rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules).
