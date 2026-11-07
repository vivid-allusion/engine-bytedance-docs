---
title: "If network requests do not use okhttp, can network monitoring data be reported to the platform?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/can_network_monitoring_data_be_reported_to_the_platform"
---

APMInsight supports automatic instrumentation for network monitoring with Okhttp. For other network libraries, it supports network monitoring by allowing users to perform their own collection of network monitoring data, which can then be reported to the server for display through the APMInsight reporting interface. Below are the network monitoring reporting interface, the detailed network monitoring data structure, and the explanation of the meaning of each field.

<span id="3f8707a5"></span>
## Reporting interfaces

```Java
//Reported network monitoring data. For the specific data structure and fields, see the JSON structure below.
JSONObject network=new JSONObject();
ApmInsightAgent.monitorNetWork(network);
```


<span id="0bdd31ad"></span>
## Descriptions of reported data structures and fields

Objective: Monitoring network success rate and end\-to\-end latency

```JSON
"1": "Unknown error",
"2": "Connection timed out",
"3": "SOCKET timed out",
"4": "IO error",
"5": "SOCKET error",
"6": "The other side closed the connection",
"7": "Error binding port",
"8": "An exception occurred in the connection",
"9": "no route to host",
"10": "Port is unavailable",
"11": "Unknown host, domain name resolution failed",
"12": "Connection reset",
"13": "Connection refused",
"14": "Server is unreachable, no route node to the server was found",
"15": "Network is unreachable",
"16": "Address is unavailable",
"17": "Address is already in use",
"18": "No HTTP response",
"19": "Client protocol error",
"20": "File is too large",
"21": "Too many redirects (usually occurs in circular redirects)",
"31": "Unknown client error",
"32": "Insufficient disk space",
"33": "File or directory does not exist",
"34": "Insufficient disk quota",
"35": "EROFS:",
"36": "Permission denied",
"37": "IO error",
"38": "json_exception",
"39": "security_exception",
"40": "No network",
"41": "Network cancelled"
```


If another error code is reported, it will be displayed in the list as `Unknown error [error code]`.

<span id="083e5d83"></span>
## Test code

Confirm that the platform has sampling configured; sampling is triggered on the client side; go to Custom settings \> Parameter settings \> Network analysis.

```Ada
JSONObject network= null;
try {
    network = new JSONObject("{\n" +
            "    \"data_type\":3,\n" +
            "    \"uri\":\"http://mock-api.com/Rz3yJMnM.mock/get\",\n" +
            "    \"timestamp\":1618901847169,\n" +
            "    \"ip\":\"10.79.136.68:8888\",\n" +
            "    \"duration\":539,\n" +
            "    \"status\":200\n" +
            "}");
    JSONObject log=new JSONObject("{\"dns\":{\"address_list\":[\"10.79.136.68\"]},\"socket\":{\"remote\":\"10.79.136.68:8888\",\"remote_host\":\"10.79.136.68\",\"remote_port\":\"8888\",\"socket_reused\":false},\"response\":{\"code\":200,\"sent_bytes\":132,\"received_bytes\":411,\"via_proxy\":true,\"network_accessed\":true},\"timing\":{\"request\":{\"duration\":539,\"request_sent_time\":1618901847302,\"response_recv_time\":1618901847304,\"start_time\":1618901847169},\"detailed_duration\":{\"ttfb\":1,\"dns\":0,\"tcp\":0,\"ssl\":0,\"send\":1,\"header_recv\":394,\"body_recv\":5}},\"base\":{\"method\":\"GET\",\"url\":\"http:\\/\\/mock-api.com\\/Rz3yJMnM.mock\\/get\"},\"error\":{\"error_code\":0},\"other\":{\"libcore\":\"okhttp\",\"version\":\"\",\"is_main_process\":true}}");
    network.put("request_log",log.toString());
} catch (JSONException e) {
    e.printStackTrace();
}
ApmInsightAgent.monitorNetWork(network);
```


Filter logcat logs by keyword: With ApmInsight, you can see the following logs.

```Apache
2021-04-20 18:52:29.637 31667-31667/com.example.apm.insight.demo D/ApmInsight: Receive:NetData
```


<span id="265bb0f0"></span>
## Description of network status fields

Network log fields present in reported logs.

```JavaScript
"network_type": 5,        
"network_type_code": 13,
```



|Field |DescriptionS |
|---|---|
|network_type |Network type.<br><br><br>* 0：NONE<br><br>* 1：MOBILE<br><br>* 2：MOBILE_2G<br><br>* 3：MOBILE_3G<br><br>* 4：WIFI<br><br>* 5：MOBILE_4G |
|network_type_code |Network status code. |


```PHP
/** Network type is unknown */
public static final int NETWORK_TYPE_UNKNOWN = TelephonyProtoEnums.NETWORK_TYPE_UNKNOWN; // = 0.
/** Current network is GPRS */
public static final int NETWORK_TYPE_GPRS = TelephonyProtoEnums.NETWORK_TYPE_GPRS; // = 1.
/** Current network is EDGE */
public static final int NETWORK_TYPE_EDGE = TelephonyProtoEnums.NETWORK_TYPE_EDGE; // = 2.
/** Current network is UMTS */
public static final int NETWORK_TYPE_UMTS = TelephonyProtoEnums.NETWORK_TYPE_UMTS; // = 3.
/** Current network is CDMA: Either IS95A or IS95B*/
public static final int NETWORK_TYPE_CDMA = TelephonyProtoEnums.NETWORK_TYPE_CDMA; // = 4.
/** Current network is EVDO revision 0*/
public static final int NETWORK_TYPE_EVDO_0 = TelephonyProtoEnums.NETWORK_TYPE_EVDO_0; // = 5.
/** Current network is EVDO revision A*/
public static final int NETWORK_TYPE_EVDO_A = TelephonyProtoEnums.NETWORK_TYPE_EVDO_A; // = 6.
/** Current network is 1xRTT*/
public static final int NETWORK_TYPE_1xRTT = TelephonyProtoEnums.NETWORK_TYPE_1XRTT; // = 7.
/** Current network is HSDPA */
public static final int NETWORK_TYPE_HSDPA = TelephonyProtoEnums.NETWORK_TYPE_HSDPA; // = 8.
/** Current network is HSUPA */
public static final int NETWORK_TYPE_HSUPA = TelephonyProtoEnums.NETWORK_TYPE_HSUPA; // = 9.
/** Current network is HSPA */
public static final int NETWORK_TYPE_HSPA = TelephonyProtoEnums.NETWORK_TYPE_HSPA; // = 10.
/** Current network is iDen */
public static final int NETWORK_TYPE_IDEN = TelephonyProtoEnums.NETWORK_TYPE_IDEN; // = 11.
/** Current network is EVDO revision B*/
public static final int NETWORK_TYPE_EVDO_B = TelephonyProtoEnums.NETWORK_TYPE_EVDO_B; // = 12.
/** Current network is LTE */
public static final int NETWORK_TYPE_LTE = TelephonyProtoEnums.NETWORK_TYPE_LTE; // = 13.
/** Current network is eHRPD */
public static final int NETWORK_TYPE_EHRPD = TelephonyProtoEnums.NETWORK_TYPE_EHRPD; // = 14.
/** Current network is HSPA+ */
public static final int NETWORK_TYPE_HSPAP = TelephonyProtoEnums.NETWORK_TYPE_HSPAP; // = 15.
/** Current network is GSM */
public static final int NETWORK_TYPE_GSM = TelephonyProtoEnums.NETWORK_TYPE_GSM; // = 16.
/** Current network is TD_SCDMA */
public static final int NETWORK_TYPE_TD_SCDMA =
        TelephonyProtoEnums.NETWORK_TYPE_TD_SCDMA; // = 17.
/** Current network is IWLAN */
public static final int NETWORK_TYPE_IWLAN = TelephonyProtoEnums.NETWORK_TYPE_IWLAN; // = 18.
/** Current network is LTE_CA {@hide} */
public static final int NETWORK_TYPE_LTE_CA = TelephonyProtoEnums.NETWORK_TYPE_LTE_CA; // = 19.
/**
* Current network is NR (New Radio) 5G.
* This will only be returned for 5G SA.
* For 5G NSA, the network type will be {@link #NETWORK_TYPE_LTE}.
*/
public static final int NETWORK_TYPE_NR = TelephonyProtoEnums.NETWORK_TYPE_NR; // 20.


// No default value when there is no network
public static final int NET_DEFAULT = -10000;
```
