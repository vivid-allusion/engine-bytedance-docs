---
title: "Why can an IAM user with an instance-level IAM policy still view all instances?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Why-can-an-iam-user-with-an-instance-level-iam-policy-still-view-all-instances"
---

This issue usually occurs for the following two reasons:


* **Reason 1: The IAM user is not added to DBW user management**

   If the IAM user has never been added in the DBW console under **Corporate security** \> **User management** \> **Personal user management**, the system falls back to the IAM layer to determine permissions.

   * **Symptom**: If the IAM user has an IAM system policy (such as `DbwFullAccess`), they have view permissions for all instances by default.

   * **Solutions**: Add the IAM user on the **Personal user management** page in DBW, and select only the instances that need authorization in their **Permission management**.

* **Reason 2: The target instance does not have security control enabled**

   DBW's internal fine\-grained instance authorization logic relies on the security control feature.

   * **Symptom**: If security control is not enabled for the instance, DBW cannot apply the internally configured instance permissions.

   * **Solution**: Go to the **Instance list** page and **enable security control** for the target instance.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The <code>Resource</code> field in IAM custom policies only controls "operation permissions," not visibility. Even if you restrict Resource in your IAM policy, as long as you can pass the IAM DescribeInstances check (which usually requires <code>Resource: *</code>), you can still see the list. Actual visibility filtering must be done in the DBW console.</div>
