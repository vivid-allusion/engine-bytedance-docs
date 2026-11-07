---
title: "Enable data plane auditing"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/enabe-data-plane-audit"
---

Cloud Search provides two types of audit logs: control panel audit log and data plane audit log. Control panel audit log is enabled by default, recording events in the operation audit service; data plane audit log requires manual activation, recording data access events through built\-in plugins directly to the instance. This article explains how to enable data plane audit log.

<span id="e17fc9d7"></span>
## Precautions


* Security audit features are supported only on Elasticsearch instances version 7.10.2 and above, and OpenSearch instances version 2.9.0 and above. For Elasticsearch instances, the built\-in system plugin is `opendistro_security`. For OpenSearch instances, the built\-in system plugin is `opensearch-security`.

* After enabling data plane audit log, audit log index data will consume instance storage space, and extracting audit events will incur minor computational overhead, which may increase read/write latency and impact performance to some extent. Evaluate whether to enable data plane audit log based on your business needs.

* Enabling data plane audit log for the first time on an instance will trigger a rolling restart. It is recommended to enable this feature during off\-peak hours. Turning data plane audit log on or off after the initial activation does not trigger instance restart or update.

* Only select instances that support audit features. Audit functions consume additional resources. It is recommended to create new instances specifically for storing audit logs.

* When modifying the transfer instance, the current cluster will restart. It is recommended to perform this operation during off\-peak hours.

* It is recommended to configure monitoring alerts for the instance and upgrade configurations promptly when thresholds are exceeded. For detailed information on configuring monitoring alerts, see [Configure alarms with one click](https://docs.byteplus.com/docs/cloudsearch/one_click_alarm) and [Recommended alert rules](https://docs.byteplus.com/docs/6465/1219834).


<span id="023bc65e"></span>
## Prerequisites

Before enabling data plane audit log, ensure the system parameter `ActionAutoCreateIndex` is set to `true`; otherwise, automatic partitioning of data plane audit log indexes will be blocked.

For how to configure the `ActionAutoCreateIndex` parameter, see [Modify parameter configuration](https://docs.byteplus.com/docs/cloudsearch/system-parameters).

<span id="ea9c5534"></span>
## Enable data plane audit log


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name to enter the instance details page.

4. In the left navigation bar of the instance details, select **Observability \> Security audit**, then turn on the switch in the **Data plane auditing** section.

5. In the pop\-up **Enable data plane auditing** window, select **Transfer to instance**, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only instances that support audit functions can be selected. Because audit functions consume additional resources, we recommend creating a new instance specifically for storing audit logs.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking <strong>OK</strong>, the instance's running state will switch to <strong>Updating</strong>. <strong>When the instance status switches back to running</strong>, the data plane audit log function is successfully enabled.   </div>
   


<span id="9d018f68"></span>
## Other operations

After enabling the data plane audit log feature, the following operations are supported:


* **Disable data plane auditing**: turning off the data plane audit log does not trigger instance restart or update.

* **Configure auditing parameters**: after enabling the data plane audit log, the **Data plane audit log** page adds two parameters, `AuditOpenDays` and `AuditKeepDays`, to control the open days and retention days of the data plane audit log index. To modify parameter configuration, see [Managing the lifecycle of audit log indices](https://docs.byteplus.com/docs/cloudsearch/lifecycle-audit-log-index).

* **Modify transfer instance**: the instance that stores audit logs supports modification. Click **Modify transfer instance** in the data plane audit log area. In the pop\-up **Modify transfer instance** window, select a new transfer instance and click **OK** to complete the modification.

* **View audit logs**: the **Data plane audit log** page displays the current audit log list of the instance. For details on viewing data plane audit logs, see [Querying data plane audit logs](https://docs.byteplus.com/docs/cloudsearch/query-data-plane-audit-logs#47f30a39).
