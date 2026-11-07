---
title: "Managing an access log"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Managing-an-access-log"
---

## Enable the access log feature

### Action description

* Ensure the Network Load Balancer (NLB) instance has a TLS listener added. If not created, see [Adding a TLS listener](https://docs.byteplus.com/en/docs/clb/NLB-Adding-a-listener).

* Torch Log Service (TLS):

   * Make sure you have enabled TLS.

   * **After enabling the access log delivery to TLS feature, if the log topic has not been configured with key\-value index, the system will automatically configure key\-value index based on log fields. If index has already been configured, it will not be modified or overwritten.**

   * Please properly plan your log service resources and use clear naming conventions to avoid accidentally deleting access log resources in the log service console or having them used by other services.

* After enabling the access log delivery to TLS feature, it will take approximately 1 minute for log data to be collected and uploaded to the log service before it becomes available for viewing.

### Procedures

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target NLB instance name.

4. On the **Access log analysis** tab, click **Configure**.

5. Turn on the **Access Log Delivery TLS** switch and select the log project and log topic.

   |Parameter |Explanation |Instance |
   |---|---|---|
   |Log project |Select a Log Project. A Log Project is the fundamental resource management unit in the TLS, used for tenant resource isolation and access control.<br><br><br>* **Create log project**: Enter the name of the log project.<br><br>* **Select existing**: choose a log project from the dropdown.  |New log project<br><br>nlb\-log\-project\-1 |
   |Log topic |Select a Log Topic for the logs. A Log Topic is the fundamental unit in Log Service for log management (e.g., collection, storage, query, and analysis).<br><br><br>* New Log Topic: Enter the log topic name. The system automatically enables automatic log partition splitting for newly created log topics.<br><br>* Select existing: Select a log topic from the dropdown. If the existing log topic does not have automatically split log partitions enabled, exceeding the capacity of existing partitions may lead to data loss. Therefore, it is recommended to enable Automatic sharding.  |New log topic<br><br>nlb\-log\-topic\-1 |

6. Click **Confirm** to complete the action.

## View and modify the index

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target Network Load Balancer instance name.

4. On the **Access log analysis** tab, click **Index configuration** on the right.

5. View the key\-value index configured by the system by default. You can also modify it as needed.

## Analyze access log

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the project and region.

3. Click the target NLB instance name.

4. On the **Access log analysis** tab, input the search and analysis statement.

   A search and analysis statement consists of a search statement and an SQL analysis statement, separated by a pipe symbol (|). This syntax indicates that data statistics and analysis are performed on the results that match the search conditions.

5. Click **Search** to view the analysis results Displayed in charts.

## Disable the access log feature

After you disable access log for your NLB instance, neither the log project nor the log topic will be deleted by the NLB service. You can manage or delete them later as needed.

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target Network Load Balancer instance name.

4. On the **Access log analysis** tab, click **Edit** on the right to open the configuration window.

5. Turn off the **Access log** switch.

6. Click **Confirm** to complete the action.

## Related documents

[ModifyNetworkLoadBalancerAccessLog](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAccessLog)
