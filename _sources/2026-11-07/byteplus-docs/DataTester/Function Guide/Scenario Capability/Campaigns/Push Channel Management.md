---
title: "Push Channel Management"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Push-Channel-Management"
---

<span id="_1-概述"></span>
# 1. Overview

Push operations currently support the following access methods:


* App Push：

   * JPush

   * GeTui push

   * Umeng push/UPush

* Webhook: can connect to own or other access channels

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">4.9.0 version has added Webhook access methods that support custom interface types.   </div>
   

More ways to reach them will be released one after another.

<span id="_2-app-push"></span>
# 2. App Push

<span id="_2-1-极光推送"></span>
## 2.1 JPush

To use JPush for user access, you need to follow the following steps to complete the configuration of the JPush channel:


1. Prepare your JPush account, if not, please register or buy in advance;

2. Configure your JPush account in "Push Channel Management/JPush Channel";

3. Integrate the SDK of JPush in the App, obtain the RegistrationID of JPush and report it to BytePlus through the AppLog SDK;


<span id="_2-1-1-准备极光推送账号"></span>
### 2.1.1 Prepare JPush account

JPush has a free version and a paid version. If you want to use the push channel of Huami OV and other manufacturers, please buy the paid version.

<span id="_2-1-2-配置极光推送通道"></span>
### 2.1.2 Configure the JPush channel

Enter "Engagement/Campaigns/Push Channel", edit the AppKey, MasterSecrect and other information of the JPush account, enter the account number, and open it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31a79a1c91364d2a9a117b41e8e25a71~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92874934161b485fb43ff7832a5e2b58~tplv-goo7wpa0wc-image.image" width="600px" /></div>



* If you want to use the manufacturer's push channel or push report function (requires an JPush VIP account), please check the box in the configuration interface.

* The channel call frequency can be configured. Please fill in the threshold for your JPush service activation (the range is between 50\-10000, if the input value exceeds the range, it will be set to 10000). If JPush ordinary customers recommend 600, JPush VIP customers recommend 1200. If you need to increase the threshold, you can contact your JPush business.

   * If the set push rate exceeds the threshold of the channel (or vendor channel), some push failures may occur.

   * A single call supports pushing multiple users (it will be adjusted according to the user push level, and the upper threshold is 1000).


<span id="_2-1-3-在极光后台配置发送回执（可选，需要极光vip账号）"></span>
### 2.1.3 Send a receipt in the background configuration of JPush (optional, JPush VIP account is required.)

If you are using a JPush VIP account and want to enable the push reporting function, you need to configure the receipt URL in the background of JPush.

Enter the JPush background/receipt management, and set the delivery receipt and click receipt to:

```Plain
https://abtest.volceapplog.com/PushCallback/api/v1/JPush/{AppId of DataRangers app}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dd90a4b26cc43c09803166ff2fa26eb~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-4-集成极光推送sdk并获取registrationid"></span>
### 2.1.4 Integrate Jiguang Push SDK and get RegistrationID

For the integration process of JPush SDK, please refer to the official documentation of JPush:


* [JPush Android SDK Integration](https://docs.jiguang.cn/en/jpush/client/Android/android_guide)

* [JPush iOS SDK integration](https://docs.jiguang.cn/en/jpush/client/iOS/ios_guide_new)


Then, you need to write code to get the RegistrationID of JPush and report it to the BytePlus side as jpush_registration_id public property through the AppLog SDK.

Android code example:

```Plain
String resistrationId = JPushInterface.getRegistrationID (this);
HashMap<String,Object> param = new HashMap<String,Object> ();
param.put ("jpush_registration_id",resistrationId);
//SaaS
AppLog.setHeaderInfo (param);
//private deployment
AppLog.profileSet(params);
```


iOS code example:

```Plain
[JPUSHService registrationIDCompletionHandler:^(int resCode, NSString *registrationID) {
    if(resCode == 0){
      NSLog(@"registrationID successfully obtained：%@",registrationID);
      //saas
      [BDAutoTrack setCustomHeaderBlock:^NSDictionary<NSString *,id> * _Nonnull{
        return @{@"jpush_registration_id":registrationID};
      }];
      //private deployment
      [BDAutoTrack profileSet:^NSDictionary<NSString *,id> * _Nonnull{
        return @{@"jpush_registration_id":registrationID};
      }];
    }
    else{
      NSLog(@"registrationID obtain failed，code：%d",resCode);
    }
}];
```


<span id="_2-2-个推推送"></span>
## 2.2 GeTui push

To use a GeTui to reach users, you need to follow the following steps to complete the configuration of the GeTui channel:


1. Prepare your personal GeTui account, if not, please register or buy in advance;

2. Configure your personal GeTui account in "Push Channel Management/GeTui Push Channel";

3. Integrate the SDK of the GeTui in the App, get the ClientID of the GeTui and report it to the BytePlus side through the AppLog SDK;


<span id="_2-2-1-准备个推推送账号"></span>
### 2.2.1 Prepare a GeTui account

There are free and paid versions of GeTui push. If you want to use the push reporting function, please purchase the paid version.

<span id="_2-2-2-配置个推推送通道"></span>
### 2.2.2 Configure a GeTui channel

Enter "Engagement/CampaignsPush Channel Management", edit the AppID, AppKey, MasterSecrect and other information of the GeTui account, enter the account, and open it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9671624b8a0341228c47784e37dec911~tplv-goo7wpa0wc-image.image) </span>

If you want to use the push report function (you need a GeTui VIP account), please check the box in the configuration interface.

<span id="_2-2-3-配置个推的发送回执"></span>
### 2.2.3 Configure a GeTui send receipt

If you use a VIP account and want to activate the GeTui reporting function, you need to contact customer service of the GeTui to configure the receipt URL.

The receipt URL is set to:

```Plain
https://console.volcengine.com/PushCallback/api/v1/GeTui/{AppId of DataRangers app}
```


<span id="_2-2-4-集成个推推送sdk并获取clientid"></span>
### 2.2.4 Integrate GeTui SDK and get ClientID

For the integration process of the GeTui SDK, please refer to the official documentation of GeTui:


* [Android SDK integration](http://docs.getui.com/getui/mobile/android/androidstudio/)

* [iOS SDK integration](http://docs.getui.com/getui/mobile/ios/xcode/)


Then, you need to write code to get a ClientID of the GeTui and report it to the BytePlus side as getui_client_id public property through the AppLog SDK.

Android code example:

```Plain
String resistrationId = com.igexin.sdk.PushManager.getInstance().getClientid (this);
HashMap<String,Object> param = new HashMap<String,Object> ();
param.put ("getui_client_id",resistrationId);
//SaaS
AppLog.setHeaderInfo (param);
//private deployment
AppLog.profileSet(params);
```


iOS code example:

```Plain
//SaaS
[BDAutoTrack setCustomHeaderBlock:^NSDictionary<NSString *,id> * _Nonnull{
        return @{@"getui_client_id":GeTuiSdk.clientId};
}];
//private deploymentte deployment
[BDAutoTrack profileSet:^NSDictionary<NSString *,id> * _Nonnull{
        return @{@"getui_client_id":GeTuiSdk.clientId};
}];
```


<span id="_2-3-友盟推送"></span>
## 2.3 Umeng push

To use Umeng Push(UPush) for user reach in the growth analysis platform, you need to follow the following steps to complete the configuration of the Umeng channel:


1. Prepare your friendly push account, if not, please register or buy in advance;

2. Configure your Umeng account in "Push Channel Management/Umeng Push Channel";

3. Integrate the SDK pushed by Youmeng in the App, obtain the RegistrationID of Youmeng and report it to BytePlus through the AppLog SDK;


<span id="_2-3-1-准备友盟推送账号"></span>
### 2.3.1 Ready to push the account

Youmeng Push has a free version and a Pro version. If you want to use the push reporting function, please buy the Pro version.

<span id="_2-3-2-配置友盟推送通道"></span>
### 2.3.2 Configure the Umeng push channel

Enter "Engagement/CampaignsPush Channel Management", edit the Youmeng account AppKey, MasterSecrect and other information, click Save, and open the Youmeng push channel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46d3853e6f3b47079041a393308706ef~tplv-goo7wpa0wc-image.image) </span>

If you want to use the push reporting function (U\-Push Pro account required), please check the configuration screen.

<span id="_2-3-3-集成友盟推送-sdk-或-api-并获取-devicetoken"></span>
### 2.3.3 Integrate the Umeng to push the SDK or API and get DeviceToken [#](https://www.volcengine.com/docs/6285/65977#_2-3-3-%E9%9B%86%E6%88%90%E5%8F%8B%E7%9B%9F%E6%8E%A8%E9%80%81-sdk-%E6%88%96-api-%E5%B9%B6%E8%8E%B7%E5%8F%96-devicetoken)

For the configuration process of Youmeng Push SDK, please refer to the official document of Youmeng:


* [Android SDK Integration Documentation](https://developer.umeng.com/docs/67966/detail/153908)

* [iOS SDK Integration Documentation](https://developer.umeng.com/docs/67966/detail/66734)

* [API Integration Documentation](https://developer.umeng.com/docs/67966/detail/68343)


You need to obtain the DeviceToken of the Umeng and pass it to the SDK of DataRangers as `upush_device_token`public property.

> deviceToken is the id generated by the [Umeng +] push notification to identify the device, with a length of 44 bits and cannot be customized or modified. DeviceTokens corresponding to different applications on the same device are different.


* [Get DeviceToken for Android](https://www.volcengine.com/docs/6285/65977)

* [Get DeviceToken above iOS13](https://developer.umeng.com/docs/66632/detail/126489)


Android code example:

```Plain
String resistrationId = mPushAgent.getRegistrationId();
HashMap<String,Object> param = new HashMap<String,Object> ();
param.put ("upush_device_token",resistrationId);
//SaaS
AppLog.setHeaderInfo (param);
//private deployment
AppLog.profileSet(params);
```


iOS13 code example:

```Plain
#include <arpa/inet.h>
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    if (![deviceToken isKindOfClass:[NSData class]]) return;
    const unsigned *tokenBytes = (const unsigned *)[deviceToken bytes];
    NSString *hexToken = [NSString stringWithFormat:@"%08x%08x%08x%08x%08x%08x%08x%08x",
                          ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                          ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                          ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
    NSLog(@"deviceToken:%@",hexToken);
}
```


```Plain
//saas
[BDAutoTrack setCustomHeaderBlock:^NSDictionary<NSString *,id> * _Nonnull{
        return @{@"upush_device_token":hexToken};
}];
//private deployment
[BDAutoTrack profileSet:^NSDictionary<NSString *,id> * _Nonnull{
        return @{@"upush_device_token":hexToken};
}];
```


<span id="_2-3-4-配置友盟的发送、点击回执"></span>
### 2.3.4 configure the sending and clicking receipt of the Umeng

If you are using a U\-Push Pro account and want to enable push reporting, additional configuration is required. For details, see the U\-Push Pro [integration documentation](https://developer.umeng.com/docs/67966/detail/130645).

The URL used by the DataFinder to receive the receipt is as follows, which must be assigned to `receipt_url`and left `receipt_type`blank.

```Plain
https://console.volcengine.com/PushCallback/api/v1/UPush/{AppId of DataRangers app}
```


<span id="_3-webhook"></span>
# 3. Webhook

In addition to using the Push and other common methods provided by the system to reach users, in actual operation, some more personalized reach channels (such as in\-app letters on websites) may also be used, or some personalized processing may be required before reaching them (such as adding a red envelope to the customer's account before sending the Push).

In order to help you connect with these own or personalized touch channels, the system provides a Webhook interface docking method. When the touch is executed, your service interface will be notified by a callback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since the 4.9.0 version, the Webhook channel supports <strong>standard interface access</strong> and <strong>custom interface access</strong> (new).</div>


<span id="c0f9a7c1"></span>
## 3.1 Custom interface access

<span id="c0a0e3a3"></span>
### 3.1.1 Create custom interface access

When creating a new webhook channel, select the access method as custom interface access. The configuration details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8aa5f90db8e24142b2fcf0aa920250ac~tplv-goo7wpa0wc-image.image) </span>


1. Configure Webhook docking related parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5036570dddb54ba29d49c8227f91a0ec~tplv-goo7wpa0wc-image.image) </span>

   
   |Core configuration item |Configuration instructions |
   |---|---|
   |Request address |Configure the Webhook URL address for distribution. Format example: `http://localhost:6666/payload`. It can be supported starting with http/https. |
   |Authentication Mode & Authentication Related Configuration |According to the authentication requirements of the access webhook access, configure whether signature authentication is required, as well as the signature algorithm, location and other information.<br><br>For example, the access webhook uses the md5_32 algorithm for signature authentication. You can select the corresponding signature algorithm and add the corresponding authentication signature Key selection to the header. When the subsequent DataTester accesses the webhook, it will carry the authentication information configured here in the header of the push message. The pseudo\-code generated by the signature is as follows:<br><br>```Python```<br>```#MD5/sha1/sha256 digest algorithm: Splice the key directly behind the message body for digest```<br>```sign = encrypt_algorithm(body + secret_key)```<br>``````<br>```# hmac sha256```<br>```sign = hmac_sha256(body, secret_key)```<br> |
   |Interface sending method |Support single sending and batch sending. When choosing batch sending, you need to set the upper limit of the number of IDs per sending (between 1 and 500). |
   

2. Configure message\-related parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/caca3b34a99e409eabd651803084d0c4~tplv-goo7wpa0wc-image.image) </span>

   
   |Core configuration item |Configuration instructions |
   |---|---|
   |Message ID mechanism |Select whether you need to generate a message ID as needed, and support the **AB platform to generate** a message ID or a **third\-party generated** message ID when using the message ID.<br><br><br>* AB platform generation: A message ID is automatically generated by DataTester.<br><br>   In this way, you need to configure the message ID parameter anywhere in Body, Header or Query, and set the **parameter type** to **reserved word**, and the **default value** is selected as **message ID**.<br><br>* Third\-party generation: Message IDs are provided by third\-party platform generation and returned by the webhook server level. In this way, you need to configure the message ID Jsonpath path of the response data, as shown in the following figure:<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/531cd7ba301b4154992a50908d3e6f7e~tplv-goo7wpa0wc-image.image) </span><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The message ID is mainly used to connect the sender and the receipt.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When sending, a message ID is generated/maintained for each message.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When reporting the receipt event through the receipt interface, you also need to bring the message ID, and DataTester will determine the task, batch, experimental version and other information based on the message ID, and report the data.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you choose not to generate a message ID, reporting receipt events will not be supported.</div><br> |
   |Body/Header/Query Configuration |According to the actual message sending needs, configure the parameters that need to be carried in the message Body, Header, and Query in the future. The configuration points are as follows:<br><br><br>* Be sure to have a user ID parameter, that is, the **parameter type** is a **reserved word** , and the **default value** is selected as **user ID**.<br><br>* If you need to generate a message ID, you must have a message ID parameter, that is, the **parameter type** is a **reserved word**, and the **default value** is selected as the **message ID**.<br><br>* Additional parameters can be added and configured as needed **parameter type**, **default value**, **whether required**.<br><br><br>The configuration example is as follows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ecb954f7d674280bcb24404feae6f0d~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If in the above steps, the <strong>interface sending mode</strong> is configured to <strong>batch</strong>, the parameters added in Header and Query only support parameters of <strong>constant</strong> type.</div><br> |
   |Success/failure response configuration |Configure the success and failure response rules of push notification respectively. The HTTP status code is required, and the content of the response body is optional. The configuration example is as follows:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc109ed8d8f841239431a7e3ef0e19be~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The judgment rules are as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If not configured success and failure: the default is based on <strong>whether the HTTP status code is 200</strong> to determine success or not.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The success and failure response rules are configured, and the decision logic is:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Success: As long as there is one success, it will be successful</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Failure: As long as there is one failure, it will fail</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Success rules take precedence over failure rules</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If neither the success nor failure rules match, success is considered if the success rule is not set, otherwise an unknown error is returned</div><br> |
   

3. Basic configuration.

   In order to avoid sending too many messages to the same user in a short period of time, you can configure the frequency control configuration for users to receive messages according to the interface prompts.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0227167c6840416eb71132d75248683b~tplv-goo7wpa0wc-image.image) </span>


<span id="fb414656"></span>
### Report 3.1.2 Receipt incident

If you need to collect receipt data statistics reports such as arrivals and clicks of custom webhook channels, you can report receipt events through the HTTP interface. It can be reported through the API of the following receipt event:

**Description**: Custom webhook channel receipt callback interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A maximum of 500 requests are reported.</div>


* <div data-tips="true" data-tips-type="warning">The request domain name is consistent with the HTTP API event tracking report, see <a href="https://www.volcengine.com/docs/6285/152564#_1-%E8%AF%B7%E6%B1%82%E6%8E%A5%E5%8F%A3">HTTP API</a>.</div>


* <div data-tips="true" data-tips-type="warning">The channel_id in the path below is the custom webhook channel ID, which can be obtained on the <code>channel configuration -webhook</code>page.</div>



**Path**：/datapush/receipt/api/v2/webhook/{channel_id}

**Method**：POST

**Request**：

```JSON
[
    {
        "message_id": "abc",  //Message ID
        "type": "click/show" //Indicates the type of message receipt, click: click show: delivery
    },
    ...
]
```


**Response:** 

```JSON
//http status code=200
{
    "code":0, //0-Success, other codes fail
    "message":""  //reason for failure
}
```


**Example of reporting:** 

```Plain
curl -XPOST -H "Content-Type: application/json" 'https://{your_sdk_domain}/datapush/receipt/api/v2/webhook/{channel_id}' -d '
[
    {
        "message_id": "abc",
        "type": "show"
    },
    {
        "message_id": "abc",
        "type": "click"
    }
]
'
```


<span id="f8063bb9"></span>
## 3.2 Standard interface access

Webhook interface provides single push, batch push two ways, the specific docking steps are as follows:


1. Create and configure a new webhook channel in the growth analysis platform.

2. Develop and launch webhook service interface.


<span id="_3-1-创建和配置webhook通道"></span>
### 3.2.1 Create and configure webhook channels

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/241e29c4f7b640e5a5892e46b041e88e~tplv-goo7wpa0wc-image.image) </span>

Enter "Analysis/Push Operation/Push Channel Management", switch to "Webhook", and click New Channel;

Channel name: Try to use a name that the operation and business personnel can directly understand, such as "Send in\-app letter".

The URL address of the callback: When the reach is executed, the growth analysis platform will call your service through this URL to actually execute the reach;

Enable aggregated batch push: confirm whether to use batch push method;

Parameter template: The parameter values that need to be configured when creating a task to use this channel; when the touch is executed, the platform will send the parameter values configured by the user to your service

Custom extension parameters: Customized channel passthrough parameters, similar to parameter templates, except that parameter values need to be set and cannot be configured when creating push tasks

<span id="_3-2-开发webhook服务接口"></span>
### 3.2.2 Development webhook service interface

<span id="_3-2-1-单次推送"></span>
#### Single push

On a single push, the growth analysis platform will call the webhook interface through the POST method, passing the data as follows:


* push_id: uuid used to identify a single message

* app_id: App ID

* Sign: Signature information for security verification

* Timestamp: message sending timestamp

* Task: Push task information:

   * task_id: push task id

   * task_name: push task name

   * channel_id: push channel id

   * channel_name: push channel name

   * push_experiment_id: Push the experimental id, only send it when pushing the experiment

   * push_experiment_name: Push the name of the experiment, only send it when pushing the experiment

* receipt_properties: Receipt attribute packaging, usually do not need to care about the internal details of this structure, when reporting receipt data, directly as the attribute map can be used

* Params: The name and value of the push parameter

   * The number and name of parameters are the same as the webhook channel definition

   * The value of the parameter is filled in by the operator when creating the activity

* user_info: the user id of the push message

* trigger_event: trigger conditions

   * Automatic push: The user event record related to this push task provides the context of the push;

   * Manual push: There is no such part, no need to deal with it.


An example of the request data for a webhook interface call is as follows:

```Plain
{ 
        "push_id":"882f7c1c-af41-4351-9ec1-04a574597055", // uuid used to identify a single message
        "app_id": "234901", // App ID
        "sign": "f67ebb5fac42feacdee69d77bb0314cf", // Verify signature information
        "timestamp":1606789775, // send timestamp
        "task":{ // push task information
                "task_id":100, // send task id
                "task_name":"test_push", // task name
                "channel_id":14,         // channel id
                "channel_name":"发优惠券", // channel name
                "push_experiment_id": 129103, // push experiment id
                "push_experiment_name": "老用户年终回馈实验" // push experiment name
            },
        "receipt_properties": { // The receipt property is packaged, and users usually do not need to care about the internal details of this structure. When sending the receipt message, it can be directly used as a property map.
            "push_id": "882f7c1c-af41-4351-9ec1-04a574597055",
            "user_unique_id" : "hulan@163.com",
            "push_config_id" : 231122, //Mandatory, task ID，number type
            "push_batch_id": 2311222343112, //Mandatory, push batch ID, number type
            "channel_id": 14, //Mandatory, webhook channel id for this push task
            "channel_type" : "webhook", //can be omitted, push channel type 
            "ab_version": "231892", // experiment version ID
            "push_experiment_id": 129103, //experiment ID  
            "task_unit_id":12  // Mandatory, push node ID  
         },       
        "params": { // parameter templates configured in webhook channel by users
            "action_type": "老用户反馈", // custom template parameter“action type”
            "bonus_type": "抵用金", // custom template parameter“bonus type”
            "count" : 200, // custom template parameter“money count”
            "content_message":"亲爱的${user_nickname} , 您好！\n\r老客户年终回馈，送您${count}元抵用券，给咱娃新年好课选起来咯！" 
         },

        "user_info":{ // user ID, custom user/public property information
            "user_unique_id": "hulan@163.com", // push user unique identifier
            "device_id": "EA7583CDA6678BC", // optional, user device ID 
            "ssid": "12345678901", //optional, user unique ID
            "user_nickname":"汤圆麻麻" // custom passthrough user public property 
        },   
         "trigger_time":{ // Manual time trigger condition. When the push task is automatically triggered, it is empty. Commonly used in webhooks to confirm the reach of C-end users and data preprocessing time.
          "trigger_type": 1, //Numerical. 1-push immediately, 2-scheduled but not routine, 3-scheduled routine. Other value can be discarded.
          "trigger_routine": "true", // whether routinely repeated send 
          "trigger_cycle": "daily", // If trigger_routine is false, this field does not appear. During routine push, the candidate values for this field are daily, weekly, and monthly.
          "trigger_weekday": "MON", // This field only appears when trigger_cycle is weekly, indicating the specific day of the week for the push. Multiple selections are allowed, separated by commas. The candidate values for this field are MON, TUE, WEDS, THU, FRI, SAT, SUN. For example, a value of "MON, FRI, SUN" indicates sending on Monday, Friday, and Sunday.
            "trigger_monthday": "1, 10, 20", // This field only appears when trigger_cycle is monthly, indicating the specific date of each month for the push. Multiple selections are allowed, separated by commas. The candidate values for this field are 1-31, for example, values of "1, 10, 20" indicate sending on the 1st, 10th, and 20th of each month.
          "trigger_timestamp": "9:00", // If trigger_routine is false, this field does not appear. During routine push, the field value format is HH:MM, indicating that the push was made at that time point.
         "trigger_datewindow"："2020/01/02-2021/05/20" // task send time window, format is “YYYY/MM/DD-YYYY/MM/DD”.
        }
         "trigger_events":{ // Record user event behavior sequence when automatic event flow is triggered.
        }
}
```


Webhook interface response specification requirements:

```Plain
{
    "code":200, // 200 indicates success, non-200 indicates failure.
    "message": "Success" // messages
}
```


<span id="_3-2-2-批量推送"></span>
#### Batch push

After enabling bulk push, the growth analysis platform will call the webhook interface through the POST method, and the request body is an **array** of the following structure:


* push_id: uuid used to identify a single message

* app_id: App ID

* Sign: Signature information for security verification

* Timestamp: message sending timestamp

* Task: Push task information:

   * task_id: push task id

   * task_name: push task name

   * channel_id: push channel id

   * channel_name: push channel name

   * push_experiment_id: Push the experimental id, only send it when pushing the experiment

   * push_experiment_name: Push the name of the experiment, only send it when pushing the experiment

* receipt_properties: Receipt attribute packaging, usually do not need to care about the internal details of this structure, when sending a receipt message or reporting arrival click data, directly as the attribute map can be used

* Params: The name and value of the push parameter

   * The number and name of parameters are the same as the webhook channel definition

   * The value of the parameter is filled in by the operator when creating the activity

* user_info: the user id of the push message

* trigger_time: manually push trigger conditions. Empty when the push task is automatically active.

* trigger_event: trigger conditions

   * Automatic push: The user event record related to this push task provides the context of the push;

   * Manual push: There is no such part, no need to deal with it.


An example of the request data for a webhook interface call is as follows:

```Plain
[    
    { 
        "push_id":"882f7c1c-af41-4351-9ec1-04a574597055", // uuid used to identify a single message
        "app_id": "234901", // App ID
        "sign": "f67ebb5fac42feacdee69d77bb0314cf", // Verify signature information
        "timestamp":1606789775, // send timestamp  
        "task":{ // push task information
                "task_id":100, // push task id
                "task_name":"test_push", // task name
                "channel_id":14,         // channel id
                "channel_name":"发优惠券", // 通道名称
                "push_experiment_id": 129103, // 推送实验id
                "push_experiment_name": "老用户年终回馈实验" // 推送实验名称
            },
        "receipt_properties": { // The receipt property is packaged, and users usually do not need to care about the internal details of this structure. When sending the receipt message, it can be directly used as a property map.
            "push_id": "882f7c1c-af41-4351-9ec1-04a574597055",
            "user_unique_id" : "hulan@163.com",
            "push_config_id" : 231122, //Mandatory, task ID，number type
            "push_batch_id": 2311222343112, //Mandatory, push batch ID, number type
            "channel_id": 14, //Mandatory, webhook channel id for this push task
            "channel_type" : "webhook", //can be omitted, push channel type 
            "ab_version": "231892", // 实验版本ID，推送实验使用
            "push_experiment_id": 129103, //实验ID，推送实验使用   
            "task_unit_id":12  // Mandatory, push node ID
         },       
        "params": { // parameter templates configured in webhook channel by users
            "action_type": "老用户反馈", // custom template parameter“action type”
            "bonus_type": "抵用金", // custom template parameter“bonus type”
            "count" : 200, // custom template parameter“money count”
            "content_message":"亲爱的${user_nickname} , 您好！\n\r老客户年终回馈，送您${count}元抵用券，给咱娃新年好课选起来咯！" 
         },

        "user_info":{ // user ID, custom user/public property information
            "user_unique_id": "hulan@163.com", // push user unique identifier
            "device_id": "EA7583CDA6678BC", // optional, user device ID 
            "ssid": "12345678901", //optional, user unique ID
            "user_nickname":"汤圆麻麻" // custom passthrough user public property 
        },   
         "trigger_time":{ // Manual time trigger condition. When the push task is automatically triggered, it is empty. Commonly used in webhooks to confirm the reach of C-end users and data preprocessing time.
          "trigger_type": 1, //Numerical. 1-push immediately, 2-scheduled but not routine, 3-scheduled routine. Other value can be discarded.
          "trigger_routine": "true", // whether routinely repeated send 
          "trigger_cycle": "daily", // If trigger_routine is false, this field does not appear. During routine push, the candidate values for this field are daily, weekly, and monthly.
          "trigger_weekday": "MON", // This field only appears when trigger_cycle is weekly, indicating the specific day of the week for the push. Multiple selections are allowed, separated by commas. The candidate values for this field are MON, TUE, WEDS, THU, FRI, SAT, SUN. For example, a value of "MON, FRI, SUN" indicates sending on Monday, Friday, and Sunday.
            "trigger_monthday": "1, 10, 20", // This field only appears when trigger_cycle is monthly, indicating the specific date of each month for the push. Multiple selections are allowed, separated by commas. The candidate values for this field are 1-31, for example, values of "1, 10, 20" indicate sending on the 1st, 10th, and 20th of each month.
          "trigger_timestamp": "9:00", // If trigger_routine is false, this field does not appear. During routine push, the field value format is HH:MM, indicating that the push was made at that time point
         "trigger_datewindow"："2020/01/02-2021/05/20" // task send time window, format is “YYYY/MM/DD-YYYY/MM/DD”
        }
         "trigger_events":{ // Record user event behavior sequence when automatic event flow is triggered.
        }
    },
    {},
]
```


Webhook interface response specification requirements:


* HTTP 200, Body is an empty array, all sent are considered successful;

* HTTP 200 has a Body, which considers that part of the transmission failed and returns detailed error information, which will generate a Response Body as shown in the following code;

* Non\-HTTP 200 status, considered all failed.


The response body for a request is as follows:

```Plain
[ 
    { "success": true },
    { 
        "success": false,
        "fail_reason": ".....",
      // 以下是receipt_properties中参数
        "push_id": "882f7c1c-af41-4351-9ec1-04a574597055",
        "user_unique_id" : "hulan@163.com",
        "push_config_id" : 231122, 
        "push_batch_id": 2311222343112, 
        "channel_id": 123, 
        "channel_type" : "webhook",
        "ab_version": "231892", 
        "push_experiment_id": 129103
     },
     ... 

]
```


<span id="_3-3-webhook安全校验"></span>
### 3.2.3 Webhook Security Verification

To make webhook interfaces more secure, you can perform security checks on webhook calls.

We provide a combination of signature + IP whitelist for verification.

<span id="_3-3-1-签名校验"></span>
#### signature verification

When you receive a webhook call request, you can use the sign parameter to verify the content of the request.

The verification method is as follows:

```Plain
sign = md5("【app_id】:【task_id】:【push_id】:【user_unique_id】:【timestamp】:【app_secret】")
```


Of which:


* app_id, task_id, push_id, user_unique_id, timestamp can be obtained from the webhook request;

* app_secret can be found in "Push Operation\ General Settings" (as shown below)


<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ae2ac50e733f828ae80be3423e6e5610) </span>

**Example:** 

If appsecret is 123456, the webhook request is:

```Plain
{
    "push_id":"882f7c1c-af41-4351-9ec1-04a574597055", // uuid
    "app_id": 165031,
    "sign": "f67ebb5fac42feacdee69d77bb0314cf",
    "timestamp":1606789775,
    "task":{ // send task information
        "task_id":100,
        "task_name":"test_push",
        "channel_id":14,
        "channel_name":"发优惠券"
    },
    "params":{ // push parameter
        "key1":"value1",
        "key2":2
    },
    "user_info":{ // user information
        "user_unique_id":"69826555537",
        "device_id":"3MYRAOL36CVIYK7EDREISWBIA36EQ26KTZOLJMOQIRAXV4VTV5YA01",
        "getui_client_id":"" // optional
    },
    "trigger_events":[ // trigger condition, only available for automatic activity
        {
            "time":1587626788, // event happen time
            "event_name":"gt_init_info",
            "params":{// event parameter
                "lev":131,
                "coin_left":392,
                "coin_type":"钻石",
                "scene_id":1003,
                "user":"1018908035",
                "scene_lev":2
            }
        },
        {
            "time":1587628681,
            "event_name":"gt_ad_button_click",
            "params":{
                "ad_position":"点位1",
                "ad_type":"激励视频",
                "ad_position_type":"双倍金币",
                "lev":154,
                "scene_id":1016,
                "code_id":101232,
                "user":"1018908035",
                "scene_lev":3
            }
        }
    ]
}
```


The final calculated sign is:

```Plain
sign = md5("165031:100:882f7c1c-af41-4351-9ec1-04a574597055:69826555537:1606789775:123456") = "f67ebb5fac42feacdee69d77bb0314cf"
```


If the sign you calculated is different from the sign in the webhook request, the request may be forged.

<span id="_3-3-2-ip白名单"></span>
#### IP whitelist

With BytePlus Growth Analytics SaaS Edition, webhook invocation requests are issued from the following Internet Protocol Address:


* 220.243.131.248

* 220.243.131.249

* 123.58.10.224

* 123.58.10.225


<span id="_3-4-webhook回执事件上报"></span>
### 3.2.4 Webhook Receipt Event Report

<span id="_3-4-1-服务端上报"></span>
#### Server level reporting

If you need statistical reports on receipt data such as arrival and click of the webhook channel, you can report the receipt event through the HTTP interface and add the receipt attribute. For reporting methods, please refer to the help document "Application Access \- Server Level Access \- HTTP API"). An example of the reporting address is:

```Plain
https://{your_sdk_domain}/v2/event/list
```


Events/properties are defined as follows:


|**Name** |**Is it preset?**  |**Is it necessary** |**Incidental Attribute** |**Description** |
|---|---|---|---|---|
|rangers_push_show |Yes |Yes |Use the properties in the receipt_properties |The message reaches the event reported by the user. Active event. |
|rangers_push_click |Yes |Yes |Use the properties in the receipt_properties |A reported event is triggered when a message is opened by the user. If the webhook docking system is a third\-party/self\-developed push system, this event tracking needs to be done on the customer's App side. Active event. |
|rangers_webhook_XXX |No |No |Use the properties in the receipt_properties |Customer\-defined webhook receipt success events, such as in\-app message sent successfully, coupon sent successfully, payment successful and other deep conversion events, are not required. |


Take rangers_push_show example of reporting an event tracking event:

```Plain
https://{your_sdk_domain}/v2/event/list

POST
header:
Content-Type: application/json
X-MCS-AppKey: your_app_key

body:

[{
        "events": [{
                "event": "rangers_push_show", //Contact event name, mandatory
                "params": "{
                    \"push_config_id\": 231122, //Mandatory, task ID, int 64 type.
                    \"push_batch_id\": 2311222343112, //Mandatory, push batch ID, int 64 type.
                    \"push_id\": \"21234\", //Message ID,string type
                    \"channel_id\": 123, //Mandatory, push channel ID, int 32 type
                    \"channel_type\": \"\",//push channel type，string type
                    \"ab_sdk_version\": \"\",//Mandatory, experiment vid，string type, corresponding to the ab-version field
                    \"$task_unit_id\": 231122,//Mandatory, push node ID, int32 type, corresponding to the task_unit_id field
                   }", 
                   "local_time_ms": 1608455325028, //Event millisecond timestamp, mandatory
                  }],
        "user": {
                "user_unique_id": "hulan@163.com", //Mandatory, request for user_unique_id field in user_info，string type
                "ssid": "12345678901", //ssid field in request body user_info, string type
                "bddid": "EA7583CDA6678BC", //saas use bddid field, report the device_id field in the request body user_info,string type
                "device_id": "EA7583CDA6678BC",//private deployment use device_id field，report the device_id field in the request body user_info,string type
        },
        "header": {
                "app_id": 234901, //Mandatory, app_id is mandatory，int32 type
                "ab_sdk_version": "", //Mandatory, experiment vid，string type, corresponding to the ab-version field           
        }
}]
```


Response return value:

```Plain
{
    "Type": "Web/Mp(MiniProgram)",    
    "e": 0,        // Is there an error? 0 indicates normal
    "message": "success",    // output results, success indicates success
    "sc": 1,        // number of successfully processed items
    "server_time": 1616587176    // server-side processing time
}
```


<span id="_3-4-2-客户端上报"></span>
#### Client side report

The client side reports the receipt data using event tracking sdk. The event reporting method is the same as other custom event tracking (refer to the integration method of each version of sdk: [Android SDK access ](https://www.volcengine.com/docs/6285/65980)). The events and attributes of the receipt data are defined as follows:


|Event name |**Attribute** |Description |
|---|---|---|
|rangers_push_show |push_config_id |Push task id, required |
||push_batch_id |Push batch id, strong need |
||channel_id |Push channel id, required |
||ab_sdk_version |Experimental version id, required |
||push_id |Message ID, not required |
||channel_type |Push channel type, not required |
||$task_unit_id |Strong demand, push node id |
|rangers_push_click |push_config_id |Push task id, required |
||push_batch_id |Push batch id, strong need |
||channel_id |Push channel id, required |
||ab_sdk_version |Experimental version id, required |
||push_id |Message ID, not required |
||channel_type |Push channel type, not required |
||$task_unit_id |Strong demand, push node id |


Take the Android SDK as an example: account login, event public properties, and user properties follow other event tracking without change. The demo of the reported message arrival (rangers_push_show) event is as follows:

```Plain
// take rangers_push_show(message arrived) for instance
// report event+params
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("push_config_id", 231122); //event property, push task id , mandatory
    paramsObj.put("push_batch_id",20); //push batch, mandatory
    paramsObj.put("push_id","21234");  //message id. optional
    paramsObj.put("channel_id",124);   //Mandatory, push channel ID
    paramsObj.put("channel_type","21234"); //push channel type，string type optional
    paramsObj.put("ab_sdk_version","21234"); //Mandatory, experiment vid，string type
    paramsObj.put("$task_unit_id",124);   //Mandatory, push node ID
} catch (JSONException e) { 
    e.printStackTrace();
}
AppLog.onEventV3("rangers_push_show", paramsObj);
```


<span id="_4-微信公众号推送（仅私有化部署支持）"></span>
# 4. WeChat official account push (only private deployment support)

<span id="_4-1-公众号接入"></span>
## 4.1 Access to official account

WeChat side access reference document [WeChat official account development access guide ](https://developers.weixin.qq.com/doc/offiaccount/Basic_Information/Access_Overview.html), fill in the callback server address URL, Token, EncodingAESKey and other information. The callback server address URL can be obtained through "Access WeChat official account" \- "Service URL".

Click on "Group Settings" \- "Data Management" \- "WeChat official account" to access the official account.


* Official account name: Access official account name.

* Official account AppID: Access the official account AppID on the WeChat side, which can be obtained on the "WeChat Public Platform \- Development \- Basic Configuration" page.

* Get access_token:

   * WeChat server: that is, obtain access_token from the official WeChat server.

      * Token: Access to the WeChat public platform to develop and fill in the Token.

      * Secret: AppSecret, available on the "WeChat Public Platform \- Development \- Basic Configuration" page.

   * Central control server: that is, get access_token from your central control server.

      * Central control server address.

      * access_token Parsing: Parsing access_token JSONPath expression from the return value, such as: $result.token .

* EncodingAESKey: EncodingAESKey filled in by accessing the WeChat public platform development.


<span id="_4-2-公众号推送"></span>
## 4.2 Official account push


* Official account template message


The WeChat official account template is configured in the background of WeChat open API. Existing templates can be selected for message configuration, and configuration jump actions are supported.


* Select official account: Select "Group Settings" \- "Data Management" \- "WeChat official account" module to access the official account.

* Template selection: The selected template can be configured in the WeChat open API background.

* jump action

   * Open H5: H5 jump link needs to be configured

   * Open Mini Program: You need to configure the Mini Program appID to jump to and its specific page path.

* WeChat user tag


Through this page, you can configure to modify the user's label in batches, and the label is created for the selected official account.


* Select official account: Select "Group Settings" \- "Data Management" \- "WeChat official account" module to access the official account.

* Labeling: Labeling users in batches.

* Unlabel: Unlabel users in batches.
