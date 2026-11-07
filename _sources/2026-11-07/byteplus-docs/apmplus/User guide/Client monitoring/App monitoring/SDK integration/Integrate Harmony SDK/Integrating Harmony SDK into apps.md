---
title: "Integrating Harmony SDK into apps"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_Harmony_SDK_into_applications"
---

This topic introduces the detailed integration steps for the Harmony SDK. After integrating the SDK, you can use analysis features on the Server\-side Monitoring platform.

## **Considerations**

* The Harmony SDK is restricted to use in the Chinese mainland (excluding Hong Kong, Macao, and Taiwan).

* Calling the SDK initialization API does not collect user information. Calling the SDK startup API will begin collecting user information. Ensure that user authorization has been obtained before collecting user information according to [SDK privacy policy](https://docs.byteplus.com/en/docs/apmplus/The_SDK_privacy_policy).

## Demo description

[APMPlus_Harmony](https://github.com/volcengine/APMPlus_Harmony)

* The demo has integrated all of APMPlus's performance and stability monitoring capabilities.

* You can simulate some anomalies and performance data through the demo.

* You can configure it with your own AppID and AppToken and report data to the platform to test SDK features.

## **Step 1: Create a product**

1. Register an account on the  platform, and then create an application in the RUM console. For details, see [Integrating clients](https://docs.byteplus.com/en/docs/apmplus/Create_a_client_application).

   After creation is complete, you can see the AppID and AppToken on the platform.

2. After the product is created, you need to purchase events before you can view the reported data on the platform. For details, see [Activate RUM service](https://docs.byteplus.com/en/docs/apmplus/Activate_client_monitoring).

   You can contact online customer service on the BytePlus platform to apply for a trial. Provide the AppID to apply for a free trial quota.

## **Step 2: Obtain the SDK package and import dependencies**

#### Automatic integration (recommended)

Install the APMPlus SDK via `ohpm`.

```JSON
ohpm i @volcengine/apmplus@2.0.6
```

#### Manual integration

1. Obtain the har package from a third\-party repository or online customer service.

2. Copy the har package into the project, such as the `entry/libs` directory.

3. Add the offline har package dependency in the `oh-package.json5` file of the main entry module.

   ```Java
   "dependencies": {
       "@volcengine/apmplus": "file:./libs/apmplus.har"
   }
   ```

## **Step 3: Initialize the SDK and enable monitoring**

> **warning**

> No user personal information is collected during the SDK initialization stage.

1. Add the following code in the AbilityStage or the onCreate lifecycle of the Ability.

   ```JSON
   APMPlus.init(this.context);
   ```

2. Start monitoring and begin collecting data.

   > **warning**

   > Please call the method to collect data only after the user agrees to the privacy policy.

   ```Java
   APMPlus.setDeviceId("device_id");// OOptional. Set the device_id. If not set, the default device_id will be used. The updated value can be called at any time.
   APMPlus.setUserId("user_id");// Optional. User identifier with no default value. The updated value can be called at any time.
   
   let builder = new APMPlusBuilder("AppID", "AppToken");// Required
   builder.debug = true;// Optional. Configure output logs during the testing stage. They must be disabled for online release.
   builder.channel = "volcengine";// Optional. String type. Channel
   builder.startMonitor = true;// Optional. Whether to enable startup monitoring.
   builder.netMonitor = true;// Optional. Whether to enable network monitoring. HttpMonitor is required later for supplementary monitoring.
   builder.logRecovery = true;// Optional. Whether to enable custom Vlog retrieval
   
   APMPlus.start(builder);
   ```

   > **tip**

   > For instructions on obtaining the AppID and AppToken, see [How to query AppID and AppToken?](https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken)

3. The har package is in binary abc format. Check the project\-level `build-profile.json5` and set `useNormalizedOHMUrl` to `true`.

   ```Plain
   {
     "app": {
       "products": [
         {
            "buildOption": {
              "strictMode": {
                "useNormalizedOHMUrl": true
              }
            }
         }
       ]
     }
   }
   ```

## Step 4: Upload the symbol table (optional)

1. Add dependencies to `./hvigor/hvigor-config.json5` file in the project.

   ```JSON
   "dependencies": {
     "apmplus_upload": 'latest',
   }
   ```

2. Add the following code to `hvigorfile.ts` in the project.

   ```JSON
   import { ApmPlusPlugin } from 'apmplus_upload';
   
   const config = {
       aid : 1234, // The app ID of the application
       updateVersionCode : 1000000, // The number-type version code of the application
       api_key : 4321,// Go to All features -> symbol table management on the platform, select Android as the OS, and you can see the API key and token.
       api_token : 'xxxxxx'// Go to All features -> symbol table management on the platform, select Harmony as the OS, and you can see the API key and token.
   };
   
   export default {
       system: appTasks, 
       plugins:[ApmPlusPlugin(config)] 
   }
   ```
