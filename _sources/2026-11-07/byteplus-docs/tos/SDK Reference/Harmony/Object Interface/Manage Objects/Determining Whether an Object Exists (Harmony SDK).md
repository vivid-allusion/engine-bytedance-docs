---
title: "Determining Whether an Object Exists (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Check-whether-an-object-exists-harmony-sdk"
---

You can determine whether an object exists through the Harmony SDK's `headObject` interface.

<span id="430dda2d"></span>
## Precautions

Before determining whether an object exists, your account must have the `tos:GetObject` permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

<span id="1d34831b"></span>
## Sample Code

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
    
    const objectKey = 'example_dir/example.txt';

    const res = await client.headObject({
      Bucket: bucketName,
      Key: objectKey,
    });
    console.log('The object exists.');
    console.log('headObject Request ID:', res.RequestId);
  } catch (error) {
    if (error instanceof TosServerError) {
      if (error.StatusCode === 404) {
        
        console.log(`The object doesn't exist`);
        return;
      }
    }

    handleError(error);
  }
}

main();
```


<span id="afe20b02"></span>
## **Relevant Documentation**

Regarding the API interface for determining whether an object exists, please refer to [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
