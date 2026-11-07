---
title: "Task configuration"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_en-us"
---

This document introduces how to create log delivery tasks in BytePlus CDN. You can create up to 20 tasks.

The task creation wizard includes two steps:


1. Configure delivery settings: Configure how logs are delivered.

2. Select domains: Select the domains for log delivery.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260331073913-458064312276.png) </span>

<span id="step-1-configure-delivery-settings"></span>
## Step 1: Configure Delivery Settings

In this step, you can specify to deliver real\-time logs to a supported log analysis service or a custom HTTP server.

<span id="byteplus-log-service-tls"></span>
### BytePlus Log Service (TLS)

<span id="prerequisites"></span>
#### Prerequisites

If you are delivering real\-time logs to TLS for the first time, when you click **BytePlus Torch Log Service (TLS)**  under **Destination**, the page will prompt you to activate TLS service and then authorize CDN to access TLS. Please follow the instructions on the console page.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260311093839-246307871934.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you authorize CDN to access TLS, the <code>ServiceRoleForCDN</code> role will be added to your BytePlus primary account.</div>


* <div data-tips="true" data-tips-type="tip">For IAM accounts to have permission to create log delivery tasks, they need to be granted the <code>CDNLogsFullAccess</code> system policy.</div>



If the prerequisites are met, when you click **BytePlus Torch Log Service (TLS)**  under **Destination**, you need to complete the following configuration to enable CDN to deliver real\-time logs to your specified log topic. See the configuration instructions below.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260331074416-1684070818744.png) </span>

<span id="configuration-instructions"></span>
#### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Collection Region |The service region from which CDN nodes collect logs. Currently, you can only specify **Outside Chinese Mainland**, which means logs are collected from CDN nodes located outside the Chinese Mainland. |
|Delivery Region |Indicates the physical region where TLS stores logs. You can choose a region close to you to reduce log query latency.<br><br>&nbsp;<br><br>Available regions include:<br><br><br>* China (Hong Kong)<br><br>* Asia Pacific (Jakarta)<br><br>* Asia Pacific (Johor)<br><br><br>The default region is "Asia Pacific (Jakarta)". |
|Log Project |Indicates the log project to which the logs belong. A log project is like a folder that contains one or more files (log topics).<br><br>&nbsp;<br><br>The default log project is `cdn-log`. You can also click **Create Log Project** to create a custom log project, or select an existing project from the dropdown list.<br><br>&nbsp;<br><br>Log project input requirements are as follows:<br><br><br>1. Length must be 3\-64 characters, can include Chinese characters, lowercase letters, numbers, underscores (_), and hyphens (\-). Chinese characters count as 3 characters.<br><br>2. Cannot start or end with a hyphen (\-) or underscore (_).<br><br>3. Cannot start with `tls_`, `tos_`, `tls-` , or `volc_`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The dropdown list only shows log projects you created by clicking <strong>Create Log Project</strong>. Log projects you created in TLS will not appear in the list.</div><br> |
|Log Topic |Indicates the log topic where logs are stored. A log topic is like a file contained in a folder (log project).<br><br>&nbsp;<br><br>Log topic input requirements are the same as log project input requirements. |
|Log Retention Period |Indicates how long logs are stored in TLS, ranging from 1 to 3649 days.<br><br>&nbsp;<br><br>To store logs permanently, enter `3650`. |
|Sampling Rate |Indicates the log sampling rate, ranging from 0.00 to 100.00, accurate to 2 decimal places.<br><br>&nbsp;<br><br>Sampling rate refers to the proportion of logs delivered. For example, if you set the sampling rate to 10, it means that for every 100 logs collected on CDN nodes, CDN will randomly select 10 logs to deliver to your specified location. |
|Remarks |Indicates remarks for this delivery configuration.<br><br>&nbsp;<br><br>Remarks input requirements are as follows:<br><br><br>1. Length must be 3\-64 characters, can include Chinese characters, letters, numbers, underscores (_), and hyphens (\-). Chinese characters count as 3 characters.<br><br>2. Cannot start or end with a hyphen (\-) or underscore (_). |


<span id="alibaba-cloud-simple-log-service-sls"></span>
### Alibaba Cloud Simple Log Service (SLS)

<span id="prerequisites"></span>
#### Prerequisites

If you are delivering real\-time logs to SLS for the first time, you need to complete the following steps:


1. Activate SLS service under your Alibaba Cloud account.

2. Create a Project and Logstore in SLS.

3. Obtain your Alibaba Cloud account's AccessKey ID and AccessKey Secret. This account needs permissions to manage SLS.


If you have completed the above steps, when you click **Alibaba Cloud Simple Log Service (SLS)**  under **Destination**, you need to complete the following configuration to have CDN deliver real\-time logs to your specified Logstore. See the configuration instructions below.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260331074327-1621349883941.png) </span>

<span id="configuration-instructions"></span>
#### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Collection Region |Indicates which service region's CDN nodes to collect logs from. Currently, you can only specify **Outside Chinese Mainland**, which means logs are collected from CDN nodes located outside the Chinese Mainland. |
|Log Project Endpoint |Indicates the public domain name of the Project. For example, `ap-southeast-1.log.aliyuncs.com`.<br><br>&nbsp;<br><br>The endpoint cannot have leading or trailing spaces. |
|Log Project |Indicates the Project you created, with a length not exceeding 64 characters. |
|Logstore |Indicates the Logstore you created, with a length not exceeding 64 characters. |
|AccessKey ID |Indicates your Alibaba Cloud account's AccessKey ID, with a length not exceeding 128 characters. |
|AccessKey Secret |Indicates your Alibaba Cloud account's AccessKey Secret, with a length not exceeding 128 characters. |
|Sampling Rate |Indicates the log sampling rate, ranging from 0.00 to 100.00, accurate to 2 decimal places.<br><br>&nbsp;<br><br>Sampling rate refers to the proportion of logs delivered. For example, if you set the sampling rate to 10, it means that for every 100 logs collected on CDN nodes, CDN will randomly select 10 logs to deliver to your specified location. |
|Remarks |Indicates remarks for this delivery configuration.<br><br>&nbsp;<br><br>Remarks input requirements are as follows:<br><br><br>1. Length must be 3\-64 characters, can include Chinese characters, letters, numbers, underscores (_), and hyphens (\-). Chinese characters count as 3 characters.<br><br>2. Cannot start or end with a hyphen (\-) or underscore (_). |


<span id="http-endpoint"></span>
### HTTP Endpoint

<span id="prerequisites"></span>
#### Prerequisites


* You have obtained the access point of the HTTP server. If the HTTP server requires request authentication, you also need to obtain the authentication key.

* The HTTP server has implemented the token algorithm described below. When receiving log delivery requests from CDN, the HTTP server authenticates the requests.


<span id="configuration-instructions"></span>
#### Configuration Instructions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After completing the configuration, click <strong>Test</strong> to validate it. You can only proceed to the next step if the test passes.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260331074248-1453363538012.png) </span>


|**Configuration** |**Description** |
|---|---|
|Collection Region |Indicates which service region's CDN nodes to collect logs from. Currently, you can only specify **Outside Chinese Mainland**, which means logs are collected from CDN nodes located outside the Chinese Mainland. |
|HTTP Endpoint |Indicates the access point, port, and log storage path of the HTTP server. The port and path are optional. The access point must start with `http://` or `https://`, cannot contain spaces at the beginning or end, and cannot exceed 1,024 characters. For example, `https://www.example.com:8080/cdn-logs`. |
|Compression |Indicates whether to enable GZip compression when CDN delivers logs. If the HTTP server can handle GZip\-compressed content, you can enable file compression to reduce the size of delivered logs. |
|Require Authentication |Indicates whether the HTTP server requires request authentication. |
|Authentication Key |This setting appears only if you enable **Require Authentication**. The authentication key is used to calculate the token, with a length of 6\-40 characters. The authentication key is only known to the HTTP server and the client.<br><br>&nbsp;<br><br>See the authentication process and token algorithm below. |
|Sampling Rate |Indicates the log sampling rate, ranging from 0.00 to 100.00, accurate to 2 decimal places.<br><br>&nbsp;<br><br>Sampling rate refers to the proportion of logs delivered. For example, if you set the sampling rate to 10, it means that for every 100 logs collected on CDN nodes, CDN will randomly select 10 logs to deliver to your specified location. |
|Set Request Headers |Indicates specific headers that need to be included in the request when CDN delivers logs to the HTTP server. You can add up to 10 headers.<br><br>&nbsp;<br><br>The header cannot be `User-Agent` or start with `x-bdcdn-`. The header name and header value cannot exceed 1,024 characters. |
|Remarks |Indicates remarks for this delivery configuration.<br><br>&nbsp;<br><br>Remarks input requirements are as follows:<br><br><br>* Length must be 3\-64 characters, can include Chinese characters, letters, numbers, underscores (_), and hyphens (\-). Chinese characters count as 3 characters.<br><br>* Cannot start or end with a hyphen (\-) or underscore (_). |


<span id="authentication-process-and-token-algorithm"></span>
#### Authentication Process and Token Algorithm

**Authentication Process**


1. Before sending a log delivery request, CDN calculates a token based on the authentication key and token algorithm. Additional fields participating in the token calculation include a specified timestamp, the path in the server endpoint, and a random integer generated by CDN (rand). The range of rand is 0\-2147483647.

2. Send a POST request to the HTTP server.

   * The request URL includes the `auth_key` query parameter, with the parameter value formatted as `timestamp-rand-token`.

   * The request URL format is `http://[http_server_address]:[port]/[uri]?auth_key=timestamp-rand-token`

      Request URL example: `http://https://www.example.com:8080/cdn-logs?auth_key=1744870608-14567-6459280fed54315c2960f9ae2e91807d`

   * The request body contains multiple logs, separated by `\n`.

3. After receiving the request, the HTTP server calculates the token based on the authentication key, the path, timestamp, and random number. See the token example and sample code below.

4. The HTTP server determines whether the two tokens are the same. If the tokens are the same, authentication is passed.


**Token Algorithm**


* MD5(uri\-timestamp\-rand\-key)


**Token Example**

Assume:


* Server endpoint is `https://www.example.com:8080/cdn-logs`.

* Authentication key is `1a2c!=A?1`.

* The request timestamp is `1744870608`.

* Random integer generated by CDN (rand) is `14567`.


Then the token calculation formula is `MD5(/cdn-logs-1744870608-14567-1a2c!=A?1)`, and the calculated token is `6459280fed54315c2960f9ae2e91807d`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this example, if the server endpoint does not include a path, the token calculation formula would be <code>MD5(-1744870608-14567-1a2c!=A?1)</code>.</div>


**Token Calculation Sample Code**

Refer to the following sample code to implement token calculation logic on the HTTP server.

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e04302d80d63c80856cde42b1e99ab24.txt" name="Sample Code for Go.txt">Sample Code for Go.txt</Attachment>


&nbsp;

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7950346a19ce87b251975ee59d1a0343.txt" name="Sample Code for Java.txt">Sample Code for Java.txt</Attachment>


&nbsp;

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bf9b9f8dfcb896c98ae826d865c632b8.txt" name="Sample Code for PHP.txt">Sample Code for PHP.txt</Attachment>


&nbsp;

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7de0d15ca67e107fb7bd1bf6e0c38082.txt" name="Sample Code for Python.txt">Sample Code for Python.txt</Attachment>


&nbsp;

 &nbsp;

<span id="splunk-logging"></span>
### Splunk Logging

<span id="prerequisites"></span>
#### Prerequisites

Before delivering real\-time logs to Splunk, you need to enable the HTTP Event Collector (HEC) feature in Splunk and obtain the HEC endpoint and HEC token.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260331074150-789921054991.png) </span>

<span id="configuration-details"></span>
#### Configuration Details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After completing the configuration, click <strong>Test</strong> to verify if your settings are valid. You can proceed to the next step only after the test passes.</div>



|**Configuration** |**Description** |
|---|---|
|Collection Region |Indicates the region from which logs are collected on CDN nodes. Currently, you can only specify **Global (Excl. Mainland China)** , which means collecting logs from CDN nodes located outside Mainland China. |
|HEC Endpoint |Indicates the HTTP Event Collector (HEC) endpoint URL of Splunk. You can refer to the [Splunk Documentation](https://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector) for more information. |
|HEC Token |Indicates the HTTP Event Collector (HEC) token of Splunk. |
|Sampling Rate |Indicates the log sampling rate. The range is 0.01 \- 100.00, accurate to 2 decimal places. The default is 100%.<br><br>&nbsp;<br><br>The sampling rate refers to the proportion of logs delivered. **Setting to 0 is not supported.**  |
|Gzip Compression |Indicates whether to enable Gzip compression when CDN delivers logs. Disabled by default. You can enable this option to reduce the size of delivered logs. |
|Description |Indicates remarks for this delivery configuration.<br><br>&nbsp;<br><br>The input requirements for remarks are as follows:<br><br><br>1. The length is 3 \- 64 characters, and can contain Chinese, letters, numbers, underscores (_), and hyphens (\-). One Chinese character occupies 3 characters.<br><br>2. It cannot start or end with a hyphen (\-) or an underscore (_). |


<span id="google-bigquery"></span>
### Google Cloud BigQuery

<span id="prerequisites"></span>
#### Prerequisites

Before delivering real\-time logs to Google Cloud BigQuery, you need to complete the following preparations in Google Cloud Platform (GCP):


1. Create the resource hierarchy in BigQuery: **Project** \> **Dataset** \> **Table**.

2. Create a **Service Account** with appropriate BigQuery access permissions and download its JSON key file.

3. A schema that can receive the standard fields of CDN real\-time logs has been configured for this table.

   **Configuration method**: When creating a table in the BigQuery console, navigate to the **Schema** configuration section, enable the **Edit as text** mode, and then paste the JSON code from the attachment into the text box to generate the correct table schema.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22e3134ba6154e3e92b6adc68c313af7~tplv-goo7wpa0wc-image.image" name="schema.json">schema.json</Attachment>
   


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260331074101-1559017950580.png) </span>

<span id="configuration-details"></span>
#### Configuration Details


|**Configuration** |**Description** |
|---|---|
|Source Region |Indicates the region from which logs are collected on CDN nodes. Currently, you can only specify **Outside Chinese Mainland**, which means collecting logs from CDN nodes located outside the Chinese Mainland. |
|Service Account Key File |Upload the JSON key file for your Google Cloud Service Account. This file contains authentication credentials used to authorize BytePlus CDN to access your BigQuery resources and stream logs.<br><br>&nbsp;<br><br>After parsing the uploaded JSON file, the system extracts the following key fields for authentication and configuration:<br><br><br>* **private_key**: The RSA private key of the service account, used to sign the JWT (JSON Web Token) for identity verification.<br><br>* **client_email**: The unique email address of the service account, used as the issuer field in the JWT.<br><br>* **private_key_id**: The unique identifier of the private key, used to quickly locate the corresponding public key for signature verification.<br><br>* **token_uri**: The URL to obtain the OAuth 2.0 token.<br><br>* **project_id**: Part of the URL used to build the BigQuery API request. |
|GCP Project ID |Indicates the GCP Project ID where BigQuery is located. If you uploaded the Service Account JSON file, the system will automatically extract and populate this field. You can also modify it manually. |
|Dataset ID |Indicates the Dataset ID you created in BigQuery. |
|Table ID |Indicates the Table ID you created in BigQuery. |
|Sampling Rate |Indicates the log sampling rate. The range is 0.01 \- 100.00, accurate to 2 decimal places. The default is 100%.<br><br>&nbsp;<br><br>The sampling rate refers to the proportion of logs delivered. **Setting to 0 is not supported.**  |
|Remarks |Indicates remarks for this delivery configuration.<br><br>&nbsp;<br><br>The input requirements for remarks are as follows:<br><br><br>1. The length is 3 \- 64 characters, and can contain Chinese, letters, numbers, underscores (_), and hyphens (\-). One Chinese character occupies 3 characters.<br><br>2. It cannot start or end with a hyphen (\-) or an underscore (_). |


<span id="step-2-select-domains"></span>
## Step 2: Select Domains

In this step, you select which domains' real\-time logs to deliver.


* If you want to deliver real\-time logs for all domains, set **Domains** to **All Domains**. For domains you add to CDN in the future, their real\-time logs will also be delivered.

* If you want to deliver real\-time logs for specific domains, set **Domains** to **Selected Domains**, and then select these domains. You can select up to 200 domains.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a delivery task associated with all domains already exists, you cannot create a delivery task associated with specified domain name, and vice versa.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_940d39bf60ff9ef38db93da77c4a17db.png) </span>

<span id="iam-account-permission-description"></span>
### IAM Account Permission Description

In Step 2, IAM accounts can only add domains they have permission to operate. Additionally, if an IAM account is granted relevant policies with project restrictions (as shown in the figure below), meaning the IAM account has permission to access only domains that belong to the specified BytePlus project, then this IAM account cannot specify **Selected Domains**.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e56963947672662191778a3211ab5038.png) </span>

<span id="view-log-delivery-tasks"></span>
## View Log Delivery Tasks

After creating a delivery task, your task appears in the task list.


* If a task configuration needs adjustment, you can click **Modify** in the **Actions** column.

* To view the delivery task configuration, you can click **Expand View** in the **Task Details** column of the corresponding task.

* For logs delivered to TLS, you can click **Query Logs** in the **Actions** column, and then query and analyze logs on the **Query and analysis** page. See [Log Query Examples](https://docs.byteplus.com/en/docs/byteplus-cdn/log-query-examples_en-us).


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ad62c57bbdbf794acadce7d08d9d4fd3.png) </span>

<span id="fb8fd7d2"></span>
## Delete Log Delivery Tasks

If you no longer need a real\-time log task, you can first disable the task and then delete it.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you delete a task that delivers logs to TLS, the corresponding log topic is also deleted.</div>
