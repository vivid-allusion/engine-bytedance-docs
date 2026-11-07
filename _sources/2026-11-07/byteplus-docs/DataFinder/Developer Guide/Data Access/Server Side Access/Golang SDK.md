---
title: "Golang SDK"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Golang_SDK"
---

<span id="_1-集成sdk"></span>
# 1. Integrated SDK

The Golang SDK has been open\-sourced, and the open\-source address is: [datarangers-sdk-go](https://github.com/volcengine/datarangers-sdk-go). It is recommended to use the latest version. ${version} indicates the version number of the SDK.

Download the SDK:

```go
go get github.com/volcengine/datarangers-sdk-go
```


Or update the local SDK:

```go
go get -u github.com/volcengine/datarangers-sdk-go
```


Or add sdk dependencies in go.mod:

```go
require (
   github.com/volcengine/datarangers-sdk-go ${version}
)
```


If ${version} is not passed, it indicates the latest version.

Go version requirement \> = 1.17.

<span id="_2-sdk-上报模式介绍"></span>
# 2. Introduction to SDK reporting mode

The Growth Analytics SDK supports multiple reporting modes, and you need to choose a usage mode first.


* HTTP mode, wide range of use, simple deployment, high QPS. The SDK reports directly through the HTTP interface.

* KAFKA mode (only supports privatization): suitable for the same network environment, simple deployment, high QPS, and high stability. The SDK reports directly through Kafka.



|Pattern |Usage scenario |Deployment complexity |Reliability |Performance reporting |Remarks |
|---|---|---|---|---|---|
|HTTP |Most scenarios can be used, and if the cross\-network latency is relatively high, batch mode can be used. |simple |high |High, support batch reporting |You can refer to the section "Best Practices" \-\- \> "Viewing Reporting Delays" to view the reported delays. |
|KAFKA |The same network, it is recommended to use this mode. |simple |very high |high |SDK version \> = 1.1.4, privatization version 4.1 (inclusive) is supported. |


It is recommended to use HTTP, and use logagent to report data that fails due to network jitter and other reasons.

<span id="_3-sdk-初始化"></span>
# 3. SDK initialization

The SDK needs to be initialized before use, and then reported using the interface it provides.

<span id="60d57b66"></span>
## Preparation: Get the data upload address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="253049c0"></span>
### SaaS\-cloud\-native


|SaaS\-cloud native environment<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|
|https://gator.uba.ap\-southeast\-1.bytepluses.com |* Report address: https://mcs.tobsnssdk.com<br><br>* OpenAPI Domain Name: https://analytics.byteplusapi.com |


<span id="fe49c867"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_3-1-使用配置文件进行初始化"></span>
## 3.1 Initialization with configuration files

It is recommended to use the configuration method for initialization

```go
package main

import (
   //introduce sdk
   sdk "github.com/volcengine/datarangers-sdk-go"
)

func main() {
   //Initialize, YAML_PATH replace with real configuration file
   sdk.InitByFile("{YAML_PATH}")
   
   //... interface call
   
   //Avoid the program from exiting immediately
   time.Sleep(60 * time.Second)
}
```


<span id="_3-1-1-http-模式"></span>
### 3.1.1 HTTP mode

Need to configure `sdk.mode = http`

<span id="83aef7cb"></span>
#### 3.1.1.1 SaaS\-cloud native configuration

```yaml
sdk:
  mode: http
  env: saas_native #Set up environment information as SaaS cloud native
#  logLevel: debug
http:
  addr: https://gator.volces.com  #Reported IP or domain name
appKeys:
  ${APP_ID}: ${APP_KEY}
#asyn:
#routine: 20 #It is recommended to be less than 1024, the number of concurrency
#  queueSize: 10240
```


Http.addr: Data reporting address, configure different addresses according to the access environment, see the above [Preparation: Get the data upload address](https://docs.byteplus.com/docs/DataFinder/Golang_SDK#60d57b66)section for details.

<span id="_3-1-1-2-私有化配置"></span>
#### 3.1.1.2 Configuration of privatization

```yaml
sdk:
  mode: http
#  logLevel: debug
http:
  addr: ${SDK_DOMAIN} #For the reported IP or domain name, please add http://or https://.
#  timeout: 30 # secenods
#asyn:
#routine: 20 #It is recommended to be less than 1024, the number of concurrency
#  queueSize: 10240
```


If the cross\-network latency is relatively large, or the pursuit of higher QPS, batch reporting can be initiated.

```yaml
batch:
  enable: true
#  size: 20
#  waitTimeMs: 100
```


<span id="71adecb7"></span>
### 3.1.2 KAFKA mode

**This model is only supported in privatization**

Set `sdk.mode = kafka`

```yaml
sdk:
  mode: kafka
kafka:
#Kafka brokers, if there are multiple, configure multiple
  kafka_brokers:
    - 127.0.0.1:9192
```


<span id="_3-2-直接在程序中进行初始化"></span>
## 3.2 Initialization directly in the program

Customize `sdk. SysConf`, then initialize

```go
package main

import (
   sdk "github.com/volcengine/datarangers-sdk-go"
)

func main() {
   //Initialize and set relevant parameters
   sysconf := &sdk.SysConf{
      ... 
   }
   sdk.InitBySysConf(sysconf)

   //Avoid the program from exiting immediately
   time.Sleep(60 * time.Second)
}
```


<span id="_3-2-1-http-模式"></span>
### 3.2.1 HTTP mode

<span id="7179b79a"></span>
#### 3.2.1.1 SaaS\-cloud native initialization

```go
import (
   sdk "github.com/volcengine/datarangers-sdk-go"
)

sysconf := &sdk.SysConf{
   //setting mode
   SdkConfig: sdk.SdkConfig{
      Mode: sdk.MODE_HTTP,
      Env:  sdk.ENV_SAAS_NATIVE,
   },
   //Set domain and appKey
   HttpConfig: sdk.HttpConfig{
      HttpAddr: "https://gator.volces.com",
   },
   //Multiple apps can be set, please replace them with real parameters.
   AppKeys: map[int64]string{
      int64(appId): os.Getenv("SDK_APP_KEY_1"),
   },
}
sdk.InitBySysConf(sysconf)
```


<span id="_3-2-1-2-私有化初始化"></span>
#### 3.2.1.2 Initialization of privatization

```go
import (
   sdk "github.com/volcengine/datarangers-sdk-go"
)

sysconf := &sdk.SysConf{
   //setting mode
   SdkConfig: sdk.SdkConfig{
      Mode: sdk.MODE_HTTP,
   },
   //Set the sdk domain, pay attention to replace it with real parameters here
   HttpConfig: sdk.HttpConfig{
      HttpAddr: os.Getenv("SDK_DOMAIN"),
   },
}
sdk.InitBySysConf(sysconf)
```


<span id="f8cb68dc"></span>
### 3.2.2 KAFKA mode

**This model is only supported in privatization**

Set `sdk.mode = kafka`

```go
import (
    sdk "github.com/volcengine/datarangers-sdk-go"
)

func main() {
    //initialize
    sdk.InitBySysConf(&sdk.SysConf{
       //setting mode
       SdkConfig: sdk.SdkConfig{
          Mode: sdk.MODE_KAFKA,
       },
       //Set the SDK kafka broker address, and replace it with real parameters. The broker format is usually ip: port, such as 127.0.0.1:9192
       KafkaConfig: &sdk.KafkaConfig{
          KafkaBrokers: []string{os.Getenv("SDK_KAFKA_BROKER_1"), os.Getenv("SDK_KAFKA_BROKER_2")},
       },
    })
}
```


<span id="_3-3-sdk-配置参考"></span>
## 3.3 SDK Configuration Reference


|**Configuration module** |**Configuration item** |**Meaning** |**Remarks** |
|---|---|---|---|
|sdk |mode |Reporting mode (case\-insensitive): http, ka. | |
||env |Enumeration type, pri means privatized environment, saas_native means SaaS\-cloud native, not necessary, sdk can automatically determine according to the configuration. | |
||logLevel |Log level, the default is trace. Support configuration:<br><br>trace, debug, info, warn, error, fatal | |
|asyn |routine |The number of core coroutines in the asynchronous coroutine pool, the default is 20. | |
||queueSize |Asynchronous queue size, default is 10240. | |
||waitTimeout |When the queue is full, the waiting timeout is set to 0 to indicate unlimited waiting. The unit of time is milliseconds | |
|http |addr |DataFinder's domain name or ip, supports http and https, for example https://{specific domain address}<br><br>In a SaaS\-cloud native environment, it is configured to:<br><br><br>* https://gator.volces.com | |
||timeout |HTTP timeout. | |
|batch |enable |Boolean type, indicating whether to enable bulk reporting. Default is false, do not use batch. |Only HTTP mode is supported. |
||size |The number of batch reports. ||
||waitTimeMs |Batch report, when the batchSize is insufficient, the maximum waiting time. ||
|file |path |The file directory where the log is saved needs to ensure the write permission of the file. The default is<br><br>logs/datarangers.log。 |Configuration in file mode; in http mode, messages that fail to report are recorded in `errPath`. |
||maxSize |The maximum number of individual files is 100m by default. ||
||maxBackup |The maximum number of backup files, which defaults to 0, indicates that all files are preserved. ||
||maxAge |The maximum number of days to save, the default is 0, indicating that all files will be preserved. ||
||errPath |Report failure to save the file directory of the log, you need to ensure the write permission of the file, the default is<br><br>logs/error\-datarangers.log。 ||
|kafka |kafka_brokers |Array format, kafka brokers address | |
||topic |Topic, the default is sdk_origin_event | |
||sync_kafka_producer_conf.required_acks |Synchronous mode, \-1: wait for all replicas 0: wait for local | |
||sync_kafka_producer_conf.retry_config.max |Maximum number of retries for message sending | |
||sync_kafka_producer_conf.flush_config.bytes |Message sent, more than the number of bytes forced flush | |
||sync_kafka_producer_conf.flush_config.messages |Message sent, force flush if the number of messages exceeds | |
||sync_kafka_producer_conf.flush_config.frequency_ms |Message sent, more than a period of time forced flush | |
||sync_kafka_producer_conf.flush_config.max_messages |Message sent, buffer maximum number of messages | |
|openapi |ak |OpenAPI ak, please contact the account manager to obtain. | |
||sk |OpenAPI sk, please contact the account manager to obtain. ||
|Does not involve |appKeys |SaaS\-cloud\-native environments, report the set appkeys, and you can set multiple. Several possible ways are:<br><br>```yaml```<br>```appKeys:```<br>```  ${APP_ID_1}: ${APP_KEY_1}```<br>```  ${APP_ID_2}: ${APP_KEY_2}```<br> | |


<span id="_3-4-验证配置"></span>
## 3.4 Verify the configuration

<span id="_3-4-1-查看启动日志"></span>
### 3.4.1 View the startup log

Startup prints the following log, which can be monitored to determine if the configuration is as expected. Mainly focus on `SdkConfig. Mode "," HttpConfig`and other configurations.

```plain
[DEBUG:]2023/02/27 15:54:20 user config :{"SdkConfig":{"Mode":"file","Env":"pri","LogLevel":""},"BatchConfig":{"Enable":false,"Size":0,"WaitTimeMs":0},"FileConfig":{"EventSendEnable":false,"Path":"logs/datarangers.log","MaxSize":100,"MaxBackup":0,"MaxAge":0,"ErrPath":"logs/error-datarangers.log"},"HttpConfig":{"HttpAddr":"","SocketTimeOut":0,"Headers":null},"AsynConfig":{"Routine":20,"QueueSize":10240},"OpenapiConfig":{"HttpAddr":"","Ak":"","Sk":""},"VerifyConfig":{"Url":""},"AppKeys":null}
```


<span id="_3-4-2-http-模式"></span>
### 3.4.2 HTTP mode

Refer to the HTTP mode method in "Authentication Configuration" in the "Java SDK" document.

<span id="8e3b7f56"></span>
### 3.4.3 KAFKA mode (only supports privatization)

Check the Kafka topic: `sdk_origin_event`if there is any data.

<span id="_4-使用sdk"></span>
# 4 Using the SDK

Before use, you need to initialize the SDK first. For initialization, refer to "SDK Initialization". After initialization, you can use the interface to report.

<span id="_4-1-接口"></span>
## 4.1 Interface

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the following interfaces, appType identifies the application type, which is currently only supported:</div>



* <div data-tips="true" data-tips-type="tip">App: Represents uploading data related to the mobile end of the app at the server level.</div>


* <div data-tips="true" data-tips-type="tip">Web: Represents uploading data related to the web side of the application at the server level.</div>


* <div data-tips="true" data-tips-type="tip">MP: means uploading data related to the application Mini Program at the server level.</div>



<div data-tips="true" data-tips-type="tip">See the description in the code comments for other interface parameters.</div>


```go
// SendEvent
//eventParam: event property
//custom: user custom event public properties
// Deprecated: instead of SendEventInfo
func SendEvent(appType AppType, appid int64, uuid string, eventname string, eventParam map[string]interface{}, custom map[string]interface{}, did ...int64) error

//SendEventInfo reports event information
//event: event information
//custom: event public property
func SendEventInfo(appType AppType, appId int64, uuid string, event *EventV3, custom map[string]interface{}) error

//SendEventInfoWithItem report the incident of carrying the item
//event: event information
//custom: event public property
//itemList: item information
func SendEventInfoWithItem(appType AppType, appId int64, uuid string, event *EventV3, custom map[string]interface{}, itemList []*Item) error

//SendEventInfos reports multiple events
//events: event information
//custom: event public property
func SendEventInfos(appType AppType, appId int64, uuid string, events []*EventV3, custom map[string]interface{}) error

//SendEventWithHeader uses header to report events
//header: the header of the event
//event: event information
func SendEventWithHeader(appType AppType, appId int64, hd *Header, event *EventV3) error

// SendProfile
//profileAction: user common property action type
//profileParam: user public property
func SendProfile(apptype AppType, appid int64, uuid string, profileAction ProfileActionType, profileParam map[string]interface{}, did ...int64) error 

//ItemSet the item properties
//itemName: item name
//itemParamList: item attribute information
func ItemSet(appid int64, itemName string, itemParamList []map[string]interface{}) error
```


<span id="_4-2-sdk-demo"></span>
## 4.2 SDK DEMO

SDK DEMO can be viewed in the open source example folder: [demo link](https://github.com/volcengine/datarangers-sdk-go/tree/main/_example).

<span id="_4-3-发送普通事件"></span>
## 4.3 Sending ordinary events

```go
//application id
appId := {APP_ID}
//user id
uuid := {uuid}
//event public property, if not needed, you can pass nil
commonParams := map[string]interface{}{
   "common_string1": "common_value1",
   "common_int1":    13,
}
eventName := "app_send_event_info"
eventV3 := &sdk.EventV3{
   Event:       eventName,
   Params: map[string]interface{}{
      "app_send_event_param1": "value1",
      "app_send_event_param2": "value2",
   },
}
sdk.SendEventInfo(sdk.APP, appId, uuid, eventV3, commonParams)
```


<span id="_4-4-设置用户属性"></span>
## 4.4 Setting user properties

```go
//application id
appId := example.AppId
//user id
uuid := example.Uuid
//user attributes
properties := map[string]interface{}{
   "list":      []string{"a"},
   "profile_a": "param_11",
}

sdk.ProfileSet(sdk.APP, appId, uuid, properties)
```


<span id="_4-5-设置item属性"></span>
## 4.5 Setting item properties

```go
//application id
appId := example.AppId

//item attributes
itemParamList := []map[string]interface{}{
   {"id": 121, "category": "economics"},
   {"id": 122, "category": "literature"},
   {"id": 123, "category": "fiction"},
   {"id": 124, "category": "fiction"},
   {"id": 125, "category": "fiction"},
}

err := sdk.ItemSet(appId, "book", itemParamList)
```


<span id="_4-6-发送携带item的时间"></span>
## 4.6 Time of delivery of carrying items

```go
//application id
appId := {APP_ID}
//user id
uuid := {uuid}
//event public property, if not needed, you can pass nil
commonParams := map[string]interface{}{
   "common_string1": "common_value1",
   "common_int1":    13,
}
eventName := "app_send_event_info"
//Event time
localTimeMs := time.Now().UnixMilli()
eventV3 := &sdk.EventV3{
   Event:       eventName,
   LocalTimeMs: &localTimeMs,
   Params: map[string]interface{}{
      "app_send_event_param1": "value1",
      "app_send_event_param2": "value2",
   },
}
sdk.SendEventInfo(sdk.APP, appId, uuid, eventV3, commonParams)
```


<span id="1614cc2a"></span>
## 4.7 Reporting anonymous user events

If you need to use the server to report anonymous user event information, you need to set the value of the user_unique_id to " (empty string), and then set other device information that can be associated, such as device_id, web_id, anonymousId. If the user logs in, they can get user_unique_id, and want to log in after the real name behavior can be associated with the behavior before the anonymous, then after setting the correct user_unique_id, but also need to bring the anonymous set of device_id, web_id.

When using `AppType = sdk.*APP*`, deviceId is device_id, when using `AppType = sdk. WEB`, `AppType = sdk.MP`, deviceId is web_id.

```Plain
appId := example.AppId
// set device_id
did := example.Did
// set uuid as ""
uuid := ""
// event public property
custom := map[string]interface{}{
    "common_param_1": "value_1",
}
// put in header
hd := &sdk.Header{
    Aid:          &appId,
    Custom:       custom,
    DeviceId:     did,
    UserUniqueId: &uuid,
}
// event occurrence time
localTimeMs1 := time.Now().UnixMilli()
// event property
eventParams := map[string]interface{}{
    "param1": "value1",
}
eventV3 := &sdk.EventV3{
    Event:        "go_sdk_send_with_header", //
    LocalTimeMs:  &localTimeMs1,
    AbSdkVersion: &[]string{"11,12"}[0],
    Params:       eventParams,
}
// report
sdk.SendEventWithHeader(sdk.APP, appId, hd, eventV3)
```


<span id="_5-注意事项"></span>
# 5 Precautions


1. If the server level can obtain the device information of users such as client_ip, device_model, etc., you can use the imported parameter to report the interface of the Header. Otherwise, by default, the public properties for the event are either null or unknown.

2. If you use `v1.1.0`, `v1.1.1`, and `v1.1.2`, the three versions have reported user attributes and need to be processed; if you only report events, you don't need to deal with them:

   a. Does not affect event reporting, only affects user properties

   b. If the SDK is not upgraded to the latest version, and user attributes are not reported in other ways, it can be ignored.

   c. If the SDK needs to be upgraded to the latest version `> = v1.1.3`, or use other methods to report data, you need to contact the account manager to process the data before the upgrade, otherwise the new user attribute report will not take effect.

3. When using the Golang SDK for data access, the event tracking real\-time verification function is not currently supported for access verification.
