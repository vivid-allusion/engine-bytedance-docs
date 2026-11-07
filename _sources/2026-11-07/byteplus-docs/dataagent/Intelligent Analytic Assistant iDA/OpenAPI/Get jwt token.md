---
title: "Get jwt token"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Get_jwt_token"
---

This article introduces the overall process of obtaining tokens for OpenAPI calls, interface call restrictions and public error codes, and focuses on the necessary token application and use methods for OpenAPI calls .

<span id="309f3188"></span>
# Overall process


1. Generate a clientId and client secret for each OpenAPI caller, which are the credentials for calling the interface.

2. Users exchange JWT tokens containing user identity information using the clientId/client secret call interface.

3. When the user calls the service interface, the JWT Token is attached to the request header, for example: `Authorization: Bearer jwt_token`.

4. When the interface is called, IDA uses the public key to check the JWT Token gateway token to complete the inspection and audit of limited viewership.

5. When calling any IDA interface, in order to facilitate subsequent troubleshooting, it is recommended to add `x-request-id`and `request-id`(to ensure a unique string) to the request headers. Two headers are required because there are many IDA components as a whole, and the tags used between each component may be different. These two parameters are entered into IDA's back\-end logs, providing strong support for analyzing and locating problems when you encounter them, so as to more efficiently resolve possible failures.

6. Return business results.


**The overall process is as follows:** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4223552bc1ac4571bd40b1ad8862b54a~tplv-goo7wpa0wc-image.image" width="715px" /></div>


<span id="17fa271c"></span>
# Token Application

<span id="382cb893"></span>
## Get clientId and clientSecret


1. Create credentials.

   Enter the "open API" \- "Certificate Management" page, click "Create Certificate" to apply for `clientId`and `clientSecret`. The applied certificate types are divided into two types: user and system (only system admin is supported).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/480a0e47be064f13b16417031ade2366~tplv-goo7wpa0wc-image.image) </span>

2. You can copy the `clientId`and `clientSecret obtained by the application`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8e153eb8864433bb720c07dfea38353~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Be sure to properly and confidentially manage <code>clientId</code>and <code>clientSecret</code>, which are the credentials that call the interface, exposing it to other users will lead to data leakage risk.   </div>
   

<span id="13c40f95"></span>
## Get jwtToken

<span id="a6c7de6b"></span>
# Request description

Request address: The interface address used by the calling interface in different environments is different.


* If it is a private deployment environment, the calling interface uses the same address prefix as the private environment access address.


<span id="e6a9dceb"></span>
### Request example

```JSON
# Replace clientId and clientSecret
curl --location --request POST 'https://console.volcengine.com/aeolus/api/v3/openapi/jwtToken' \
-H 'Content-Type: application/json' \

-d '{
  "metadata": {
    "clientId": "{clientId}",
    "clientSecret": "{clientSecret}",
    "proxyUser": "abc****@21**********",
    "expire": 3600
  }
}'
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the user has opened the "Developer Background" \- "Credential Management" page, they can choose to directly copy the relevant request parameters provided below the credentials, just replace the obtained clientId and clientSecret, and the proxyUser and expire parameter systems have been filled in for you.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c6dbed2951e4c5d9a0e07c0ab9c090d~tplv-goo7wpa0wc-image.image" width="2858px" /></div>


<span id="9a97fd45"></span>
### Request parameters


|Name |Type |Is it required? |Sample value |Describe |
|---|---|---|---|---|
|clientId |string |Required |123abc |Login credential ID, obtained in the previous step |
|clientSecret |string |Required |123abc |Login credential key, obtained in the previous step |
|proxyUser |string |optional |user_1 |The username corresponding to the token.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This username is valid only for system type credentials.</div><br> |
|expire |integer |optional |3600 |Token expiration time, the default value is 3600, in seconds<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Token expiration time is up to <strong>3 days</strong> , which is 259,200 seconds</div><br> |


<span id="bbc076b9"></span>
### Return parameters


|Parameter |Type |Description |
|---|---|---|
|code |string |Return status code , if the request is successful, return aeolus/ok, the following is the error code and its explanation:<br><br><br>* aeoli/openapiClient/tokenExpired: token has expired<br><br>* aeoli/openapiClient/tokenError: token is incorrect<br><br>* Aeoli/openapiClient/requestRateExcess: token call exceeds frequency limit<br><br>* Aeoli/openapiClient/blocked: The request has been blocked |
|data |object |Contains the specific information returned by the interface, including jwtToken and proxyUser here. |
|data.jwtToken |string |On behalf of the user's identity information, the user needs to wear jwtToken in the request header when calling the business interface. |
|data.proxyUser |string |The username corresponding to the token |
|msg |string |Natural language description of operation results |


<span id="6ff7ce7b"></span>
### Back to example

```JSON
{
    "code": "aeolus/ok",
    "data": {
        "jwtToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.ey*****************************************************************************************************************************************************************************.********************-*************************************************************************************-****************************************************************************************************************************-***-********************************************-******************************************************-*************************-****************************************************************************-************-*************************************-*********************************************************************************************************************************************************-****************-******************5sus",
        "proxyUser": "user_1"
    },
    "msg": "成功" //success
}
```


<span id="e94c7853"></span>
# Token usage

The user needs to bring the content of jwtToken in the request header when calling the interface, for example: `Authorization: Bearer jwt_token`

An example of calling the current user interface using curl is as follows:

```shell
curl -X GET 'https://{domain}/aeolus/api/v3/open/misc/current_user' \
-H 'Authorization: Bearer jwt_token'
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The {domain} in the link above refers to the environment domain name</div>


   * <div data-tips="true" data-tips-type="tip">If it is a private deployment environment, the address prefix used by the calling interface is the same as the private environment access address</div>


* <div data-tips="true" data-tips-type="tip">The clientId is not interoperable between various environments</div>



<span id="a4550d37"></span>
# Interface call restriction

In order to ensure service stability and block malicious attacks, the IDA backend uses the following methods to restrict requests:

(1) limited viewership of (the current interface external service carrying capacity has reached a high level, if it still does not meet the needs, you can contact the BytePlus technical support team to apply for modification);

(2) Blocking, used to keep some closed APIs or temporarily ban users' abnormal requests;

(3) Audit, every OpenAPI call is recorded, including the caller, interface, parameters, and call time.

<span id="29a7e47f"></span>
# Common Error Code


|Error code |Error message |Explain |
|---|---|---|
|aeolus/openapiClient/tokenExpired |Token has expired | |
|aeolus/openapiClient/tokenError |Token is incorrect | |
|aeolus/openapiClient/requestRateExcess |Request frequency over limit | |
|aeolus/openapiClient/blocked |Request has been intercepted | |
|aeolus/validation/validationFailed |Interface parameter validation failed, parameters do not meet the check rules |request parameter error |
|aeolus/user/unauthorized |user has no permission |The user has no relevant resource permissions (dashboard, subscription). |
|aeolus/openapiClient/passwordNotMatch |clientId or secret or proxy user does not match | |


<span id="2f8dca17"></span>
# Set global variables

After setting the global variable, subsequent access verification OpenAPI interface does not need to be pasted repeatedly. For details, see [Set token and domain global variables](https://docs.byteplus.com/docs/dataagent/118663).
