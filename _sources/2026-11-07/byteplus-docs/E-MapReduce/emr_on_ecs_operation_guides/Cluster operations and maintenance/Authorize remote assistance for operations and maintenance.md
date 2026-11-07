---
title: "Authorize remote assistance for operations and maintenance"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Operations_and_maintenance_permissions_management"
---

The resources of an EMR on ECS cluster belong to the user. EMR provides semi\-managed cloud service capabilities based on these resources, and the user has full control permissions over the cluster. In general, when a cluster encounters an issue and requires support from O&M personnel, the O&M personnel do not have direct access to the cluster.

To better serve customers and improve O&M efficiency, EMR provides the **Authorized operation and maintenance** feature, which allows users to grant appropriate O&M permissions to O&M personnel from the console page. This article introduces how to use the O&M authorization feature.

<span id="68481abc"></span>
# Limits

The **Authorized operation and maintenance** feature is currently an allowlist feature. You can apply for access by or [creating a ticket](https://console.byteplus.com/workorder/create).

<span id="3393abf9"></span>
# Procedure


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the top menu bar, select the region as needed.

3. Click **Resources\>on ECS** in the left menu.

4. Select the cluster for which you want to authorize O&M, and on the **Cluster overview** page, click **Cluster operations\>Authorized operation and maintenance**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abb641e5f4a5484daabe34cce9de3b35~tplv-goo7wpa0wc-image.image) </span>

5. Select the authorization plan and expiration time according to your actual needs, check the box to indicate you have read the authorization notice, and click **Confirm** to complete the authorization. See the table below for detailed explanations of the authorization plans.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When authorizing, follow the principle of least privilege and grant only the minimum permissions required for O&M personnel to complete their tasks.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e13382399094c80b657f1e6cd36cfcd~tplv-goo7wpa0wc-image.image) </span>

   
   |**Authorization scope** |**Parameter and option note** |**Authorization logic** |
   |---|---|---|
   |console authorization |* ordinary authorization: Grants O&M personnel the EMR ReadOnlyAccess permission, which only allows viewing of cluster information through the console.<br><br>* Advanced Authorization: Grants O&M personnel the EMR FullAccess permission, allowing O&M operations on the cluster through the console interface |After authorization, the system automatically creates an IAM role for the cluster. O&M personnel access the console by assuming the IAM role with their O&M platform account.<br><br>After the authorization expires, the IAM role is automatically reclaimed. |
   |Cloud as a Service Licensing |temporary account: You must enter the temporary cloud server account and password granted to the O&M personnel. You can create a temporary temporary account through the User management page in the EMR console or ECS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The temporary account password is only entered during authorization. After it is entered, the EMR console will no longer display it. Operations personnel can view the password through the operations platform.</div><br> |After authorization, O&M personnel use the temporary account created by the user to access cloud server resources.<br><br>After the authorization expires, operations personnel cannot use this account. The account information will not change and can be deleted by the user. |
   

6. During the O&M authorization period, users can view the authorization details and expiration time on the **Cluster overview** page. During the authorization period, users can click **Modify authorized operation and maintenance** as needed or based on suggestions from O&M personnel to modify **Authorization method**, **cut\-off time**, or select **End this authorization**.

7. View operation records. You can view the operations performed by O&M personnel in the EMR cluster in the following ways:

   
   |**Authorization method** |**View operations** |
   |---|---|
   |console authorization |Log in to[E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?), select **Operation logs** from the list on the left, and filter operation logs of the primary account within the authorization period **Operator**. |
   |Cloud as a Service Licensing |Log in to the cloud server and filter Operation logs where **Operator** is **temporary account**. |
