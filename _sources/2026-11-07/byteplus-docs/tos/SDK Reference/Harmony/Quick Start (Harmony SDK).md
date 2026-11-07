---
title: "Quick Start (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-harmony-sdk"
---

This document introduces how to quickly use the TOS Harmony SDK to perform common operations, such as creating buckets, uploading, downloading, and deleting objects.

<span id="649e2772"></span>
## Prerequisites


1. [Install Harmony SDK](https://docs.byteplus.com/docs/tos/install-harmony-sdk)

2. [Initializing the Client (Harmony SDK)](https://docs.byteplus.com/docs/tos/Initialize-the-client-harmony-sdk)


<span id="392cbffa"></span>
## Create Bucket

A bucket in TOS serves as a globally unique namespace, functioning as a data container for storing object data. <SOURCE_TEXT\>The following code demonstrates how to create a bucket.</SOURCE_TEXT\>

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

async function main() {
  try {
   
    await client.createBucket({
      Bucket: bucketName,
    });
    
    const { data } = await client.listBuckets();

   
    const theBucket = data.Buckets.find(it => it.Name === bucketName);
    console.log('the bucket info', theBucket);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional examples of bucket creation, see <a href="https://docs.byteplus.com/docs/tos/Create-bucket-harmony-sdk">Bucket Creation (Harmony SDK)</a>.</div>


<span id="3c17404b"></span>
## Upload Object

After the storage bucket is successfully created, objects can be uploaded to the bucket. The following code demonstrates how to upload an object to the newly created bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more examples of uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Upload-object-overview-node-js-sdk">Uploading Objects</a>.</div>


```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

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

async function main() {
  try {
    const bucketName = 'harmonyos-sdk-test-bucket'; 
    const objectName = 'example_dir/example.txt'; 
    
    await client.putObject({
      Bucket: bucketName,
      Key: objectName,
      Content: Content: buffer.from('a123').buffer,
    });

    
    const res = await client.headObject({
      Bucket: bucketName,
      Key: objectName,
    });
    // object size: 4
    console.log('object size:', res.ContentLength);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more examples of uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Overview-of-uploading-objects-harmony-sdk">Overview of Uploading Objects (Harmony SDK)</a>.</div>


<span id="9ee42be2"></span>
## Download Object

The following code demonstrates how to download an object from a bucket.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

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

const toString = (arr: ArrayBuffer) => {
  return buffer.from(arr).toString();
}

async function main() {
  try {
    const bucketName = 'harmonyos-sdk-test-bucket'; 
    const objectName = 'example_dir/example.txt'; 
   
    const res = await client.getObject({
      Bucket: bucketName,
      Key: objectName,
    });

   
    let allContent = ''
    while (true) {
      const buf = reader.read(10000);
      allContent += toString(buf)
      if (buf.byteLength === 0) {
        reader.close();
        break;
      }
    }

    console.log('object size:', allContent.length);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional examples of download objects, refer to <a href="https://docs.byteplus.com/docs/tos/Overview-of-downloading-objects-harmony-sdk">Overview of Download Objects (Harmony SDK)</a>.</div>


<span id="9828badc"></span>
## Enumeration of Objects

The following code demonstrates how to list objects in a bucket.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

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

async function main() {
  try {
    const bucketName = 'harmonyos-sdk-test-bucket';
    const res = await client.listObjectsType2({
      Bucket: bucketName,
      MaxKeys: 10,
    })
    console.log(`listObjectsType2 bucketName: ${bucketName}, len is ${res.Contents.length}`);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional examples of object enumeration, refer to <a href="https://docs.byteplus.com/docs/tos/List-objects-v2-harmony-sdk">Object Enumeration V2 (Harmony SDK)</a>.</div>


<span id="31f7297f"></span>
## Delete Object

The following code demonstrates how to delete an object from a bucket.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

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

async function main() {
  try {
    const bucketName = 'harmonyos-sdk-test-bucket';
    const objectName = 'delete-object-test'; 

    const res = await client.deleteObject({
      Bucket: bucketName,
      Key: objectName,
    });
    console.log(`deleteObject bucketName: ${bucketName} status: ${res3.StatusCode}`);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional examples on deleting objects, refer to <a href="https://docs.byteplus.com/docs/tos/Delete-objects-harmony-sdk">Deleting Objects (Harmony SDK)</a>.</div>
