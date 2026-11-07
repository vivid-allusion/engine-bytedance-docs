---
title: "Managing Event Notifications (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-event-notifications-node-js-sdk"
---

If you want to keep track of resource changes in TOS in real time, you can set up event notification rules through the Go SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Only bucket Owners can create event notification services.

* Setting up event notifications relies on function services. You need to create and publish function services in BytePlus in advance.


<span id=".6K6-572u5LqL5Lu26YCa55-l"></span>
## **Set up event notifications**

The following code sets the event notification rule for the bucket.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const cloudFunctionConfiguration = {
      // Event notification name
      RuleId: 'TestNotification',
      // Events to subscribe to
      Events: ['tos:ObjectCreated:Put'],
      // Set prefix and suffix information for matching objects
      Filter: {
        TOSKey: {
          FilterRules: [
            {
              Name: 'prefix',
              Value: 'test-',
            },
            {
              Name: 'suffix',
              Value: '-ci',
            },
          ],
        },
      },
      // The function service for setting up subscription events, this parameter is required.
      CloudFunction: 'Provide the ID of your cloud function',
    };
    const { requestId: putNotificationRequestId } = await client.putBucketNotification({
      bucket: bucketName,
      cloudFunctionConfigurations: [cloudFunctionConfiguration],
    });
    console.log('putBucketNotification Request ID: ', putNotificationRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W5LqL5Lu26YCa55-l"></span>
## **Get event notifications**

The following code is used to obtain the event notification rule for the bucket.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const { data, requestId: getNotificationRequestId } = await client.getBucketNotification({
      bucket: bucketName,
    });
    console.log('getBucketNotification Request ID: ', getNotificationRequestId);
    console.log('CloudFunctionConfigurations Length:  ', data.CloudFunctionConfigurations.length);
    for (const conf of data.CloudFunctionConfigurations) {
      // Event notification name
      console.log('Cloud Function Configuration ID:', conf.RuleId);
      // Subscribed events
      console.log('Cloud Function Configuration Events: ', conf.Events);
      // Set prefix and suffix information for matching objects
      console.log('Cloud Function Configuration Filter: %o', conf.Filter);
      // Set function service for subscribing to events
      console.log('Cloud Function Configuration CloudFunction: ', conf.CloudFunction);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
