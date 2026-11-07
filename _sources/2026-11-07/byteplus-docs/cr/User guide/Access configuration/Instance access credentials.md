---
title: "Instance access credentials"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Get-access-credentials"
---

Before using CR instances, you need to configure access credentials first. This topic describes how to configure and manage instance access credentials.

<span id="eUaq5mXv"></span>
## Background

CR instance access credentials include an access password and a temporary access instruction.


* CR instance password: the fixed password of CR, which is the password used for docker login. After configuration, you can use this password to log in to the instance and manage images.

* Temporary access instruction: The default validity period is 1 hour, and the customizable range is 10 minutes to 12 hours. Within the validity period, you can use the temporary access instruction to quickly log in to the instance.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an instance. For instructions, see [Creating Standard instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

<span id="1c4hdoHW"></span>
## Set a CR instance password


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation pane, click **Instance list**, find the target instance and click **Enter instance**. 

2. Click **Set repository instance password**, set and confirm the password, and then click **Confirm**.


<span id=".6I635Y-W5Li05pe26K6_6Zeu5oyH5Luk"></span>
## Get temporary access instruction

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The default validity period of the temporary access credential is 1 hour, and the customizable range is 10 minutes to 12 hours. Log in to the instance with the temporary access instruction within the validity period.</div>



1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation pane, click **Instance list**, find the target instance and click **Enter instance**. 

2. On the instance details page, click **Overview** in the left navigation pane.

3. At the top of the instance overview area, click **Get temporary access instruction**.

4. In the **access instruction expiration time** field, select or enter the credential end time, and then click **Confirm.** 

5. Click **Get access command**, and click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4833fd7bad18fa5d2469066a4ec608d4.png) </span> at the upper right of the instruction to copy the instruction.


<span id=".5L-u5pS56K6_6Zeu5a-G56CB"></span>
## Change the CR instance password

After you set the CR instance password for the first time, you can modify the CR instance password.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation pane, click **Instance list**, find the target instance and click **Enter instance**. 

1. On the instance details page, click **Overview** in the left navigation pane.

2. At the top of the instance overview area, click **Change repository instance password**.

3. In the **Change repository instance password** dialog box, set a new password. After you confirm the password, click **Confirm ** to complete the modification of the CR instance password.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For instructions on obtaining a temporary login key for an instance via Terraform, see [Obtaining instance temporary login keys](https://docs.byteplus.com/en/docs/cr/Obtain_a_temporary_key_for_a_login_instance).
