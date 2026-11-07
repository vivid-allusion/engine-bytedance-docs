---
title: "Managing lifecycle policies"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Managing_lifecycle_policies"
---

Cloud Search allows users to perform automatic operations on indices by using predefined lifecycle policies. This reduces storage costs, optimizes performance, and minimizes manual maintenance. This topic introduces how to manage lifecycle policies.

<span id="eSpiGFwC"></span>
# Prerequisites


* A BytePlus account has been registered with real name authentication completed. For account registration and real name authentication, refer to [Create account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account#create-byteplus-account) and [Verify account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Cross\-service access has been authorized to allow Cloud Search to access other services. For detailed steps, refer to [Cross-service Authorization](https://docs.byteplus.com/en/docs/cloudsearch/cross-service-authorization).

* Before managing lifecycle policies, create an Elasticsearch or OpenSearch instance. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).


<span id="s7zhkqCV"></span>
# Creating a lifecycle policy


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the project and region where you want to create a lifecycle policy.

3. In the left navigation bar, select **Index management**.

4. From the dropdown list, select the instance for which you want to manage lifecycle policies, enter the username and password, check **15 days license free** as needed, and then click **Authorized view index**.

5. On the **Index management** page, select the **lifecycle strategy** tab, and click **Create strategy**.

6. On the **Create Lifecycle Policy** panel, configure the following parameters, and click **OK**.



|**Parameter** |**Description** |
|---|---|
|policy name |The name of the lifecycle policy. The name must meet the following requirements:<br><br><br>   * Cannot start with a digit or underscore (_).<br><br>   * Contains 1 to 128 characters.<br><br>   * Contains only lowercase letters, digits, underscores (_), and hyphens (\-). |
|index matching rule |Configure index matching rules. An index matching rule contains the following fields:<br><br><br>   * Index<br><br>      Enter indices. Separate multiple indices with commas (,) or line breaks.<br><br>   * priority<br><br>      Priority of the index matching rule.<br><br><br>You can click **Add row** to add multiple index matching rules. |
|Life Cycle Rules |Configure at least one lifecycle rule based on your requirements. Cloud Search supports the following rules:<br><br><br>   * Rollover<br><br>      Creates a new index when the index meets specific conditions. This rule contains the following fields:<br><br>      * time limit (optional)<br><br>         When the index reaches the age specified in this field after creation, the **Rollover** rule will be triggered. Unit: **hour** or **Day**. The value **0** indicates that this condition does not take effect.<br><br>      * Minimum number of indexed documents (optional)<br><br>         When the indexed document count reaches the number specified in this field, the **Rollover** rule will be triggered. The value **0** indicates that this condition does not take effect.<br><br>      * minimum index storage (optional)<br><br>         When the primary shard storage of the index reaches the size specified in this field, the **Rollover** rule will be triggered. The value **0** indicates that this condition does not take effect.<br><br>      You must configure at least one condition. If you configure multiple conditions, the **Rollover** rule is triggered when any of the conditions is met.<br><br>   * Force Merge<br><br>      Sets the index to read\-only mode when the index meets specific conditions. This rule contains the following fields:<br><br>      * time limit<br><br>         When the index reaches the age specified in this field after creation, the **Force Merge** rule is triggered. Unit: **hour** or **Day**. The value must be greater than 0.<br><br>      * Maximum Number of Segments<br><br>         The maximum number of merged segments.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After an index is set to read\-only mode, the index may no longer be written. Exercise caution when you turn on the <strong>Force Merge</strong> rule.      </div><br>      <br><br>   * Transfer to temperature data node<br><br>      Transfers an index to warm data nodes when specific conditions are met. This rule contains the following fields:<br><br>      * time limit<br><br>         When the index reaches the age specified in this field after creation, the **Transfer to temperature data node** rule is triggered. Unit: **hour** or **Day**.<br><br>      * number of copies (optional)<br><br>         The number of replicas for the index in warm data nodes.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the current instance has no warm data nodes, you cannot turn on the      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Transfer to temperature data node</strong> rule. You can upgrade the instance to add warm data nodes. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/upgrading">Upgrading instance specifications</a>.      </div><br>      <br><br>   * Moving to a cold data node<br><br>      Transfers an index to cold data nodes when specific conditions are met. This rule contains the following fields:<br><br>      * time limit<br><br>         When the index reaches the age specified in this field after creation, the **Moving to a cold data node** rule is triggered. Unit: **hour** or **Day**.<br><br>      * number of copies (optional)<br><br>         The number of replicas for the index in cold data nodes.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the current instance has no cold data nodes, you cannot turn on the      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Moving to a cold data node</strong> rule. You can upgrade the instance to add cold data nodes. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/upgrading">Upgrading instance specifications</a>.      </div><br>      <br><br>   * Index delete<br><br>      Deletes an index when specific conditions are met. This rule contains the following fields:<br><br>      * time limit<br><br>         When the index reaches the age specified in this field after creation, the **index delete** rule will be triggered. Unit: **hour** or **Day**.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you set this field to <strong>0</strong>, the index will be deleted soon. Proceed with caution.      </div><br>       |
|Description |The description of the lifecycle policy. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Created lifecycle policies will apply only to new indices. Existing indices retain their original policies.</div>


<span id="IrC3o856"></span>
# Editing a lifecycle policy


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the project and region where you want to edit a lifecycle policy.

3. In the left navigation bar, select **Index management**.

4. From the dropdown list, select the instance for which you want to manage lifecycle policies, enter the username and password, check **15 days license free** as needed, and then click **Authorized view index**.

5. On the **Index management** page, select the **lifecycle strategy** tab, find the desired lifecycle policy, and click **Edit** in the **Actions** column.

6. On the **Edit Lifecycle Policy** panel, modify parameters as needed, and click **OK**.


<span id="7BPw3yUT"></span>
# Deleting a lifecycle policy


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the project and region where you want to delete a lifecycle policy.

3. In the left navigation bar, select **Index management**.

4. From the dropdown list, select the instance for which you want to manage lifecycle policies, enter the username and password, check **15 days license free** as needed, and then click **Authorized view index**.

5. On the **Index management** page, select the **lifecycle strategy** tab, find the desired lifecycle policy, and click **Delete** in the **Actions** column.

6. In the dialog box that appears, confirm the lifecycle policy information, and click **Delete**.
