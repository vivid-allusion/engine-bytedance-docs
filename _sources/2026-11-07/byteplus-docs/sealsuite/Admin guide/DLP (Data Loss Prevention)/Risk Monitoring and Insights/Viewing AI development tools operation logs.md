---
title: "Viewing AI development tools operation logs"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/viewing-ai-development-tools-operation-logs"
---

With the AI Development Tool Operation Logs provided by SealSuite, administrators can monitor in real time how employees use AI collaboration tools on endpoints to access sensitive code repositories. The logs record not only basic access behaviors, but also model API addresses and account compliance information in depth, providing a key basis for enterprises to identify "shadow AI" risks.

<span id="15f221bb"></span>
## Scenario Description

When an employee endpoint hits an **AI power builder operation control policy**, the system automatically generates an audit log. Administrators can use such logs to achieve the following objectives:


* **Quantify risks**: Assess the frequency and scale of employees using non\-compliant AI tools, such as a personal version of Cursor, to process internal code.

* **Trace compliance risks**: When a code leakage risk occurs, accurately trace the involved employee, device, specific local repository path, and requested external model API.

* **Optimize policies**: Adjust access policies or guide employees to migrate to compliant tools in a timely manner based on the audited shadow AI usage preferences.


<span id="84d30f81"></span>
## Procedure


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Investigation Audit** \> **Audit Log**.

3. At the top of the right\-side page, switch to the **AI Development Tools Operation Log** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab06ec72b0ec4306a52148e27819ee29~tplv-goo7wpa0wc-image.image) </span>

4. The log list page supports the following operations:

   * **Filter and search**: Supports combined filtering by "Event ID", "Event Time", "User", "Device", "Operations" (Read locally / Upload Inference), "AI development tools", and other dimensions.

   * **View details**: Click **Details** in the **Action** column of the target log to view complete forensic information.

   * **Export logs**: Click **Export List** in the upper\-right corner of the list to save the filtered logs as a CSV file locally for further analysis.


<span id="8a521420"></span>
## Log Detail Field Description

On the log details page, the system displays all forensic details of the audit event.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Log Reporting Frequency</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>Audit</strong>: To balance performance and audit requirements, access behaviors involving the same code repository and the same AI tool are usually reported only once per day. If the Base URL or account changes, the system reports the event again in real time.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Deny</strong>: For security and compliance requirements, an alert log is generated in real time each time a blocking action is triggered.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bfa9e3bdc1b4c8ea7eb5456dc49edc3~tplv-goo7wpa0wc-image.image) </span>

The key fields are described as follows.

<span id="a1092060"></span>
### Operation Info


* **Operations**

   * **Upload Inference**: Indicates that the AI tool sends code content to a large language model API for logical inference. This behavior is directly associated with data outbound risks.

   * **Read locally**: Indicates that the AI tool reads files in the local code repository. This behavior usually occurs when the AI tool builds a code index, generates completion prompts, or performs local static analysis.

* **AI Development Tool Name**: Displays the specific tool that triggered the behavior, such as TRAE IDE.

* **Code Repository Address**: Displays the remote repository link associated with the local repository, such as a GitHub or GitLab link.

* **Code Repository Local Path**: Records the physical storage path of the file on the endpoint device.

* **Model Base URL**: Records the actual large language model API address requested by the AI tool, directly indicating the final destination of the code data. If the address is an enterprise\-built model API or a company\-authorized third\-party large language model platform, it is compliant. If the address is an unauthorized public API, there is a compliance risk that code may be leaked to external vendors and used for model training. Pay close attention to such cases.

* **Login Account**: Displays the specific login account name, such as an email address. Check whether the account belongs to the enterprise domain or is associated with an organization recognized by the company.

* **Account Type**: Identifies whether the login account is a personal account or an enterprise account.

   We advise you to check whether the employee uses an enterprise account that was centrally purchased or authorized by the enterprise.

* **Account Company Name**: If the account is an enterprise account, displays the associated organization name.


<span id="851de7ba"></span>
### User and Device Information

This section provides information about the user and device that triggered the audit event.


* **User Information**: Includes basic information about the involved employee, such as name, department, and email address.

* **Device Information**: Displays the name, operating system, IP address, Feilian version, and other information of the risky endpoint. Administrators can use this information to quickly trace the historical compliance records of the employee or device.


<span id="12282536"></span>
## Related Operations


* **Export logs**: Click **Export List** in the upper\-right corner of the log list to save the filtered logs as a CSV file locally, facilitating further analysis or compliance archiving by the security team.

* **Log forwarding**: SealSuite supports forwarding AI Development Tool Operation Logs in real time to the enterprise's own Syslog or Elasticsearch service for unified security analysis or long\-term tracing.

   * **Forwarding configuration**: For detailed instructions, see [Log Export and Auditing](https://docs.byteplus.com/docs/sealsuite/docs-zk9yxy9szc).
