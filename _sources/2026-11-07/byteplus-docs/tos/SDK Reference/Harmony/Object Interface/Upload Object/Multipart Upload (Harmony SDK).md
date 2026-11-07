---
title: "Multipart Upload (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/multipart-upload-harmony-sdk"
---

When uploading large objects, the data can be divided into multiple parts for separate upload. Finally, the merge operation is invoked to combine the uploaded parts into a single object.

<span id="cce445b2"></span>
## **Precautions**


* Before initiating multipart upload, you must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Before canceling a multipart upload task, you must have the `tos:AbortMultipartUpload` permission. For details on how to perform this operation, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Shard numbering starts at 1, with a maximum value of 10,000. Except for the last fragment, the minimum size of all other fragments is 4 MiB.

* When uploading objects, object names must comply with specific standards. For detailed information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale data storage. Its internal partitions store object index data. To horizontally scale the maximum throughput for uploading and downloading objects, and to reduce the probability of hotspot partitions, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id="0b063297"></span>
## Multipart Upload Procedure

Multipart upload typically consists of the following three steps:


1. Initialize the multipart upload task: Call the createMultipartUpload method, which returns the globally unique UploadID created by TOS.

2. Upload Part: Invoke the uploadPart method to upload part data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the same multipart upload task (identified by UploadID), the part number (PartNumber) specifies the relative position of the part within the entire object. If data is uploaded multiple times using the same shard number, TOS will overwrite the original data and retain only the most recently uploaded version.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The response header contains the MD5 value of the data, which can be obtained via the Etag. When merging parts, you must specify all part information (part number and ETag value) from the current multipart upload task.   </div>
   

3. Completing Multipart Upload: After all parts have been uploaded, invoke the completeMultipartUpload method to merge all parts into a single object.


<span id="e047505a"></span>
## Sample Code

<span id="0f051f5e"></span>
### **Complete Process of Multipart Upload**

The following code demonstrates the complete process of uploading a local file using multipart upload, specifying the ACL as Private, setting the storage type to low\-frequency storage, and adding custom metadata during the upload.

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
    const bucketName = 'harmony-sdk-test-bucket';
    const objectName = 'example_dir/multipartExample';
    
    const filePath = './example_dir/multipartExample';
 
    const res = await client.createMultipartUpload({
      Bucket: bucketName,
      Key: objectName,
      ACL: ACLType.ACLPrivate,
      StorageClass: StorageClassType.StorageClassIa,
    });
    console.log('CreateMultipartUploadV2 Upload ID:', res.UploadId);

 
    const stats = await fs.statSync(filePath);
  
    const totalSize = stats.size;
   
    const partSize = 5 * 1024 * 1024;
    let offset = 0;
  
    let partNumber = 1;
    const partsInfo: UploadedPart[] = [];
    while (offset < totalSize) {
      const uploadResult = await client.uploadPart({
        Bucket: bucketName,
        Key: objectName,
        PartNumber: partNumber,
        UploadID: res.UploadId,
        Content: fs.createReadStream(filePath, {
          start: offset,
          end: offset + partSize - 1,
        }),
      });
      const eTag = uploadResult.ETag;
      console.log(`partNumber${partNumber} Etag:`, eTag);
      partsInfo.push(new UploadedPart(partNumber, eTag));
      partNumber++;
      offset += partSize;
    }
    console.log('parts information', partsInfo);

   
    const completeRes = await client.completeMultipartUpload({
      Bucket: bucketName,
      Key: objectName,
      UploadID: res.UploadId,
      Parts: partsInfo,
    });

    console.log('result status:', completeRes.StatusCode);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="95fba824"></span>
### **List Uploaded Chunks**

The following code is used to enumerate information about the uploaded parts of a specified object within a designated storage bucket.

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
    const objectName = '*** Provide your object name ***';
   
    const uploadId = '*** Provide upload ID ***';

   
    let marker = 0;
    while (true) {
      const res= await client.listParts({
        Bucket: bucketName,
        Key: objectName,
        UploadId: uploadId,
        PartNumberMarker: marker,
      });
      
      if (!res.IsTruncated || res.NextPartNumberMarker === undefined) {
        break;
      }
      marker = res.NextPartNumberMarker;

      for (const part of res.Parts) {
        console.log(`Part Number: `, part.PartNumber);
        console.log(`ETag: `, part.ETag);
        console.log(`Size: `, part.Size);
      }
    }
  } catch (error) {
    handleError(error);
  }
}
main();
```


<span id="7bca135a"></span>
### Cancel Multipart Upload Task

You can cancel a multipart upload task using the **abortMultipartUpload** method. Once a multipart upload task is canceled, TOS will delete all previously uploaded part data. You will also be unable to perform any further operations on this multipart upload task.

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
    const bucketName = 'harmony-sdk-test-bucket';
    const objectName = '*** Provide your object name ***';
  
    const uploadId = `*** Provide upload ID ***`;


    const res = await client.abortMultipartUpload({
      Bucket: bucketName,
      Key: objectName,
      UploadID: uploadId,
    });

    console.log('result status:', res.StatusCode);
  } catch (error) {
    handleError(error);
  }
}
main();
```


<span id="3447b476"></span>
## **Relevant Documentation**


* For the API documentation on creating a multipart upload task, please refer to [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on uploading parts, refer to [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For API documentation on merging multipart uploads, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For API documentation on aborting multipart upload tasks, refer to [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
