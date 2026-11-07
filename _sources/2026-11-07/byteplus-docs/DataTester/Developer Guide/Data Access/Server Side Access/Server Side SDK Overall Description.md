---
title: "Server Side SDK Overall Description"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Server-Side-SDK-Overall-Description"
---

<span id="一-概述"></span>
# Overview

<span id="_1-什么时候使用服务端sdk"></span>
## 1. When to use the server side SDK

In some scenarios, where the content of the experiment takes place almost on the back\-end service (e.g. feed stream recommendation policies, payment amount options, etc.), it is most appropriate to offload on the back\-end.

<span id="_2-「a-b测试」分流接口和用户行为上报"></span>
## 2. "A/B testing" diversion interface and user behavior reporting

A/B Testing provides separate Java, Python, PHP, Go, Node.js, and streaming agents at the server side for experimental streaming. After obtaining the diversion information, you can;


* Use the interface that comes with the official SDK to automatically expose the experiment; all subsequent user actions of the user will participate in the calculation.

* The server side dedicated interface in the RangerAppLog SDK reports the corresponding user behavior  **(with experimental ab_sdk_version)**  as experimental indicators. For specific information and sample code, please [refer to the documentation](https://www.volcengine.com/docs/6285/65984#_4-%E8%AF%B7%E6%B1%82%E7%A4%BA%E4%BE%8B).


<span id="dae32dda"></span>
## 3. Server side SDK configuration

> MetaHost address description for each environment



|Environment |MetaHost Configuration |Trackhost configuration |
|---|---|---|
|Privatization |Private deployment customers report the applied domain name for event tracking data, please replace it according to the actual domain name. ||


<span id="二-java-sdk"></span>
### Java SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please see the detailed documentation Java complete SDK introduction: <a href="https://docs.byteplus.com/docs/DataTester/Java-SDK">Java SDK</a>.</div>


<span id="三-python-sdk"></span>
### Python SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the complete introduction of the Python SDK, please see the detailed documentation: <a href="https://docs.byteplus.com/docs/DataTester/Python-SDK">Python SDK</a>.</div>


<span id="五-go-sdk"></span>
### Go SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please see the detailed documentation for the complete Go SDK introduction: <a href="https://docs.byteplus.com/docs/DataTester/Go-SDK">Go SDK</a>.</div>


<span id="六-分流-agent"></span>
### Traffic shunt agent

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For complete instructions on the use of the traffic shunt agent, please see the detailed documentation: <a href="https://docs.byteplus.com/docs/DataTester/Traffic-Shunt-Agent">Traffic Shunt Agent</a>.</div>


<span id="七-node-js-sdk"></span>
### Node.js SDK


1. Download the SDK

   Download address: [https://www.npmjs.com/package/@datatester/node-sdk](https://www.npmjs.com/package/@datatester/node-sdk)

2. Streaming with SDK

   In server side project engineering, the local fetch shunt code example is as follows:

   ```Plain
   const abClient = new AbClient("token")
   const attrs = new Map()
   attrs.set("key", "value")
   
   const config = testerClient.activate("key", "decisionId", "trackId", attrs, {val: "defaultValue"})
   const value = config.val
   if (value === 'xx') {
      // hit xx
   } else if (value === 'yy') {
       // hit yy
   } else {
       // undertake
   }
   
   // json type
   const jsonValue = JSON.parse(value)
   if (jsonValue['key']) {
    // 
   }
   ```
   


<span id="208dc101"></span>
# FAQ

<span id="51cf1c51"></span>
### How do server side SDK decision_id and track_id pass values?

decision_id: Local offload user ID, not for event reporting

track_id/trackId: Event reporting user ID, used for event reporting, needs to be replaced with the customer's real user ID

usage scenario description


* If server side experiments are all real\-name users, it is recommended that both decision_id and track_id use the user id (uuid).

* If there are anonymous users

   * At the same time, the client side SDK is integrated, and it is recommended that the decision_id be the ssid passed through the client side sdk;

   * If you simply integrate server side sdk, do server side sdk experiment, decision_id a unique identifier that can identify the user, such as device id.


<span id="e11fc53f"></span>
### How to obtain the metaHost and trackHost of the server side SDK, and what do they represent?

MetaHost: Obtain the meta information address, the private part is generally the system access address; trackHost: Data reporting address, generally there will be these two addresses in the deployment document provided after the system is deployed. If the corresponding document is not found, you can ask the project manager or volcano service personnel to obtain it.

<span id="63698888"></span>
### Is server side meta information stored? Where would the storage be located?

It will be stored in the service memory where the server side SDK runs. Meta information (including experimental name, version allocation, target audience, whitelist, etc.) is generally small and will not take up much memory. The server side meta information will be updated every 60s by default. This interval can be modified. If you want to modify it, you can modify it through setInterval api.

<span id="a1ce39bb"></span>
### Does server side sdk support offloading anonymous users?

Only the java, go, and php versions of the SDK support offloading anonymous users. Note that you need to strictly refer to the help documentation for anonymous user access instructions. Take java as an example for anonymous users, the trackid is an empty string, and you need to set the device id through the setDeviceId or setWebId methods.

```JSON
User user = new User.UserBuilder().create("decisionID", "") //trackId has a value to set the corresponding value, but no value to set the empty string.
        .setDeviceId(6981329701821561868L) Private deployment uses this method
        .setWebId(7018215618686981329L) //Web and Mini Programs use this method
        .build();
```


<span id="70bcb875"></span>
### What is the Meta Data (Meta Information) pulled by the server side SDK?

The server side SDK regularly obtains the latest experimental meta information from the remote Meta service, including experiment name, version assignment, target audience, whitelist, and so on.

<span id="4068bd1a"></span>
### How often does the server side SDK request the meta service to pull metadata?

Initialization will be requested once, and then it will be requested every 10s. This time interval can be customized through the API and used by referring to the setInterval method in the integration document.

<span id="e415b03f"></span>
### How to offload the server side SDK?

The server side SDK is a local offload. During initialization, it will obtain the latest experimental meta information from the Meta service, including experimental name, version allocation, target audience, whitelist, etc., and then offload in real time when calling the active interface.

<span id="8725d51c"></span>
### **How to use Redis to implement group\-in\-group\-not\-group logic?** 

Please refer to the integration example below, redis implementation

```JSON
/**  Implement the UserAbInfoHandler interface and implement the methods declared in the interface  * Enter the group but not the group, Redis realizes it.  */
public class NotOutGroupRedisImplement implements UserAbInfoHandler {
    /**          * Store offload results          * @param userId          * @param hashMap shunt result parameter and value, key = shunt parameter, value = corresponding version identifier          *  @return     */
    @Override
    public boolean createOrUpdate(String userId, HashMap<String, String> hashMap) {
        long res = 0 ;
        for (Map.Entry<String, String> entry : hashMap.entrySet()) {
             res = JedisUtils.getJedis().hset(userId, entry.getKey(), entry.getValue());
        }
        return res > 0 ;
    }
    /**          * Query the group corresponding to the user          *  @param userId          * @return The shunt result corresponding to the user key = shunt parameter, value = the identification of the corresponding version          */
    @Override
    public HashMap<String, String> query(String userId) {
        Map<String, String> resMap = JedisUtils.getJedis().hgetAll(userId);
        return (HashMap<String, String>) resMap;
    }
}
```


Configure the logic of inbound and inbound groups in AB split code

```Java
AbClient abClient = new AbClient.Builder(appKey).build();
NotOutGroupRedisImplement notOutGroupHandler = new NotOutGroupRedisImplement();
abClient.setUserAbInfoHandler(notOutGroupHandler);
Variable variable1 = abClient.activate("variantKey", user, defaultValue);
java
```


<span id="766e26a9"></span>
### What is the impact of the network disconnection of metahost and trackhost?

The metahost network is interrupted, resulting in the inability to synchronize to the latest experimental information, and what has been obtained is not affected (there is a local cache)

The TrackHost network is interrupted, which will cause the event reporting to fail. The streaming can be successful, but the server side cannot receive the incoming group information.

<span id="dcbed7f6"></span>
### Can metahost and trackhost configure IP without a domain name?

You can configure IP, but you need to match the port when configuring IP.

<span id="b93fe0a7"></span>
### Report the event data through the server side API, pass the data on the 13th on 7.14, and check the incoming group data on the same day, but there is no indicator data?

Upload data through the server side API, if the local_time_ms is the same day, the data is real\-time, if it is not the same day, the data is non\-real\-time, only write metadata, do not write in the real\-time table,and need to view the next day.

<span id="061fde93"></span>
### The getAllExperimentConfigs method of the server side SDK, described as "Get the variant details of all experiments hit by the user", does all experiments include both client side experiments + server side experiments?

The api provided by server side sdk can only handle server side experiments, that is, only the relevant data of server side experiments can be obtained.

<span id="23008e77"></span>
### How to test the data reporting address/trackhost fails?

Use the curl command to verify, you need to modify the appkey in the command (for the appkey of the application), the domain name xxx.com and local_time_ms the current timestamp.

Private deployment: use the data to report the address and domain name.

Attention: Note: When configuring trackHost, only the domain name is required, and the domain name should not end with "/".

```JSON
curl -X POST -H "Content-Type: application/json" -H "X-MCS-AppKey: appkey" -d '{"user":{"user_unique_id":"XXX"},"header":{"app_name":"xxx"},"events":[{"event":"predefine_pageview","params":"{}","local_time_ms":1630467848888}]}' https://XXXX.com/v2/event/json
```


<span id="1a1028fc"></span>
### If the same user hits multiple experiments, will the user information saved in Redis conflict?

No conflict. The data structure saved to Redis is a hash. The corresponding structure is:

Stream ID \- \> Experiment ID \- \> AB test VID

decisionID \-\> perimentId \-\> ab_vid
