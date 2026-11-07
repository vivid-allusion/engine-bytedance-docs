---
title: "Add-on upgrade check"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Add-on_upgrade_check"
---

VKE provides the add\-on upgrade check feature. Before an add\-on is upgraded, VKE can check key risk points, such as the cluster environment, VKE workload status, and add\-on version compatibility. This identifies risks that may cause change failures or business impact in advance and prevents add\-ons from being upgraded directly in an abnormal environment.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · apply for trial</strong></a>]: This feature is currently in beta. Submit an application to use it.</div>


<span id="zn8aw2Zq"></span>
## Supported check scenarios

The add\-on upgrade check feature applies to the following common check scenarios. Some check items are defined by the add\-ons themselves and evolve with add\-on versions.


|**Check scenario** |**Scenario description** |
|---|---|
|Add\-on status check |Verify whether the add\-on is in a healthy state and can be upgraded. |
|Add\-on workload status check |Verify whether all Pods managed by the workloads associated with the add\-on, such as Deployments, DaemonSets, and StatefulSets, are running as expected. |
|Add\-on version consistency check |Verify whether different replicas of the same add\-on are running the same version. This prevents issues such as DaemonSet replicas not being upgraded and version mismatches. |
|Cluster configurations |Verify whether common environment information meets add\-on change requirements, such as cluster configurations and the number of available VPC IPs. |
|Custom resource check |Define custom check rules to verify add\-on resources that require attention. For example, cloud\-controller\-manager checks Services, and apmplus\-opentelemetry\-collector checks its own CRDs. |
|Custom checks in business scenarios |Each add\-on provides check rules tailored to specific business scenarios, which can be used to access the cluster API server of the user. For example, mgpu checks node resources, and vpc\-cni checks incompatible features in ConfigMaps. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The supported check items vary by add\-on. To learn the detailed check items supported by a specific add\-on, refer to the <a href="https://docs.byteplus.com/en/docs/vke/Add-on-release-notes">release notes</a> of the add\-on.</div>


<span id="q3AEm0xh"></span>
## Prerequisites


* The target add\-on has no running or pending upgrade check tasks.

* The target add\-on has the **Upgradable** tag.


<span id="EoyACE7l"></span>
## Procedure


<Tabs>
<Tab zoneid="uQWhbARy2M" title="Manually trigger">
<TabTitle>Manually trigger</TabTitle>

Before upgrading an add\-on, you can manually initiate an upgrade check to independently verify whether the current add\-on and its cluster meet the upgrade conditions. This operation does not trigger a version change.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. On the page that appears, click the name of the target cluster.

3. On the cluster management page, click **Addons** in the left navigation bar.

4. On the **Addons** page, find the add\-on to be upgraded and click `...` \> **Upgrade check**.

5. In the message that appears, confirm the information about the add\-on to be checked and click **Confirm**.

   You will be redirected to the **Add\-on upgrade check** page. You can refresh the page and wait for the add\-on upgrade check to complete.

6. After the add\-on upgrade check is complete, click **View details** in the **Actions** column that corresponds to the add\-on to view the add\-on upgrade check result.

   * If all add\-on upgrade check items have passed the check, you can upgrade this add\-on. For detailed operations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

   * If any upgrade check items fail, resolve the issues based on the cause, impact, and remediation suggestions displayed in the console, and then perform the add\-on upgrade check again.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a48a28c0bb9394d6650bc14be8764742.png) </span> 


</Tab>
<Tab zoneid="otR5GxukCY" title="Automatic trigger">
<TabTitle>Automatic trigger</TabTitle>

When you directly upgrade an add\-on, the system automatically triggers an add\-on upgrade check. For detailed instructions, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).


* Check passed: The system continues the add\-on upgrade, and you can track the upgrade progress in the add\-on change records.

* Check failed: The system stops this upgrade, and the add\-on remains at its pre\-upgrade version and state. You can view the cause of the failure in the upgrade check records and resolve the issue by following the remediation suggestions provided by the system.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To improve the success rate of add\-on upgrades, we recommend first manually triggering an upgrade check, reviewing any failed check items, and resolving the issues in advance.</div>



</Tab>
</Tabs>


<span id="ujIaa9ZS"></span>
## What to do next

VKE enables you to view upgrade check records. Upgrade check records provide a history of previous add\-on upgrade checks, helping you troubleshoot check failures and confirm the resolution status of check items.


1. In the left navigation bar of the cluster management page, click **Addons**.

2. In the upper\-right corner of the **Addons** page, click **Check log for add\-on upgrades**.

3. View previous check tasks in the record list. You can filter check records by add\-on name.

4. In the **Actions** column that corresponds to the target add\-on, click **View details** to view check details.

   If the **Pending** tab on the **Check details** page contains failed check items or items that require attention, promptly resolve the issues by following the remediation suggestions.
