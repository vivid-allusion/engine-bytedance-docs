---
title: "Configure a Web data protection policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy"
---

Web data protection policies detect data that employees transmit through websites and cloud applications. They help enterprises identify risks from outbound sensitive information and audit or block outbound sensitive text. Configure detection rules for outbound text, file uploads, and file downloads based on different applications and employee scopes.

<span id="doxcngFmAYbmp0Bmgh8Cug1LZph"></span>
## Feature description

<span id="doxcn3EsxYrE81mlAZLyvnzzGbe"></span>
### When a policy is triggered

Set rules for specified employees or devices to check text and files they send in specified websites and cloud applications.

For example, check whether files uploaded by the sales department to a public cloud drive contain customer information. In this example, select the sales department, the target cloud drive, and **Sensitive File Uploads**, then add classification and grading rules that identify customer information. When sales department employees upload files to this cloud drive, the system records an audit log if the files contain customer information defined by the rules. Employees or devices added to **excluded objects** are not controlled by this policy.

**Classification and grading rules** define the sensitive content to identify, such as customer mobile numbers, ID card numbers, or enterprise business data. Prepare rules in data identification, then select these rules in **Outgoing content** of the policy. Outbound text and file uploads use this method to identify sensitive content. File downloads only check file size and file type.

<span id="doxcn8aZw6fIFDbfKtsT2GTdbje"></span>
### Which actions can be checked


|Action |Detection basis |Use cases and actions |
|---|---|---|
|Outbound text |Whether outbound text matches classification and grading rules. |Detect sensitive text submitted through web forms, online messages, and more. The current outbound action can be audited or blocked. |
|File uploads |Whether the content of uploaded files matches classification and grading rules. |Audit the upload of sensitive files to websites and cloud applications. The current upload is not blocked.<br><br>Files are inspected asynchronously after upload. The system checks their content and records policy matches after the upload has completed. Therefore, file upload detection supports audit only and does not intercept the current upload. |
|File download |File size, file type, and application scope. |Record or block download actions that meet the conditions. Sensitive content in downloaded files is not scanned. |


<span id="doxcnGR4fbFGSNTBwgJFUfWmwDO"></span>
## Prerequisites


* A traffic diversion policy is configured so that Endpoint traffic requiring control passes through Secure Web Gateway (SWG). For details, see [Configure a traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies?lang=en).

* Enterprise root certificate configuration and distribution are complete, and Endpoints trust the enterprise root certificate. For HTTPS traffic, make sure the traffic of the target application can be decrypted. If an SSL decryption policy with "Do not decrypt" is matched, sensitive content cannot be detected. For details, see [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies?lang=en).

* If sensitive content in text or uploaded files needs to be detected, the corresponding classification and grading rules are prepared. Use built\-in rules or add custom rules based on enterprise requirements. For details, see [Manage classification and grading rules](https://docs.byteplus.com/en/docs/sealsuite/managing-classification-and-grading-rules?lang=en).


<span id="doxcns6K7aumfGG1cyckBHwbJde"></span>
## Add a Web data protection policy

<span id="doxcnt3MYpydnbaaXz8FLI2Deqc"></span>
### Step 1: Enter basic information


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **DLP** \> **Strategy Center**.

3. On the **Control Strategy** tab, select **Network DLP**, then click **Create policy**.

4. On the **Add NDLP Strategy** page, enter the following basic information.



|Configuration item |Description |
|---|---|
|Policy name |Required. Customize a name to identify the policy, such as "Block outbound sensitive text on public collaboration platforms". |
|Policy Description |Optional. Add a description of the policy purpose and scope. Up to 100 characters are supported. |
|Priority |Defines the policy execution order (0\-100). **A higher value indicates a higher priority**. If multiple policies with the same priority are matched, the policy with the latest update time is executed. If a policy has never been modified, its update time is its creation time. |
|Manage labels |Select a tag to associate with the current policy (optional). The drop\-down list shows only the tags granted to the current administrator. Associated tags isolate policy permissions between administrators in different regions or business lines.<br><br>To add or adjust the tag options visible in the drop\-down list, a super administrator must modify the "management tag scope" for your administrator role in **Enterprise Settings** \> **Administrator Permissions**. For details, see [Edit Administrator permissions](https://docs.byteplus.com/en/docs/sealsuite/docs-editing-or-deleting-administrator?lang=en). |


<span id="doxcnBEpjz26upe98xNNxV33hxe"></span>
### Step 2: Select an action

In the **Action** section, select how to handle policy matches. The action is set at the policy level. You then configure the actions to detect. The action applies only to the current outbound action and does not affect user access to the application itself.

File upload detection supports audit only. To detect sensitive content in uploaded files, select **Audit**. If you select **Block**, detection of **Sensitive File Uploads** is not supported.


|Action |Description |
|---|---|
|Audit |Records policy\-matched actions without affecting employee access to applications. This is suitable for observing outbound sensitive data conditions before adjusting the protection scope. |
|Block |Blocks policy\-matched actions and records the blocking reason. This can be used to block outbound sensitive text. |


<span id="doxcntEHfTNSedOagBJS3WIXhlb"></span>
### Step 3: Configure detection actions

In the **Control Action** section, enable the switches for the actions to detect, then click the corresponding **Expand** to configure the application scope and detection conditions. Application scopes are configured separately for each action. Check the selected applications one by one.

<span id="doxcnwXeA9uPPHqHQw0dNmFTKee"></span>
#### Outbound text

Detect sensitive text that employees enter, paste, or submit through websites and cloud applications, such as text in web forms, online messages, and online documents.


1. Enable **Sensitive Text** and click **Expand**.

2. In the **Select cloud applications** section, select the applications to detect. Search by application name or domain name, select applications by category in **Built\-in Applications**, or select enterprise\-configured resources in **Custom Resources**.

3. In the **Outgoing content** section, click **Add Data**.

4. In the window that appears, browse by category or search for the rules to detect, then select the corresponding data. View rule information through **Details**. After confirmation, click **Confirm**.

5. Check the added **Categorized and graded data** and **Data sensitive level**, and confirm that the rules align with your protection objectives.

   If no suitable rule is available, click **Go to manage hierarchical classification data** in the selection window to open the data identification page. Prepare rules, then return to the configuration.


For information about maintaining application resources, see [SWG Web resource library management](https://docs.byteplus.com/en/docs/sealsuite/swg-web-resource-library-management?lang=en).

If a classification and grading rule identifies content through sensitive words, it must reference a sensitive word library in **DLP** \> **Data Identification** \> **Sensitive Thesaurus**. Select a built\-in sensitive word library, or add an enterprise custom sensitive word library first. Then reference it in a classification and grading rule and apply the rule to the Web data protection policy. For details, see [Manage sensitive word libraries](https://docs.byteplus.com/en/docs/sealsuite/managing-sensitive-thesaurus?lang=en) and [Manage classification and grading rules](https://docs.byteplus.com/en/docs/sealsuite/managing-classification-and-grading-rules?lang=en).

<span id="doxcn28qwKGrgGBneHuGWbtrdif"></span>
#### File uploads

Detect sensitive content in files that employees upload, send, or submit through websites and cloud applications, such as uploaded attachments, imported files, and submitted materials.


1. Confirm that the policy **Action** is **Audit**.

2. Enable **Sensitive File Uploads** and click **Expand**.

3. In the **Select cloud applications** section, select the applications whose file upload actions need to be detected.

4. In the **Outgoing content** section, click **Add Data**, select the classification and grading rules to detect, and confirm. The configuration method is the same as outbound text.

   File upload auditing is used to discover and trace outbound sensitive file transfers. It does not intercept the current file upload.


<span id="doxcnTBxwFAeei8vPPjgjjBnymc"></span>
#### File download

File download detection conditions are set by application scope, file size, and file type. Downloaded files are not scanned for sensitive content through classification and grading rules.


1. Enable **Sensitive File Downloads** and click **Expand**.

2. In the **Select cloud applications** section, select the applications whose download actions need to be detected.

3. Set **File size**, in MB, to define the lower size limit for files to detect.

   When set to **0**, file size is not limited. Only other policy conditions, such as application scope, file type, and effective objects, are detected.

4. Set **File type**.

   Select built\-in common file types, such as compressed files, WPS spreadsheets, and presentations.


<span id="doxcnGKHRkNiI2uNnlGiwZDEuab"></span>
### Step 4: Set effective objects


1. In the **Scope** section, select the policy scope.

   * **User**: Select by department, role, or member. Search to quickly locate target employees.

   * **Device**: Select by device or group. Search by employee, device name, or device ID.

2. To set exceptions for some objects, enable **Exclude object** and select the objects to exclude.

3. Check the action, application scope of each action, detection conditions, and effective objects. Click **Confirm** to save the policy.

4. Return to the policy list, check the **Policy Status** of the policy, and enable the policy as needed.


<span id="doxcnVJMskSxmxbIn9JmydIGXth"></span>
## Manage the policy lifecycle

In the **Network DLP** policy list, you can perform the following operations.


* **View quantity and status**: At the top of the list, policies are counted separately by audit and block, and by enabled and disabled status. In the list, view the priority, action, creation time, latest modification time, effective objects, and excluded objects of a single policy. This helps you check the current protection scope.

* **Search and filter**: Locate policies by audit or block type, effective status, personnel, device, policy name, and classification and grading rule name. For example, before adjusting a classification and grading rule, filter by rule name to find policies that reference it and check the impact scope. When troubleshooting a control issue for an employee, filter by personnel and effective status.

* **Enable or disable**: Use the **Policy Status** switch to control whether a policy participates in control. To temporarily pause a policy, disable it and retain the configuration. You can re\-enable it later as needed. Before disabling a policy, check the affected applications and effective objects.

* **Edit**: In the **Actions** column of the target policy, click **Edit**. Adjust the application scope, detection content, action, or effective objects, then save the policy. Before changing audit to block, review historical logs to confirm match conditions. File upload detection supports audit only. You cannot block file uploads by adjusting the action.

* **Delete**: In the **Actions** column of the target policy, click **Delete**. Follow the on\-page prompts to remove a policy that is no longer needed.


<span id="doxcnMMT7XNUOEAsW8qFATAXPGf"></span>
## View related logs

Policy configuration operations and employee policy\-matched actions are recorded in different logs.


* **Web Data Protection logs**: Go to **DLP** \> **Investigation Audit** \> **Audit Log** \> **Network DLP** to view records of employee outbound text, file uploads, and file downloads that match policies. Logs help trace what action occurred, who triggered it, which policy was matched, and what action was taken. Locate records by event time, employee, application, outbound action, and matched policy. Then view sensitive data identification results and related action information in the details. For outbound text and file uploads, focus on matched sensitive data. For file downloads, focus on file name, type, and size. Do not interpret a download log as confirmation that sensitive content detection has been completed for the file content.

* **Administrator operation logs**

   Go to **Audit Logs** \> **Admin Log** and filter by the operation module **Web Data Protection Policy**. View management operations such as policy creation, modification, and deletion to trace policy configuration changes.
