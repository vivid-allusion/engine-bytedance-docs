---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DevMind-overview"
---

This topic covers the capabilities of each DevMind module and explains how to use DevMind to analyze bucket data.

<span id="jF2RWv0I"></span>
## Introduction

DevMind is a one\-stop data analysis and decision\-making platform for TOS. Focused on buckets, DevMind integrates usage statistics, log analysis, Storage Lens, and Insight Assistant. Together, these features provide a comprehensive view of storage health in four key areas: cost, performance, security, and efficiency. DevMind transforms large volumes of storage data from "silent logs" into "decision\-making evidence."

Among these capabilities, log analysis and Storage Lens are powered by Torch Log Service (TLS) [Cloudlens for TOS](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS). The related billing rules are defined by TLS. For more information, see [Billing notes](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en#4fe96fce).

The following table describes the DevMind modules.


|Module |Description |
|---|---|
|Usage statistics |This module displays basic metrics, such as storage and retrieval capacity, traffic, and request counts, as time\-series line charts. This allows you to quickly understand short\-term resource usage. For more information, see [Usage statistics](https://docs.byteplus.com/en/docs/tos/docs-usage-statistics?lang=en). |
|Log analysis |You can use the per\-bucket access logs to observe traffic, requests, page views, unique visitors, operational behaviors, and access details for each bucket from perspectives such as resource usage, heat statistics, access analysis, security analysis, and query and analysis. For more information, see [Configuring log analysis kanban](https://docs.byteplus.com/en/docs/tls/Configure-log-analysis-dashboard). |
|Storage Lens |This module provides multidimensional analytics dashboards with daily aggregation. You can view snapshots, trends, top N, incremental changes, and bubble charts across four dimensions: region, storage type, bucket, and prefix. This dashboard is ideal for capacity planning and structural analysis. For more information, see [Configuring Storage Lens dashboards](https://docs.byteplus.com/en/docs/tls/Configure-pivot-dashboard). |
|Insight Assistant |This module provides access to TOS Agent, which is a natural\-language Q&A bot. Use it to ask questions, analyze data, and pinpoint issues in a conversational way. For more information, see [Using TOS Agent](https://docs.byteplus.com/en/docs/tos/Using-TOS-Agent?lang=en). |


<span id="Dmz6ziv6"></span>
## Constraints and limitations


|Category |Description |
|---|---|
|Activation and authorization |The first time you use DevMind, enable and authorize access to Cloudlens for TOS on the **Log analysis/Storage Lens** page. This will allow TOS to push access logs and operational data to Cloudlens for TOS. |
|Data accuracy |The metrics and statistical results in all DevMind modules are for reference only. They are not intended for billing or metering purposes. |
|Resource visibility |The regions and buckets that appear in the drop\-down lists of each module are consistent with your account permissions. You will not see any resources that you are not authorized to access. |
|AI\-generated results |The responses from Insight Assistant are generated automatically by AI and may not always be accurate. We recommend using them for reference only. Before making critical decisions, such as expanding capacity, making cost\-related changes, or troubleshooting, verify the information against the original data in the relevant dashboard. |


<span id="7hkIGyjo"></span>
## Billing notes

DevMind itself is free. However, you may incur charges for using log analysis and Storage Lens, which are provided by TLS Cloudlens for TOS. The following table describes the billing details.


|**Module** |**Additional cost** |**Billing notes** |
|---|---|---|
|Usage statistics |No (TOS) |Usage statistics is included with TOS and becomes available when TOS is activated. There are no additional charges. |
|Log analysis |Yes (TLS) |Log analysis is provided by TLS Cloudlens for TOS. For billing details, see [Billing notes](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en#4fe96fce). |
|Storage Lens |Yes (TLS) |Storage Lens is provided by TLS Cloudlens for TOS. For billing details, see [Billing notes](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en#4fe96fce). |
|Insight Assistant |No (TOS); Yes (other services) |* TOS will not charge you for using Insight Assistant.<br><br>* VeArk provides the underlying capability and charges based on model usage. For more information on billing rules, see [Model pricing](https://docs.byteplus.com/en/docs/82379/1544106?lang=en).<br><br>* When Insight Assistant invokes log analysis or Storage Lens, you will be charged according to their respective billing rules. |


<span id="WkPLh4WY"></span>
## Use cases

DevMind addresses core needs, including storage operations, cost optimization, security auditing, and routine operations. It also provides targeted data analysis capabilities for various roles. The following scenarios cover everything from routine monitoring and troubleshooting to cost management and content retrieval. These scenarios will help you quickly identify the right feature for your needs.


|Use case |Description |Recommended features |
|---|---|---|
|Storage cost trend analysis |Operations and finance personnel need a clear view of storage usage, including its composition and trends. They must be able to identify the fastest\-growing buckets and prefixes (directories), as well as assess cost growth against expectations, in order to support budget planning. |**Usage statistics**: It provides key metrics such as storage usage, object versions, and incomplete multipart uploads organized by region, storage type, bucket, and prefix. Trend charts of this data help pinpoint the sources of sudden usage spikes.<br><br>**Insight Assistant**: You can use natural language questions to gain insight into storage usage. For example, you can ask, "Which bucket has seen the most growth in the last week?" |
|Access anomaly troubleshooting |When users report inaccessible files or an increase in error codes, operations personnel must quickly determine the source of the problem. Log analysis provides visual dashboards and easy diagnostics with the help of Insight Assistant. |**Log analysis**: It identifies anomaly types quickly through request trends, status code distribution, and latency charts. It also supports drill\-down analysis by IP address, referrer, operation type, and more.<br><br>**Insight Assistant**: You can paste the error link or details into the chat box of the assistant. The assistant will automatically check permission policies, object existence, key validity, and other factors. Then, it will provide a root cause analysis and suggestions for remediation. |
|Security audit and anomalous access traceability |Security administrators must regularly audit access records to identify abnormal activity, such as frequent access from suspicious IP addresses, hotlinking from external sites, or unauthorized operations. This process requires tracing down to the individual objects. |**Storage Lens**: It provides object‑level access behavior analysis and filtering by IP address, referrer, and operation type. It also generates rankings to pinpoint suspicious sources precisely, such as the top X most frequently accessed IP addresses or objects.<br><br>**Log analysis**: You can use it to identify macro\-level anomaly trends. Then, use Storage Lens to drill down to specific objects for root cause tracing. |
|Hotspot identification and distribution optimization |Businesses that rely on content, such as image and video hosting and software distribution, need to identify frequently accessed files to plan content delivery network (CDN) preheating or data tiering strategies. This ensures a good user experience while optimizing distribution costs. |**Storage Lens**: You can use the access count ranking to quickly identify the objects that are accessed most frequently and where they are accessed from. This will help you develop an effective CDN preheating strategy.<br><br>**Log analysis**: You can analyze the access time distribution of hotspots to identify traffic spikes and inform elastic scaling decisions. |


<span id="Sje4SSQ4"></span>
## Quickly accessing DevMind


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the **DevMind** page, select the **Usage statistics**, **Log analysis**, **Storage Lens**, or **Insight Assistant** module depending on your needs.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The first time you use DevMind, go to the <strong>Log analysis/Storage Lens</strong> page. Then, click <strong>Enable and Authorize</strong> and follow the instructions to complete the authorization process.   </div>
   

&nbsp;

&nbsp;

&nbsp;

&nbsp;
