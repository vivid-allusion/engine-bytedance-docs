---
title: "Invocation Methods"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Invocation_Methods"
---

This document provides an overview of the overall OpenAPI invocation process, interface call limitations, and common error codes, with a focus on the required methods for applying for and using tokens during OpenAPI invocation。

<span id="daa2c33d"></span>
# Overall process


1. A client ID and client secret are generated for each OpenAPI caller; these serve as credentials for invoking the interface.

2. The user uses the client ID and client secret to call the interface and exchange for a JWT token containing user identity information.

3. When invoking business interfaces, the user should include the JWT token in the request header, for example: `Authorization: Bearer jwt_token`.

4. When the interface is called, DataWind uses a public key to verify the JWT token and performs rate limiting and auditing.

5. When invoking any DataWind interface, to facilitate troubleshooting, it is recommended to add both the 'x\-request\-id' and 'request\-id' headers (ensuring each is a unique string). Two headers are needed because DataWind consists of multiple components, and different components may use different identifiers. These two parameters will be recorded in DataWind's backend logs, providing strong support for analysis and troubleshooting when issues arise, thereby enabling more efficient resolution of potential faults.

6. Return business results


**The overall process is as follows:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a0287f6b8b849d59f1bfdcd6766d800~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-token申请接口"></span>
# Token application

<span id="076bfc9e"></span>
## Obtain client ID and client secret

Go to "Open Platform" \-\> "Developer Console", click "Create Credential" to apply for `client ID` and `client secret`. There are two types of credentials: user and system (system is only supported for system administrators). As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a80afe8f37d3451c8d695b45f597cac1~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c49234875064c44b1116cab9600f7ef~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/248afc2ba6d24eed8f53244cbbd7bbfb~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Be sure to properly and securely manage your <code>clientId</code> and <code>clientSecret</code>. These are the credentials for calling the interface. Exposing them to other users will result in a risk of data leakage.</div>


<span id="31310ff9"></span>
## Obtain JWT token

<span id="a8536f7e"></span>
### Request description

Request URL: The interface URL used for invocation varies by environment.


* For private deployment environments, the interface URL prefix is the same as the private environment access address.

* For Volcano Engine SaaS environments, if the access address is `https://console.volcengine.com/bi/datawind`, then the interface URL prefix is `https://console.volcengine.com/bi/datawind/aeolus`.


<span id="e6212cc2"></span>
### Request example

```JSON
curl --location --request POST 'https://console.volcengine.com/bi/datawind/aeolus/api/v3/openapi/jwtToken' \
--header 'Content-Type: application/json' \
--data-raw '{
  "metadata": {
    "clientId": "{clientId}",
    "clientSecret": "{clientSecret}",
    "proxyUser": "abc****@21**********",
    "expire": 3600
  }
}'
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you have opened the "Developer Console" \- "Credential Management" page, you can choose to directly copy the relevant request parameters provided below the credentials. You only need to replace clientId and clientSecret with the ones you obtained; the system has already filled in the proxyUser and expire parameters for you.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d802200080b54f209c690fc96b78ac99~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="ba9db4da"></span>
### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|clientId |integer |Required |123abc |Login credential ID, obtained in the previous step |
|clientSecret |integer |Required |123abc |Login credential key, obtained in the previous step |
|proxyUser |string |Optional |user_1 |The username corresponding to the token |
|expire |integer |Optional |3600 |The token expiration time. The default value is 3600 seconds.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The maximum token expiration time is 3 days</div><br> |


<span id="b5e61925"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|code |string |Return status code. If the request is successful, returns aeolus/ok. The following are error codes and their explanations:<br><br><br>* aeolus/openapiClient/tokenExpired: The token has expired<br><br>* aeolus/openapiClient/tokenError: The token is incorrect<br><br>* aeolus/openapiClient/requestRateExcess: The token call exceeds the frequency limit<br><br>* aeolus/openapiClient/blocked: The request has been intercepted |
|data |object |Contains the specific information returned by the interface, including jwtToken and proxyUser |
|data.jwtToken |string |Represents the user's identity information. When calling business interfaces, the user needs to include the jwtToken in the request header. |
|data.proxyUser |string |The username corresponding to the token |
|msg |string |A natural language description of the operation result |


<span id="c9e01aa9"></span>
### Response example

```JSON
{
    "code": "aeolus/ok",
    "data": {
        "jwtToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.ey*****************************************************************************************************************************************************************************.********************-*************************************************************************************-****************************************************************************************************************************-***-********************************************-******************************************************-*************************-****************************************************************************-************-*************************************-*********************************************************************************************************************************************************-****************-******************5sus",
        "proxyUser": "user_1"
    },
    "msg": "成功"
}
```


<span id="c41012f7"></span>
# Token usage

When invoking the interface, the user should include the content of the JWT token in the request header, for example: `Authorization: Bearer jwt_token`

The following is an example of invoking the current user interface using curl:

```sql
curl -X GET 'https://{domain}/aeolus/api/v3/open/misc/current_user' \
-H 'Authorization: Bearer jwt_token'
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In the above link, {domain} refers to the environment domain name</div>


   * <div data-tips="true" data-tips-type="tip">For private deployment environments, the address prefix used to call the interface is consistent with the private environment access address</div>


   * <div data-tips="true" data-tips-type="tip">For Volcano Engine SaaS environments, the interface address prefix is <code>https://console.volcengine.com/bi/datawind</code></div>


* <div data-tips="true" data-tips-type="tip">The clientId is not shared across different environments</div>



<span id="39594840"></span>
# Interface call limitations

To ensure service stability and prevent malicious attacks, the DataWind backend uses the following methods to limit requests:

(1) Rate limiting (the current external service capacity of the interface has reached a high level; if requirements are still not met, contact the Volcano Engine technical support team to request a modification);

(2) Blocking, used to reserve some APIs that are not open or to temporarily block abnormal user requests;

(3) Auditing, every openapi call will be recorded, including the caller, interface, parameters, and call time.

<span id="96b0bf26"></span>
# Common error codes

For details, see [Common Error Codes](https://docs.byteplus.com/docs/DataWind/Common_Error_Codes).
