---
title: "Managing Cross-Region Replication (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Managing-cross-region-replication-node-js-sdk"
---

TOS supports cross\-region replication, allowing you to copy objects from one region to buckets in different regions. When cross\-region replication rules are enabled, when you upload a new file in the source bucket, TOS automatically syncs the file to the destination bucket. This function is used to meet the requirements of off\-site disaster recovery and data replication.

<span id=".6K6-572u6Leo5Yy65Z-f5aSN6KeE5YiZ"></span>
## **Setting up cross\-regional multiplexing rules**

<span id=".5rOo5oSP5LqL6aG5"></span>
### **Precautions**


* After cross\-region rules are turned on, the corresponding files will be synchronized.

* Cross\-region replication uses an asynchronous replication mechanism that can take anywhere from a few minutes to a few hours, depending on the size of your file.

* A single bucket can create up to 100 cross\-region replication rules.

* Cross\-region replication can only be enabled if the source and destination buckets have the same versioning state.

* To set cross\-regional replication rules for buckets, you must be the bucket owner by default.

* When the CRR task is executed, when StorageClassType and StorageClassInheritDirectiveType are set at the same time, the configuration of StorageClassType shall prevail.

* When only StorageClassInheritDirectiveType is set, the configuration value is `StorageClassIDSourceObject`consistent with the source object, and the configuration item value is `StorageClassIDDestinationBucket`consistent with the target bucket.

* When neither StorageClassType nor StorageClassInheritDirectiveType is set, the default policy is used to match the storage type of the target bucket.


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the cross\-region replication rules for buckets.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, StatusType, StorageClassInheritDirectiveType } from '@volcengine/tos-sdk';

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
    const rule = {
      // Rule ID
      ID: 'rule_id',
      // Specify whether to enable cross-region replication rule
      Status: StatusType.Enabled,
      // Specify the prefix of the objects to be matched for cross-region replication, empty means replicate all objects.
      PrefixSet: [],
      // Specify the destination information to replicate to.
      Destination: {
        // Target bucket name
        Bucket: 'dst_bucket',
        // Target region information
        Location: 'dst_region',
        // Specify the storage class rule for the copied object
        // StorageClassInheritDirectiveSourceObject: Consistent with the source object
        // StorageClassInheritDirectiveDestinationBucket: Consistent with the target bucket
        StorageClassInheritDirective: StorageClassInheritDirectiveType.StorageClassInheritDirectiveSourceObject,
      },
      // Do you need to duplicate historical objects?
      HistoricalObjectReplication: StatusType.Disabled,
    };
    // Set Role
    const role = 'your role';
    const { requestId: putReplicationRequestId } = await client.putBucketReplication({
      bucket: bucketName,
      role,
      rules: [rule],
    });
    console.log('putBucketReplication Request ID: ', putReplicationRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5p-l55yL6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## **View cross\-region replication rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain cross\-regional replication rules for buckets, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the cross\-region replication rule for the bucket.

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
    const { data, requestId: getReplicationRequestId } = await client.getBucketReplication({
      bucket: bucketName,
      // When ruleId is not specified, it queries all cross-region replication rules in the current bucket.
      // When ruleId is specified, it returns the specified rule.
      // ruleId: 'ruleId',
    });
    console.log('getBucketReplication Request ID: ', getReplicationRequestId);
    console.log('Replication rules length:  ', data.Rules.length);
    // View detailed information on cross-origin access rules.
    for (const rule of data.Rules) {
      // Rule ID
      console.log('rule id:', rule.ID);
      // Rule status
      console.log('rule status:', rule.Status);
      for (const prefix of rule.PrefixSet || []) {
        // Rule prefix
        console.log('rule prefix:', prefix);
      }
      // Destination Bucket
      console.log('rule destination bucket:', rule.Destination.Bucket);
      // Destination Location
      console.log('rule destination location:', rule.Destination.Location);
      // Storage Class
      console.log('rule destination storage class:', rule.Destination.StorageClass);
      // Storage Class Rule
      console.log('rule dst storage class inherit directive:', rule.Destination.StorageClassInheritDirective);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5p-l6K-i6Leo5Yy65Z-f5aSN5Yi26L-b5bqm"></span>
## **Query cross\-region replication progress**

<span id=".5rOo5oSP5LqL6aG5"></span>
### **Precautions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To get the cross\-regional replication progress of a bucket, you must be the bucket owner by default.</div>


* <div data-tips="true" data-tips-type="warning">Historical data replication progress is expressed as a percentage and is only valid for storage spaces where historical data replication is enabled.</div>


* <div data-tips="true" data-tips-type="warning">The new data replication progress is represented by the point in time of the new data.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the cross\-region replication progress of the bucket.

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
    const { data, requestId: getReplicationRequestId } = await client.getBucketReplication({
      bucket: bucketName,
      // When ruleId is not specified, query all cross-region replication rules in the current bucket.
      // When ruleId is specified, return the specified rule.
      // ruleId: 'ruleId',
    });
    console.log('getBucketReplication Request ID: ', getReplicationRequestId);
    console.log('Replication rules length:  ', data.Rules.length);
    // View detailed information on cross-origin access rules.
    for (const rule of data.Rules) {
      // Rule ID
      console.log('rule id:', rule.ID);
      // Historical copy progress
      console.log('rule historical object:', rule.Progress.HistoricalObject);
      // Incremental progress time point
      console.log('rule new object:', rule.Progress.NewObject);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## **Delete cross\-region replication rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To remove the cross\-regional replication rule for a bucket, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code removes the cross\-region replication rule for buckets.

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
    const { requestId: deleteReplicationRequestId } = await client.deleteBucketReplication({
      bucket: bucketName,
    });
    console.log('deleteBucketReplication Request ID: ', deleteReplicationRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```
