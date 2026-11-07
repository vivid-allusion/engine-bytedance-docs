---
title: "Restore Object (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Restore-objects-node-js-sdk"
---

Restore the archive object and the cold archive object. After recovery, the object can be obtained through the download object interface. Parameters allow you to specify different retrieval methods.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The first call to the RestoreObject interface returns 202. If the file is being restored, calling the RestoreObject interface again will return a 409 error. If the object has been restored, calling the RestoreObject interface again returns 200 OK.

* For buckets with multiple versions open, the specified version of the object can be restored by specifying the VersionId. If the VersionId is not specified, the current object is restored by default.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code is used to restore the object.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, TierType } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
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
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey
    const objectKey = '*** Provide your object key ***';

    const { requestId } = await client.restoreObject({
      bucket: bucketName,
      key: objectKey,
      days: 1,
      restoreJobParameters: {
        Tier: TierType.TierStandard,
      },
    });
    console.log('restoreObject Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```
