---
title: "Configuring audit log collection parameters"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/audit-collection-parameters"
---

After data plane auditing is enabled, you can configure audit log collection parameters on the Kibana page. Log collection parameters have default values, and you can modify them as needed.

<span id="d17d7bd6"></span>
## Procedure


1. Log on to the Kibana page by using the public endpoint. For more information, refer to [Logging on to the visualization tool](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

2. In the Kibana menu bar, select **Security \> Audit logs**.

3. Configure the log collection parameters as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/389d5aa772704ae48309eab1c95a542e~tplv-goo7wpa0wc-image.image) </span>


<span id="dcf6455c"></span>
## Log collection parameters


|**Category** |**Parameter** |**Description** |
|---|---|---|
|Audit logging |Storage location |The location that stores audit outputs. The value is fixed to internal_elasticsearch. |
||Enable audit logging |The toggle switch for audit logging. The switch has the same effect as the **Data plane audit log** switch on the ES instance details page.<br><br><br>* Enabled<br><br>* Disabled |
|Layer settings |REST layer |The switch of the HTTP request collection feature.<br><br><br>* Enabled<br><br>* Disabled |
||REST disabled categories |A list of HTTP event types ignored during the collection process. When the value of the parameter is empty, HTTP events of all types are collected.<br><br>For more information on event types, refer to the **Event types** table. |
||Transport layer |The switch of the RPC request collection feature.<br><br><br>* Enabled<br><br>* Disabled |
||Transport disabled categories |A list of RPC event types ignored during the collection process. When the value of the parameter is empty, RPC events of all types are collected.<br><br>For more information on event types, refer to the **Event types** table. |
|Property settings |Bulk requests |The switch of the bulk request writing feature (`_bulk`). When the switch is turned on, the system records an audit log for each document that is written. We recommend that you turn off the switch.<br><br><br>* Enabled<br><br>* Disabled |
||Request body |The switch of the request body recording feature.<br><br><br>* Enabled<br><br>* Disabled |
||Resolve indices |The switch of the feature that extracts index names from requests. This feature takes effect only when the RPC request collection feature is enabled.<br><br><br>* Enabled<br><br>* Disabled |
||Sensitive headers |The switch of the sensitive header filtering feature. We recommend that you turn on the switch.<br><br><br>* Enabled<br><br>* Disabled |
|Ignored list |Ignored users |A list of accounts to be ignored during collection. The wildcard character `*` is allowed. If an account is included in the list, audit logs generated for the account are ignored.<br><br>Typical usage: To ignore system administrators, set this parameter to `bytees_*,admin,kibanaserver`. |
||Ignored requests |A list of the requests to be ignored during collection. The wildcard character `*` is allowed. If the type or action path of a request is included in the list, audit logs generated for the request are ignored.<br><br>Typical usage: To ignore query requests, set this parameter to `SearchRequest,MultiSearchRequest,indices:data/read/*`. |


**Event types**


|**Event Type** |**Event** |**Event Tracking Layer** |**Description** |
|---|---|---|---|
|Failure |FAILED_LOGIN |REST, Transport |Identity authentication failed. This event may occur when the user does not exist or the password is incorrect. |
||MISSING_PRIVILEGES |Transport |The user does not have the permission to execute the request. |
|Exception |SSL_EXCEPTION |REST, Transport |No trusted SSL or TLS certificate is available. |
||OPENDISTRO_SECURITY_INDEX_ATTEMPT |Transport |Unauthorized request. This event occurs when a non\-admin or unauthorized user attempts to modify the internal user or permission index of the security plugin. |
||BAD_HEADERS |REST, Transport |Risky request. This event occurs when the request attempts to overwrite the internal headers of the security plugin. |
|Success |AUTHENTICATED |REST, Transport |Permission authentication succeeded. |
||GRANTED_PRIVILEGES |Transport |The request was executed successfully. |
|Tag |INDEX_EVENT |Transport |Index management event: indices:admin/\*. |
