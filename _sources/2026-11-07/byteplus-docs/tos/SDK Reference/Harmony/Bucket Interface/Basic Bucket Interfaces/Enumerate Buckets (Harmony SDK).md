---
title: "Enumerate Buckets (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-harmony-sdk"
---

Obtain the list of storage buckets (Bucket) using ListBuckets. You can list all storage buckets under all regions of the current account that meet the specified criteria.

<span id="69f4af4f"></span>
## Precautions


* Before listing buckets, you must have the `tos:ListBuckets` permission.

* The ListBuckets API returns all buckets in all regions for the current account.


<span id="1b85389e"></span>
## Sample Code

The following code is used to list all buckets across all regions for the current account.

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

async function main () {
  try {
    const res = await client.listBuckets();
    for (const bkt of res.Buckets) {
      console.log('the bucket name is: ', bkt.Name)
    }
  } catch (error) {
    handleError(error);
  }
}
main();
```


<span id="79dea9ce"></span>
## **Relevant Documentation**

For API documentation on listing buckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
