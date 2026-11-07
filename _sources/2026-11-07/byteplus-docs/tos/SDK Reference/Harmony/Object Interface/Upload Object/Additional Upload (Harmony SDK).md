---
title: "Additional Upload (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-harmony-sdk"
---

The appendObject interface is used to append data to an object. Append write refers to adding content to the end of an already uploaded object. This interface can only be used with objects of type Appendable. Objects created via direct upload and multipart upload are of the Normal type.

**Precautions**


* Before performing append upload to an object, you must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific requirements. For detailed information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage. Its internal partitions store object index data. When uploading and downloading objects, to maximize horizontal scalability and throughput, and to reduce the likelihood of hotspot partitions, please avoid naming objects in a lexicographically increasing order. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When multi\-versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.

* Append upload for objects does not support requests using Chunk\-Encoded transfer encoding. When performing append uploads on network streams, please retrieve data iteratively and then append upload.


<span id="98e6fbc3"></span>
## Limitations

The object size limitations when using the AppendObject interface are specified as follows:


* The size of the object after appending must not exceed 5 GiB.

* When an object created using AppendObject is subjected to a PutObject operation, the object is overwritten and its type changes from Appendable to Normal. Conversely, objects uploaded via PutObject do not support append write operations.

* Objects created by AppendObject do not support copying.

* The AppendObject interface cannot be used if the object type is Infrequent Access Storage or Archive Flashback Storage.

* If your bucket has versioning enabled or suspended, the AppendObject interface cannot be used.


<span id="2acabb9a"></span>
## **Sample Code**

The following code is used to upload a character stream by appending it to the target bucket.

```TypeScript
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
    const bucketName = 'node-sdk-test-bucket';
    const objectName = 'example_dir/example.txt';
  
    await client.appendObject({
      Bucket: bucketName,
      Key: objectName,
    
      Content: buffer.from('Hello TOS').buffer,
      Offset: 0,
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


<span id="beaae7f8"></span>
## **Relevant Documentation**

For documentation on the append upload API, please refer to [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
