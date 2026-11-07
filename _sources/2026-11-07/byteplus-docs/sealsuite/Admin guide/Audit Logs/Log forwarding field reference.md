---
title: "Log forwarding field reference"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/log-forwarding-fields"
---

Select a log name by module to view the corresponding log sample and field descriptions.


* **General:**  [Administrator operation logs](https://docs.byteplus.com/en/docs/31/121788#.566h55CG5ZGY5pON5L2c5pel5b-X), [employee login logs](https://docs.byteplus.com/en/docs/31/121788#.5ZGY5bel55m75b2V5pel5b-X), [API call logs](https://docs.byteplus.com/en/docs/31/121788#.YXBpLeiwg-eUqOaXpeW_lw==)

* **Wi\-Fi management:**  [Employee Wi-Fi connection logs/guest Wi-Fi connection logs/agentless endpoint network connection logs](https://docs.byteplus.com/en/docs/31/121788#.5ZGY5belLXdpLWZpLei_nuaOpeaXpeW_ly3orr_lrqItd2ktZmkt6L-e5o6l5pel5b-XLeWTkee7iOerr-e9kee7nOi_nuaOpeaXpeW_lw==)

* **VPN management:**  [VPN connection logs](https://docs.byteplus.com/en/docs/31/121788#.dnBuLei_nuaOpeaXpeW_lw==), [VPN access logs](https://docs.byteplus.com/en/docs/31/121788#.dnBuLeiuv-mXruaXpeW_lw==), [CPE access logs](https://docs.byteplus.com/en/docs/31/121788#.Y3BlLeiuv-mXruaXpeW_lw==)

* **AI security:**  [Agent full-link audit logs](https://docs.byteplus.com/en/docs/31/121788#.YWdlbnQt5YWo6ZO-6Lev5a6h6K6h5pel5b-X), [Skill protection logs](https://docs.byteplus.com/en/docs/31/121788#.c2tpbGwt6Ziy5oqk5pel5b-X), [Agent behavior guardrail alert logs](https://docs.byteplus.com/en/docs/31/121788#.YWdlbnQt6KGM5Li65oqk5qCP5ZGK6K2m5pel5b-X)

* **Endpoint Security:**  [Endpoint antivirus - virus scan logs](https://docs.byteplus.com/en/docs/31/121788#.57uI56uv6Ziy55eF5q-SLeeXheavkuafpeadgOaXpeW_lw==)

* **Dynamic Control:**  [Dynamic Control logs](https://docs.byteplus.com/en/docs/31/121788#.5Yqo5oCB5o6n5Yi25pel5b-X)

* **Zero Trust:**  [Application gateway access logs](https://docs.byteplus.com/en/docs/31/121788#.5bqU55So572R5YWz6K6_6Zeu5pel5b-X), [ZTNA connection logs](https://docs.byteplus.com/en/docs/31/121788#.enRuYS3ov57mjqXml6Xlv5c=), [Zero Trust proxy access logs](https://docs.byteplus.com/en/docs/31/121788#.6Zu25L-h5Lu75Luj55CG6K6_6Zeu5pel5b-X)

* **Endpoint management:**  [Device information logs](https://docs.byteplus.com/en/docs/31/121788#.6K6-5aSH5L-h5oGv5pel5b-X)

* **Data Loss Prevention (DLP):**  [DLP log forwarding field format](https://docs.byteplus.com/en/docs/sealsuite/dlp-log-outgoing-field-format)


<span id=".6YCa55So"></span>
## General

<span id=".566h55CG5ZGY5pON5L2c5pel5b-X"></span>
### Administrator operation logs

In **Export Logs**, search for **Admin Activity Log**.

Administrator operation logs record policy changes, system configuration modifications, and personnel permission adjustments performed by Administrators in the Admin Console. They include the operator, operation time, execution environment, change details, and operation result, and can be used to trace configuration changes.

Administrator operation logs also record configuration changes that have been integrated into auditing, such as ZTNA traffic steering policies, ACLs, clusters, Layer 7 applications, client rate limiting, and automatic enablement.

**Log sample:** 

```Plain Text
<14>1 2024-10-24T21:11:08+08:00 - xxx 2511297 - - {
        "tenant_id": "b7******",
        "x_key": "admin_audit_log",
        "user": {
                "open_id": "ou_XqQW******",
                "username": "张三",
                "user_email": "zhangsan@example.com",
                "departments": ["xxx/RD"]
        },
        "env": {
                "os": "web",
                "client_ip": "10.x.x.x",
                "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36"
        },
        "option": {
                "module": "101",
                "module_message": "动态控制",
                "sub_module": "1",
                "sub_module_message": "动态决策",
                "action": "admin/dynamic_security/engine/groups/1615",
                "action_message": "更新规则组"
        },
        "events": [{
                "status": "success",
                "model": "dynamic_rule_group",
                "model_message": "规则组",
                "action": "update",
                "action_message": "更新了规则组",
                "updates": [{
                        "ids": null,
                        "updates": {
                                "策略名称": {
                                        "from": "",
                                        "to": "审计规则"
                                },
                                "触发方式": {
                                        "from": null,
                                        "to": "应用风险"
                                }
                        }
                }]
        }, {
                "status": "success",
                "model": "dynamic_rule_group",
                "model_message": "规则组",
                "action": "update",
                "action_message": "更新了规则组",
                "updates": [{
                        "ids": null,
                        "updates": {
                                "启用策略": {
                                        "from": "",
                                        "to": "审计规则"
                                }
                        }
                }]
        }],
        "success": true,
        "timestamp": 1729775468
}

```


**Field descriptions:** 


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|tenant_id |String |b7f5\*\*\*\* |Unique tenant ID.<br><br>This field is recorded only in private deployment scenarios. |
|x_key |String |admin_audit_log |Log type.<br><br>**Note**<br><br>This field is supported in server version 3.0.7 and later. |
|user |Object |\- |User information. |
|\-\- open_id |String |ou_xxx |User open ID, in the format `ou_xx`. |
|\-\- username |String |张三 |User name. |
|\-\- user_email |String |zhangsan@example.com |User email address. |
|\-\- departments |Array of String |["xxx/RD"] |List of departments to which the user belongs. |
|env |Object |\- |Operation execution environment information. |
|\-\- os |String |web |Operating system. |
|\-\- client_ip |String |8.8.8.8 |Client IP address. |
|\-\- user_agent |String |Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36 |UA, the identification information of the login client. |
|option |Object |\- |Operation information. |
|\-\- module |String |101 |Operation module. |
|\-\- module_message |String |动态控制 |Operation module description. |
|\-\- sub_module |String |1 |Operation submodule. |
|\-\- sub_module_message |String |动态决策 |Operation submodule description. |
|\-\- action |String |admin/dynamic_security/engine/groups/1615 |Operation performed. |
|\-\- action_message |String |更新规则组 |Operation description. |
|events |Array of Object |\- |Change event details. |
|\-\- status |String |success |Event change status. |
|\-\- model |String |dynamic_rule_group |Changed object. |
|\-\- model_message |String |规则组 |Changed object description. |
|\-\- action |String |update |Change action. |
|\-\- action_message |String |更新了规则组 |Change action description. |
|\-\- updates |Array of Object |\- |Change details. |
|\-\-\-\- ids |Object |null |Entity where the change occurred. |
|\-\-\-\- updates |Object |\- |Change content sent. |
|\-\-\-\-\-\- key |String |策略名称 |Change content key. |
|\-\-\-\-\-\- from |String |Empty |Original content. |
|\-\-\-\-\-\- to |String |审计规则 |Changed content. |
|success |Boolean |true |Whether the operation succeeded. |
|timestamp |Number |1600000000 |Timestamp when the operation was performed. |


<span id=".5ZGY5bel55m75b2V5pel5b-X"></span>
### Employee login logs

In **Export Logs**, search for **Employee Login Log**.

Employee login logs record employee login and logout operations. They include employee information, client information, operation type, execution result, and time, which help troubleshoot login issues and trace account activity.

**Log sample:** 

```Plain Text
<14>1 2023-05-24T12:38:32+08:00 - xxx 19461 - - {
        "x_key": "employee_login",
        "open_id": "ou_dV1**zYA",
        "user_name": "张X",
        "user_email": "zhangx@example.com",
        "client_ip": "10.10.*.*",
        "user_agent": "Mac/2.1.12(CorpLink/2.1.12 (darwin; Mac 13.2.1; zh))",
        "app_version": "2.1.12",
        "device_model": "Apple/MacBookPro16,2",
        "events": "[{\"success\":true,\"error_code\":\"\",\"error_message\":\"\",\"error_message_en\":\"\",\"name\":\"users\",\"action\":\"logout\",\"changes\":[{\"ids\":[2198],\"attrs\":null}]}]",
        "action": "logout",
        "success": true,
        "timestamp": 1684903112
}

```


**Field descriptions:** 


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |employee_login |Log type.<br><br>**Note**<br><br>This field is supported in server version 3.0.7 and later. |
|open_id |String |ou_xxx |User ID, in the format `ou_xx`. |
|user_name |String |张三 |User name. |
|user_email |String |zhangsan@example.com |User email address. |
|client_ip |String |10.10.10.\* |Client IP address. |
|user_agent |String |Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36 |UA, the identification information of the login client. |
|app_version |String |2.1.0 |Version number. |
|device_model |String |Apple/MacBookPro16,2 |Device type. |
|events |String |[{"success":true,"error_code":"","error_message":"","error_message_en":"","name":"users","action":"logout","changes":[{"ids":[2198],"attrs":null}]}] |Event details. |
|action |String |login |Operation type, including login, logout, and login/code/verify. |
|success |Boolean |true |Whether the login succeeded. |
|timestamp |Number |1600000000 |Login time, in Unix seconds. |


<span id=".YXBpLeiwg-eUqOaXpeW_lw=="></span>
### API call logs

In **Export Logs**, search for **API Request Log**.

API call logs record API requests and their processing results. They include the request path, call time, duration, response status, and error information, which help troubleshoot API call issues.

**Log sample:** 

```Plain Text
<14>1 2024-10-24T21:11:08+08:00 - xxx 2511297 - - 
{
  "tenant_id": "********",
  "x_key": "openapi_request_log",
  "timestamp": 1770985595105,
  "create_time": 1770985599746313000,
  "request_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "user_agent": "Mac/2.1.12(CorpLink/2.1.12 (darwin; Mac 13.2.1; zh))",
  "request_content_type": "application/json",
  "response_content_type": "application/json; charset=utf-8",
  "client_ip": "xxx.xxx.xxx.xxx",
  "method": "POST",
  "canonical_path": "/api/open/v1/user/batch_create",
  "execution_time": 1634,
  "request_path": "/api/open/v1/user/batch_create?department_id=od_********",
  "access_key_id": "*",
  "http_status": 200,
  "error_message": "参数错误",
  "error_code": 40000,
  "request_payload": "{\"email\":\"test_user@example.com\",\"mobile\":\"138********\"}",
  "response_body": "{\"code\":40000,\"action\":\"alert\",\"message\":\"参数错误\"}",
  "flags": 12,
  "is_success": false
}

```


**Field descriptions:** 


|Field |Type |Example |**Description** |
|---|---|---|---|
|tenant_id |String |b7f5\*\*\*\* |Unique tenant ID.<br><br>This field is recorded only in private deployment scenarios. |
|x_key |String |openapi_request_log |Log type identifier. |
|create_time |Number |1770985599746313000 |Nanosecond timestamp when the log record is generated on the server. |
|access_key_id |Number |6 |AK/SK used to call the API. |
|timestamp |Number |1770985595105 |Millisecond timestamp when the API request occurred (Unix Timestamp). |
|request_id |String |3c64ee48\-\-\-\*\*\*\*\-a21e0d483692 |Unique request identifier, corresponding to `X-Request-Id` in the HTTP Header. |
|user_agent |String |Mac/2.1.12(CorpLink/2.1.12 (darwin; Mac 13.2.1; zh)) |User\-Agent information of the client, used to identify the system and version that initiated the request. |
|request_content_type |String |application/json |Content type of the request body. |
|response_content_type |String |application/json; charset=utf\-8 |Content type of the response body. |
|client_ip |String |114.251.xxx.xxx |Public IP address of the client that initiated the request. |
|method |String |POST |HTTP method used to access the API. |
|canonical_path |String |/api/open/v1/security/edlp/events/evidence/:type |Canonical path of the API, used to uniquely identify the API feature. |
|execution_time |uint64 |1543 |Total execution time of the API request, in milliseconds (ms). |
|request_path |String |/api/open/v1/security/edlp/events/evidence/screenshot?event_id=xxxx |Full path of the actual request, including Query parameters. |
|http_status |int16 |200 |Standard HTTP response status code. |
|error_message |String |服务器错误 |Error description returned by the API. |
|error_code |int32 |50000 |Error code. `0` indicates success. A non\-`0` value indicates a business exception. |
|request_payload |String | |Raw request body data. A maximum of 2 KB is recorded. Data exceeding the limit is truncated. |
|response_body |String | |Raw response body data. A maximum of 12 KB is recorded. Data exceeding the limit is truncated. |
|flags |Number |12 |Bitmask of the log collection status, used to track data capture status:<br><br><br>* **bit 0**: The request body exceeds 2 KB and is truncated.<br><br>* **bit 1**: The response body exceeds 12 KB and is truncated.<br><br>* **bit 2**: The request payload has been recorded.<br><br>* **bit 3**: The response body has been recorded. |
|is_success |Boolean |false |Request success criterion. Logic: `true` if `http_status` is 2xx and `error_code` is 0. |


<span id=".d2ktZmkt566h55CG"></span>
## Wi\-Fi management

<span id=".5ZGY5belLXdpLWZpLei_nuaOpeaXpeW_ly3orr_lrqItd2ktZmkt6L-e5o6l5pel5b-XLeWTkee7iOerr-e9kee7nOi_nuaOpeaXpeW_lw=="></span>
### Employee Wi\-Fi connection logs/guest Wi\-Fi connection logs/agentless endpoint network connection logs

These three types of logs record network connections for employees, guests, and agentless endpoints. They include the authentication account, device, connection time, connection result, and disconnection information. The three log types share the same field structure and are distinguished by log type and account type.


* Employee Wi\-Fi connection logs, guest Wi\-Fi connection logs, and agentless endpoint network connection logs use the same data structure. Different network connection records are represented by the `x_key` and `account_type` field values.

* The `x_key` field is supported in server version 3.0.7 and later.


**Log sample:** 

```Plain Text
<14>1 2023-05-24T12:48:48+08:00 - xxx 19461 - - {
        "x_key": "wifi_connect_employee",
        "radius_id": 1,
        "connect_time": "2006-01-02T15:04:05Z07:00",
        "disconnect_time": "2006-01-02T15:04:05Z07:00",
        "connection_result": 1,
        "connection_group_id": "DEFAULT",
        "connection_ip": "10.0.0.*",
        "account_id": 1,
        "account_username": "zhangsan",
        "account_type": 1,
        "device_id": "0000000000",
        "device_name": "xxxxx",
        "calling_station_id": "3a:af:28:df:f8:79",
        "called_station_id": "20:4c:03:2b:30:6c",
        "creators": "1",
        "creators_ex": [{
                "open_id": "ou_xxx",
                "user_name": "张三",
                "user_email": "zhangsan@example.com"
        }],
        "remark": "",
        "option": "connect"
}

```


**Field descriptions:** 


|Field |Type |Example |**Description** |
|---|---|---|---|
|x_key |String |wifi_connect_employee |Log type.<br><br><br>* `wifi_connect_employee`: Employee Wi\-Fi connection log.<br><br>* `wifi_connect_guest`: Guest Wi\-Fi connection log.<br><br>* `wifi_connect_terminal`: Agentless endpoint network connection log. |
|radius_id |Number |1 |RADIUS node ID. |
|connect_time |String |2006\-01\-02T15:04:05Z07:00 |Time when the Wi\-Fi connection was established. |
|disconnect_time |String |2006\-01\-02T15:04:05Z07:00 |Time when the Wi\-Fi connection was disconnected. This field has a value only in disconnection logs. |
|connection_result |Number |1 |Connection status:<br><br><br>* 1: Successful.<br><br>* 2: Failed.<br><br>* 3: Degraded. |
|connection_group_id |String |DEFAULT |Permission string of the connection. |
|connection_ip |String |10.0.0.\* |IP address allocated by DHCP. |
|account_id |Number |1 |Wi\-Fi account ID. |
|account_username |String |zhangsan |Wi\-Fi account username. |
|account_type |Number |1 |Wi\-Fi account type:<br><br><br>* 1: Guest Wi\-Fi.<br><br>* 2: Employee Wi\-Fi.<br><br>* 3: Employee wired network.<br><br>* 4: Agentless endpoint. |
|portal_login_type |String |xxx |Employee portal authentication type. |
|nas_identifier |String |xxx |NAS identifier carried in authentication. |
|nas_id |Number |1 |Network device ID matched by authentication. |
|nas_port_id |String | |NAS port information. |
|session_id |String | |Authentication log identifier ID. |
|ssid |String |feilian\-inc |Wireless signal identifier. |
|device_id |String |00000000000000 |DID of the authenticated device. |
|device_name |String |xxx |Device name of the authenticated device. |
|calling_station_id |String |3a:af:28:df:f8:79 |MAC address of the NAS. |
|called_station_id |String |20:4c:03:2b:30:6c |MAC address of the authenticated device. |
|creators |String |1 |* For employee Wi\-Fi and employee wired network, this field indicates the user ID of the account.<br><br>* For guest Wi\-Fi, this field indicates the applicant ID. Multiple IDs are separated by `\\|`. |
|creators_ex |Array of Object |[] |Array type. Explains the information of each user in creators in order. |
|. open_id |String |ou_xxx |User OpenID, which can be used for OpenAPI queries, in the format `ou_xx`. |
|. user_name |String |张三 |User name. |
|. user_email |String |zhangsan@xxx.cn |User email address. |
|remarks |String |null |* If the connection fails, this field shows the failure reason.<br><br>* If the connection succeeds, this field is empty. |
|option |String |connect |Log type. Enumerated values include connect, disconnect, and update. |


<span id=".dnBuLeeuoeeQhg=="></span>
## VPN management

<span id=".dnBuLei_nuaOpeaXpeW_lw=="></span>
### VPN connection logs

In **Export Logs**, search for **VPN Connect Log**.

VPN connection logs record when employee endpoints establish and disconnect VPN connections. They include the employee, device, VPN node, connection time, and operation type, which help trace connection status.

**Log sample:** 

```Plain Text
<14>1 2023-05-24T12:48:48+08:00 - xxx 19461 - - {
        "x_key": "vpn_connect_log",
        "open_id": "ou_dV***zYA",
        "user_name": "张三",
        "user_email": "zhangsan@example.com",
        "client_ip": "10.10.*.*",
        "device_id": "641162*****58ff43f991312093",
        "device_os": "Mac 13.2.1",
        "device_model": "Apple/MacBookPro16,2",
        "vpn_id": 1,
        "vpn_ip": "10.*.*.*",
        "connect_time": "2023-05-24T12:48:45+08:00",
        "app_version": "Mac v2.1.12",
        "option": "connect"
}

```


**Field descriptions:** 


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |vpn_connect_log |Identifies the log type.<br><br>**Note**<br><br>This field is supported in server version 3.0.7 and later. |
|open_id |String |ou_xxx |User OpenID, which can be used for OpenAPI queries, in the format `ou_xx`. |
|user_name |String |张三 |User name. |
|user_email |String |example@xxx.cn |User email address. |
|client_ip |String |10.10.10.\* |Client IP address. |
|device_id |String |00000000000000 |Client device ID. |
|device_os |String |Mac 12.4 |Client system. |
|device_model |String |Apple/MacBookPro16,2 |Client system information. |
|vpn_id |Number |1 |VPN node ID. |
|vpn_ip |String |10.0.0.\* |Private IP address of the VPN node. |
|vpn_ipv6 |String |00::0 |Private IPv6 address of the VPN node. |
|connect_time |String |2006\-01\-02T15:04:05Z07:00 |Time when the VPN connection was established. |
|disconnect_time |String |2006\-01\-02T15:04:05Z07:00 |Time when the VPN connection was disconnected. This field has a value only in disconnection logs. |
|app_version |String |2.1.10 |Version number. |
|option |String |connect |Log type. Enumerated values include connect and disconnect. |


<span id=".dnBuLeiuv-mXruaXpeW_lw=="></span>
### VPN access logs

In **Export Logs**, search for **VPN Access Log**.

VPN access logs record resource access after an endpoint establishes a VPN connection. They include the source address, destination address, port, protocol, access time, and action, which help audit network access.

**Log sample:** 

```Plain Text
<14>1 2023-05-24T12:58:43+08:00 - xxx 13643 - - {
        "x_key": "vpn_conntrack",
        "user": "USER_ou_dV1jLvVzYA",
        "uip": "10.10.*.*:55299",
        "sip": "10.241.*.*",
        "dip": "142.251.*.*",
        "sport": "63031",
        "dport": "443",
        "protocol": "tcp",
        "host": "www.example.com",
        "action": "accept",
        "timestamp": "1684904321"
}

```


**Field descriptions:** 


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |vpn_conntrack |Identifies the log type.<br><br>**Note**<br><br>This field is supported in server version 3.0.7 and later. |
|email |String |admin@example.local |User email address. |
|mobile |String |18800\*\*\*\*\*\* |User mobile number. |
|did |String |62d9065661a6e66\*\*\*\*\*0ec839b |Device ID. |
|smac |String |3c:22:fb:33:86:70 |Source MAC address. |
|os |String |Mac |Device operating system. |
|os_version |String |12.4 |Operating system version. |
|device_brand |String |Apple |Device brand. |
|device_model |String |MacBookPro15,4 |Device model. |
|app_version |String |v2.0.11 |Version number. |
|user |String |USER_ou_xxx |User, in the format `USER_{open_id}`. |
|uip |String |10.10. *.*  |User IP. |
|sip |String |20.20. *.*  |Source IP. |
|dip |String |10.92. *.*  |Destination IP. |
|sport |String |51293 |Source port. |
|dport |String |18009 |Destination port. |
|protocol |String |udp |Protocol. |
|host |String |example.com |Domain name. |
|action |String |accept |Action. |
|timestamp |String |1684904321 |Access time, in Unix seconds. |


<span id=".Y3BlLeiuv-mXruaXpeW_lw=="></span>
### CPE access logs

In **Export Logs**, search for **CPE Access Log**.

CPE access logs record network access behavior of branch gateways. They can be used to audit resource access through gateways by branch offices.

**Log sample:** 

```Plain Text
<14>1 2023-05-24T13:10:14+08:00 - xxx 19461 - - {
        "x_key": "cpe_conntrack",
        "sip": "169.254.*.*",
        "dip": "100.64.*.*",
        "sport": "59618",
        "dport": "80",
        "protocol": "tcp",
        "host": "100.64.*.*",
        "action": "continue",
        "timestamp": "1752837441",
        "user": "*",
        "identity": "*",
        "uip": "111.19.*.*:6192", 
        "rule": "rule-1"
}

```


**Field descriptions:** 


|Field |Type |Example |**Description** |
|---|---|---|---|
|x_key |String |cpe_conntrack |Log type.<br><br>**Note**<br><br>This field is supported in server version 3.1.5 and later. |
|sip |String |169.254.. |Source IP. |
|dip |String |100.64.. |Destination IP. |
|sport |String |59618 |Source port. |
|dport |String |80 |Destination port. |
|protocol |String |tcp |Communication protocol. |
|host |String |100.64.. |HTTP address. |
|action |String |continue |Access result.<br><br><br>* accept: Allow.<br><br>* continue: Identifying. |
|timestamp |String |1752837441 |Access time, Unix timestamp in seconds. |
|user |String | |Reserved field. You can ignore it. |
|identity |String | |Reserved field. You can ignore it. |
|uip |String |111.19..:6192 |Reserved field. You can ignore it. |
|rule |String |rule\-1 |Reserved field. You can ignore it. |


<span id=".YWkt5a6J5YWo"></span>
## AI security

<span id=".YWdlbnQt5YWo6ZO-6Lev5a6h6K6h5pel5b-X"></span>
### Agent full\-link audit logs

Agent full\-link audit logs record events during Agent task execution. They include sessions, event types, and related user information, and can be used to trace task processes.

**Log sample:** 

```Plain Text
 <14>1 2026-08-12T14:13:00+08:00 - feilian 8537 - - {
 "x_key":"agent_audit_event",
 "object_key":"2_6964b3a68541c3e1c6f4c0c031769a48_1786515xxxxx",
 "session_id":"rollout-2026-08-12T09-50-55-019ff3aa-5a7d-7cb0-9047-026686xxxxx",
 "timestamp":1786503981053,
 "cwd":"",
 "type":"model_output",
 "user_id":2,
 "open_id":"ou_aEB1L81Ne9",
 "username":"linfei",
 "user_email":"linfei.123@bytedance.com",
 "mobile":"",
 "department_path":"feilian",
 "roles":"",
 "device_id":"6964b3a68541c3e1c6f4c0c03xxxxx",
 "device_name":"Lxxxxx-DESKTOP",
 "device_hostname":"Lxxxxx-DESKTOP",
 "device_serial_number":"8TDBNZ3",
 "device_os":"Windows",
 "device_os_version":"Windows Windows11_v10.0",
 "app_version":"3318",
 "app_build_number":"5368",
 "agent_key":"codex",
 "session_title":"rollout-2026-08-12T09-50-55-019ff3aa-5a7d-7cb0-9047-026686abe081",
 "content":"{\"session_id\":\"rollout-2026-08-12T09-50-55-019ff3aa-5a7d-7cb0-9047-026686abe081\",\"text\":\"好呀。11:06 要发给谁、发送什么内容？\",\"timestamp\":1786503981053,\"watcher_source\":\"session_file\"}",
 "image_keys":[],
 "create_time":1786515180213701676}

```


**Field descriptions:** 


|Field |Type |Example |**Description** |
|---|---|---|---|
|x_key |String |agent_audit_event |Fixed value.<br><br>Fixed Value. |
|create_time |Number |1770985599746313000 |Record creation time.<br><br>Record Creation Time. |
|access_key_id |Number |6 |AK/SK primary key. |
|timestamp |Number |1770985595105 |Event timestamp (ms). |
|request_id |String |3c64ee48\-08d7\-11f1\-8add\-a21e0d483692 |Unique request ID. Corresponds to X\-Request\-Id in the Header.<br><br>Obtained from "X\-Request\-Id" header, usually in UUID format. |
|user_agent |String |Mac/2.1.12(CorpLink/2.1.12 (darwin; Mac 13.2.1; zh)) |UA of the client. Obtained from the "User\-Agent" header. |
|request_content_type |String |application/json |Content type of the request body.<br><br>Request content type, obtained from "Content\-Type" header. |
|response_content_type |String |application/json; charset=utf\-8 |Content type of the response body.<br><br>Response content type, obtained from "Content\-Type" header. |
|client_ip |String |114.251.196.103 |IP address of the client. |
|method |String |POST |Access method. |
|canonical_path |String |/api/open/v1/security/edlp/events/evidence/:type |Canonical path of the API, used to uniquely identify the API feature.<br><br>Canonical path to identify the API, for example /api/open/v1/security/edlp/events/evidence/:type. |
|execution_time |uint64 |1543 |Total execution time of the API request, in milliseconds (ms).<br><br>Execution time of request in millisecond. |
|request_path |String |/api/open/v1/security/edlp/events/evidence/screenshot?event_id=xxxx |Full path of the actual request.<br><br>Actual requested path, for example /api/open/v1/security/edlp/events/evidence/screenshot?event_id=xxxx. |
|http_status |int16 |200 |Response status code. |
|error_message |String |服务器错误 |Error description returned by the API.<br><br>Error message of response. |
|error_code |int32 |50000 |Error code. 0 indicates success. A non\-0 value indicates a business exception.<br><br>SealSuite error code, 0 if successful. |
|request_payload |String | |Raw request body data. A maximum of 2 KB is recorded. Data exceeding the limit is truncated.<br><br>Request payload, truncated if size limit is exceeded. Limit is up to 2KB. |
|response_body |String | |Raw response body data. A maximum of 12 KB is recorded. Data exceeding the limit is truncated.<br><br>Response body data, truncated if size limit is exceeded. Limit is up to 12KB. |
|flags |Number |12 |Bitmask of the log collection status.<br><br>Bitmask tracking log capture status:<br><br><br>* bit 0 = request payload too large.<br><br>* bit 1 = response body too large.<br><br>* bit 2 = request payload was logged.<br><br>* bit 3 = response body was logged. |
|is_success |Boolean |false |Request success criterion. Logic: true if http_status is 2xx and error_code is 0.<br><br>true if http_status \>=200 AND http_status <400 AND error_code=0. |


<span id=".YWdlbnQt6KGM5Li65oqk5qCP5ZGK6K2m5pel5b-X"></span>
### Agent behavior guardrail alert logs

In **Export Logs**, search for **Agent Behavior Guardrail Alert Log**.

Agent behavior guardrail alert logs record Agent risk behaviors and guardrail action results. They include the matched policy, device, behavior type, target object, and action, which help trace risk behaviors.

**Log sample:** 

```Plain
<14>1 2026-08-13T10:13:10+08:00 - feilian - - {
  "tenant_id": "xxxxx",
  "event_id": "did-001-1786503xxxx",
  "strategy_key": "abg_policy_xxx",
  "strategy_name": "默认 Agent 行为护栏策略",
  "policy_version": "20260813.1",
  "did": "did-001",
  "uid": 1001,
  "device_os": "windows",
  "agent_object": "cursor",
  "process_key": "cursor",
  "process_matcher_id": 123456,
  "resource_key": "net-prod-api",
  "behavior_type": "network",
  "target_object": "api.example.com",
  "detail_domain": "api.example.com",
  "detail_remote_ip": "10.x.x.x",
  "detail_resolved_addresses": "10.1.2.3,10.x.x.x",
  "action": "block",
  "result": "blocked",
  "rule_id": "98765xxxx",
  "process_path": "",
  "command_line": "",
  "related_app_id": "",
  "extension_id": "",
  "publisher": "",
  "event_time": 1786503981,
  "report_time": 1786503990
}

```


**Field descriptions:** 


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|tenant_id |String |tenant\-g |Tenant ID. It comes from the server context and provides the tenant dimension for forwarding and troubleshooting. This field is recorded only in private deployment scenarios. |
|event_id |String |did\-001\-1786503981\-0 |Unique event identifier. If the client does not report it, the server fills it based on did, receive time, and event sequence number. |
|strategy_key |String |abg_policy_001 |Key of the matched behavior guardrail policy. It corresponds to the policy_id reported by the client. |
|strategy_name |String |默认 Agent 行为护栏策略 |Snapshot of the matched policy name. The server backfills it based on strategy_key. If it cannot be obtained, it may be the same as the policy key. |
|policy_version |String |20260813.1 |Policy version matched by the client. |
|did |String |did\-001 |Device DID. |
|uid |Number |1001 |User UID. The value is 0 if unknown. |
|device_os |String |windows |Device operating system. The server uses the client OS and converts it to lowercase. |
|agent_object |String |cursor |Historical object field. Currently from the same source as process_key and used for compatibility with legacy links. |
|process_key |String |cursor |Primary key of the Agent or process object. |
|process_matcher_id |Number |123456 |Matched process matcher ID. The value is 0 if unknown. |
|resource_key |String |net\-prod\-api |Resource key. |
|behavior_type |String |network |Behavior type. Enumerated values: file, network, command, and registry. |
|target_object |String |api.example.com |Target object. For file, it is the file path. For network, the domain name is preferred, followed by remote IP and resolved address. For command, it is the command line. For registry, it is the registry key. |
|detail_domain |String |api.example.com |Network behavior domain details. Empty for non\-network behaviors or when no domain name exists. |
|detail_remote_ip |String |10.1.2.3 |Network behavior remote IP details. Empty for non\-network behaviors or when no remote IP exists. |
|detail_resolved_addresses |String |10.1.2.3,10.1.2.4 |List of IP addresses resolved from the domain in network behavior. Multiple values are joined with commas. |
|action |String |block |Guardrail action. Current enumerated values: audit and block. Empty or unknown actions are handled as block. |
|result |String |blocked |Action result. Current enumerated values: audited and blocked. |
|rule_id |String |987654321 |Matched rule ID. The server forwards it as a string. Empty if not reported. |
|event_time |Number |1786503981 |Event occurrence time, as a Unix timestamp in seconds. If the client does not include timestamp, the server receive time is used as fallback. |
|report_time |Number |1786503990 |Time when the server receives and reports the forwarded event, as a Unix timestamp in seconds. The forwarding row time preferentially uses this time. |


<span id=".c2tpbGwt6Ziy5oqk5pel5b-X"></span>
### Skill protection logs

Skill protection logs record risk events when endpoints match Skill protection policies. They include risk item details, related users and devices, remediation status, and matched policies, which can be used to trace Skill security events and remediation.

**Log sample:** 

```JSON
<14>1 2026-09-18T10:13:10+08:00 - feilian - - -
{
  "x_key": "skill_protect",
  "tenant_id": "tenant-1",
  "event_id": "event-1",
  "file_status_updated_at": 1786503990,
  "first_alert_at": 1786503981,
  "skill_id": "skill-1",
  "skill_name": "demo-skill",
  "skill_path": "/skills/demo-skill",
  "sha256": "9f86d081884c7d659a2feaa0c55ad015...",
  "md5": "098f6bcd4621d373cade4e832627b4f6",
  "risks": [
    {
      "threat_type": "code.malicious_code",
      "threat_name": "恶意代码",
      "description": "检测到可疑命令执行逻辑",
      "evidence": [
        {
          "file_code": "exec(command)",
          "file_path": "index.js",
          "file_line": 8
        }
      ]
    }
  ],
  "user": {
    "id": 1001,
    "name": "示例用户",
    "department": "/研发中心",
    "mobile": "138****0000",
    "email": "user@example.com",
    "hire_time": "2024-01-02",
    "expire_time": 1800000000,
    "status": 1
  },
  "device": {
    "id": "device-1",
    "name": "Example Device",
    "os": "macOS",
    "ip": "10.0.0.1",
    "app_version": "7.8.9",
    "build_number": "20260826"
  },
  "file_status": "deleted",
  "file_status_code": 5,
  "policy": {
    "key": "policy-1",
    "name": "默认 Skill 防护策略"
  },
  "cloud_query_method": 1
}
```


**Field descriptions:** 


|Field |Type |Example |Description |
|---|---|---|---|
|x_key |String |skill_protect |Log type identifier. Fixed as skill_protect. |
|tenant_id |String |tenant\-1 |Tenant ID from the ClickHouse event snapshot. This field is recorded only in private deployment scenarios. |
|event_id |String |event\-1 |Event ID. |
|file_status_updated_at |Number |1786503990 |Latest alert time of the current aggregate snapshot, as a Unix timestamp in seconds, from last_seen. This field is not the time when an independently recorded remediation action occurred. |
|first_alert_at |Number |1786503981 |First alert time, as a Unix timestamp in seconds, from first_seen. |
|skill_id |String |skill\-1 |Unique Skill identifier. |
|skill_name |String |demo\-skill |Skill name. |
|skill_path |String |/skills/demo\-skill |Skill path on the device. |
|sha256 |String |9f86d081... |SHA\-256 value of the Skill file or content. |
|md5 |String |098f6bcd... |MD5 value of the Skill file or content. |
|risks |Array |\- |Risk item array. If no risk is available, an empty array is output and the field is not omitted. One Skill can contain multiple risks, and the original order of risk items is preserved. |
|\-\- threat_type |String |code.malicious_code |Risk type identifier. |
|\-\- threat_name |String |恶意代码 |Localized risk name. If the stored value is empty, the name is queried by threat_type. If it remains empty, the field is omitted. |
|\-\- description |String |检测到可疑命令执行逻辑 |Risk description. |
|\-\- evidence |Array |\- |Risk evidence array, corresponding to alert_details in the stored risk item. |
|\-\- file_code |String |exec(command) |Code snippet that matches the risk. |
|\-\- file_path |String |index.js |File path where the evidence is located. |
|\-\- file_line |Number |8 |Line number where the evidence is located. The value is 0 if no line number exists. |
|user |Object |\- |Associated user. The object is always output. If organization information enrichment fails, at least id is retained. |
|\-\- id |Number |1001 |User ID from ClickHouse user_id. This field is always output. The value is 0 if unknown. |
|\-\- name |String |示例用户 |User name from organization structure user information. Omitted if empty. |
|\-\- department |String |/研发中心 |User department path. The primary department path is used first. Omitted if missing. |
|\-\- mobile |String |138\*\*\*\*0000 |User mobile number. Omitted if empty. |
|\-\- email |String |user@example.com |User email address. Omitted if empty. |
|\-\- hire_time |String |2024\-01\-02 |Raw value of the user's hire date. Omitted if empty. |
|\-\- expire_time |Number |1800000000 |User expiration time, as a Unix timestamp in seconds. Omitted if not set. |
|\-\- status |Number |1 |User status. Omitted when the value is 0. |
|device |Object |\- |Associated device. The object is always output. If device information enrichment fails, at least the id, os, and app_version from ClickHouse are retained. |
|\-\- id |String |device\-1 |Device DID from ClickHouse device_id. This field is always output. |
|\-\- name |String |Example Device |Device name from the device service. Omitted if empty. |
|\-\- os |String |macOS |Device operating system. The ClickHouse snapshot value is used first. If the device service query succeeds, the real\-time device value overwrites it. Omitted if empty. |
|\-\- ip |String |10.0.0.1 |Client IP address most recently reported by the device, from the device service. Omitted if empty. |
|\-\- app_version |String |7.8.9 |SealSuite client version. The ClickHouse snapshot value is used first. If the device service query succeeds, the real\-time device value overwrites it. Omitted if empty. |
|\-\- build_number |String |20260826 |Client build number from the device service. Omitted if empty. |
|file_status |String |deleted |Remediation status name, converted from disposition_action.<br><br>Enumerations and mappings:<br><br><br>* not_disposed (code=1): Not remediated. Used only for compatibility with legacy states.<br><br>* isolated (code=2): Isolated.<br><br>* trusted (code=3): Trusted.<br><br>* disinfected (code=4): Disinfected.<br><br>* deleted (code=5): Deleted.<br><br>* not_isolated (code=8): Not isolated. Unknown actions, not remediated actions, file restoration, and cancel trust actions converge to this state.<br><br>* allowlisted (code=9): Added to allowlist.<br><br>* unknown_{code} (other values): Unrecognized status. For example, code 10 is output as unknown_10. |
|file_status_code |Number |5 |Numeric remediation status code corresponding to the status name in file_status. See the enumerations and mappings for file_status. For example, 5 indicates deleted. |
|policy |Object |\- |Matched Skill protection policy. An empty object is output when no policy information exists. |
|\-\- key |String |policy\-1 |Configuration key of the matched policy. Omitted if empty. |
|\-\- name |String |默认 Skill 防护策略 |Matched policy name. Omitted if empty. |
|cloud_query_method |Number |1 |Cloud query method. ClickHouse cloud_query_type is passed through directly.<br><br>Enumerations and mappings:<br><br><br>* 0 = Skill Hash cloud query: Query risk results by Skill Hash.<br><br>* 1 = Skill content cloud query: Upload Skill content and query risk results.<br><br>* Other values = Unknown method: The server does not rewrite unknown values. The receiver must retain the original value and handle it as an unknown type. |


<span id=".57uI56uv5a6J5YWo"></span>
## Endpoint Security

<span id=".57uI56uv6Ziy55eF5q-SLeeXheavkuafpeadgOaXpeW_lw=="></span>
### Endpoint antivirus \- virus scan logs

In **Export Logs**, search for **Anti\-Virus \- Virus Scan Log**.

Virus scan logs record virus events detected on endpoints. They include the device, detection policy, threat file, threat level, and remediation action, which help analyze virus alerts and remediation.

**Log sample:** 

```Plain Text
<14>1 2023-05-24T13:10:14+08:00 - xxx 19461 - - {
        "x_key": "anti_virus",
        "event_id": "xxxx",
        "open_id": "xxx",
        "username": "",
        "user_email": "example.xxx.cn",
        "mobile": "",
        "timestamp": 17012345678,
        "report_time": 17012345678,
        "config_key": "xxx",
        "config_name": "xxx",
        "device_ip": "10.0.*.*",
        "device_id": "xxxxxxxx",
        "scan_mode": "realtime_scan",
        "scan_scene": "sensitive_file_protect",
        "scan_id": "xxx",
        "threat_object_flag": "av_object_file",
        "threat_object_id": "c:\\users\\mimikatz.exe+7862ac21eb3****247c188c5f8179f",
        "threat_file_path": "",
        "threat_file_hash": "xxx",
        "threat_file_size": 123,
        "threat_file_type": "win32exe",
        "process_name": "",
        "threat_type": "virus",
        "raw_malware_name": "Generic.Trojan.Mimikatz.Marte.!s!.A.301958EE",
        "threat_level": 1,
        "remediation": "remind_only"
}

```


**Field descriptions:** 


|Field |Type |Example |**Description** |
|---|---|---|---|
|x_key |String |anti_virus |Log type.<br><br>**Note**<br><br>This field is supported in server version 3.0.7 and later. |
|event_id |String |9312dc30\-b0a4\-43d2\-add1\-6707ec\*\* |Event ID. |
|open_id |String |ou_W9Yz\*\*\*8e |User ID, in the format `ou_xx`. |
|username |String |张三 |User name. |
|user_email |String |example@xxx.cn |User email address. |
|mobile |String |18800\*\* |User mobile number. |
|timestamp |Number |1662626747 |Event occurrence time, in Unix timestamp format. |
|report_time |Number |1662626747 |Event reporting time, in Unix timestamp format. |
|config_key |String |2212dc30\-2222\-1111\-00aa\-6707ecf2c1c0 |Key of the endpoint antivirus policy. |
|config_name |String |策略 AAA |Name of the endpoint antivirus policy. |
|device_ip |String |10.10.10.\* |Device IP. |
|device_id |String |62d9065661a6e66\*0ec839b |Device ID. |
|device_name |String |Example's Device |Device name. |
|device_hostname |String |CORPLINK\-PC |Device hostname. |
|device_serial_number |String |5053565a4331384b365\*\*\*\*64e4e48384a |Device serial number. |
|device_os |String |windows |Operating system, including windows, mac, and linux. |
|app_version |String |2.1.0 |Version number. |
|scan_mode |String |realtime_scan |Detection mode. |
|scan_scene |String |sensitive_file_protect |Scan scenario. |
|scan_id |String |e21b829f\-18a5\-4437\-b7e0\-0192a0\*\* |Scan task ID. |
|threat_object_flag |String |av_object_file |Type of the suspicious object. |
|threat_object_id |String |c:\users\mimikatz.exe+7862ac21e\*\*\*\*c188c5f8179f |Suspicious object ID. |
|threat_file_path |String |c:\users\mimikatz.exe |Path of the suspicious file on the user's machine. |
|threat_file_hash |String |7862ac21eb3f8c4e8247c188c5f8179f |Hash of the suspicious file. |
|threat_file_size |String |1355680 |Size of the suspicious file. |
|threat_file_type |String |win32exe |Type of the suspicious file. |
|process_name |String |mimikatz.exe.zip |Related process name. |
|threat_type |String |virus |Threat category.<br><br>phishing is phishing software. |
|raw_malware_name |String |Generic.Trojan.Mimikatz.Marte.!s!.A.301958EE |Raw threat name. |
|threat_level |Number |1 |Threat level. |
|remediation |String |remind_only |Default remediation method.<br><br><br>* remind_only\-Relaxed.<br><br>* remind_quarantine_recoverable\-Moderate.<br><br>* remind_quarantine_unrecoverable \- Strict. |
|disposition_action |Number |1 |0 // Report virus.<br><br>1 // Report virus.<br><br>2 //Quarantine file.<br><br>3 //Restore file.<br><br>4 //Delete file.<br><br>5 //Disinfect file.<br><br>6 //Add trusted file.<br><br>7 //Add trusted directory.<br><br>8 //Delete trusted file.<br><br>9 //Delete trusted directory.<br><br>10 //Add trusted file name.<br><br>11 //Delete trusted file name.<br><br>12 //Add trusted file MD5.<br><br>13 //Delete trusted file MD5.<br><br>14 //Add trusted file SHA1.<br><br>15 //Delete trusted file SHA1. |


<span id=".5Yqo5oCB5o6n5Yi2"></span>
## Dynamic Control

<span id=".5Yqo5oCB5o6n5Yi25pel5b-X"></span>
### Dynamic Control logs

In **Export Logs**, search for **Dynamic Engine Log**.

Dynamic Control logs record the execution of Dynamic Control policies. They include trigger conditions, matched rules, remediation actions, and execution results, which help troubleshoot policy triggering and remediation issues.

**Log sample:** 

```Plain Text
<14>1 2023-05-24T13:05:05+08:00 - xxx 19461 - - {
        "x_key": "dynamic_engine",
        "id": "738e8595-ff45-4343-8326-bb3***088",
        "open_id": "ou_dV1***zYA",
        "username": "张三",
        "user_email": "zhangsan.9612@example.com",
        "did": "62c24a*****17be079189b968bb7d7",
        "trigger": "period_5_min",
        "trigger_label": "",
        "action_key": "wifi-device-downgrade",
        "timestamp": 1684904700,
        "action_record_type": 1,
        "context": {
                "user_id": 2198,
                "user_agent": "",
                "did": "62c24a3***b968bb7d7",
                "ip": "",
                "event": {},
                "params": {
                        "user_id": "21 ** 8"
                },
                "result": null
        },
        "is_manual": false,
        "undo": false,
        "result_code": 0,
        "group_id": 49,
        "rule_id": 406
}

```


**Field descriptions:** 


|Field |Type |Example |**Description** |
|---|---|---|---|
|x_key |String |dynamic_engine |Log type.<br><br>**Note**<br><br>This field is supported in server version 3.0.7 and later. |
|action_key |String |abort\-request |Remediation action. |
|action_record_type |String |1 |Remediation type:<br><br><br>* 1: Execute.<br><br>* 2: Automatic recovery.<br><br>* 3: Manual recovery. |
|context |String |{"user_id":7,"user_agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7） AppleWebKit/605.1.15 （KHTML， like Gecko） Version/15.6.1 Safari/605.1.15"，"did":""，"ip":"10.10.."，"event":{}，"params":{"roles":[1]}，"result":[{"name":"abort_request"，"undo":false，"args":"["用户所属角色被管理员禁止登录"，"role has been limited"]"}]} |Context. A JSON string that contains parameters during remediation and the remediation result. |
|did |String |62d90656\*\*0ec839b |Device ID. |
|id |String |101 |Remediation record ID. |
|is_manual |String |false |Whether the operation is manual. |
|result_code |String |0 |Execution result:<br><br><br>* 0: Executed successfully.<br><br>* 1: Rate\-limited.<br><br>* 2: Manually recovered.<br><br>* 99: Unknown error. |
|timestamp |String |1662626747 |Operation time, in Unix timestamp format. |
|trigger |String |web_login |Trigger point. |
|trigger_label |String |门户登录（登录尝试） |Trigger point (Chinese). |
|undo |String |false |Whether the operation is automatic recovery. |
|user_id |String |ou_W9Y\*\*\*r8e |User ID. |
|group_id |String |45 |Triggered rule group ID. |
|rule_id |String |461 |Triggered rule ID. |


<span id=".6Zu25L-h5Lu7"></span>
## Zero Trust

<span id=".5bqU55So572R5YWz6K6_6Zeu5pel5b-X"></span>
### Application gateway access logs

In **Export Logs**, search for **Application Gateway Access Log**.

Application gateway access logs record user requests to internal web systems through the application gateway. They include the request URL, method, response status, duration, and user information, which help audit application access.

**Log sample:** 

```Plain Text
<14>1 2025-11-28T15:24:10+08:00 - xxx 9493 - - {
        "tenant_id": "00000000",
        "x_key": "agw_access_log",
        "sip": "114.251.*.*",
        "sport": "63074",
        "protocol": "HTTP/1.1",
        "schema": "https",
        "method": "POST",
        "host": "fakebaidu.com",
        "uri": "/EWS/Exchange.asmx",
        "intranet_ip": "127.0.0.1",
        "referer": "",
        "user_agent": "AppleExchangeWebServices/835 ExchangeSync/2007",
        "status": 401,
        "size": 0,
        "duration": 0.01093102,
        "level": "error",
        "timestamp": 1764314646,
        "trace_id": "fb4d8abe-d2b1-4a47-b848-c2abf5******",
        "user": {
                "open_id": "ou_JwBN******",
                "username": "张三",
                "user_email": "zhangsan@example.com",
                "departments": ["测试"]
        },
        "api_resource_groups": [{
                "id": 5,
                "name": "全部资源",
                "app_id": 37,
                "api_resources": [{
                        "headers": ["GET", "POST", "PUT", "DELETE", "OPTIONS"],
                        "path": "/*"
                }]
        }],
        "app_name": "网关测试",
        "app_gateway_name": "测试节点"
}

```


**Field descriptions:** 


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|tenant_id |String |00000000 |Tenant ID. This field is recorded only in private deployment scenarios. |
|x_key |String |agw_access_log |Log type.<br><br>**Note**<br><br>This field is supported in server version 3.1.5 and later. |
|sip |String |114.251. *.*  |Source IP, the IP address of the client that requests the gateway. |
|sport |String |62596 |Source port, the client port that requests the gateway. |
|protocol |String |HTTP/1.1 |HTTP protocol version. |
|schema |String |http |Protocol scheme, http or https. |
|method |String |POST |Request method. |
|host |String |fakebaidu.com |Request domain name. |
|uri |String |/firm/pricvate |Request path. |
|intranet_ip |String |127.0.0.1 |Private IP address of the gateway server. |
|referer |String |[http://fakebaidu.com/firm/private](http://fakebaidu.com/firm/private) |Field in the HTTP request header. |
|user_agent |String |Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/141.0.0.0 Safari/537.36 |Field in the HTTP request header. |
|status |int32 |200 |Status field returned by the HTTP request. |
|size |int32 |93264 |HTTP request size. |
|duration |float64 |0.319 |HTTP request duration. |
|level |String |info |Gateway log level. |
|timestamp |int64 |1760605802 |Timestamp. |
|trace_id |String |fb4d8abe\-d2b1\-4a47\-b848\-c2abf5\*\*\*\*\*\* |Trace ID. |
|user.open_id |String |ou_xd7J\*\*\*\*\*\* |User ID, in the format ou_xx. |
|user.username |String |张三 |User name. |
|user.user_email |String |zhangsan@example.com |User email address. |
|user.departments |Array of String |测试 |Department to which the user belongs. |
|api_resource_groups |APIResourceGroup[] |{<br><br>"id": 6,<br><br>"name": "全部资源",<br><br>"app_id": 208,<br><br>"api_resources": [<br><br>{<br><br>"headers": [<br><br>"GET",<br><br>"POST",<br><br>"PUT",<br><br>"DELETE",<br><br>"OPTIONS"<br><br>],<br><br>"path": "/\*"<br><br>}<br><br>]<br><br>} |API resource to which the current request belongs. |
|app_name |String |网关测试 |Gateway application to which the current request belongs. |
|app_gateway_name |String |测试节点 |Gateway to which the current request belongs. |


<span id=".enRuYS3ov57mjqXml6Xlv5c="></span>
### ZTNA connection logs

In **Export Logs**, search for **ZTNA Connect Log**.

ZTNA connection logs record when employees enable and disconnect proxies. They include the employee, device, connection and disconnection time, connection address, and access cluster information, which help trace proxy connections.

**Log sample:** 

```JSON
{
  "x_key": "ztna_connect_log",
  "did": "example-device-id",
  "open_id": "ou_example",
  "user_name": "示例员工",
  "user_email": "user@example.com",
  "department": "示例企业/研发部",
  "connect_at": "2026-09-16T09:00:00+08:00",
  "disconnect_at": "2026-09-16T10:00:00+08:00",
  "internal_ip": "10.0.0.10",
  "internal_ipv6": "",
  "client_ip": "192.0.2.10",
  "active_client_ip": "192.0.2.11",
  "os": "Mac",
  "os_version": "15.0",
  "app_version": "3.3.20",
  "device_brand": "Apple",
  "device_model": "MacBookPro",
  "connect_type": 1,
  "cluster_id": 10,
  "cluster_name": "示例接入集群",
  "option": "disconnect"
}

```


**Field descriptions:** 


|Field |Type |Example |Description |
|---|---|---|---|
|x_key |String |ztna_connect_log |Forwarded log type identifier. This field belongs to the common forwarding wrapper. |
|did |String |example\-device\-id |Device ID. |
|open_id |String |ou_example |Employee OpenID, obtained by supplementing user information during forwarding. |
|user_name |String |示例员工 |Employee name. |
|user_email |String |user@example.com |Employee email address. |
|department |String |示例企业/研发部 |Department path string, not a department ID array. |
|connect_at |String |2026\-09\-16T09:00:00+08:00 |Connection start time. The source field connect_time is renamed in the template. |
|disconnect_at |String |2026\-09\-16T10:00:00+08:00 |Disconnection time. The source field disconnect_time is renamed in the template. |
|internal_ip |String |10.0.0.10 |Endpoint private IPv4 address. |
|internal_ipv6 |String |Empty string |Endpoint private IPv6 address. It can be empty when no data exists. |
|client_ip |String |192.0.2.10 |Source IP address of the connection request. |
|active_client_ip |String |192.0.2.11 |Active client IP address, which may differ from the source IP of the connection request. |
|os |String |Mac |Operating system identifier, not the operating system version. |
|os_version |String |15.0 |Operating system version. |
|app_version |String |3.3.20 |SealSuite client version. |
|device_brand |String |Apple |Device brand. |
|device_model |String |MacBookPro |Device model. |
|connect_type |Number |1 |1: Automatic node selection. 2: Manual node selection. 3: Unknown. |
|cluster_id |Number |10 |Associated cluster ID. |
|cluster_name |String |示例接入集群 |Cluster name snapshot. It can be empty when no information exists. |
|option |String |disconnect |connect: Connect. disconnect: Disconnect. |


<span id=".6Zu25L-h5Lu75Luj55CG6K6_6Zeu5pel5b-X"></span>
### Zero Trust proxy access logs

In **Export Logs**, search for **Zero Trust Access Log**.

Proxy Layer 4 access logs and proxy Layer 7 access logs share the "Zero Trust proxy access logs" forwarding item. They record the Access Policy matched when users access applications through a proxy gateway, the allow or block result, source address, destination address, device, and process information. The log forwarding type is `tgw_access_log`. It is displayed as "Zero Trust Access Log" in **Export Logs** and supports Syslog and Elasticsearch.

Layer 4 logs are generated by the proxy gateway and sent by the log collection service on the gateway node. Optional fields may be omitted if they have no value.

**Log sample:** 

```JSON
{
  "x_key": "tgw_access_log",
  "user": "USER_ou_example",
  "identity": "DEPARTMENT_od_example,ROLE_or_example",
  "did": "example-device-id",
  "os": "Mac",
  "sip": "192.0.2.10",
  "dip": "192.0.2.20",
  "sport": "53000",
  "dport": "443",
  "protocol": "tcp",
  "host": "app.example.com",
  "process_name": "example-client",
  "process_sig": "",
  "process_path": "/Applications/Example.app",
  "action": "accept",
  "rule": "示例应用||示例策略|12|34|0",
  "timestamp": "1789549200"
}

```


**Field descriptions:** 


|Field |Type |Example |Description |
|---|---|---|---|
|x_key |String |tgw_access_log |Forwarded log type identifier. |
|tenant_id |String |example |Tenant identifier, supplemented based on context in multi\-tenant sending scenarios. This field is recorded only in private deployment scenarios. |
|user |String |USER_ou_example |Employee identifier with the USER_ prefix. |
|identity |String |DEPARTMENT_od_example,ROLE_or_example |Department, role, and other identity identifiers, separated by commas. |
|did |String |example\-device\-id |Device ID. |
|os |String |Mac |Operating system identifier. |
|sip |String |192.0.2.10 |Request source IP observed by the proxy gateway. |
|dip |String |192.0.2.20 |Destination IP. After domain access is allowed, the resolved result can be populated. |
|sport |String |53000 |Source port, represented as a string. |
|dport |String |443 |Destination port, represented as a string. |
|protocol |String |tcp |Protocol, such as tcp, udp, or icmp. |
|host |String |app.example.com |Destination domain name or destination IP. |
|process_name |String |example\-client |Process name reported by the client. |
|process_sig |String |Empty string |Process signature reported by the client. |
|process_path |String |/Applications/Example.app |Process path reported by the client. |
|action |String |accept |Access Policy processing result, such as accept (allow) or drop (block). |
|rule |String |示例应用\\|\\|示例策略\\|12\\|34\\|0 |Matched rule name. Application rules usually include the application name, tag name, policy name, policy ID, application ID, and address sequence number. Default rules may use other names. |
|timestamp |String |1789549200 |Event occurrence time, as a Unix timestamp string in seconds. |
|email |String |user@example.com |Optional employee email address. Omitted if not collected. |
|mobile |String |Masked mobile number |Optional employee mobile number. Omitted if not collected. |
|smac |String |00:00:00:00:00:00 |Optional source MAC address. Omitted if not collected. |
|os_version |String |15.0 |Optional operating system version. Omitted if not collected. |
|device_brand |String |Apple |Optional device brand. Omitted if not collected. |
|device_model |String |MacBookPro |Optional device model. Omitted if not collected. |
|app_version |String |3.3.20 |Optional client version. Omitted if not collected. |
|uip |String |192.0.2.10 |Optional user address information. Omitted if not collected. |
|path |String |/example |Optional path. Layer 4 proxy logs usually do not include this field. |


<span id=".57uI56uv566h55CG"></span>
## Endpoint management

<span id=".6K6-5aSH5L-h5oGv5pel5b-X"></span>
### Device information logs

Device information logs record information about devices and their associated users. They include the device identifier, operating system, hardware configuration, device status, owner, and other fields, which help associate device information in external log platforms.

**Log sample:** 

```Plain Text
<14>1 2023-05-24T13:10:14+08:00 - xxx 19461 - - {
        "x_key": "device_info",
        "did": "668d9d86e6f****8a98e62725",
        "device_name": "JWVQRXWYXL",
        "os": "Mac",
        "os_ver": "14.6.1",
        "os_model": "macOS 14.6.1",
        "os_detail_version": "23G93",
        "app_ver": "3014",
        "brand": "Apple",
        "model": "Mac15,6",
        "language": "en-US",
        "client_ip": "10.10.*.*",
        "mac_addrs": "[\"4e:80:b2:60:15:8f\",\"66:6e:fe:47:42:2c\",\"66:6e:fe:47:42:2d\",\"a2:a9:97:42:15:e0\",\"36:0c:ed:a4:76:c0\",\"80:a9:97:42:15:e0\",\"66:6e:fe:47:42:0c\",\"36:0c:ed:a4:76:c4\",\"36:0c:ed:a4:76:c8\",\"66:6e:fe:47:42:0d\"]",
        "serial_number": "JWVQRXWYXL",
        "created_at": "2024-07-16T15:31:57+08:00",
        "updated_at": "2024-08-26T17:07:07+08:00",
        "is_live": true,
        "device_status": 1,
        "device_info": {
                "product_id": "",
                "serial_number": "JWVQRXWYXL",
                "memory_total": 36864,
                "memory_available": 11619,
                "disk_total": 471482,
                "disk_available": 385065,
                "cpu_model": "Apple M3 Pro",
                "cpu_serial_number": "",
                "gpu_model": "Apple M3 Pro",
                "nic_type": "Wi-Fi  (0x14E4, 0x4388)",
                "login_user": "admin",
                "is_vm": false,
                "nic_detail_list": [{
                        "nic_type": "en2",
                        "mac_addr": "36:0c:ed:a4:76:c4",
                        "active": false,
                        "description": "en2",
                        "has_traffic": false,
                        "ipv4": "",
                        "ipv6": [],
                        "is_default": "0"
                }, {
                        "nic_type": "en4",
                        "mac_addr": "66:6e:fe:47:42:0c",
                        "active": false,
                        "description": "en4",
                        "has_traffic": false,
                        "ipv4": "",
                        "ipv6": [],
                        "is_default": "0"
                }],
                "os_install_date": 1720556814,
                "ssd_serial_numbers": ["0ba0225c433cd629"]
        },
        "ext_attr_list": [{
                "id": 86,
                "def": {
                        "id": 86,
                        "name": "是否是公司设备",
                        "key": "是否是公司设备",
                        "desc": "",
                        "type": 3,
                        "is_required": false,
                        "is_unique": false
                },
                "value": true
        }],
        "groups": [{
                "id": 6,
                "name": "公司资产",
                "mode": 2
        }, {
                "id": 107,
                "name": "设备分组示例",
                "mode": 2
        }],
        "user_id": "ou_PO1***P2Va",
        "full_name": "username",
        "mobile": "",
        "email": "abc@def.com",
        "department_id": "od_yN***vzz",
        "status": 1,
        "department_path": "example/xxxx/yyyy",
        "icon_url": "https://xxxxxxx",
        "roles": [{
                "name": "Employees",
                "id": "or_N1**EV"
        }],
        "third_party_user_id": "92**3e1"
}

```


**Field descriptions:** 


|Field |Type |Example |**Description** |
|---|---|---|---|
|x_key |String |device_info |Log type.<br><br>**Note**<br><br>This field is supported in server version 3.0.7 and later. |
|did |String |62d9065661a6e66\*0ec839b |Device did. |
|device_name |String |Example's Device |Device name. |
|os |String |Windows |Operating system. |
|os_ver |String |10 |System version. |
|os_model |String |macOS 14.6.1 |Operating system type. |
|os_detail_version |String |23G93 |Detailed operating system version. |
|app_ver |String |2.0.13 |Version number. |
|brand |String |Apple |Brand. |
|model |String |MacBookPro16,2 |Model. |
|language |String |zh\-CN |Language. |
|client_ip |String |10.10.10.\* |Client IP. |
|mac_addrs |String |4e:80:b2:60:15:8f |MAC address. |
|serial_number |String |5053565a4331384b365134373... |Device serial number. |
|created_at |String |2006\-01\-02 15:04:05.999 \-0700 MST |Creation time. |
|updated_at |String |2006\-01\-02 15:04:05.999 \-0700 MST |Update time. |
|software_num |Number |1 |Number of software items. |
|is_live |Boolean |1 |Whether the device is active. |
|device_status |Number |0 |Device status:<br><br><br>* 0: Device invalid.<br><br>* 1: Device active.<br><br>* 2: Device hibernating. |
|device_info |Object |\- |Device information. |
|. product_id |String |1 |Product ID. |
|. serial_number |String |JWVQRXWYXL |Serial number. |
|. memory_total |Number |36864 |Total memory size, in MB. |
|. memory_available |Number |11619 |Available memory size, in MB. |
|. mem_serial_numbers |Array of String |null |Memory serial numbers. |
|. disk_total |Number |500000 |Total disk size, in MB. |
|. disk_available |Number |100000 |Available disk size, in MB. |
|. cpu_model |String |Apple M3 Pro |CPU model. |
|. cpu_serial_number |String |1 |CPU serial number. |
|. gpu_model |String |Apple M3 Pro |GPU model. |
|. nic_type |String |en4 |NIC model. |
|. login_user |String |admin |User name. |
|. is_vm |Boolean |false |Whether it is a virtual machine. |
|. nic_detail_list |Array of Object |\- |NIC details. |
|.. nic_type |String |en2 |NIC type. |
|.. mac_addr |String |36:0c:ed:a4:76:c4 |MAC address. |
|.. active |Boolean |false |Whether it is active. |
|.. description |String |en2 |Description. |
|. os_install_date |String |1662626747 |Installation time, in Unix timestamp format (seconds). |
|. hdd_serial_numbers |Array of String |null |Disk serial numbers. |
|. ssd_serial_numbers |Array of String |["0ba0225c433cd629"] |Disk serial numbers (solid\-state). |
|ext_attr_list |Array of Object |\- |Extended attribute list. |
|. id |Number |86 |Attribute value ID. |
|. def |Object | |Attribute definition. |
|. value |Any |city |Attribute value. |
|groups |Array of Object |\- |Device groups. |
|. id |Number |1 |Primary key ID. |
|. name |String |xxx |Group name. |
|. mode |Number |1 |Distinguishes manual and automatic. |
|user_id |String |ou_xxx |User ID, in the format `ou_xxx`. |
|full_name |String |张三 |User name. |
|mobile |String |18800\*\* |User mobile number. |
|email |String |zhangsan@example.com |User email address. |
|department_id |String |od_xxx |Department ID, in the format `od_xxx`. |
|status |Number |1 |User status:<br><br><br>* 1: Enabled.<br><br>* 2 : Disabled.<br><br>* 3 : Resigned. |
|department_path |String |/1/2 |Department path. |
|icon_url |String |/api/v1/attach/download?key=xxxxx |User avatar. |
|third_party_user_id |String |1 |Third\-party user ID. |
|roles |Array of Object |\- |Roles. |
|. name |String |角色 A |Role name. |
|. id |String |or_xxx |Role ID, in the format `or_xxx`. |
