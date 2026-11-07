---
title: "Reference: Java SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Java_SDK_Integration_FAQ"
---

<span id="18ec5651"></span>
## SDK log

The logging of the SDK uses the slf4j interface to support logback and log4j logging. The package where you are located is: `com.datarangers`, you need to view the log, please configure the package log path. You can also view the logs under the package under the console.

First determine if there is an ERROR log, and check whether the startup parameters are configured as expected.

<span id="2ac6e194"></span>
## Use the SDK to report events, but the data cannot be found in the finder system

Check according to the following path:


1. First check the curl command provided by "How to use" \> "Verify configuration" to verify the basic configuration.

2. Check the version of the SDK and finally use the latest version; check the configuration save or mode to determine what mode is reported. When using FILE reporting mode, the data is only saved locally and is not reported.

3. Check the log for errors.

4. Check whether the reported event name conforms to the specification and whether the local_time_ms of the event is normal. If local_time_ms is a future data or is too old (more than 7 days old), it will be discarded.

5. You can check whether there is any abnormal data in "Data Management" \> "Data Quality".

6. Wait 5 minutes, refresh the page, and check if the metadata exists. When metadata exists, go to behavioral scrutiny or event analysis to query.

7. Contact the account manager.


<span id="a751012b"></span>
## The event was reported successfully, but the event property does not exist in the finder behavior review

Check according to the following path:


1. In "Data Management" \> "Event Properties", check whether the event property exists and whether the property type meets expectations.

2. Check whether there is a "number of abnormal attributes" in the reported event in "Data Management" \> "Data Quality".

3. Check whether the event property is an event property or a public event property in "Data Management" \> "Event Properties".

4. If the property is under the "any_event" event, it is the event public property, otherwise it is the event property.

5. When the event public attribute is reported, it is placed under the custom field of the header, that is, the custom parameter of the interface.

6. The event property is placed under params.


<span id="02206f3f"></span>
## SDK debugging

The core logic of SDK sending is `com.datarangers.asynccollector. Consumer #run ()`, HTTP sending logic, and finally use `com.datarangers.util. HttpUtils #request`to send. You can debug and debug in relevant places to further locate the problem.

<span id="e035b8f3"></span>
## SSL certificate configuration


* Certificate error: **PKIX path building failed: sun.security .provider.certpath**


This error is due to the lack of trust certificates in the local JDK. It is recommended that customers import certificates first.

Or configure: `datarangers.sdk.htpConfig.trustDisable = true`.


* Custom certificate path configuration


If the customer's certificate location is not in the default location and needs to be customized, you can configure the relevant parameters:

```Properties
#Enable certificate path custom configuration
datarangers.sdk.httpConfig.customKeyTrustEnable=true

#configure the keyMaterial path
datarangers.httpConfig.keyMaterialPath={keyMaterialPath}
#Configure keyword Password
datarangers.httpConfig.keyPassword={keyPassword}
#Configure storePassword
datarangers.httpConfig.storePassword={storePassword}
#Configure the trustMaterial path
datarangers.httpConfig.trustMaterialPath={trustMaterialPath}

#Trust strategy, only support self, all two
datarangers.httpConfig.trustStrategy=self
```
