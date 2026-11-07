---
title: "How to Delete Service Discovery Configuration?"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/How-do-I-delete-service-discovery-configurations"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue Description

A user configured service discovery by using PodMonitor in a VKE cluster. After checking the metrics, the user deleted the PodMonitor CR configuration.

The user found that after deleting the configuration, the job corresponding to the deleted service was still present.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause Analysis

When the PodMonitor CRD object was deleted, the system did not simultaneously delete the corresponding PodScrape configuration. As a result, the configuration remained in effect.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

When you delete service discovery configurations, you also need to delete the corresponding Monitor and Scrape configurations. Perform the following steps:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following content uses PodMonitor as an example. To delete a ServiceMonitor, replace <code>podmonitor </code>with <code>servicemonitor </code>and <code>vmpodscrape </code>with <code>vmservicescrape</code>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the left menu bar, click **Cluster**. In the cluster list on the right side, select the target cluster.

3. Click the name of the cluster to go to the cluster configuration page.

4. Click **Workload \> Resource Explorer** on the left menu bar. Search for the `podmonitor` keyword in the resource list to find the object.

5. Click the object name to go to the details page, select the configuration to delete, and under the **Operation** column, select `...` \> **Delete** to delete the PodMonitor configuration.

6. Return to the **Resource Explorer** list, and search for `vmpodscrape `in the resource list.

7. Click the object name to go to the details page, select the configuration to delete, and under the **Operation** column, select `...` \> **Delete** to delete the PodScrape configuration.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result Validation

After the service discovery configuration is deleted, run the `up `query on the Explore page. If the corresponding job is no longer active, the service discovery configuration has been deleted.

&nbsp;
