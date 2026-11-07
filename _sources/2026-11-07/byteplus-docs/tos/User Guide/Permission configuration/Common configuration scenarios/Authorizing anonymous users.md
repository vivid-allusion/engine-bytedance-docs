---
title: "Authorizing anonymous users"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-anonymous-user-authorization"
---

This topic describes typical scenarios and authorization instructions for anonymous user authorization. We recommend using bucket policies for authorization.

<span id=".5o6I5LqI5Yy_5ZCN55So5oi35qG25YWs5YWx5Y-q6K-75p2D6ZmQ"></span>
## Granting anonymous users public read\-only permission on buckets

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only covers the steps to authorize using bucket policies. If you only need to grant anonymous users read or write permissions on a bucket or bucket ACL, you can set the bucket ACL. For detailed steps, see <a href="https://docs.byteplus.com/docs/tos/docs-configuring-a-bucket-acl">Configuring bucket ACLs</a>.</div>



1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. Click on **Buckets** in the left navigation bar, and click on the target bucket name on the **Buckets** page.

3. Select **Permissions \> Bucket policies** in the left navigation bar.

4. On the **Bucket policies** page, under the **Visual View** tab, click **Create policy**.

5. On the **Create Bucket Authorization Policy** page, select the **Public Read\-Only (Including ListBucket Operations)**  template and click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy information. In this scenario, it is sufficient to keep the default template parameters.

7. After setting up, click **Next** to confirm the policy information currently configured.

8. After confirming the information is correct, click **Create** to complete the creation of the policy.


After creating the authorization policy, you can view the created policies in the policy management list.

<span id=".5o6I5LqI5Yy_5ZCN55So5oi35oyH5a6a6LWE5rqQ5YWs5YWx5Y-q6K-75p2D6ZmQ"></span>
## Granting anonymous users public read\-only permission on specified resources


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. Click on **Buckets** in the left navigation bar, and on the **Buckets** page, click the target bucket name.

3. Select **Permissions \> Bucket policies** from the left navigation bar.

4. On the **Bucket policies** page, under the **Visual View** tab, click on **Create Policy**.

5. On the **Create Bucket Authorization Policy** page, select the **Public Read\-Only (Excluding ListBucket Operations)**  template and click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy information as prompted by the interface.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Parameters to be set in this scenario are as follows, all other parameters should remain default.</div>



|**Type** |**Description** |
|---|---|
|Resource |Select the **Specified object(s)** , click the **Add Field**, and set the specified resource field. |
|Condition |Click the **Add Field** to set the conditions and values you need. For an explanation of the parameters related to conditions, please see [Conditions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#nk9G2rUC). |



7. Upon completing the settings, click **Next** to confirm the current policy information.

8. After confirming the information is correct, click **Create** to complete the creation of the policy.

   After the authorization policy is created, you can view the created policies in the policy management list.


<span id=".5o6I5LqI5Yy_5ZCN55So5oi35oyH5a6a6LWE5rqQ5oyH5a6a5p2D6ZmQ"></span>
## Granting specified permissions on specified resources to anonymous users


1. Login to the [TOS console](https://console.byteplus.com/tos).

2. Click on **Buckets** in the left sidebar, then on the **Buckets** page, click on the target bucket name.

3. Select **Permissions \> Bucket policies** in the left sidebar.

4. On the **Bucket policies** page, under the **Visual View** tab, click **Create policy**.

5. On the **Create Bucket Authorization Policy** page, select the **Public read/write** template, and click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy details following the interface prompts.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The parameter settings required for this scenario are detailed below; all other parameters can be set to default.</div>



|**Type** |**Description** |
|---|---|
|Resource |Select the **Specified object(s)** , click the **Add field**, and configure the specified resource fields. |
|Action |Select the generic actions that require authorization. For details on actions, please see [Supported actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8). |
|Condition |Click the **Add field** to set the conditions and values you need. For more information about condition parameters, see [Conditions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#nk9G2rUC). |



7. After setting, click **Next** to confirm the current configuration of the policy information.

8. After confirming the information is correct, click **Create** to complete the creation of the policy.


After the authorization policy is created, you can view the created policies in the policy management list.

<span id=".5o6I5LqI5Yy_5ZCN55So5oi35Y2V54us5a-56LGh5Y-q6K-75p2D6ZmQ"></span>
## Granting anonymous users read\-only permission on individual objects

If you only need to grant anonymous users read\-only or read\-write permission on individual objects, you can set the object's ACL. For details, see [Configuring object ACLs](https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl).
