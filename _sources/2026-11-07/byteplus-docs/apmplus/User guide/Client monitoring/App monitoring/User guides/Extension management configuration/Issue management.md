---
title: "Issue management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Issue_management"
---

Issue management includes issue overview, My Issue, issue auto assign, and My Issue Notification. You can search for issue distribution, issues pending your action, and automatically assign an assignee to an issue based on feature values such as stack trace.

<span id="d0a57928"></span>
## issue overview

<span id="3f8f2b1c"></span>
### Filter dimensions

Filter dimension description:

Supported filter dimensions: time, operating system, issue new status, APP version, APP minor version, issue status, tag, assignee, exception type.


* Exception types supported by iOS: crash, hang, OOM crash, Extension crash, crash protection, MetricKit crash, MetricKit lag, MetricKit CPU anomaly, MetricKit disk monitor, custom error, lag, severe lag, Dart exception, leak, large object, JavaScript error, request error, CPU anomaly, exception file, exception folder, expired file.

* Android supported exception types: Java crash, Java startup crash, Native crash, ANR, application exit cause, custom error, lag, severe lag, Dart exception, leak, large object, JavaScript error, request error, battery anomaly, CPU anomaly, exception file, exception folder, expired file, total traffic too high, background traffic too high, traffic too high before startup.


<span id="c2be9c0b"></span>
### Overview report


* Issue processing data: all, processing rate, resolved, being fixed, pending.

* Handling distribution: Distribution of issue status.

* Exception type: By default, the distribution of **exception type** is displayed. You can select other metrics from the dropdown to view their distributions, including **App version**, **App version code**, and **custom Tag**.


<span id="d09d4a21"></span>
### Issues list


* Issue list columns: exception detail, exception type, number of affected users, occurrence count, most recent occurrence time, log report time, status, assignee.

* Download: Click the download button in the upper right corner to download the first 10,000 records and display the data in the list in the `.xlsx` file format.

* Settings: Click the settings button in the upper right corner. In addition to the columns that are checked by default, you can also choose to display other metric columns as needed, including **Year\-over\-Year occurrence count**, **Year\-over\-Year exception impacted users rate**, and **start and end versions**. The **exception detail** column must always be displayed and cannot be deselected.

* Exception detail: Click the specific **exception detail** to go to the details page for the corresponding exception type. For example, the exception type of this issue is lag. Click the Exception Details to go to the Lag Details page.


<span id="6e5ecb85"></span>
## My Issue

<span id="056a1f52"></span>
### Filter dimensions

Filter dimension description:

Supported filter dimensions: time, operating system, issue new status, APP version, APP minor version number, issue status, tag, and exception type.


* Exception types supported by iOS: crash, hang, OOM crash, Extension crash, crash protection, MetricKit crash, MetricKit lag, MetricKit CPU anomaly, MetricKit disk monitor, custom error, lag, severe lag, Dart exception, leak, large object, JavaScript error, request error, CPU anomaly, exception file, exception folder, expired file.

* Supported Android exception types: Java crash, Java start crash, Native crash, ANR, application exit reason, custom error, lag, severe lag, Dart exception, leak, large object, JavaScript error, request error, battery anomaly, CPU anomaly, exception file, exception folder, expired file, excessive total traffic, excessive background traffic, excessive traffic before startup.


<span id="4fc25bcb"></span>
### Process statistics

View the current status and progress of My Issue in the processing statistics section.


* Issue processing data: All, resolved, under repair, pending.

* Issue processing progress: The current status of issue resolution.


<span id="d9b62acb"></span>
### Issue lists


* Issue list columns: exception detail, exception type, affected user count, occurrence count, recent occurrence time, log report time, status, assignee.

* Download: Click the download button in the upper right corner to download the first 10,000 entries from the list in `.xlsx` file format.

* Setting: Click the setting button in the upper right corner. In addition to the columns that are checked by default, you can select additional metric columns to display as needed, including Year\-over\-Year occurrence count, Year\-over\-Year exception impacted users rate, and start/end version. The data in the **exception detail** column must be displayed and cannot be unchecked.

* Exception details: Click the specific **exception detail** to open the issue details page.


<span id="d5c2e1ca"></span>
## My Issue Notification

The My Issue Notification feature is turned off by default. To turn on this feature, please manually enable it by switching on the **My Issue Notification switch** button. After issue notifications are enabled, notifications for issues assigned to you will be sent according to the configured notification method.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The issue types currently supported for receiving change notifications are crash, lag, custom error, and iOS Crash Protection.</div>


<span id="a57f679f"></span>
### Configure issue notifications


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> My Issue Notification**.

4. After clicking the **edit** button, turn on the **My Issue Notification** switch.

5. After completing the following configuration, click **Save**.

   Parameter description:

   
   |Notification method |Issue notifications are supported via **Lark**, **email**, **WeCom**, and **DingTalk**. |
   |---|---|
   |Lark webhook |Enter the Lark webhook. When the alert method is set to **Lark**, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   |People to @\-mention in Lark |Lark users for whom alert notification configuration is based on User ID or Open ID. When the alert method is set to **Lark**, this field is optional.<br><br>To obtain User ID and Open ID, refer to [How to obtain User ID, Open ID, and Union ID](https://open.feishu.cn/document/home/user-identity-introduction/open-id).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group robot.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Please ensure that the User ID and Open ID are correct; otherwise, the notification cannot be delivered to the user.</div><br> |
   |Email |Configure email When the alert method **email** is selected, this field is required. |
   |WeCom webhook |Enter WeCom webhook. When the alert method **WeCom** is selected, this field is required.<br><br>For details on webhook configuration, see [How to configure webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   |People to be @\-mentioned in WeCom |WeCom users whose alert notifications are configured according to their mobile phone number or User ID. When the alert method is set to **WeCom**, this field is optional.<br><br>To obtain the User ID, refer to [User ID](https://developer.work.weixin.qq.com/document/path/98728#.5piO5paHdXNlcmlk).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Individuals who receive notification must be in the same group as the group bot.</div><br> |
   |DingTalk webhook |Enter DingTalk webhook. When the alert method is set to **DingTalk**, this field is required.<br><br>For details on webhook configuration, see [How do I configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   |People to @\-mention in DingTalk |DingTalk users configured for alert notification by mobile phone number or User ID. When the alert method is set to **DingTalk**, this item is optional.<br><br>To obtain the User ID, refer to [User ID](https://open.dingtalk.com/document/orgapp/basic-concepts#title-o8w-yj2-t8x).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group bot.</div><br> |
   

   After configuration is complete, the notification logic description is as follows:

   * All users under the same root user account can be assignees for issues and can assign issues to each other.

   * If you assign an issue to yourself, you will not receive a notification. If you assign an issue to someone else, you will receive a notification according to that person's issue notification settings. Similarly, when another person assigns an issue to you, you will receive a notification according to the issue notification method you have set.

   * When the assignee is deleted, they will not receive a notification.


<span id="6452d1c8"></span>
## issue auto assign

The issue auto assign feature designates an assignee for each issue according to predefined rules after the platform collects crashes and exceptions, saving manual effort in assigning issues and preventing issues from remaining unattended for extended periods of time. You can view the assignment results in the issue list.

<span id="4bf291e4"></span>
### Create rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The issue auto assign feature is enabled by default, and only the root user can turn this feature on or off.</div>



1. Log in to [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> issue auto assign**.

4. On the **issue auto assign** page, complete the following configuration, then click **create rule**.

   Configuration description:

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |issue auto assign |If the switch is turned on, the platform will automatically assign an assignee to the issue. Enabled by default; only the root user can enable or disable. |
   |Operating System |Select an operating system.<br><br><br>* **Android**<br><br>* **iOS** |
   

5. In the **Create Rule** dialog box, complete the following configuration, and then click **Confirm**.

   Configuration description

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Rule name |Custom name used to identify rules. |
   |Issue type |* Issue types supported by the Android operating system: **Java crash**, **Java startup crash**, **Native crash**, and **ANR**.<br><br>* Issue types supported by the iOS operating system: **crash**, **OOM crash**, **hang**, and **Extension crash**. |
   |Eigenvalue |Different issue types support different feature values.<br><br>Use "AND" between features, and use "OR" among values within a feature.<br><br>For example, if the above configuration is applied, when **the stack trace contains 123** and **the crash thread contains com.gateio.a** and (**the app version** is 1.0.0 or 1.0.2), the issue will be assigned to the assignee apmplus\-test. |
   |assignee |To add an assignee, add a member in the account permission management section. For more details, refer to [Permission management](https://docs.byteplus.com/en/docs/apmplus/Client_permissions_management). |
   |Priority |Priority of sliding rail configuration The smaller the number, the higher the priority. |
   


<span id="edce499d"></span>
### Issue lists


* Issue list: Rule name, rule content, priority, assignee, creator, last modified time, actions.

* Sorting: The list is sorted by priority from high to low, and items with the same priority are sorted by modification time from most recent to oldest.

* **edit**: Modify rule information. All users can perform this action.

* **delete**: Delete this rule. All users can perform this action.

* **Copy**: Copy this rule; all users can perform this action.

* filter

   * OS version: After selecting Android or iOS, the list displays the rules for the selected operating system.

   * Search: Search for rules by rule name or content.

   * Date: Filter rules based on the range of modification time.

   * Assignee: According to assignee filter rules.
