---
title: "Deploy resource management"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Deploy_resource_management"
---

After integrating deployment resources, you can manage them. This article introduces operations for managing deploy resources.

<span id=".5p-l55yL6YOo572y6LWE5rqQ"></span>
## View deploy resources

You can view information such as the name of the deployment resource, connection type, region, cluster connection information, sharing scope, and other details.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For container service clusters, deploy resource permissions correspond to the permissions of the BytePlus account that owns the resources.</div>


* <div data-tips="true" data-tips-type="tip">For custom clusters, deploy resource permissions correspond to the permissions defined in the Kubeconfig file.</div>


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. Select **Resource management** in the left navigation bar.

3. On the **Resource management** page, switch to the **deploy resource** tab. You can view information about the deploy resources that have already been connected in the table.

4. (Optional) For VKE clusters, click the jump icon next to the cluster name to quickly access the corresponding VKE cluster details page.


<span id=".5L-u5pS56YOo572y6LWE5rqQ"></span>
## Modify deploy resources


1. On the **deploy resources** tab, click **edit** in the **actions** column to open the **edit deploy resources** dialog box. Modify the information as needed.

2. Click **OK** to complete the modification.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a connected container service cluster is deleted, the deployment cluster information will display the original cluster ID. Clicking the ID will clear the information, and you will need to select a cluster again.</div>


<span id=".5Yig6Zmk6YOo572y6LWE5rqQ"></span>
## Delete deploy resources

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Caution: After you delete a deploy resource, any pipeline that references this deploy resource will fail to run, and any application that references this deploy resource will fail to deploy. Please proceed with caution.</div>



1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Resource management \> Deploy resource** to enter the **Deploy resource** page.

3. Click **delete** in the **actions** column. A secondary confirmation dialog will appear.

4. Review the information for the deploy resource to be deleted. Once confirmed, click **Confirm** to delete the deploy resource.
