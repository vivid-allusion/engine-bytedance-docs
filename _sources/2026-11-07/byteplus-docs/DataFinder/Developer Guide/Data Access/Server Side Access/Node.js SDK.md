---
title: "Node.js SDK"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Node_js_SDK"
---

DataFinder provides you with Node.js SDK, which is convenient for you to perform event tracking on some non\-web pages, such as Chrome plugins for event tracking and other scenarios. This article provides you with a hands\-on guide to Node.js SDK integration.

<span id="92c1d2d9"></span>
# Preparation

<span id="6e5d0593"></span>
## Get Appid


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="ebd7e57d"></span>
## Get the reporting address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to report and query the data normally in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="74f05166"></span>
### SaaS\-cloud\-native


|Address type |SaaS\-cloud native<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|Data reporting address<br><br>（channel_domain） |* channel_domain: https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* channel_domain: https://gator.uba.ap\-southeast\-1.bytepluses.com |* channel_domain：https://mcs.tobsnssdk.com |


<span id="822533e4"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying a private environment. If you do not know this address, please contact your project manager or customer success manager.

<span id="a826d4f3"></span>
# Integrated SDK

<span id="31ab5ac7"></span>
## Step1: Install the SDK

```JavaScript
npm i @datarangers/sdk-node 
npm i @datarangers/node-plugin-http
```


<span id="74236252"></span>
## Step2: Initialize the SDK

```JavaScript
import { DataRangersSDK } from "@datarangers/sdk-node"; 
import { httpPlugin } from '@datarangers/node-plugin-http'; 

const sdk = new DataRangersSDK({ 
    app_id: 1234, //Pass the appid of the applied item, which must be a number.
    logLevel: "verbose", //Turn on local chronology printing, the default value is silent
    }); 
```



|Parameter |Configuration instructions |
|---|---|
|app_id |Configure the app ID that is generated when you create an app on the DataFinder, see the Get Appid section above for details. |
|logLevel |To configure whether to enable local log printing, the enumeration values are as follows.<br><br><br>* "Verbose": full print<br><br>* "Error": only the error message is printed<br><br>* "Silent" (default): does not print the date |


<span id="510e5fde"></span>
## Step3: Set the data reporting address

After initializing the SDK, you need to set the data reporting address before you can report event tracking.

```JavaScript
sdk.use(
   httpPlugin(
     {
        channel_domain: "https://***.****.com" //Set the reporting domain name, and the reporting address of each environment is inconsistent. For details, please refer to the Get Reporting Address section above.
     }
   )
);
```


<span id="b732aa93"></span>
## Step4: Set public properties

When you need to set the login ID, or when there are global public properties, you can use config for configuration.

```JavaScript
sdk.config({
  user: {
    user_unique_id: "xxx", //Set the global user uuid
  },
  header: {
      os_name: 'xxx', //Set and modify public properties
  },
  custom: {
      key: 123 //Set custom public properties
  }
});
```


<span id="bfa2c3cc"></span>
## Step5: Reporting event tracking

<span id="f5bc60ca"></span>
### Report single event tracking

```JavaScript
//event tracking
sdk.collect(
  "event_1", //event tracking name
  {
    event_param_a: 123,   //event tracking properties
  }
);
```


<span id="75aa824b"></span>
### Bulk event tracking

Batch report event tracking, that is, pass in a buried array.

```JavaScript
//Bulk reporting event tracking
sdk.collect([
  {
    name: "event_2",
    params: {
      event_param_b: 234,
    },
  },
  {
    name: "event_3",
    params: {
      event_param_c: 567,
    },
  },
]);
```
