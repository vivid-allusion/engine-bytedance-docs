---
title: "Query data plane auditing logs"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/query-data-plane-audit-logs"
---

Data plane audit log requires manual activation, recording events through the built\-in system plugin to the instance itself. This article explains how to view data plane audit logs on the Kibana/Dashboards page and Cloud Search console.

<span id="f1af8c62"></span>
## Precautions

Currently, only Elasticsearch instances version 7.10.2 and above and OpenSearch instances version 2.9.0 and above support security audit features. For Elasticsearch instances, the built\-in system plugin is `opendistro_security`. For OpenSearch instances, the built\-in system plugin is `opensearch-security`.

<span id="974cd08f"></span>
## View audit logs

After enabling data plane audit, events such as reading and writing indexes, modifying index mappings and settings, and viewing cluster health are recorded. These data access events are written to indexes with fixed prefixes and suffixes:


* For Elasticsearch instances, the prefix is `.security-auditlog-` and the suffix is the date.

* For OpenSearch instances, the prefix is `security-auditlog-`, followed by the date.


<span id="fb3b92ed"></span>
### View audit logs on the Kibana/Dashboards page

You can configure the index pattern and then view audit logs on the Discover page.


1. Log in to the Kibana/Dashboards page using the public address. For related documentation, see [Log in to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool).

2. Configure the index pattern.

   1. Select **Stack Management \> Index patterns** from the Kibana menu bar, then click **Create index pattern**.

   2. Set the index pattern to `.security-auditlog-*`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d635cfb0b184d88b195dcae40aa4a34~tplv-goo7wpa0wc-image.image) </span>

   3. Select the `@timestamp` field as the time filter field.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d007c28cbbe4b6d9227481c264f73d1~tplv-goo7wpa0wc-image.image) </span>

3. View audit logs on the Discover page.

   1. Select **Discover** in the Kibana menu bar.

   2. Select the configured index pattern, set the appropriate time range, and view the audit logs.

      For log field details, refer to the **Audit Log Field Description** in this document.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc39d9bf1c554d8a91a02ffe0b20b9f7~tplv-goo7wpa0wc-image.image) </span>


<span id="47f30a39"></span>
### View audit logs in the Cloud Search console


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name to enter the instance details page.

4. In the left navigation of instance details, select **Observability \> Security audit**, then go to the **Data plane auditing** page to see the data plane audit log list for the instance.

   * In the audit log list, quickly view logs for the last 1 hour, 1 day, or 1 week, or use the time filter to set a custom query period.

   * The audit log list supports filtering logs by event type and up to twenty groups of filter criteria. Supported query event types are as follows:

      * BAD_HEADERS

      * FAILED_LOGIN

      * MISSING_PRIVILEGES

      * GRANTED_PRIVILEGES

      * OPENDISTRO_SECURITY_INDEX_ATTEMPT

      * SSL_EXCEPTION

      * AUTHENTICATED

      * INDEX_EVENT

      * COMPLIANCE_DOC_READ

      * COMPLIANCE_DOC_WRITE

      * COMPLIANCE_EXTERNAL_CONFIG

      * COMPLIANCE_INTERNAL_CONFIG_READ

      * COMPLIANCE_INTERNAL_CONFIG_WRITE


<span id="e7d15251"></span>
## Audit log field description


|**Category** |**Field name** |**Type** |**Description** |
|---|---|---|---|
|time |@timestamp |date |event time. |
|server |audit_cluster_name |string |ES instance ID. |
||audit_node_host_address |string |ES instance server host address. |
||audit_node_host_name |string |ES instance server hostname. |
||audit_node_id |string |ES instance server node ID. |
||audit_node_name |string |ES instance server node name. |
|Client |audit_request_remote_address |string |Client IP address. |
|Visitor/account |audit_request_effective_user |string |The actual user participating in the permission check, for example, admin. |
||audit_request_effective_user_is_admin |bool |Whether the actual user is admin. |
||audit_request_initiating_user |string |The user who initiated the request. Recorded only when different from the user actually involved in the permission check. |
|event type/layer |audit_category |enum |Event type. For supported event types, see [Log collection parameters](https://docs.byteplus.com/docs/cloudsearch/audit-collection-parameters#dcf6455c). |
||audit_request_layer |enum |Request level, REST or TRANSPORT. |
||audit_request_origin |enum |Request origin layer, REST or TRANSPORT. |
|HTTP request |audit_rest_request_method |enum |HTTP request methods, such as GET, PUT, POST, DELETE, HEAD, etc. |
||audit_rest_request_path |string |HTTP request path. |
||audit_rest_request_headers |object |HTTP request header. |
||audit_rest_request_params |object |HTTP request parameters. |
||audit_request_body |string |HTTP request body. |
|RPC request information |audit_transport_request_type |string |RPC request type, such as `CreateIndexRequest`. |
||audit_request_privilege |string |RPC request path, such as `indices:admin/create`. |
||audit_transport_headers |object |RPC request header. |
||audit_trace_resolved_indices |string array |Index parsed from the request. |


For more information about audit log fields, refer to the open\-source documentation [Audit log field reference](https://opendistro.github.io/for-elasticsearch-docs/docs/security/audit-logs/field-reference/).
