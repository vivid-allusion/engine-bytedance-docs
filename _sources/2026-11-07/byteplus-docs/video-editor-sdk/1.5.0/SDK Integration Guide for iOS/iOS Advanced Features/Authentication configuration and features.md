---
title: "Authentication configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-authentication-configuration-and-features"
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

<span id="d739c70a"></span>
# Online authentication

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The online authentication function is currently under development. We recommend opting for the offline authentication method instead.</div>


In online authentication mode, obtain a token based on the customer's geographic region and incorporate it into the authentication logic when launching the app, as demonstrated in the following sample code:

```Java

        let config = EOAuthorizationConfig { initializer in
            //Online authentication is used in this example.
            initializer.isOnline = true  
            //The oversea authentication service is used.
            initializer.isOversea = true           
            //Configure a token for online authentication.
            initializer.licenseTokenForOnline = //token
        }
        // Start the authentication.
        EOAuthorization.sharedInstance().makeAuth(with: config) {isSuccess, errMsg in
            self.isAuthSucceeded = isSuccess
            //Print the error message when the authentication is not successful.
            if !self.isAuthSucceeded {
                print(errMsg)
            }
        }
    } 
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For online authentication, the license file is automatically updated, eliminating the need for manual updates.</div>
