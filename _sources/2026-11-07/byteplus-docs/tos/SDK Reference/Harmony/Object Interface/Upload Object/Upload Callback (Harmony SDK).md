---
title: "Upload Callback (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback-harmony-sdk"
---

An upload callback refers to a process in which the client includes a callback (Callback) parameter in its request. After the upload is complete, the server sends a synchronous POST callback request to the third\-party application server specified in the Callback parameter. The server returns all results to the client only after receiving confirmation and a response from the third\-party application server.

<span id="afcd8276"></span>
## Sample Code

<span id="cd5c3c26"></span>
### Implementation of Upload Callback in Standard Upload

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
    const callbackUrl = '*** Provide your callback url ***';
    const objectKey = '*** Provide your object key ***';

   
   
    const callback = `
    {
      "callbackUrl" : "${callbackUrl}", 
      "callbackBody" : ${'"{\\"bucket\\": ${bucket}, \\"object\\": ${object}, \\"key1\\": ${x:key1}}"'}, 
      "callbackBodyType" : "application/json"                
    }`;  
    
    const callbackVar = `
    {
      "x:key1" : "ceshi"
    }`;
    const res = await client.putObject({
      Bucket: bucketName,
      Key: objectKey,
      Content: buffer.from('object content').buffer,
      Callback: buffer.from(callback).toString('base64'),
      CallbackVar: buffer.from(callbackVar).toString('base64'),
    });
    console.log('putObject CallbackResult: ', res.CallbackResult);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="60310e67"></span>
### Multipart upload callback

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
    const callbackUrl = '*** Provide your callback url ***';
    const callback = `
    {
      "callbackUrl" : "${callbackUrl}",
      "callbackBody" : ${'"{\\"bucket\\": ${bucket}, \\"object\\": ${object}, \\"key1\\": ${x:key1}}"'},
      "callbackBodyType" : "application/json"
    }`;  

    const callbackVar = `
    {
      "x:key1" : "ceshi"
    }`;
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
      Callback: buffer.from(callback).toString('base64'),
      CallbackVar: buffer.from(callbackVar).toString('base64'),
    });

    console.log('result callback result:', completeRes.CallbackResult);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="458bca6a"></span>
## Relevant Documentation

For a detailed introduction to upload callback, please refer to [Upload Callback](https://docs.byteplus.com/docs/tos/Upload-callback).
