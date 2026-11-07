---
title: "Authentication configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-authentication-configuration-and-features"
---

The authentication logic determines the accessible features within the BytePlus Video Editor SDK. Specific permissions are required to utilize certain features.

<span id="002eba2b"></span>
# Authentication APIs

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The online authentication function is currently under development. We recommend opting for the offline authentication method instead.</div>



|**Class** |**Field and Method** |**Type** |**Description** |**Remarks** |
|---|---|---|---|---|
|EOAuthorizationConfig |isOnline |Boolean |The value `True` specifies using online authentication and the value `False` specifies using offline authentication. |N/A |
||isOversea |Boolean |The value `True` specifies using overseas authentication services and the value `False` specifies using authentication services in Chinese mainland. |N/A |
||licensePathForOffline |NSString\* |Specifies the absolute path of the offline certificate. |N/A |
||licenseTokenForOnline |NSString\* |Specifies the token of the online certificate. |N/A |
|EOAuthorization |* (instancetype)sharedInstance; |Method |Retrieves the `EOAuthorization` instance. |N/A |
||\-(void)makeAuthWithConfig:(EOAuthorizationConfig\*)config completionHandler:(EOAuthCompletionHandler)completionHandler; |Method |Implements authentication asynchronously. The result is retrieved using the completion handler `EOAuthCompletionHandler`. |N/A |
||**typedef void** (^EOAuthCompletionHandler)(**BOOL** success, NSString\* errMsg); |Typedef |Retrieves the authentication result. 'success' indicates whether authentication is successful. 'errMsg' contains error information if authentication fails. |Troubleshoot the error based on the error message or contact a technical support representative for assistance. |


<span id="7a6fc924"></span>
# Offline authentication

In offline authentication mode, the license is one of the deliverables and located in the `EOLocalResources\Resources\License\XXX.licbag directory`. Find this file and add it to the authentication logic when starting the app, as shown in the following sample code:

```Java

        let config = EOAuthorizationConfig { initializer in 
            //The Offline authentication method is used in this example.
            initializer.isOnline = false            
            //Configure the path of offline license file. 
            initializer.licensePathForOffline = //The path of the licence file. 
        }
        //Start authentication.
        EOAuthorization.sharedInstance().makeAuth(with: config) {isSuccess, errMsg in
            self.isAuthSucceeded = isSuccess
            //Print the error message when the authentication is not successful.
            if !self.isAuthSucceeded {
                print(errMsg)
            }
        }
    } 
```


For offline authentication, you need to manually update the offline license file.

<span id="061d3e5e"></span>
# Authentication error codes

These are the authentication error codes in Video Editor SDK.


|**Error Code** |**Value** |**Description** |
|---|---|---|
|`EO_AUTH_SUCCESS` |0 |Authentication successful. |
|`EO_AUTH_CONFIG_INCORRECT` |1 |Incorrect authentication parameters. |
|`EO_AUTH_FILE_NOT_FOUND` |2 |Certificate not found. |
|`EO_AUTH_FILE_TYPE_INCORRECT` |3 |Incorrect joint certificate type. |
|`EO_AUTH_FILE_VERSION_NOT_SUPPORT` |4 |Joint certificate version not supported. |
|`EO_AUTH_FILE_CONTENT_INCOMPLETE` |5 |Incomplete certificate file. |
|`EO_AUTH_EXPIRED` |6 |Certificate expired. |
|`EO_AUTH_SUBFILE_INVALID` |7 |Invalid sub\-certificate. |
|`EO_AUTH_ID_NOT_MATCH` |8 |Package name mismatch. |
|`EO_AUTH_NO_FUNC` |9 |Missing `funcid`. |
|`EO_AUTH_NETWORK_ERROR` |10 |Network error. |
|`EO_AUTH_GET_AUTHMSG_ERROR` |11 |Failed to retrieve auth message. |
|`EO_AUTH_MD5_CHECK_FAILED` |12 |Online certificate MD5 verification failed. |
|`EO_AUTH_BAD_OFFLINE_LICBAG` |13 |Offline certificate missing specific `funcid`. |
|`EO_AUTH_NOT_RENEWAL` |14 |Authentication not renewed. |
|`EO_AUTH_NOT_GET_DEVICE_ID` |15 |Failed to retrieve device ID. |
|`EO_AUTH_EXCEED_DEVICE_LIMIT` |16 |Device limit exceeded. |
|`EO_AUTH_UNKNOWN` |200 |Unknown error. |
