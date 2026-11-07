---
title: "Enumerate Objects V2 (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-v2-harmony-sdk"
---

This article describes how to use listObjectsType2 to enumerate all objects within a specified bucket, files with a specified prefix, as well as files and subdirectories within a specified directory.

<span id="712992d7"></span>
## **Precautions**


* The ListObjects interface has been revised to ListObjectsType2. Developers are strongly encouraged to use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use List Objects V2, you must have the `tos:ListBucket` permission. For details, see [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id="dba49225"></span>
## Parameter Description

The parameters supported by ListObjectsType2 are as follows:


|**Parameters** |**Description** |
|---|---|
|Prefix |The prefix of the current query results. |
|Delimiter |The character used to group object names. |
|StartAfter |The starting point for the objects enumerated in this instance. |
|ContinuationToken |The specified enumeration operation must begin from this `token`. It can be obtained from the `NextContinuationToken` in the results of the previous listing. |
|MaxKeys |Returns the maximum number of objects to be listed; the default value is 1000. The permissible value range is (0, 1000]. |
|EncodingType |Encode the returned content and specify the type of encoding. The possible values are as follows:<br><br><br>* `undefined`: Default value; no encoding.<br><br>* `'url'`: Use URL encoding. |


<span id="4fcb56a5"></span>
## Sample Code

<span id="4b4a66d8"></span>
### **Brief Enumeration**

The following code is used to enumerate objects in the bucket named 'bucketName', listing up to 1,000 objects.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';


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

async function main() {
  try {

    const res = await client.listObjectsType2({
      Bucket: bucketName,
      MaxKeys: 1000,
    });
    for (const obj of res.Contents) {
    
      console.log('Object Key:', obj.Key);
    
      console.log('Object LastModified:', obj.LastModified);
   
      console.log('Object ETag:', obj.ETag);
  
      console.log('Object Size:', obj.Size);

      console.log('Object Owner:', obj.Owner);

      console.log('Object StorageClass:', obj.StorageClass);
  
      console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="919c8daa"></span>
### **Paginated Listing**

The following code is used to paginate the listing of the first 1000 and last 1000 objects in the bucket named bucketName.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';


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

    const res = await client.listObjectsType2({
      Bucket: bucketName,
      MaxKeys: 1000,
    });

 
    const res2 = await client.listObjectsType2({
      Bucket: bucketName,
      MaxKeys: 1000,
      ContinuationToken: res.NextContinuationToken,
    });
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="05d0f5d4"></span>
### **List all objects with the specified prefix**

The following code enumerates objects with the prefix 'prefix' in the bucket 'bucketName'.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';


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

async function main() {
  try {
    const prefix = '*** Provide your object key prefix ***';
    let continuationToken = '';
    while (true) {
      const res = await client.listObjectsType2({
        Bucket: bucketName,
        MaxKeys: 1000,
        ContinuationToken: continuationToken,
        Prefix: prefix,
      });
      
      if (!res.NextContinuationToken) {
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


<span id="37c7add8"></span>
### **Paginated Listing of All Objects in a Bucket**

The following code is used to paginate and list all objects in the 'bucketName' storage bucket.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';


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

async function main() {
  try {
    let continuationToken = '';
    while (true) {
      const res = await client.listObjectsType2({
        Bucket: bucketName,
        MaxKeys: 1000,
        ContinuationToken: continuationToken,
      });
      
      if (!res.NextContinuationToken) {
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


<span id="3f759f0c"></span>
### **List the files and subdirectories in the specified directory.** 

TOS supports only the concept of objects; it is possible to create an object with a size of zero and a slash in its name.`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated by using the two parameters `delimiter` and `prefix`:


* First, set the `delimiter` to`/`By also setting `prefix` to an empty value, you can retrieve information about objects and subdirectories in the root directory.

* When setting `delimiter` to`/`At the same time, set `prefix` as a subdirectory (subfiledir), so that objects and sub\-level directories within that subdirectory can be returned.


The following code is used to enumerate objects and subdirectories in the root directory of the bucket named bucketName.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';


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
