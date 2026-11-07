---
title: "Delete Object (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-objects-harmony-sdk"
---

When an object is no longer in use, you can delete it to reduce costs. Currently, the TOS Harmony SDK supports deleting individual objects and multiple specified objects within a bucket. For buckets with versioning enabled, you can specify and delete any version data of an object.

<span id="a6167b62"></span>
## Precautions


* Before deleting an object, you must have the `tos:DeleteObject` permission. For specific instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:DeleteObjectVersion` permission before deleting a specified version of an object. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id="0b279c3f"></span>
## Sample Code

<span id="3f76573b"></span>
### Delete Specified Object

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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
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
    const bucketName = 'harmony-sdk-test-bucket';
  
    const objectKey = '*** Provide your object key ***';
  
    const res = await client.deleteObject({
      Bucket: bucketName,
      Key: objectKey,
    });
    console.log('deleteObject Request ID:', res.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="8439b1f1"></span>
### **Delete the Specified Version of the Object**

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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
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
    const bucketName = 'harmony-sdk-test-bucket';
    
    const objectKey = '*** Provide your object key ***';
 
    const versionId = `*** Provide objectKey's version id ***`;

    
    const res = await client.deleteObject({
      Bucket: bucketName,
      Key: objectKey,
      VersionID: versionId
    });
    console.log('deleteObject Request ID:', res.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="e2dd3708"></span>
### **Batch Deletion of Specified Objects**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In a bucket with versioning enabled, when the DeleteMultiObjects API is called to delete objects in bulk, if the <code>versionId</code> is not specified in the Delete request, a delete marker will be inserted. If <code>versionId</code> is specified, the designated version of the object will be permanently deleted.</div>


<div data-tips="true" data-tips-type="warning">The response mode supported by batch object deletion can be configured via <code>quiet</code>:</div>



* <div data-tips="true" data-tips-type="warning">When <code>quiet</code> is set to <code>false</code>, the response will include the deletion result regardless of whether the object was successfully deleted.</div>


* <div data-tips="true" data-tips-type="warning">When <code>quiet</code> is set to <code>true</code>, only the results of objects that failed to be deleted are returned in the response; objects not included in the response are considered successfully deleted.</div>



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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
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
    
    const objectKey1 = '*** Provide your object key ***';
    const objectKey2 = '*** Provide your object key ***';

 
    const res = await client.deleteMultiObjects({
      Bucket: bucketName,
      Objects: [new ObjectTobeDeleted(objectKey1), new ObjectTobeDeleted(objectKey2)],
    });
    console.log('deleteMultiObjects Request ID:', res.RequestId);
    console.log('deleteMultiObjects Deleted.length:', res.Deleted.length);
    for (const item of res.Deleted) {
      console.log('deleted item Key:', item.Key);
      console.log('deleted item VersionId:', item.VersionId);
      console.log('deleted item DeleteMarker:', item.DeleteMarker);
      console.log('deleted item DeleteMarkerVersionId:', item.DeleteMarkerVersionId);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="816b0f7e"></span>
### **Bulk Deletion of Objects with Specified Versions**

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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
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
  
    const objectKey1 = '*** Provide your object key ***';
    const objectKey2 = '*** Provide your object key ***';
  
    const versionId1 = `*** Provide objectKey1's version id ***`;
    const versionId2 = `*** Provide objectKey2's version id ***`;

   
    const res = await client.deleteMultiObjects({
      Bucket: bucketName,
      Objects: [new ObjectTobeDeleted(objectKey1, versionId1), new ObjectTobeDeleted(objectKey2, versionId2)],
    });
    console.log('deleteMultiObjects Request ID:', res.RequestId);
    console.log('deleteMultiObjects Deleted.length:', res.Deleted.length);
    for (const item of res.Deleted) {
      console.log('deleted item Key:', item.Key);
      console.log('deleted item VersionId:', item.VersionId);
      console.log('deleted item DeleteMarker:', item.DeleteMarker);
      console.log('deleted item DeleteMarkerVersionId:', item.DeleteMarkerVersionId);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="f3b110ee"></span>
## **Relevant Documentation**

For API documentation on deleting objects, refer to [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
