---
title: "DLP log forwarding field format"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/dlp-log-outgoing-field-format"
---

This topic describes the DLP log forwarding field format. For details about the SealSuite log audit feature, see [View audit logs](https://docs.byteplus.com/en/docs/sealsuite/docs-zk9yxy9szc).

 &nbsp;

<span id="dlp-audit-logs"></span>
# DLP Audit Logs

```JSON
<14>1 2023-05-24T13:12:44+08:00 - xxx 19461 - - {
        "x_key": "dlp_audit",
        "event_id": "872F8367-1788-44BF-A8ED-B3BBB8******",
        "open_id": "ou_dV1j******",
        "username": "Zhang San",
        "user_email": "zhangsan@example.com",
        "mobile": "",
        "timestamp": 1684905123,
        "report_time": 1684905162,
        "config_key": "478e5422-ba25-4828-a8bf-340ec1******",
        "config_name": "Log Test",
        "device_ip": "10.x.x.11",
        "device_id": "641162933a6ade9a58ff43f991******",
        "device_name": "C02D36******",
        "device_hostname": "C02D36******",
        "device_serial_number": "C02D36******",
        "device_os": "mac",
        "app_version": "2.1.12",
        "leak_type_desc": "Application reading sensitive files",
        "leak_action_desc": "Feishu reads sensitive files",
        "leak_way_type": "im",
        "leak_way_name": "feishu",
        "leak_browser_url": "",
        "leak_browser_title": "",
        "data_level": "L3",
        "data_type": "file",
        "filename_context": [],
        "content_context": [],
        "leak_code_user_email": "",
        "leak_code_user_name": "",
        "leak_code_local_path": "",
        "leak_code_remote_url": "",
        "leak_code_repo_name": "",
        "trigger_action": 12
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_audit |Identifies the log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">SealSuite 3.0.7 and later support this field.</div><br> |
|event_id |String |9312dc30\-b0a4\-43d2\-add1\-6707ec\*\*\*\*\*\* |Event ID. |
|open_id |String |ou_W9Yz\*\*\*\*\*\* |User OpenID. You can use it for OpenAPI queries. Format: `ou_xx`. |
|username |String |Zhang San |User name. |
|user_email |String |zhangsan@example.cn |User email address. |
|mobile |String |18800\*\*\*\*\*\* |User mobile number. |
|timestamp |Number |1662626747 |Event occurrence timestamp. Unit: seconds. |
|report_time |Number |1662626747 |Event reporting timestamp. Unit: seconds. |
|config_key |String |2212dc30\-2222\-1111\-00aa\-6707ec\*\*\*\*\*\* |Policy/configuration key. |
|config_name |String |Policy AAA |Policy/configuration name. |
|device_ip |String |8.8.8.8 |Device IP address. |
|device_id |String |62d9065661a6e66ebe574d0530\*\*\*\*\*\* |Device ID. |
|device_name |String |Example's Device |Device name. |
|device_hostname |String |\- |Device hostname. |
|device_serial_number |String |\- |Device serial number. |
|device_os |String |windows |Operating system: windows/mac/linux. |
|app_version |String |2.1.0 |SealSuite app version. |
|leak_type_desc |String |Application reading sensitive files |Leakage event type description. |
|leak_action_desc |String |Feishu reading sensitive files |Leakage behavior description. |
|leak_way_type |String |browser |Leakage channel: im, note, browser, peripheral, and more. |
|leak_way_name |String |feishu |Leakage channel: application name/browser name/peripheral name. |
|leak_browser_url |String |example.com/path/xxx |Leakage channel \- browser leakage: outbound page link. |
|leak_browser_title |String |example |Leakage channel \- browser leakage: outbound page title. |
|leak_file_path |String |/path/to/file.txt |Original path of the outbound file. |
|leak_file_type |String |application/json |MIME type of the outbound file. |
|leak_file_name |String |file.txt |Name of the outbound file. |
|leak_file_extension |String |txt |Extension of the outbound file. |
|leak_file_md5 |String |cad7b244cff66fda794ab1f387\*\*\*\*\*\* |Hash of the outbound file. New versions update this field to sha256.<br><br>This value only indicates a unique identifier. Do not use it as an md5 value. |
|leak_file_size |Number |123456 |Size of the outbound file. Unit: bytes. |
|leak_file_creation_ts |Number |1729677000 |File creation timestamp. Unit: seconds. |
|leak_file_last_modify_ts |Number |1729677000 |File last modified timestamp. Unit: seconds. |
|data_level |String |L1 |Data confidentiality level associated with the matched sensitive data label. |
|data_type |String |git |Outbound data type: file/git/svn. |
|leak_code_user_email |String |abc@xxx.x |User email address of the code repository to which the outbound file belongs. |
|leak_code_user_name |String |alice |User name of the code repository to which the outbound file belongs. |
|leak_code_local_path |String |/path/xxx |Local path of the code repository to which the outbound file belongs. |
|leak_code_remote_url |String |github.com |Remote repository URL of the code repository to which the outbound file belongs. |
|leak_code_repo_name |String |Private app |Repository name of the code repository to which the outbound file belongs. |
|trigger_action |Number |1 |Client\-side disposal action.<br><br>The client\-side disposal action bitmap represents different behaviors by bit:<br><br><br>* Block: trigger_action & 2 \> 0.<br><br>* Audit: trigger_action & 4 \> 0.<br><br>* Upload source file: trigger_action & 8 \> 0.<br><br>* Upload screenshot: trigger_action & 16 \> 0.<br><br>* Upload file flow: trigger_action & 32 \> 0. |
|more_info |Object |{"remote_url":"git@github.com:example/project.git","process_name":"com.apple.git","oid":"c4b6b0","lid":"abc123","push_user":"sombody","push_email":"somebody@example.com","remote_repo":"git@github.com:example/project.git@origin/fix\-edlp\-insert","local_repo":"/Users/somebody/project/project@feature\-branch","push_file_count":1,"cmd_args":"\-axxx","cmd_cwd":"/usr/bin/xxx","tenant_id":"xxx"// Sender tenant ID(omitempty),<br><br>"tenant_name":"xxx",// Sender enterprise name(omitempty)<br><br>"sender":"xx",// Sender(omitempty)<br><br>"receiver_name":"xx",// Receiver name(omitempty)<br><br>"receiver_company":"xx",// Receiver enterprise(omitempty)<br><br>"receiver_type":1,// Receiver type(omitempty)<br><br>"receiver_contact_type":3,// Receiver contact type(omitempty)<br><br>"trans_addr_display":"xxx",// Displayed transmission destination address(omitempty)<br><br>"protocol":"xx",// Transmission destination address protocol(omitempty)<br><br>"host":"xx",// Transmission destination host IP/domain(omitempty)<br><br>"port":"233",// Transmission destination port(omitempty)<br><br>"user_name":"xx",// Transmission username(omitempty)<br><br>"share_name":"xx",// Transmission volume name/shared path name(omitempty)<br><br>"base_url":"xxx",// BaseURL of the AI model<br><br>"provider":"xx", // Model provider<br><br>"model_id":"xxx"// AI model ID<br><br>} |Extended information associated with the event. For example:<br><br><br>* (Added in 3.1.4) Repository information associated with Git push.<br><br>* (Added in 3.1.4) Related parameters for sending files from the command line.<br><br>* (Added in 3.2.6) Lark tenant information. If this information is not reported, it is not forwarded.<br><br>* (Added in 3.2.6) Destination address information reported by the file transfer tool. If this information is not reported, it is not forwarded.<br><br>* (Added in 3.3.2) Extended information for AI software audit events.<br><br>* (Added in 3.3.3) Instant messaging channel recipient information, including sender, recipient name, recipient enterprise, recipient type (`1` indicates individual, `2` indicates group), and recipient contact type (`3` indicates internal, `4` indicates external). |
|data_rule |Object | |Sensitive data information actually matched by this file sending behavior. |
|associated_rules |list |[{"name":"File Content Match","path":"/lall","level":"L3"},{"name":"Product Solution Document","path":"/Middle<br><br>[{"name":"File Content Match","path":"/lall","level":"L3"},{"name":"Product Solution Document","path":"/Middle |Product and R&D Data","level":"L3"}]<br><br>Product and R&D Data","level":"L3"}] |
|anonymous_login |Number |1 |(Added in 3.2.3) Client login status when the event reaches the server.<br><br><br>* 0: Normal login.<br><br>* 1: Login\-free mode. |
|leak_sub_file_info |String |"[{"path":"Unnamed folder test.zip/Unnamed folder test/Unnamed folder 11111/internal.example.com/longurls/client_ver\-9f9ecc6","mime":"application/json","is_hit":true},{"path":"Unnamed folder test.zip/Unnamed folder test/internal.example.com/api/admin/asset/overview/client_version?client_os=\u0026os=web","mime":"application/json"}]" |(Added in 3.2.4) Leaked file path. |
|watermark_status |Number |1 |(Added in 3.3.2) Watermark status:<br><br><br>* 1: No watermark.<br><br>* 2: Watermark present.<br><br>* 0: Not detected. |
|embed_status |Number |1 |(Added in 3.3.6) Whether the document is nested:<br><br><br>* 1: Not nested.<br><br>* 2: Nested.<br><br>* 0: Not detected. |


 &nbsp;

<span id="dlp-audit-log-context-information"></span>
# DLP Event's Context Info

The format of the log forwarding fields is determined by the raw data reported by the Endpoint client. Starting from client version **3.2.16**, the system optimizes the structure and naming of some log fields to provide more granular audit dimensions.

Log forwarding follows different field mapping rules based on the client versions installed by Endpoint users in your enterprise. Refer to the field table for the actual version. If your enterprise environment is in a version upgrade transition period, with both clients earlier than 3.2.16 and clients running 3.2.16 or later, configure your log analysis system with field matching logic for both versions. This ensures continuous and complete log collection.

 &nbsp;

<span id="client-version-3-2-15-and-earlier"></span>
## Client version 3.2.15 and earlier

The following table lists the forwarding field format supported when clients of version 3.2.15 and earlier report logs.

```JSON
<14>1 2023-05-24T13:12:44+08:00 - xxx 19461 - - {
        "x_key": "dlp_audit_context",
        "attr": 1,
        "context": "",
        "create_time": 1724047670398766000,
        "device_id": "6486e0bf55d9940989fb86e32b******",
        "event_id": "A8B93285-2BC2-4765-93A7-A4DCFF******",
        "match_len": 0,
        "match_pos": 0,
        "match_times": 10,
        "match_type": 1,
        "match_value": "data:any_string",
        "tenant_id": "00000000",
        "timestamp": 1724047267,
        "user_id": 00000
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_audit_context |Identifies the log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">SealSuite 3.0.7 and later support this field.</div><br> |
|attr |Number |1 |* `1`: File name match.<br><br>* `2`: File content match. |
|context |String |\- |Actual matched context content. |
|device_id |String |6486e0bf55d9940989fb86e32b\*\*\*\*\*\* |Device ID. |
|event_id |String |9312dc30\-b0a4\-43d2\-add1\-6707ec\*\*\*\*\*\* |Event ID. |
|match_len |Number |1 |Length of the actual matched content in the context. |
|match_pos |Number |1 |Start position of the actual matched content in the context. |
|match_times |Number |1 |Number of occurrences of this context in the entire file. |
|match_type |Number |1 |Match type.<br><br><br>* `1`: Built\-in sensitive data type.<br><br>* `2`: Custom keyword type.<br><br>* `3`: Regular expression type. |
|match_value |String |data:any_string |Expected matched content, that is, the original value configured in the backend. |
|timestamp |Number |1724047267 |Event timestamp. Unit: seconds. |


 &nbsp;

<span id="client-version-3-2-16-and-later"></span>
## Client version 3.2.16 and later

Starting from version 3.2.16, logs use an upgraded structured format. If the Endpoint is updated to this version or later, use the following table to configure log parsing.

```JSON
<14>1 2023-05-24T13:12:44+08:00 - xxx 19461 - - {
        "x_key": "dlp_audit_context",
        "attr": 1,
        "context": "",
        "create_time": 1724047670398766000,
        "device_id": "6486e0bf55d9940989fb86e32b******",
        "event_id": "A8B93285-2BC2-4765-93A7-A4DCFF******",
        "timestamp": 1724047267,
        "match_info":"[{"match_type":2,"match_value":"Test","match_times":3}]",  
        "match_pos_v1": [2,3],
        "match_len_v1": [2,2],
        "match_file_path": "C:\\Users\\Admin\\Downloads\\Archive3-BankCard213+2.zip\\Archive3-BankCard213\\DialogFileUpload-BankCard100+.txt"
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_audit_context |Identifies the log type. |
|attr |Number |1 |* `1`: File name match.<br><br>* `2`: File content match. |
|context |String |\- |Actual matched context content. |
|device_id |String |6486e0bf55d9940989fb86e32b\*\*\*\*\*\* |Device ID. |
|event_id |String |9312dc30\-b0a4\-43d2\-add1\-6707ec\*\*\*\*\*\* |Event ID. |
|timestamp |Number |1724047267 |Event timestamp. Unit: seconds. |
|match_info |String |"[{"match_type":2,"match_value":"Test","match_times":3}]" |* `match_type`: Match type.<br><br>   * `1`: Built\-in sensitive data type.<br><br>   * `2`: Custom keyword type.<br><br>   * `3`: Regular expression type.<br><br>* `match_value`: Expected matched content, that is, the original value configured in the backend.<br><br>* `match_times`: Number of occurrences of this context in the entire file. |
|match_pos_v1 |Number |[2,3] |Match start position in the context. There may be multiple positions. |
|match_len_v1 |Number |[2,2] |Match length in the context. It corresponds one\-to\-one with the start position. |
|match_file_path |String |"C:\Users\Admin\Downloads\Archive3\-BankCard213+2.zip\Archive3\-BankCard213\DialogFileUpload\-BankCard100+.txt" |Absolute file path. |


 &nbsp;

<span id="file-flow-records-associated-with-dlp-audit-logs"></span>
# DLP Event's File Flow

```JSON
<14>1 2023-05-24T13:12:44+08:00 - xxx 19461 - - {
        "x_key": "dlp_audit_file_flow",
        "action": 11,
        "app_key": "",
        "create_time": 1724047794910924500,
        "dest_node_file_id": "66C4F044-9292F61D-AA052C1F-76******",
        "dest_node_file_path": "/Users/example/Downloads/Electronic Invoice A.pdf",
        "device_id": "645b5e4c4cd9ea00d29734179a******",
        "event_id": "0D70FE9C-BE23-4C99-A819-11284C******",
        "event_timestamp": 1724046225,
        "process_name": "",
        "serial": 1,
        "site_key": "site:builtin:wyemail",
        "site_title": "",
        "site_url": "https://mail.example.com/js6/main.jsp",
        "source_node_file_id": [],
        "source_node_file_path": [],
        "tenant_id": "00000000",
        "timestamp": 1723723583,
        "user_id": 109344,
        "@timestamp": 1724047801089
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_audit_file_flow |Identifies the log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">SealSuite 3.0.7 and later support this field.</div><br> |
|action |Number |11 |Operation type:<br><br><br>* 1: Copy.<br><br>* 2: Cut.<br><br>* 3: Compress and package.<br><br>* 4: Extract.<br><br>* 5: Save.<br><br>* 6: Save as.<br><br>* 7: Rename.<br><br>* 8: Clipboard copy.<br><br>* 9: Clipboard paste.<br><br>* 11: Download.<br><br>* 12: Create.<br><br>* 13: Encrypt.<br><br>* 14: File scanned by SealSuite for the first time.<br><br>* 101: Receive. The file is created by an IM application. |
|app_key |String |feishu |Key of the application associated with the operation. |
|dest_node_file_id |String |66C4F044\-9292F61D\-AA052C1F\-76\*\*\*\*\*\* |File ID of this operation. |
|dest_node_file_path |String |/Users/example/Downloads/Electronic Invoice A.pdf |File path of this operation. |
|device_id |String |645b5e4c4cd9ea00d29734179a\*\*\*\*\*\* |Associated device ID. |
|event_id |String |0D70FE9C\-BE23\-4C99\-A819\-11284C\*\*\*\*\*\* |Key event ID. |
|event_timestamp |Number |1724046225 |Timestamp of the associated event. Unit: seconds. |
|process_name |String |\- |Process name. |
|serial |Number |1 |Operation serial number. Use it for sorting when timestamps are the same. |
|site_key |String |site:builtin:wyemail |Matched website Key. Generally available only for download actions. |
|site_title |String |\- |Matched website title. Generally available only for download actions. |
|site_url |String |[https://mail.example.com/js6/main.jsp](https://mail.example.com/js6/main.jsp) |Matched website URL. Generally available only for download actions. |
|source_node_file_id |Array |\- |String array that stores multiple source file IDs. |
|source_node_file_path |Array |\- |String array that stores multiple source file paths. |
|timestamp |Number |1723723583 |Event ID when the flow behavior occurred. |
|source_node_mime |String |["xx","xx"] |(Added in 3.3.5) File MIME list of the source node. |
|dest_node_mime |String |["xx","xx"] |(Added in 3.3.5) File MIME list of the destination node. |
|source_is_tracked |Bool |[true] |(Added in 3.3.5) Whether the source node is tracked. |
|dest_is_tracked |bool |true |(Added in 3.3.5) Whether the destination node is tracked. |


 &nbsp;

<span id="dlp-channel-block-logs"></span>
# DLP Block Log

```JSON
<14>1 2023-05-24T13:10:14+08:00 - xxx 19461 - - {
        "x_key": "dlp_block",
        "event_id": "0F074FFE-2139-4524-84A7-A2B005******",
        "open_id": "ou_dV1jLvVzYA",
        "username": "Zhang Mou",
        "user_email": "zhangmou@example.com",
        "mobile": "",
        "timestamp": 1684905008,
        "report_time": 1684905012,
        "config_key": "784b1bbb-4ecb-4e3e-b9d2-39d36b******",
        "config_name": "Outbound Test",
        "device_ip": "8.8.8.8",
        "device_id": "641162933a6ade9a58ff43f991******",
        "device_name": "C02D36******",
        "device_hostname": "C02D36******",
        "device_serial_number": "C02D36******",
        "device_os": "mac",
        "app_version": "2.1.12",
        "block_way": "desktop",
        "block_way_name": "feishu"
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_block |Identifies the log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">SealSuite 3.0.7 and later support this field.</div><br> |
|event_id |String |9312dc30\-b0a4\-43d2\-add1\-6707ec\*\*\*\*\*\* |Event ID. |
|open_id |String |ou_W9Yzw8mr8e |User OpenID. You can use it for OpenAPI queries. Format: `ou_xx`. |
|username |String |Zhang San |User name. |
|user_email |String |zhangsan@example.com |User email address. |
|mobile |String |18800\*\*\*\*\*\* |User mobile number. |
|timestamp |Number |1662626747 |Event occurrence timestamp. Unit: seconds. |
|report_time |Number |1662626747 |Event reporting timestamp. Unit: seconds. |
|config_key |String |2212dc30\-2222\-1111\-00aa\-6707ec\*\*\*\*\*\* |Policy/configuration key. |
|config_name |String |Policy AAA |Policy/configuration name. |
|device_ip |String |8.8.8.8 |Device IP address. |
|device_id |String |62d9065661a6e66ebe574d0530\*\*\*\*\*\* |Device ID. |
|device_name |String |Example's Device |Device name. |
|device_hostname |String |C02D36\*\*\*\*\*\* |Device hostname. |
|device_serial_number |String |C02D36\*\*\*\*\*\* |Device serial number. |
|device_os |String |windows |Operating system: windows/mac/linux. |
|app_version |String |2.1.0 |SealSuite app version. |
|block_way |String |web |Block channel: web & desktop. |
|block_way_name |String |feishu |Block channel application name. |


 &nbsp;

<span id="dlp-ai-intelligent-analysis"></span>
# DLP AI Agent Analyze Result

 &nbsp;

<span id="ai-file-content-analysis"></span>
## AI file content analysis

```JSON
<14>1 2025-09-04T17: 02: 17+08: 00 - xxx 732155 - - {
    "x_key": "dlp_agent_analyze",
    "file_analyze_result": {
        "event_id": "6E15****-****-****-****-385ABFB6803F",
        "create_time": 1756976537081422778,
        "timestamp": 1756976191,
        "knowledge_id": "intelligent_dlp_workflow_result_68b9****************a8159_dlp_sensitive_recog_analysis",
        "file_name": "Clipboard content.jpg",
        "history_knowledge_id": [],
        "data_type": 1,
        "data_class": "Business Data-Operational Data-Risk Control Rules",
        "data_level": "L4",
        "pre_data_type": 1,
        "pre_data_type": 1,
        "pre_data_class": "Business Data-Operational Data-Risk Control Rules",
        "pre_data_level": "L4",
        "file_topic_zh": "数据防泄露风险监控页面截图",
        "file_topic_en": "Screenshot of Data Leakage Prevention Risk Monitoring Page",
        "file_digest_zh": "显示飞连系统数据防泄露模块的风险洞察页面，包含覆盖员工5人、行为日志255条、AI推理调查40次，列表展示多条风险事件，推理结论多为“疑似主动泄密”，人工反馈均为“未反馈”，右侧为浏览器网络请求记录。",
        "file_digest_en": "Displays the risk insight page of the data leakage prevention module, including 5 covered employees, 255 behavior logs, 40 AI reasoning investigations. The list shows multiple risk events with reasoning conclusions mostly “suspected active leakage” and manual feedback all “unfeedback”. The right side shows browser network request records.",
        "reason_zh": "文件为数据防泄露模块的风险监控页面截图，内容涉及系统运营中的风险事件记录、AI推理调查等风控相关数据，属于与当前企业平台业务相关的真实数据，依据分析原则第8条，判定为企业数据。根据分类标准，风控相关的处罚记录等属于业务数据-运营数据-风控规则，敏感等级L4。",
        "reason_en": "The file is a screenshot of the risk monitoring page of the data leakage prevention module of the system. The content involves risk event records, AI reasoning investigations and other risk control-related data in system operations, which are real data related to the current enterprise's platform business. According to analysis principle 8, it is determined as enterprise data. According to the classification standard, risk control-related penalty records belong to Business Data-Operational Data-Risk Control Rules, with sensitivity level L4."
    }
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_agent_analyze |Identifies the log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">SealSuite 3.0.7 and later support this field.</div><br> |
|file_analyze_result |Object |\- |File analysis result. |
|\-\- event_id |String |6E15614E\-A6E3\-415E\-8E78\-385ABF\*\*\*\*\*\* |Event ID. |
|\-\- create_time |int64 |1756952468080341020 |Record creation time. |
|\-\- timestamp |int64 |1756952182 |Event occurrence time. |
|\-\- knowledge_id |String |intelligent_dlp_workflow_result_68b8f75cfd25725225\*\*\*\*\*\*_dlp_sensitive_recog_analysis |Result association ID returned by the Agent. |
|\-\- file_name |String |whiteboard_exported_image (1).png |File name. |
|\-\- history_knowledge_id |Array |\- |Associated historical analysis results. |
|\-\- data_type |int16 |1 |Data type. |
|\-\- data_class |String |Business Data\-Operational Data\-Business Rules |Data classification. |
|\-\- data_level |String |L3 |Data level. |
|\-\- personal_privacy |int16 |1 |(Added in 3.2.4) Whether the data is personal privacy data:<br><br><br>* 1: Yes<br><br>* 2: No<br><br>* 0: No data |
|\-\- pre_data_type |int16 |1 |Data type before correction. |
|\-\- pre_data_class |String |Business Data\-Operational Data\-Business Rules |Data classification before correction. |
|\-\- pre_data_level |String |L3 |Data level before correction. |
|\-\- file_topic_zh |String |流程图 |File topic (Chinese). |
|\-\- file_topic_en |String |Flowchart |File topic (English). |
|\-\- file_digest_zh |String |该流程图描述“点击AI分析详情”后的处理流程：外发事件未被定时任务1检测到时[...]已被检测到则获取任务状态和分析结果。 |File summary (Chinese). |
|\-\- file_digest_en |String |This flowchart describes the processing flow after "clicking AI analysis details"[...]If detected, obtain task status and analysis results. |File summary (English). |
|\-\- reason_zh |String |文件内容为业务流程逻辑，涉及……该类别敏感等级为L3。 |Judgment basis (Chinese). |
|\-\- reason_en |String |The content of the file is business process logic,[...], which has a sensitivity level of L3. |Judgment basis (English). |


 &nbsp;

<span id="ai-flow-direction-identification"></span>
## AI flow direction identification

```JSON
<14>1 2025-09-04T17: 04: 17+08: 00 - xxx 732155 - - {
    "x_key": "dlp_agent_analyze",
    "screenshot_analyze_result": {
        "event_id": "513C****-****-****-****-C5BBE7892AAA",
        "create_time": 1756976657081315174,
        "timestamp": 1756976197,
        "knowledge_id": "intelligent_dlp_workflow_result_68b9***************************69_dlp_screen_shot_analysis",
        "history_knowledge_id": [],
        "screenshot_count": 3,
        "operation_type": 3,
        "flow_direction": 3,
        "pre_operation_type": 3,
        "pre_flow_direction": 3,
        "target_type": 1,
        "target_value": "Recognition failed",
        "operation_type_reason_zh": "DLP审计日志中的外发通道为飞书（桌面软件），截图中确实打开了飞书软件，但飞书聊天窗口内未出现审计日志中的文件screenshot.jpeg，无法确认用户是否对该文件进行了手动操作，因此操作类型无法确定。",
        "operation_type_reason_en": "The outbound channel in the DLP audit log is Feishu (desktop software), and Feishu is indeed open in the screenshot. However, the file screenshot.jpeg from the audit log does not appear in the Feishu chat window, making it impossible to confirm whether the user manually operated on the file. Therefore, the operation type cannot be determined.",
        "flow_direction_reason_zh": "DLP审计日志显示外发通道为飞书，但截图中飞书聊天窗口仅展示文本消息及Pipeline通知，未出现审计日志中的文件screenshot.jpeg，无法明确文件发送对象，因此无法判断文件是内部流转还是外部流转。",
        "flow_direction_reason_en": "The DLP audit log indicates the outbound channel is Feishu, but the Feishu chat window in the screenshot only displays text messages and Pipeline notifications, without the file screenshot.jpeg from the audit log. The recipient of the file cannot be confirmed, so it is impossible to determine if the file is circulated internally or externally.",
        "target_value_reason_zh": "截图中飞书软件虽打开，但聊天窗口内未出现DLP审计日志中的文件screenshot.jpeg，无法从界面中识别出该文件的具体发送对象（如聊天对象、群组等）。",
        "target_value_reason_en": "Although the Feishu software is open in the screenshot, the file screenshot.jpeg from the DLP audit log does not appear in the chat window, so the specific recipient of the file (such as a chat contact or group) cannot be identified from the interface."
    }
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_agent_analyze |Identifies the log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">SealSuite 3.0.7 and later support this field.</div><br> |
|screenshot_analyze_result |Object |\- |Screenshot analysis result. |
|\-\- event_id |String |513C9828\-4824\-4B79\-9F79\-C5BBE7\*\*\*\*\*\* |Event ID. |
|\-\- create_time |int64 |1756955845184379987 |Record creation time. |
|\-\- timestamp |int64 |1756954162 |Event occurrence time. |
|\-\- knowledge_id |String |intelligent_dlp_workflow_result_68b90490fd25725225\*\*\*\*\*\*_dlp_screen_shot_analysis |Result association ID returned by the Agent. |
|\-\- history_knowledge_id |Array |\- |Associated historical analysis results. |
|\-\- screenshot_count |int16 |3 |Number of screenshots used for analysis. |
|\-\- operation_type |int16 |3 |Operation type. |
|\-\- flow_direction |int16 |3 |Flow direction. |
|\-\- pre_operation_type |int16 |3 |Operation type before correction. |
|\-\- pre_flow_direction |int16 |3 |Flow direction before correction. |
|\-\- target_type |int16 |1 |Flow target type. |
|\-\- target_value |String |Recognition failed |Flow target. |
|\-\- operation_type_reason_zh |String |DLP审计日志显示外发通道为“桌面软件\-其他应用”[...]无法明确判断是用户手动操作还是程序后台自动操作。 |Operation type \- judgment basis (Chinese). |
|\-\- operation_type_reason_en |String |The DLP audit log indicates [...]the operation was manual by the user or automatic by the program in the background. |Operation type \- judgment basis (English). |
|\-\- flow_direction_reason_zh |String |DLP审计日志中未明确发送对象信息[...]故无法判断文件流转方向是内部还是外部。 |Flow direction \- judgment basis (Chinese). |
|\-\- flow_direction_reason_en |String |The DLP audit log does not contain clear information about the recipient.[...]cannot be determined. |Flow direction \- judgment basis (English). |
|\-\- target_value_reason_zh |String |截图中主要显示VS Code编辑器和[...]故无法识别发送对象。 |Flow target \- judgment basis (Chinese). |
|\-\- target_value_reason_en |String |The screenshot mainly displays the VS Code editor and[...]cannot be identified. |Flow target \- judgment basis (English). |


 &nbsp;

<span id="ai-risk-insights"></span>
# DLP AI Risk Insight Alert

 &nbsp;

<span id="server-version-3-2-5-and-earlier"></span>
## Server version 3.2.5 and earlier

```JSON
<14>1 2025-09-10T12: 06: 42+08: 00 - xxx 164383 - - {
    "x_key": "dlp_agent_insight",
    "analyze_insight_result": {
        "create_time": 1757477202072943771,
        "analyze_start_time": 1757477060000000000,
        "analyze_end_time": 1757477172067427700,
        "uuid": "3-1757217795-1757476995",
        "knowledge_id": "intelligent_dlp_workflow_result_68c0f8c4dcd881a4485aff37_dlp_general_analysis",
        "history_knowledge_id": [],
        "event_start_time": 1757217795,
        "event_end_time": 1757476995,
        "event_count": 6,
        "risk_status": 1,
        "feedback_risk_status": 0,
        "result_summary_zh": "员工test2（在职）于2025年9月9日至10日期间……需立即干预并核查数据流向。",
        "result_think_zh": "首先，员工状态为在职，但外发行为存在多维度异常：……优先定性为主动泄密风险。",
        "result_summary_en": "Employee test2 (on-duty) sent 6 pieces of enterprise sensitive data……and immediate intervention and verification of data flow are required.",
        "result_think_en": "First, the employee status is on-duty, but the outbound behavior has multiple dimensional anomalies……as active leakage risk.",
        "critical_analyze_zh": [
            "{\"title\":\"用户状态分析\",\"content\":\"员工test2状态为在职，但外发行为存在多项异常，需关注其行为动机是否符合工作需求。\"}",
            ……
        ],
        "critical_analyze_en": [
            "{\"title\":\"User Status Analysis\",\"content\":\"Employee test2 is on-duty, but the outbound behavior has multiple anomalies, and it is necessary to pay attention to whether his behavior motivation is consistent with work requirements.\"}",……
        ],
        "analyze_event_ids": [
            "9258FCD7-73EC-48FC-B7F4-81CBA0F06320",
            "1029862A-5BBC-462C-B49F-D27DCF1C06C9",
            "2067DDB1-D62B-42DC-9263-8515B52ADE4E",
            "6E4C47BC-E6DD-4B64-83DA-2C8FABE51A31",
            "AA3D2E67-421B-4935-9AB7-D898FDA1179C",
            "75BDD546-106A-48E9-B182-34F0022CD08B"
        ],
        "analyze_status":2,
        "user_info": {
            "user_id": 3,
            "user_name": "test2",
            "user_email": "test2@qq.com",
            "user_mobile": "",
            "user_status": 0,
            "department_path": "Company/Level 1 Dept/Level 2 Dept/Business Team",
            "roles": [
                {
                    "name": "Role Test",
                    "id": 1,
                    "type": 2,
                    "open_id": "or_2nQanJ",
                    "mode": 0,
                    "description": "Role description test"
                }
            ]
        }
    }
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_agent_insight |Identifies the log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">SealSuite 3.0.7 and later support this field.</div><br> |
|analyze_insight_result |Object |\- |AI insight result. |
|\-\- create_time |int64 |1756977697082248066 |Record creation time. |
|\-\- analyze_start_time |int64 |1756977593000000000 |Analysis start time. |
|\-\- analyze_end_time |int64 |1756977667076640213 |Analysis end time. |
|\-\- uuid |String |2\-1756718384\-1756977584 |Unique ID of the risk insight task. |
|\-\- knowledge_id |String |intelligent_dlp_workflow_result_68b959b9fd257252257a816d_dlp_general_analysis |Result association ID returned by the Agent. |
|\-\- history_knowledge_id |String |\- |Associated historical analysis results. |
|\-\- event_start_time |int64 |1756718384 |Start time. |
|\-\- event_end_time |int64 |1756977584 |End time. |
|\-\- event_count |int32 |11 |Number of events. |
|\-\- risk_status |int8 |1 |AI analysis risk status. 1: risky, 2: no risk, 3: suspicious, 4: violation synchronization. |
|\-\- feedback_risk_status |int8 |0 |User feedback. 0: no feedback, 1: leakage risk exists, 2: confirmed no risk. |
|\-\- result_summary_zh |String |员工test_old（在职）于2025\-09\-03至2025\-09\-04期间[...]需立即由安全团队介入调查并核查接收方信息。 |Chinese AI result summary in JSON format. |
|\-\- result_think_zh |String |首先，员工状态为在职，但外发行为存在多维度异常：[...]根据通用原则，在职员工识别到3个及以上异常点，优先定性为主动泄密风险。 |Chinese AI reasoning process in JSON format. |
|\-\- result_summary_en |String |Employee test_old (active) transmitted 11 pieces of enterprise sensitive data frequently via[...]The security team should immediately investigate and verify recipient information. |English AI result summary in JSON format. |
|\-\- result_think_en |String |First, the employee status is on\-duty, but[...]as active leakage risk. |English AI reasoning process in JSON format. |
|\-\- critical_analyze_zh |String |['{"title":"用户状态分析","content":"员工test_old目前处于“在职”状态，所属部门为XX，其外发文件多涉及业务规则、风控规则等飞连业务相关数据，岗位职责范围与文件分类存在一定关联，但需结合外发行为异常性综合判断。"}',[...]] |Chinese key anomaly analysis in JSON format. |
|\-\- critical_analyze_en |String |['{"title":"User Status Analysis","content":"Employee test_old is currently "active" and belongs to the XX department. Most of the files he transmitted involve business\-related data such as business rules and risk control rules. There is a certain correlation between his job responsibilities and file classification, but the abnormality of external transmission behavior needs to be comprehensively judged."}',[...]] |English key anomaly analysis in JSON format. |
|\-\- analyze_status |int |2 |AI analysis status. 1=failed, 2=succeeded, 3=corrected. |
|\-\- analyze_event_ids |String |['76DE1C06\-227F\-4B18\-8238\-F9AAA0672414',[...]] |Suspicious event IDs associated with the analysis. |
|\-\- user_info |Object | |User information. |
|\-\-\- user_info.user_id |int32 |2 |User ID. |
|\-\-\- user_info.user_name |String |test_old |User name. |
|\-\-\- user_info.user_email |String |test@qq.com |User email address. |
|\-\-\- user_info.user_mobile |String | |User phone number. |
|\-\-\- user_info.user_status |int |0 |User status: 0 active, 1 pending onboarding, 2 pending departure, 3 departed. |
|\-\-\- user_info.department_path |String |Human Resource Management |Department to which the user belongs. |
|\-\-\- user_info.roles |Object | |Role information. |
|\-\-\-\- user_info.roles.name |String |Test |Role name. |
|\-\-\-\- user_info.roles.id |int |1 |Unique role ID. |
|\-\-\-\- user_info.roles.type |int |2 |Role type. 1: role from the role library, 2: user\-defined role. |
|\-\-\-\- user_info.roles.open_id |String |or_2nQanJ |Role open ID. |
|\-\-\-\- user_info.roles.mode |int |0 |Role mode. 0: static role, 1: dynamic role. |
|\-\-\-\- user_info.roles.description |String |Test |Role description. |


 &nbsp;

<span id="server-version-3-2-6-and-later"></span>
## Server version 3.2.6 and later

```SQL
<14>1 2026-02-02T16:23:29+08:00 - xxx 3161068 - - {
  "x_key": "dlp_agent_insight",
  "analyze_insight_result": {
    "id": 1811897029993442600,
    "event_name": "已离职员工通过非授权工具外发包含用户敏感信息的银行卡号文件",
    "event_name_en": "Resigned employee sent files containing user sensitive information (bank card numbers) via unauthorized tool",
    "summary": "已离职的审核员两次通过非企业授权工具curl外发名为\"银行卡号1.docx\"的文件，该文件包含用户银行卡号（敏感信息），违反了工作职责（不能发送带有用户信息的文件）及企业信息安全规定（不能对外发送公司机密数据）",
    "summary_en": "The resigned Douyin auditor sent the file named \"Bank Card Number 1.docx\" (containing user sensitive information: bank card numbers) twice via unauthorized tool curl, violating job responsibilities (prohibited from sending files with user information) and company information security regulations (prohibited from sending confidential data externally)",
    "analyze_process_zh": [
      {
        "title": "文件敏感性判断",
        "content": "文件名称为\"银行卡号1.docx\"，直接显示包含用户银行卡号，属于用户敏感信息，为企业敏感数据"
      },
      {
        "title": "外发目的与合理性",
        "content": "外发通道为curl（非企业授权的内部办公工具），两次外发间隔约10分钟，目的不符合抖音审核员的工作职责（禁止发送带用户信息的文件），且无授权依据，合理性不足"
      },
      {
        "title": "综合风险分析",
        "content": "员工处于已离职状态，发送的文件含敏感用户信息，违反工作职责及企业规定，构成信息安全风险"
      }
    ],
    "analyze_process_en": [
      {
        "title": "File Sensitivity Judgment",
        "content": "The file name \"Bank Card Number 1.docx\" directly indicates it contains user bank card numbers, which are user sensitive information and belong to the company's sensitive data"
      },
      {
        "title": "Sending Purpose and Rationality",
        "content": "The sending channel is curl (not an enterprise-authorized internal office tool), the interval between two sends is about 10 minutes, the purpose does not conform to the job responsibilities of Douyin auditors (prohibited from sending files with user information), and there is no authorization basis, so the rationality is insufficient"
      },
      {
        "title": "Comprehensive Risk Analysis",
        "content": "The employee is in the resigned state, the sent file contains sensitive user information, violating job responsibilities and company regulations, constituting an information security risk"
      }
    ],
    "risk_status": 1,
    "disposal_status": 1,
    "user_info": {
      "user_id": 3,
      "user_name": "aaa",
      "user_email": "a@a.a",
      "user_mobile": "",
      "user_status": 3,
      "department_path": "market",
      "roles": null
    }
  },
  "@timestamp": 1769430696359
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_agent_insight |Log type ID. |
|analyze_insight_result |Object |\- |Risk information analyzed by AI. |
|.id |Number |1811897029993442600 |Risk ID. |
|.event_name |String |Resigned employee sent files containing user sensitive information (bank card numbers) via unauthorized tool |Risk name. |
|.event_name_en |String |Resigned employee sent files containing user sensitive information (bank card numbers) via unauthorized tool |Risk name (English). |
|.summary |String |The resigned auditor sent the file named "Bank Card Number 1.docx" (containing user sensitive information: bank card numbers) twice via unauthorized tool curl, violating job responsibilities (prohibited from sending files with user information) and company information security regulations (prohibited from sending confidential data externally) |Risk detail summary. |
|.summary_en |String |The resigned Douyin auditor sent the file named "Bank Card Number 1.docx" (containing user sensitive information: bank card numbers) twice via unauthorized tool curl, violating job responsibilities (prohibited from sending files with user information) and company information security regulations (prohibited from sending confidential data externally). |Risk detail summary (English). |
|.analyze_process_zh |Array |\- |Analysis process list. |
|.title |String |File Sensitivity Judgment |Analysis process title. |
|.content |String |The file name "Bank Card Number 1.docx" directly indicates it contains user bank card numbers, which are user sensitive information and belong to the company's sensitive data |Analysis process content. |
|.analyze_process_en |Array |\- |Analysis process list (English). |
|.title |String |File Sensitivity Judgment |Analysis process title. |
|.content |String |The file name "Bank Card Number 1.docx" directly indicates it contains user bank card numbers, which are user sensitive information and belong to the company's sensitive data |Analysis process content. |
|.risk_status |Number |1 |Risk status. 1=risky, 2=no risk. |
|.disposal_status |Number |1 |Disposal status. 1=pending processing. The value is always 1. |
|.user_info |Object |\- |User information. |
|.user_name |String |Zhang San |User name. |
|.user_email |String |a@b.c |User email address. |
|.user_mobile |String |18800001111 |User mobile number. |
|.user_status |Number |1 |User account status. |


 &nbsp;

<span id="data-loss-prevention-dlp-local-file-collection-logs"></span>
# DLP \- Local Sensitive File Analysis Log

```JSON
<14>1 2026-02-02T16:23:29+08:00 - xxx 3161068 - - {
  "x_key": "dlp_collection_file",
  "collection_config_key": "192619cd00******",
  "collection_config_name": "New version test context",
  "task_id": "19274be1b5******",
  "task_start_time": 1770020577,
  "task_end_time": 1770020609,
  "user_email": "user@example.com",
  "device_id": "68664d9bfc545e0608ea663d5c******",
  "device_name": "MacBook Pro",
  "device_hostname": "MacBook Pro",
  "device_serial_number": "D0Q7******",
  "device_os": "Mac",
  "device_os_version": "Mac 15.6.1",
  "app_version": "3215",
  "app_build_number": "00000",
  "file_node_id": "4977ED58-F2E3F437-4D4DF87E-63******",
  "file_full_path": "/Users/example/Downloads/Documentation.pdf",
  "file_mine_type": "application/pdf",
  "file_extension": "pdf",
  "matches": [
    {
      "data_rule_key": "file:1925c365d0******",
      "data_rule_name": "File Content",
      "data_rule_level": "L4",
      "data_attr": 2,
      "match_type": 0,
      "match_times": 0,
      "match_pos": 0,
      "match_len": 0,
      "context": "og/Pages 2 0 R/Lang(zh) /StructTreeRoot 4220 0 R/Outlines 2702 0 R/MarkInfo\u003c\u003c/Marked true\u003e\u003e/Metadata 113698 0 R/ViewerPr",
      "expect_matched_value": "",
      "match_info": "[{\"match_name\":\"\",\"match_type\":1,\"match_value\":\"data:phone_num\",\"match_times\":57},{\"match_name\":\"\",\"match_type\":1,\"match_value\":\"data:phone_num\",\"match_times\":57}]",
      "match_pos_v1": [53, 61, 67, 96],
      "match_len_v1": [6, 6, 6, 6],
      "match_file_path": ""
    }
  ]
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_collection_file |Log type ID. |
|collection_config_key |String |192619cd00\*\*\*\*\*\* |Unique identifier of the collection configuration. |
|collection_config_name |String |New version test context |Collection configuration name. |
|task_id |String |19274be1b52e637f |Task ID. |
|task_start_time |Number |1770020577 |Task start timestamp (seconds). |
|task_end_time |Number |1770020609 |Task end timestamp (seconds). |
|user_email |String |user@example.com |User email address. |
|device_id |String |68664d9bfc545e0608ea663d5c\*\*\*\*\*\* |Unique device identifier ID. |
|device_name |String |MacBook Pro |Device name. |
|device_hostname |String |MacBook Pro |Device hostname. |
|device_serial_number |String |D0Q7\*\*\*\*\*\* |Device serial number. |
|device_os |String |Mac |Device operating system type. |
|device_os_version |String |Mac 15.6.1 |Device operating system version. |
|app_version |String |3215 |Client version number. |
|app_build_number |String |00000 |Client minor version number. |
|file_node_id |String |4977ED58\-F2E3F437\-4D4DF87E\-63\*\*\*\*\*\* |Unique file node identifier. |
|file_full_path |String |/Users/example/Downloads/Document.pdf |Full file path. |
|file_mine_type |String |application/pdf |File MIME type. |
|file_extension |String |pdf |File extension. |
|matches |Object | |Detailed matched context information. |
|.data_rule_key |String |file:1925c365d0\*\*\*\*\*\* |Associated data rule identifier. |
|.data_rule_name |String |File Content |Associated data rule name. |
|.data_rule_level |String |L4 |Associated data rule level. |
|.data_attr |Number |2 |Match attribute: 1\-file name match, 2\-file content match. |
|.match_type |Number |0 |Match type: 1\-built\-in rule, 2\-custom keyword, 3\-regular expression. |
|.match_times |Number |0 |Number of hits in the current context. |
|.match_pos |Number |0 |Start position of the matched content. |
|.match_len |Number |0 |Length of the matched content. |
|.context |String |og/Pages 2 0 R/Lang(zh) /StructTreeRoot 4220 0 R/... |Actual matched context fragment. |
|.expect_matched_value |String | |Expected matched value. |
|.match_info |String |[{"match_name":"","match_type":1,"match_value":"data:phone_num","match_times":57}, ...] |Detailed hit information in JSON. It includes hit type, data label, count, and more. |
|.match_pos_v1 |Number |[53, 61, 67, 96] |Start positions of each matched content item in the context. |
|.match_len_v1 |Number |[6, 6, 6, 6] |Lengths of each matched content item in the context. They correspond one\-to\-one with the start positions. |
|.match_file_path |String | |File path corresponding to the matched content. This field has a value for compressed packages and nested files. |


 &nbsp;

<span id="dlp-ai-tool-code-repository-audit-logs"></span>
# DLP AI Development Tool Control

```JSON
<14>1 2026-06-18T19:28:26+08:00 - xxx 519342 - - {
    "x_key": "dlp_ai_tool",
    "event_id": "9A97C4D6-BA67-496F-9E1B-F3B42F******",
    "open_id": "ou_7D2******",
    "username": "Zhang San",
    "user_email": "zhangsan@example.com",
    "mobile": "",
    "department_path": "feilian",
    "roles": "",
    "timestamp": 1781782068,
    "report_time": 1781782103,
    "device_ip": "10.x.x.x",
    "device_id": "67b808ba4a7e88493a17772f97******",
    "device_name": "Device-01",
    "device_hostname": "Host-01",
    "device_serial_number": "SN-8CDA",
    "device_os": "mac",
    "app_version": "3.3.16",
    "app_build_number": "6200",
    "anonymous_login": 0,
    "trigger_action": 4,
    "ai_tool_key": "trae_cn",
    "action_type": "hook",
    "repo_remote_url": "https://github.com/example/project.git",
    "repo_local_path": "/Users/user/workspace/project",
    "model_base_url": "https://api.example.com/v1",
    "login_account": "user@example.com",
    "account_type": 2,
    "enterprise_name": "Example Corp",
    "config_key": "7b411997-b917-4353-a0d2-422645******",
    "config_name": "AI Audit Policy"
}
```


&nbsp;


|**Field** |**Type** |**Example** |**Description** |
|---|---|---|---|
|x_key |String |dlp_ai_tool |Event classification identifier. |
|event_id |String |25bc9306\-e89b\-4744\-92fb\-690a53\*\*\*\*\*\* |Unique event ID. |
|open_id |String |ou_kWmn2GweV4 |User OpenID. |
|username |String |Zhang San |User name. |
|user_email |String |zhangsan@example.com |User email address. |
|mobile |String |13000000000 |User mobile number. |
|department_path |String |feilian |User department path. |
|roles |String |rd |User role information. |
|timestamp |Number |1781770930 |Event occurrence timestamp. Unit: seconds. |
|report_time |Number |1781770980 |Event reporting timestamp. Unit: seconds. |
|device_ip |String |10.x.x.x |Device IP address. |
|device_id |String |68ca5b93e1fa7587b154a0f9ec\*\*\*\*\*\* |Unique device identifier. |
|device_name |String |Device\-01 |Device name. |
|device_hostname |String |Host\-01 |Device hostname. |
|device_serial_number |String |SN\-8CDA |Device serial number. |
|device_os |String |mac |Device operating system. |
|app_version |String |3.3.16 |SealSuite client version. |
|app_build_number |String |6200 |SealSuite client build number. |
|anonymous_login |Number |0 |Client login status. 0 indicates normal login. |
|trigger_action |Number |4 |Disposal action actually executed by the client. The current value 4 indicates audit. |
|ai_tool_key |String |trae_cn |AI tool identifier. |
|action_type |String |hook |Operation type.<br><br><br>* edlp: Local read.<br><br>* hook: Upload inference. |
|repo_remote_url |String |[https://github.com/example/project.git](https://github.com/example/project.git) |Remote code repository address. |
|repo_local_path |String |/Users/user/workspace/project |Local code repository path. |
|model_base_url |String |[https://api.example.com/v1](https://api.example.com/v1) |AI model Base URL. |
|login_account |String |user@example.com |Login account. |
|account_type |Number |2 |Account type.<br><br><br>* 0: Unknown.<br><br>* 1: Individual.<br><br>* 2: Enterprise. |
|config_key |String |becf1471\-fa22\-4090\-b79c\-69ef32\*\*\*\*\*\* |Unique audit configuration identifier. |
|config_name |String |AI Audit Policy |Audit configuration name. |
