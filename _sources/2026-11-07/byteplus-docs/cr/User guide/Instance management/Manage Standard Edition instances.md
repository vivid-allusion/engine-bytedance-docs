---
title: "Manage Standard Edition instances"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/manage-an-instance"
---

After successfully creating a Standard Edition instance, you can view the instance details and its operational status. If you no longer use Standard Edition instances, you can also destroy the instances.

<span id=".5p-l55yL5qCH5YeG54mI5a6e5L6L6K-m5oOF"></span>
## View Standard Edition instance details


1. Log in to the [Container Registry console](https://console.byteplus.com/cr).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Instance List**. In the **Instance List** area, you can view the list of all Container Registry Instances and their running status in this region.

4. In the **Instance list** area, find the instance you want to view details for, and click **Enter instance**.

5. On the Standard Edition instance page, click **Overview** in the navigation bar on the left to view various types of information about the instance.

   
   |Module |Descriptions |
   |---|---|
   |Log in to an instance |Displays the **username**, **login instance command**, and related information required to log in to the current Standard Edition instance. You can also set, modify, or obtain credentials for accessing the Container Registry Instance in this module. For detailed instructions, refer to [Set Standard Edition instance access credentials](https://docs.byteplus.com/en/docs/cr/Get-access-credentials). |
   |Resource usage |Displays the storage usage and outbound public network traffic for the current Standard Edition instance. |
   |Quota usage |Display the usage and remaining quota for each resource quota of the current Standard Edition instance |
   |Basic Information |Displays basic information for the current Standard Edition instance, including running status, public network access status, payment type, region, access domain name, and other basic information. |
   |Getting started |Display getting started actions for Standard Edition instances to help you quickly understand their usage. |
   


<span id=".6ZSA5q-B5qCH5YeG54mI5a6e5L6L"></span>
## Destroy Standard Edition instances


1. Log in to the [Container Registry console](https://console.byteplus.com/cr).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Instance List**, then in the **Instance List** area, find the Standard Edition instance that needs to be destroyed.

4. In the **Actions** column on the right side of the target Standard Edition instance, click `···` \> **Destroy**.

5. After confirming the instance information in the system popup dialog box, click **confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you click <strong>confirm</strong>, the instance enters the pending recycle state. Instances pending recycling are retained for 7 days by default. During this period, the instance continues to be billed, and information stored in the instance, such as images, is retained to support rapid recovery. After 7 days, the instance is permanently deleted and cannot be recovered.   </div>
   

   The following actions can be performed on Standard Edition instances in the pending recycle state:

   * Restore an instance: Within 7 days after an instance is destroyed, you can restore it at any time.

      In the **Instance list** area, on the right side of a Standard Edition instance in the 'To be recycled' status, under the **Actions** column, click `···` \> **Recovery**. After confirming the instance information, you can restore the instance as well as the images, Helm Charts, and more stored within it.

   * Permanently destroy an instance: When you confirm that recovery of the Standard Edition instance is not required, you can immediately and permanently destroy the instance. Billing will cease.

      In the **Instance list** area, in the **Actions** column to the right of a Standard Edition instance in the Pending Recycle state, click `···` \> **Completely destroy**. After confirming the instance information, you can immediately and permanently destroy the instance.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After an instance is permanently destroyed, all information stored in the instance is completely destroyed and cannot be recovered. Please ensure that business operations are not affected.      </div>
      

<span id=".5b275bqV6ZSA5q-B5qCH5YeG54mI5a6e5L6L"></span>
## Permanently destroy Standard Edition instances

When you confirm that recovery of the Standard Edition instance is not needed, you can **immediately** permanently delete the instance, and billing will stop.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After an instance is permanently destroyed, all information stored in the instance is completely erased and cannot be recovered. Please ensure that business operations are not affected.</div>


* <div data-tips="true" data-tips-type="warning">If the audit log feature is enabled, after an instance is permanently destroyed, the corresponding TLS <code>project</code> and <code>topic</code> will be deleted synchronously.</div>


1. Log in to the [Container Registry console](https://console.byteplus.com/cr).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Instance List**, and then locate the Standard Edition instance that needs to be destroyed in the **Instance List** section.

4. In the **Actions** column on the right side of the target Standard Edition instance, click `···` \> **Permanently delete**.

5. On the secondary confirmation page, enter the verification information as prompted, then click **Permanently destroy** to immediately destroy the instance.


<span id=".QVBJIOaWh-ahow=="></span>
## API Documentation


* [ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries): Query instance details.

* [DeleteRegistry](https://docs.byteplus.com/en/docs/cr/deleteregistry): Delete instance.
