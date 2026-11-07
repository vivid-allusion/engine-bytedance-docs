---
title: "Migrating FSX clients"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Migrating_FSX_clients"
---

FSX client migration implements lifecycle management for FSX clients based on the FSXSet CRD. It supports features such as rolling upgrades, canary upgrades, and multi‑environment isolation. This topic describes the migration procedure, verification method, and subsequent cleanup operations for FSX clients.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before performing the migration, you need to first familiarize yourself with the migration background and the changes to the csi\-fsx add\-on. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_FSX_add-on_feature_optimization_and_fsx-service_add-on_sunsetting">[Product update] fsx\-service deprecation notice</a>.</div>


<span id="pacy6LRk"></span>
## Migration steps

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To migrate FSX clients, you need to first install the fsxset\-controller add\-on and then upgrade the csi\-fsx add\-on to v1.0.0 or later.</div>


<span id="MyeZy6O0"></span>
### Step 1: Install the fsxset\-controller add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to go to its management page.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the fsxset\-controller add\-on card and click **Deploy** to install the add\-on.


<span id="najTQosi"></span>
### Step 2: Upgrade the csi\-fsx add\-on


1. In the left navigation pane, select **Addons** and click the **Storage** tab.

2. In the upper\-right corner of the csi\-fsx add\-on card, click `...` \> **Upgrade**.

3. In the pop\-up dialog box, click **Confirm** to upgrade the add\-on.

4. After the upgrade is complete, view the add\-on version to confirm that the add\-on has been upgraded to v1.0.0 or later.


<span id="Vz29lcWz"></span>
## Validate results

<span id="TAy9Qkma"></span>
### Migrate existing configurations

If you enable the [multi-client configuration](https://docs.byteplus.com/en/docs/vke/fsx-service-add-on) feature for the original fsx\-service add\-on, when the csi\-fsx add\-on is upgraded to v1.0.0 or later, the system will automatically perform the following operations to ensure a smooth transition of configurations.


1. The system automatically creates a default FSXSet configuration named default.

2. The specified FSX client parameters (such as client resource quotas) will be automatically migrated to the FSXSet configuration named default. You can view the corresponding resources through the console or kubectl to confirm that the configurations have been automatically migrated.

3. Nodes without labels will be automatically assigned to the default group and use the default configuration.


<span id="ZQndlUm8"></span>
### Take over existing FSX clients

After you upgrade the csi\-fsx add\-on to v1.0.0 and enable FSXSet management, the system will automatically take over the existing FSX client Pods created by the fsx\-service add\-on of the earlier version. This ensures that existing FSX clients run as expected. This operation is automatically completed by the system and requires no manual intervention.

<span id="KvwMx64E"></span>
### View FSXSet resources

After upgrading csi\-fsx to v1.0.0, you can view the system‑generated FSXSet resources by using the following methods:


<Tabs>
<Tab zoneid="M09u3CsudD" title="View resources via the console">
<TabTitle>View resources via the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. In the lower\-right corner of the csi\-fsx add\-on card, click  **`...`**   **\> Client configuration**.

5. In the Client configuration panel, view the FSXSet resources in the system.

6. Find the target resource and click **Update** in the **Actions** column to view or update the FSXSet resource.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To configure more features, you can view or modify the YAML configurations of the FSXSet resources by navigating to <strong>Workload \> Resource Explorer</strong>.   </div>
   


</Tab>
<Tab zoneid="M8CBVFamDw" title="View resources via kubectl">
<TabTitle>View resources via kubectl</TabTitle>

1. [Connect to the cluster through kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to view FSXSet resources in the cluster.

   ```Bash
   kubectl get fsxset
   ```
   

   The expected result is as follows: An FSXSet resource named default is automatically created in the cluster.

   ```Bash
   NAME      GROUP     DESIREDREVISION    DESIRED   CURRENT   READY   AVAILABLE   UPDATED   MATCHED   AGE
   default   default   a751b63df3dcd4d5   1         1         1       1           1         2         57s
   ```
   





</Tab>
</Tabs>


<span id="L9DAAuy0"></span>
## Subsequent configurations

<span id="7vrSWwF2"></span>
### Clean up the fsx\-service add\-on

After you upgrade csi\-fsx to v1.0.0, it has fully taken over all features of the original fsx\-service. Therefore, after confirming that the migration is complete, you can uninstall the fsx\-service add\-on to save cluster resources. For instructions on removing the add\-on, see [Uninstalling add-ons](https://docs.byteplus.com/en/docs/vke/Uninstalling-an-add-on).

&nbsp;

&nbsp;
