---
title: "Manage alarm policies"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/manage_alarm_policy"
---

After creating an alarm policy, you can perform common management operations on existing alarm policies in the log service console, such as searching for a specific alarm policy, changing the policy status, and deleting alarm policies.

<span id=".5p-l5om-5ZGK6K2m562W55Wl"></span>
## Search alarm policies

The log service console supports filtering alarm policies by monitored log topic name and alarm policy name to help you quickly find a specified policy.

Steps are as follows.


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **common features** \> **log alarm** \> **alarm policy**.

4. On the **alarm policy** page, filter the alarm policies.

   Supports filtering by monitored object, alarm policy name, or ID.

   After entering keywords in the filter box, the page automatically filters and displays related alarm policies, supporting fuzzy search. Additionally, in the policy list, the **application status** column supports filtering by status.


<span id=".5L-u5pS5562W55Wl54q25oCB"></span>
## Disable or enable alarm policy

After creating an alarm policy, the policy defaults to **running** status. Log Service will continuously run monitoring tasks and send alarm notifications according to the alarm policy. You can also start or stop the alarm policy at any time according to business needs.


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, choose **Common Functions** \> **log alarm** \> **alarm policy**.

4. On the **alarm policy** page, find the specified alarm policy, then click **disable** or **enable** in the corresponding **operations** column.


<span id="f3f67631"></span>
## Temporarily disable alarm policy

If alarm notifications are not needed for a while, you can temporarily disable the alarm policy. During the temporary disablement of the alarm policy, the log service will suspend monitoring tasks until the alarm policy automatically resumes. You can also manually resume the alarm policy at any time during its temporary disablement.


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Features** \> **log alarm** \> **alarm policy**.

4. On the **alarm policy** page, find the specified alarm policy and select ... \> **Temporarily disable** in the corresponding **Actions** column. 

5. Set the **disable duration** in the pop\-up dialog box.

6. Click **Temporarily disable**.


<span id=".5L-u5pS55ZGK6K2m562W55Wl"></span>
## Edit alarm policy

After creating an alarm policy, you can modify it anytime to meet business needs, such as changing monitoring tasks, alarm rules, or notification content.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If there are changes in the notification group, such as notification methods, channels, or associated personnel, the corresponding alarm policy does not need to be modified. The log service will send notifications based on the latest notification group settings.</div>


* <div data-tips="true" data-tips-type="tip">After editing the alarm policy, the <strong>execution cycle</strong> and <strong>alarm sending cycle</strong> will restart timing.</div>


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. On the left navigation bar, select **Common Functions** \> **log alarm** \> **alarm policy**.

4. On the **alarm policy** page, click the specified alarm policy name, then click **Edit** in the upper\-right corner of the details page.

   You can also click **Edit** directly in the **Actions** column on the **alarm policy list** page.

5. Follow the on\-screen instructions to reset the alarm policy.


<span id=".5aSN5Yi25ZGK6K2m562W55Wl"></span>
## Copy alarm policy

When you need to quickly create multiple similar alarm policies, you can do so by copying an existing alarm policy. TLS supports copying alarm policies across regions and projects.


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Features** \> **log alarm** \> **alarm policy**.

4. On the **alarm policy** page, select one or more alarm policies and click **Copy**.

5. On the batch copy alarm policy page, fill in the information below, then click **Next: Execute Task**.

   
   |Configuration |Description |
   |---|---|
   |Target Region |Select the target Region to batch copy alarm policies to. |
   |Target project |Select the target project to batch copy alarm policies. |
   |Alarm rules |Set the new alarm policy name, monitoring target (log topic), notification group, and alarm status.<br><br><br>* The number of monitoring targets (log topics) in the target alarm policy must match that of the source alarm policy. For example, if the source alarm policy monitors only one log topic, then only one log topic should be selected here as well.<br><br>* A notification group must be set; otherwise, alarms will fail. |
   

6. After the task import status shows **Import Successful**, click **Finish**.


<span id=".5Yig6Zmk5ZGK6K2m562W55Wl"></span>
## Delete alarm policy


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Functions** \> **log alarm** \> **alarm policy**.

4. On the **alarm policy** page, find the alarm policy to delete, and select ... \> **Delete** in the corresponding **Actions** column. 

5. Confirm the information of the alarm policy to delete, and click **Delete**.
