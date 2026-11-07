---
title: "Standard Upload (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/simple-upload-harmony-sdk"
---

Standard upload refers to uploading a single object (Object) via the **putObject** method. It supports uploading strings (character streams), uploading bytes (byte streams), and uploading local files.

<span id="5bc14138"></span>
## Precautions


* Before uploading an object, you must have the `tos:PutObject` permission.

* When uploading an object, the object name must comply with specific requirements. For more information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions that store object index data. To horizontally scale the maximum throughput for uploading and downloading objects and to reduce the probability of hot partitions, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id="0cef5f54"></span>
## Sample Code

<span id="44f0d7a3"></span>
### Upload String

You can use the following sample code and the **putObject** API to upload string data to the `example_dir` directory's `example.txt` file in TOS.

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

async function main() {
  try {
    const bucketName = 'harmony-sdk-test-bucket';
    const objectName = 'example_dir/example.txt';
    
    await client.putObject({
      Bucket: bucketName,
      Key: objectName,
   
      Content: buffer.from('Hello TOS').buffer,
    });

  
    const res = await client.headObject({
      Bucket: bucketName,
      Key: objectName,
    });
    // object size: 9
    console.log('object size:', res.ContentLength);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="413fa346"></span>
### **Upload Local File Stream**

You can use the following example code and the **putObject** interface to upload a file from a specified path to `example.txt` in the `example_dir` directory of TOS.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';
import fs from 'fs';


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
    const bucketName = 'harmony-sdk-test-bucket';
    const objectName = 'example_dir/example.txt';
    const filePath = './example_dir/example.txt'
    const uploadFromStream = new rcp.UploadFromStream(fs.createStreamSync(filePath, 'r+'))
  
    await client.putObject({
      Bucket: bucketName,
      Key: objectName,
      Content: uploadFromStream,
    });

   
    const res = await client.headObject({
      Bucket: bucketName,
      Key: objectName,
    });
    // object size: 9
    console.log('object size:', res.ContentLength);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="119f47f4"></span>
### Upload from Local File

The following sample code demonstrates how to use the **putObjectFromFile** interface to upload a file by specifying its file path. The file will be uploaded to the specified `example_dir` directory in TOS as `example.txt`.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';
import fs from 'fs';


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
    const bucketName = 'harmony-sdk-test-bucket';
    const objectName = 'example_dir/example.txt';

    await client.putObjectFromFile({
      Bucket: bucketName,
      Key: objectName,
      FilePath: './example.txt',
    });

    
    const res = await client.headObject({
      Bucket: bucketName,
      Key: objectName,
    });
    // object size: 9
    console.log('object size:', res.ContentLength);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="b57f39e1"></span>
### **Configuring object metadata during upload**

You can use the following sample code to upload string data to the `example.txt` file under the `example_dir` directory using the **putObject** interface. During the upload, specify the object storage type as infrequent access, set the access permission to private, and configure the file metadata.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';
import fs from 'fs';


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
  const meta: Record<string, string> = {};
  meta.key = 'value'
  try {
    const bucketName = 'harmony-sdk-test-bucket';
    const objectName = 'example_dir/example.txt';
   
    await client.putObject({
      Bucket: bucketName,
      Key: objectName,
      
      Content: buffer.from('Hello TOS').buffer,
     
      StorageClass: StorageClassType.StorageClassIa,
   
      ACL: ACLType.ACLPrivate,
  
      Meta: meta,
    });


    const res = await client.headObject({
      Bucket: bucketName,
      Key: objectName,
    });
    console.log('object size:', res.ContentLength);
    console.log('storage class:',  res.StorageClass);
    console.log('x-tos-meta-key:', res.Meta?.['key']);
  } catch (error) {
    handleError(error);
  }
}
```


<span id="3120e6ca"></span>
## **Relevant Documentation**

For API documentation on uploading objects, refer to [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
