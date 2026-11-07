---
title: "Managing Secrets"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-Secrets"
---

After Secrets have been created or added to a cluster, you can manage them on the Secret management page. This topic describes the applicable scenarios, operational impacts, and procedures for managing Secrets.

<span id=".5pu05paw5L-d5a-G5a2X5YW4"></span>
## Updating secrets

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The VKE console allows you to update Secrets of only three types: <strong>Opaque</strong>, <strong>kubernetes.io/tls</strong>, and <strong>kubernetes.io/dockerconfigjson</strong>.</div>


After you modify Secrets, the new Secret settings apply. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke), and in the left navigation bar, select **Cluster**.

2. In the cluster list, click the name of the target cluster. The cluster management page opens. In the left navigation bar, click **Configurations** \> **Secret**.

3. In the Secret list, find the Secret to update, and in the **Actions** column, click `...`  \> **Update**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Certain parameters cannot be updated. The configurable settings in the console take precedence. For details of Secret parameters, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-Secret">Creating Secrets</a>.   </div>
   

<span id=".57yW6L6R5L-d5a-G5a2X5YW4LXlhbWw="></span>
## Editing Secret YAML files

You can modify a Secret by editing its YAML file. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke), and in the left navigation bar, select **Cluster**.

2. In the cluster list, click the name of the target cluster. The cluster management page opens. In the left navigation bar, click **Configurations** \> **Secret**.

3. In the Secret list, find the Secret to edit, and in the **Actions** column, click `...`  \> **Edit Yaml**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For a description of a Secret YAML, see <a href="https://kubernetes.io/docs/concepts/configuration/secret/">Secrets</a>.   </div>
   

4. In the pop\-up window, edit the YAML file. Click **Confirm** when you finish.


<span id=".5a-85Ye65L-d5a-G5a2X5YW4"></span>
## Exporting secrets

You can export a Secret to your local storage by exporting its YAML configuration file. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke), and in the left navigation bar, select **Cluster**.

2. In the cluster list, click the name of the target cluster. The cluster management page opens. In the left navigation bar, click **Configurations** \> **Secret**.

3. In the Secret list, find the Secret to export, and in the **Actions** column, click `...`  \> **Export**.

4. The file will be downloaded to your computer.


<span id=".5Yig6Zmk5L-d5a-G5a2X5YW4"></span>
## Deleting secrets

You can delete Secrets. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke), and in the left navigation bar, select **Cluster**.

2. In the cluster list, click the name of the target cluster. The cluster management page opens. In the left navigation bar, click **Configurations** \> **Secret**.

3. In the Secret list, find the Secret to delete, and in the **Actions** column, click `...`  \> **Delete**.

4. Click **Delete** in the confirmation dialog box to delete the Secret.
