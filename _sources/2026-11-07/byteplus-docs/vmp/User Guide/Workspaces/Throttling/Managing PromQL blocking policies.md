---
title: "Managing PromQL blocking policies"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Managing_PromQL_blocking_policies"
---

The PromQL blocking policy is a query\-control feature of VMP. It can precisely block specific PromQL queries based on request patterns (query statement matching rules) and request sources (accounts).

<span id="cVfPstIe"></span>
## Creating PromQL blocking policies

<span id="5vnBwdgj"></span>
### Limits

Each workspace supports at most 10 PromQL blocking policies.

<span id="cCwEhw4f"></span>
### Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the project and region where your business is located.

3. In the left navigation pane, select **Workspaces ** .

4. Click the name of the target workspace.

5. In the left navigation bar, click **Traffic control.** 

6. Click the **PromQL ban** tab and click **Create policy**. Specify the related parameters based on the following table.

   
   |Parameter |Description |
   |---|---|
   |Name |Enter a name for the PromQL blocking policy. |
   |PromQL matching rules |Enter the PromQL blocking match rule. When a pending PromQL query statement matches this rule, the system will trigger the blocking mechanism and intercept the query operation. Click [here](https://docs.byteplus.com/en/docs/vmp/Basic-PromQL-methods) to learn more.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The PromQL match rule must be a valid statement.</div><br> |
   |Matching pattern |Select the matching mode for the PromQL blocking policy. Supported modes are **Exact match ** and **Regex match.** <br><br><br>* **Exact Matching**: The PromQL query statement to be executed must be the same as the blocking match rule.<br><br>* **Regex match**: Uses regular expressions to match PromQL query statements, supporting flexible scenarios such as fuzzy matching and range matching. [Learn more](https://docs.byteplus.com/en/docs/vmp/Basic-PromQL-methods?lang=en#.5q2j5YiZ5Yy56YWN). |
   |Blocking target |Select the IAM users or roles that are now allowed to execute PromQL queries in this workspace.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If no IAM user or role is configured, the workspace will block all IAM users and roles that initiate queries.</div><br> |
   

7. Click **Confirm** to complete the configuration.


<span id="hifTLksW"></span>
### What to do next

After a blocking policy is created, you need to verify whether the policy is effective. Procedure:


1. [Go to the Explore page. ](https://docs.byteplus.com/en/docs/vmp/explore-metrics)

2. Select the workspace to which the target policy belongs.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The selected workspace must be consistent with the workspace of the PromQL blocking policy.   </div>
   

3. Enter the query statement and click **Query**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The entered query statement must be consistent with the PromQL match rule in the target PromQL blocking policy.   </div>
   

4. If the following message is displayed, the blocking policy is effective.


<span id="EjlonWSA"></span>
## Enable or disable PromQL blocking policy

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you disable a PromQL blocking policy, the blocking capability becomes invalid.</div>



1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the project and region where your business is located.

3. In the left navigation pane, select **Workspaces ** .

4. Click the name of the target workspace.

5. In the left navigation bar, click **Traffic control.** 

6. Click the **PromQL ban** tab.

7. Click **Enable** or **Disable** in the **Actions** column of the target policy to complete the operation.


<span id="IDSapPed"></span>
## Editing PromQL blocking policies


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the project and region where your business is located.

3. In the left navigation pane, select **Workspaces ** .

4. Click the name of the target workspace.

5. In the left navigation bar, click **Traffic control.** 

6. Click the **PromQL ban** tab.

7. Click **Edit** in the **Actions** column of the target policy to modify the related parameters.


<span id="BjVIrceX"></span>
## Deleting PromQL blocking policies

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">After you delete a PromQL blocking policy, it cannot be restored. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="default">If you delete a PromQL blocking policy, the blocking capability becomes invalid.</div>


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the project and region where your business is located.

3. In the left navigation pane, select **Workspaces ** .

4. Click the name of the target workspace.

5. In the left navigation bar, click **Traffic control.** 

6. Click the **PromQL ban** tab.

7. Click **Delete** in the **Actions** column of the target policy.

8. After you confirm that the policy to be deleted is correct, click **Confirm** to delete the policy.
