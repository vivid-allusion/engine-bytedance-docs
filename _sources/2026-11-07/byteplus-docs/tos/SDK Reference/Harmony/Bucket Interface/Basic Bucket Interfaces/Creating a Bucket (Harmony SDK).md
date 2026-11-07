---
title: "Creating a Bucket (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-bucket-harmony-sdk"
---

A bucket is the globally unique namespace in TOS, functioning as a data container for storing object data. The name of a newly created bucket must be unique within TOS. This article describes how to create a bucket.

<span id="ec10033b"></span>
## Precautions


* Storage bucket [naming conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts) are as follows:

   * Only lowercase letters (a–z), digits, and hyphens (\-) are permitted.

   * Only digits or letters are permitted at the beginning and end.

   * The length must be between 3 and 63 characters.

* When accessing TOS through other BytePlus products located in the same region as TOS, it is recommended to use the internal network endpoint. For more information about regions and Endpoints, see [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a storage bucket, you must ensure that your account has the `tos:CreateBucket` permission. You can grant the relevant permissions through IAM policies. For detailed steps, please refer to [ IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id="084f6304"></span>
## Sample Code

<span id="437234cf"></span>
### Create Bucket

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

const bucketName = 'harmonyos-sdk-test-bucket';

function handleError(error: Error) {
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

async function createBucket() {
  try {
   
    await client.createBucket({
      Bucket: bucketName,
    });
    
    const res = await client.listBuckets();

   
    const theBucket = res.Buckets.find(it => it.Name === bucketName);
    console.log('the bucket info', theBucket.Name);
  } catch (error) {
    handleError(error);
  }
}

createBucket();
```


<span id="7c82de42"></span>
### Specify the storage type during creation.

```TypeScript
import { TosClient, TosClientError, TosServerError, StorageClassType } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

const bucketName = 'harmonyos-sdk-test-bucket';

function handleError(error: Error) {
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
async function createBucketWithStorageClass() {
  try {
   
    await client.createBucket({
      Bucket: bucketName,
    
      StorageClass: StorageClassType.StorageClassIa,
    });
   
    const res = await client.headBucket({
       Bucket: bucketName,
    })
    console.log('the bucket storageClass is', res.StorageClass);
  } catch (error) {
    handleError(error);
  }
}

createBucketWithStorageClass();
```


<span id="f8edd29d"></span>
### **Specify AZ Type During Creation**

```TypeScript
import { TosClient, TosClientError, TosServerError, StorageClassType } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

const bucketName = 'harmonyos-sdk-test-bucket';

function handleError(error: Error) {
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
async function createBucketWithAZ() {
  try {
   
    await client.createBucket({
      Bucket: bucketName,
   
      AzRedundancy: AzRedundancyType.AzRedundancyMultiAz,
    });
   
    const res = await client.headBucket({
       Bucket: bucketName,
    })
    console.log('the bucket az type is', res.AzRedundancy);
  } catch (error) {
    handleError(error);
  }
}

createBucketWithAZ();
```


<span id="45803cde"></span>
## Relevant Documentation

For API documentation on creating buckets, refer to [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
