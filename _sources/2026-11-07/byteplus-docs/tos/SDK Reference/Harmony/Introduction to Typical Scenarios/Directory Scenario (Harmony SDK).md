---
title: "Directory Scenario (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Directory-scenarios-harmony-sdk"
---

In TOS, only the concept of objects is defined, and data is stored internally using a flat structure. To facilitate object grouping and simplify permission management, you can organize objects using a directory hierarchy.

<span id="7b68eb93"></span>
## **Create Directory**

The following code is used to create the directory 'exampledir'.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
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

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {

    const key = 'exampledir/';
    const res = await client.putObject({
      Bucket: bucketName,
      Key: key,
    });
    console.log('putObject Request ID: ', res.RequestId);

    
    const key2 = 'exampledir/test/';
    const res2 = await client.putObject({
      Bucket: bucketName,
      Key: key2,
    });
    console.log('putObject Request ID: ', res2.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="0c212912"></span>
## **Simulated Directory Query**

TOS only has the concept of objects; it is possible to create an object with a size of zero and a trailing slash.`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


* First, set `delimiter` to`/`By also setting `prefix` to empty, you can return objects and subdirectory information in the root directory.

* When setting the `delimiter` to`/`By setting `prefix` to a subdirectory (subfiledir), objects within the subdirectory and its subordinate directories can be returned.


The following code is used to enumerate objects and subdirectories in the root directory.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
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

function printObjectContents(contents: ListedObject[]) {
  console.log('Contents Length:', contents.length);

  for (const obj of contents) {
    
    console.log('Object Key:', obj.Key);
    
    console.log('Object LastModified:', obj.LastModified);

    console.log('Object ETag:', obj.ETag);
   
    console.log('Object Size:', obj.Size);
  
    console.log('Object Owner:', obj.Owner);
   
    console.log('Object StorageClass:', obj.StorageClass);
 
    console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
  }
}

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
   
    let continuationToken = '';
    while (true) {
      const res = await client.listObjectsType2({
        Bucket: bucketName,
        MaxKeys: 1000,
        ContinuationToken: continuationToken,
        Delimiter: '/',
      });

      console.log('Sub Dir Length:', res.CommonPrefixes.length);
      for (const prefix of res.CommonPrefixes) {
        console.log('Sub Dir:', prefix.Prefix);
      }

      if (!res.NextContinuationToken) {
        break
      }
      continuationToken = res.NextContinuationToken;
    }
  } catch (error) {
    handleError(error);
  }
}
main();
```


<span id="4f2c03bf"></span>
## **Delete files in the directory.** 

The following code is used to delete all files located in the `exampledir/` directory within the storage bucket.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint",
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

function printObjectContents(contents: ListedObject[]) {
  console.log('Contents Length:', contents.length);

  for (const obj of contents) {
   
    console.log('Object Key:', obj.Key);
  
    console.log('Object LastModified:', obj.LastModified);
   
    console.log('Object ETag:', obj.ETag);
   
    console.log('Object Size:', obj.Size);
   
    console.log('Object Owner:', obj.Owner);
    
    console.log('Object StorageClass:', obj.StorageClass);
   
    console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
  }
}

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
 
    const dir = 'exampledir/';
    let continuationToken = '';
    while (true) {
      const res = await client.listObjectsType2({
        Bucket: bucketName,
        MaxKeys: 1000,
        ContinuationToken: continuationToken,
        Prefix: dir,
      });

      for (const obj of res.Contents) {
        const res = await client.deleteObject({
          Bucket: bucketName,
          Key: obj.Key,
        });
        console.log('deleteObject %s Request ID:', obj.Key, res.RequestId);
      }
      if (!res.IsTruncated || !res.NextContinuationToken) {
        break;
      }
      continuationToken = res.NextContinuationToken;
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
