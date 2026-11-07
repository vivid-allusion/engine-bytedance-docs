---
title: "Data Output Overview"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Data_Output_Overview"
---

DataFinder provides you with a data output function to push the buried data collected through the SDK to the target address in real time (such as your business data warehouse), meeting your needs to synchronize event tracking data to the data warehouse for flexible analysis (not applicable to scenarios with high timeliness requirements). This article provides you with an overview of the functional capabilities of the data output module and the operating procedures in each product environment.

<span id="4c11f294"></span>
# Precautions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current data output function of DataFinder is mainly suitable for scenarios where data is synchronized to your data warehouse for secondary analysis. For scenarios with high real\-time requirements, it is not recommended to build a data processing flow based on DataFinder's real\-time data output function. That is, DataFinder's data output function currently does not guarantee the timeliness of data push, and there may be problems such as delay and data duplication caused by delay.</div>



|**Sub\-project** |**Limitation Notes: SaaS\-Cloud Native** |
|---|---|
|Function switch |To ensure the security of your and your users' data, the data output function is turned off by default. Before you start using it, you need to contact the administrator to open the data output module permission. |
|Data transmission method |SaaS\-cloud native: Only supports real\-time transmission of event tracking data to the target data source, and the data source type supports BytePlus Kafka, BMQ. |
|Geographical restrictions |SaaS\-Cloud Native: No geographical restrictions, currently supported in North China 2 (Beijing), South China 1 (Guangzhou), and Johor. However, it is important to note that if whitelisting is enabled on the receiving end, you need to add the DataFinder's Internet Protocol Address to the whitelist. |
|Feature fee |The data output usage quota needs to be purchased separately, and the final price is subject to the page display when purchasing and placing an order. |
|Account permission requirements |Your operation account needs to have the data output function permission of data management , see for authorized operation [Role Management](https://docs.byteplus.com/docs/DataFinder/Role_Management). |


<span id="390ea879"></span>
# Data output logic

<span id="77ad0870"></span>
# Operation guidance

<span id="f6fed559"></span>
# Data format description: Kafka/BMQ data source

The topic is a single piece of data json, and the data format example is as follows:

```JSON
{
    "user": {
        "user_unique_id": "9482854997",
        "device_id": 7582024008078508042,
        "open_udid": "ef9c4eb3f2a29926",
        "ssid": "1736106870031597563",
        "oaid": "6516326280"
    },
    "header": {
        "app_id": 20003079,
        "app_name": "rangers_2100208426_test_export",
        "app_version": "0.3.7",
        "app_package": "android.app",
        "app_channel": "自然激活", //register spontaneously
        "access": "3G",
        "client_ip": "180.164.79.156",
        "carrier": "T-mobile",
        "os_name": "android",
        "os_version": "2.3.4",
        "custom": "{\"platform_type\":\"ios\",\"age\":88,\"getui_client_id\":\"377488140166484\"}",
        "app_language": "zh_CN",
        "language": "en",
        "app_region": "China",
        "region": "China",
        "device_model": "Nexus S",
        "device_brand": "google",
        "resolution": "320*568",
        "timezone": 8,
        "tz_name": "Asia/Shanghai",
        "tz_offset": -28800,
        "platform": "android",
        "user_agent": "Dalvik/2.1.0 (Linux; U; Android 2.3.4; zh-CN; Nexus S Build/NRD90M)",
        "browser": "firefox",
        "browser_version": "66.0.5",
    },
    "params": "{\"duration\":0,\"is_background\":false,\"session_id\":\"7391c12f5f93254a0e5b3415f7dff1ea2bd7\",\"session_duration\":0}",
    "event_name": "app_launch",
    "session_id": "7391c12f5f93254a0e5b3415f7dff1ea2bd7",
    "server_time": 1724652079,
    "log_type": "launch",
    "local_time_ms": 1724651633000,
    "staging_flag": false,
}
```


<span id="a528ba4c"></span>
# Data format description: Webhook data source

The following is an introduction to the format of the transmitted data when transferring data offline/in real time through the webhook channel, as well as a description of each transmitted field.

<span id="06f463c3"></span>
## Real\-time transmission: Distributing data examples

The body of a request is a JSON array that contains 1 to 50 events.

```json
[{
  "user": {
    "user_unique_id": "mock_user_unique_id",
    "web_id": 6934486383370142000,
    "ssid": "acf3dd8f-7a18-42b1-996b-56a20156249c"
  },
  "header": {
    "app_id": 10000010,
    "app_name": "mock_web",
    "access": "",
    "client_ip": "221.122.122.122",
    "carrier": "",
    "os_name": "mac",
    "os_version": "10_15_5",
    "custom": "{\"app_id\":10000010,\"screen_width\":1440,\"screen_height\":900}",
    "language": "zh-CN",
    "device_model": "Macintosh",
    "resolution": "1440x900",
    "width": 1440,
    "height": 900,
    "timezone": 8,
    "tz_offset": -28800,
    "platform": "web",
    "browser": "Chrome",
    "browser_version": "78.0.3904.108",
    "referrer": "",
    "referrer_host": ""
  },
  "params": "{\"app_name\":\"mock_web\",\"referrer\":\"\",\"user_unique_id\":\"\",\"time\":1601590110322,\"is_bav\":1,\"title\":\"测试页面\",\"event_index\":1616590857270,\"url\":\"http://demo.com.cn/product/list\",\"url_path\":\"/product/list\"}",
  "event_name": "predefine_pageview",
  "session_id": "aa7b79a1-4e27-44fe-bed8-56adfffddc07",
  "datetime": 1601590110,
  "server_time": 1601590110,
  "log_type": "mario_event",
  "local_time_ms": 1601590110322
},{其他事件},{其他事件}]
```


<span id="b8108ec4"></span>
## Real\-time transmission: individual event specific field descriptions

```plain
//An event
Event {
          User user //The format requirements within user are described in the following text
          Header header //The format requirements within header are described in the following text
          string params  //Event parameters, single-layer json map, need to be dumped into a string
          string event_name  // Event name
          string session_id
          uint64 server_time  //The time log reached server
          string log_type 
          uint64 local_time_ms    //Event happen timestamp(millisecond)
}

//user field inside event

User {
     string user_unique_id  // unique User id
     uint64 device_id  // equipment id
     string open_udid  // openudid
     string client_udid  // device id generated by the client itself
     string mc    // equipment mac address
     string build_serial    // hardware serial number
     string serial_number    // serial number
     string idfa    // idfa
     uint64 web_id 
     string ssid 
     string idfv 
     string oaid 
     string user_unique_id_type    // The caliber of the user_unique_id type field, used in tob scenarios, the default caliber is empty or default_user_unique_id_type
}

//header field inside event

Header {
     uint32 app_id  // app_id
     string app_name  // app name
     string app_version  // app version
     string app_package  // app package name
     string display_name  // app name
     string app_channel  // app distribution channel
     string access  // network access type
     string client_ip  // client ip
     string carrier    // carrier
     string os_name    // operating system name
     string os_version    // operating system version
     string custom // custom event public attribute, which is a json string
     uint32 client_port    // client port
     string app_key    // app key
     uint32 version_code    // version code
     string vendor_id    // app vendor id
     string app_language    // app language 
     string language    // operating system language
     string app_region    // app setting region
     string region    // operating system region
     string device_model    // device model
     string device_brand    // device brand
     string device_manufacturer    // device manufacturer
     string resolution    // screen resolution
     string display_density    // screen pixel display level
     uint32 density_dpi    // screen pixel display density
     sint32 width    // screen width
     sint32 height    // screen height
     string cpu_abi    // cpu type
     float timezone    // timezone
     string tz_name    // timezone name
     sint32 tz_offset    // timezone offset
     string mcc_mnc    // nation+running trademark record
     uint32 os_api    // client operating system API version number
     string rom    // rom
     string rom_version    // rom version
     string sim_region    // sim region
     string sim_serial_number    // sim series number
     bool is_jailbroken    // is the device jailbroken
     string platform    // platform type
     string ab_sdk_version    // ab_test field
     string utm_source    // advertisement source
     string user_agent    // user_agent
     string utm_medium    // advertisement medium
     string utm_campaign    // advertisement name
     string browser 
     string browser_version 
     string referrer 
     string referrer_host 
     string app_version_minor    //4-digit version number
     string utm_term    //advertisement keyword term
     string utm_content    //advertisement content
     string sdk_version_v2    //string type sdk version
     string tracer_data    // SDK tracer custom field，json string
     uint64 harmony_os_api    // 524~530 are unique identifiers of the HarmonyOS system
     string harmony_os_version 
     string harmony_release_type 
     uint64 harmony_build_version 
     uint64 harmony_major_version 
     uint64 harmony_senior_version 
     uint64 harmony_feature_version 
 
}
```
