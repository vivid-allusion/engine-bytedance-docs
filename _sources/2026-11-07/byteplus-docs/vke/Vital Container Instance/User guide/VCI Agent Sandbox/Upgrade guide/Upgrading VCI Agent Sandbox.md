---
title: "Upgrading VCI Agent Sandbox"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Upgrading_VCI_Agent_Sandbox"
---

This topic describes how to upgrade an Agent Sandbox. Before upgrading, thoroughly review the target version's ‌changes and impact analysis to ensure a full understanding of the changes.

<span id="2aT7Wuhk"></span>
## Preparations


* You have confirmed Kubernetes compatibility, version changes, and impacts. For details, see [Version change log](https://docs.byteplus.com/en/docs/vke/Version_change_log).

* You have administrator permissions for the cluster where the Agent Sandbox application is deployed. For details, see [Configuring RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions).

* As updates to some versions involve associated impacts, assess the scope of impact in advance and perform the upgrade during off\-peak business hours.

* If the current version is v0.1.1 and the warm pool feature is used, first scale in the number of warm pool replicas to 0 before the upgrade.

* If you need to retain the ability to access the Sandbox via a Kubernetes Service, plan the value of the `controller.defaultSandboxService` parameter in advance.


<span id="OWAy4e2p"></span>
## Upgrade procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Helm**.

3. On the **Helm** page, select the target **cluster** and **namespace**, and then find the Agent Sandbox application to upgrade.

4. On the right side of the Agent Sandbox application, click `...`\> **Update** in the **Actions** column.

5. On the **Update Helm** page, expand **agent\-sandbox** from the **Application template** drop\-down list in the **Orchestration template** section, and then select the target version.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9cd24c2079b7b2d7318986c8672b92d.png) </span>

6. Click the edit icon next to `values.yaml` and fill in the deployment parameters. For parameter details, see the [installation guide](https://docs.byteplus.com/en/docs/vke/Installation_guide).

7. After confirming the parameters are correct, click **Confirm** at the bottom of the page to submit the update.

   VKE will automatically complete the rolling upgrade of the Helm Release. You can observe the release status and workload changes on the **Helm details page**.


<span id="XBV0weUi"></span>
## Post\-upgrade verification

After the upgrade is complete, we recommend performing checks in the following order to ensure that the application is running normally.


1. On the **Helm** page, confirm that the agent\-sandbox application status is **Deployed** and its Chart version matches the target version.

2. Click the Helm application name. On the **Helm details page**, check the workload type and status of agent\-sandbox\-controller. The expected results are that the type has switched to Deployment, and that all its Pods are in the Running status.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent\-sandbox\-controller workload type is ‌Deployment‌ ‌in v0.4.6 or later‌, and StatefulSet before this version.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <strong>status</strong> of all agent\-sandbox\-controller resources must be ready (the Status column shows <strong>Ready: n/n</strong>).   </div>
   

3. Create a test Sandbox to verify that it can normally reach the Running state and be accessed. For detailed instructions, see [Lifecycle management](https://docs.byteplus.com/en/docs/vke/Lifecycle_management).

4. (Optional) If anomalies occur after the upgrade, roll back to the previous stable version on the **Helm** page using the **Historical version** feature. Rollback will also result in a brief window during which the add\-on is unavailable. Proceed with caution.
