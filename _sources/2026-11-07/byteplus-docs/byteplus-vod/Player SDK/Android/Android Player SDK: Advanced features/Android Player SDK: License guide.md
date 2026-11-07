---
title: "Android Player SDK: License guide"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-license-guide-android"
---

A license is a usage agreement between you and BytePlus VOD. To use the SDKs provided by BytePlus VOD, you must have a license. This article describes how to purchase, acquire, configure, and monitor licenses.

<span id="9746d558"></span>
## Acquire a license

You can acquire a license on the BytePlus VOD console. For details, see [SDK Management](https://docs.byteplus.com/en/byteplus-vod/docs/sdk-management).

<span id="9abddade"></span>
## Configure the license

To configure the license when initializing the SDK, see the following sample code:

```Java
// Pass in the address of the license when initializing the SDK
String vodLicense = "assets:///license/vod.lic";
Env.init(new Config.Builder()
        .setLicenseUri(vodLicense)
        // Other initialiation parameters
        .build();
```


<span id="6ab24192"></span>
## Monitor the license

After initializing the SDK, you can monitor the status of the license and the additional features. The status code indicates whether the license is available or expired. See the following sample code:

```Java
import com.pandora.ttlicense2.LicenseManager;
import com.pandora.ttlicense2.C;

// Check the status of the license
int vodLicenseResult = LicenseManager.checkSDKAuth(C.SDK.SDK_VOD_PLAY);

// Check the status of the additional features
int featureH265Result = LicenseManager.checkFeatureAuth(C.SDK.SDK_VOD_PLAY，C.Feature.FEATURE_BVC1);
```


The following table lists the status codes of the license:


|**Status code** |**Constant definitions in the SDK** |**Description** |
|---|---|---|
|0 |C.LicenseStatus.*LICENSE_STATUS_INVALID* |The license is invalid for one of the following reasons:<br><br><br>* The license file is invalid or tampered with.<br><br>* No license has been found, or the license address is incorrect. |
||||
||||
|1 |C.LicenseStatus.*LICENSE_STATUS_OK* |The license authentication has been passed. |
|2 |C.LicenseStatus.*LICENSE_STATUS_EXPIRED* |The license has expired. |
|401 |*C.LicenseStatus.LICENSE_STATUS_ERROR_PARAM_PACKAGE_NAME* |The actual application package name does not match the package name that you fill in when purchasing the license. |
|402 |*C.LicenseStatus.LICENSE_STATUS_ERROR_PARAM_FEATURE_NAME* |* The license does not cover the additional feature.<br><br>* The name of the additional feature is incorrect. |
||||
||||
|403 |*C.LicenseStatus.LICENSE_STATUS_ERROR_PARAM_MODULE_NAME* |The SDK enumeration pass error. |


The following table lists the status codes of the additional features:


|**Additional feature** |**Constant definitions in the SDK** |
|---|---|
|H.265 |C.Feature.*FEATURE_BVC1* |
|Client\-side super resolution |C.Feature.*FEATURE_SUPER_RESOLUTION* |


<span id="5f4468a9"></span>
## Handle license authentication failure

In essence, the license authentication failure may be due to one of the following reasons:


* The SDK authentication fails.

* The authentication of an additional feature fails.


In this case, the SDK cannot start playing the video and returns an error message in the `onError` callback. See the following sample code:

```Java
ttVideoEngine.setListener(new VideoEngineListener() {    
    // ...
    @Override
    public void onError(Error error) {
        Log.v("VideoPlay", "onError " + error);
        if (error.code == Error.LicenceFailed) {
            // internalCode indicates the reason for the authentication failure
            switch (error.internalCode) {
                case Error.h265CheckFailed:
                    // The authentication of the H.265 feature fails
                    break;
                case Error.DashCheckFailed:
                case Error.BashCheckFailed:
                    // The authentication of the DASH feature fails
                    break;
                default:
                    // The SDK authentication fails
                    break;
            }
        } else {
        
        }
    }
}
```


If you have enabled TTVideoEngineLog, logcat will output the logs, as follows:

```Plain
<TTVideoEngine>videoEngine failed:domain:kTTVideoErrorDomainVideoOwnPlayer, code:-30001, internalCode:0, description:version:null,10,Mi 10
        rom memory totle:114930200576,availe:72815374336
        ram memory totle:7806540,availe:2883304
        sdcard totle:114930200576,availe:72815374336
            error:play errorauth failed,authResult:0&&time:1616475725000
```


Pay attention to the following logs:


* **Code: \-30001** indicates the authentication fails. auth failed is the error message.

* **internalCode: 0** indicates the reason for the authentication failure.

   
   |**Error code** |**Constant definitions in the SDK** |**Description** |
   |---|---|---|
   |0 |Not applicable |The SDK authentication fails. |
   |\-310000 |Error.h265*CheckFailed* |The authentication of the H.265 feature fails. |
   |\-310001 |Error.*DashCheckFailed* |The authentication of the DASH feature fails. |
   |\-310002 |Error.*BashCheckFailed* ||
   

* **AuthResult: 0** indicates that the authentication result is 0. According to the table in the [Monitor the license](https://docs.byteplus.com/docs/byteplus-vod/docs-license-guide-android#6ab24192) section, 0 means that the license is invalid for one of the following reasons:

   * The license file is invalid or tampered with.

   * No license has been found, or the license address is incorrect.


In most cases, when the license authentication fails, you can troubleshoot according to the error messages. Pay special attention to the validity period of your license. We suggest that you renew the license on the BytePlus VOD console two months before the license expires.
