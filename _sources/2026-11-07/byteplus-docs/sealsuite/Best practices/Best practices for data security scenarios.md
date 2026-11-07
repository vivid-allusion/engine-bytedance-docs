---
title: "Best practices for data security scenarios"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Best-practices-for-data-security-scenarios"
---

This document aims to provide enterprises with a detailed set of best practices for implementing data classification and auditing strategies. By integrating SealSuite's Data Loss Prevention (DLP) capabilities, enterprises can safeguard their data security and simultaneously boost the efficiency of their auditing processes.

 &nbsp;

<span id="feature-overview"></span>
# Feature overview

SealSuite's Data Loss Prevention (DLP) offers businesses flexible and robust data security through sophisticated data classification. Enterprises have the flexibility to categorize their data into various levels of confidentiality based on their unique business requirements and the data's sensitivity. This classification strategy enables businesses to identify the required data confidentiality levels and ensures the adequate protection of essential information.

Meanwhile, the DLP System ensures the transmission and access activities of data meet the enterprise's security policies and compliance requirements by automating the DLP audit policy, monitoring file\-sharing behavior in real time, and automatically executing the audit process.

 &nbsp;

<span id="scenario-one:-data-protection-for-the-r&d-department-in-the-manufacturing-industry"></span>
# Scenario One: Data protection for the R&D department in the manufacturing industry

 &nbsp;

<span id="scenario-description"></span>
## Scenario description

The R&D department is the enterprise's innovation engine in the manufacturing industry, managing core sensitive data, including engineering drawings and 3D models. This data is crucial for protecting the enterprise's intellectual property rights. R&D personnel frequently use various applications to create and edit data, but data sharing must occur through authorized channels. Lark Mail, as the main audit point, ensures that all shared files meet security standards.

 &nbsp;

<span id="procedure"></span>
## Procedure


1. **Define sensitive data**: Classify engineering R&D data, 3D models, 2D engineering drawings, and general design documents as Level 4 sensitive data. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, under the **File Transfer Control** tab, click **Go to manage sensitive documents**.

   4. In the list of all data on the left, select your target custom category.

      If no custom categories exist, you need to create a new custom category. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   5. In the specified custom category, click on **Add New Sensitive File**, and choose **New Sensitive File** or **New Code Repository**:

      * For guidance on adding **New Sensitive File**, please refer to step f.

      * For guidance on adding **New Code Repository**, please refer to step g.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f6da7f3f30345dabf7f5d769b3f0274~tplv-goo7wpa0wc-topic.webp) </span>

   6. (Optional) Should you opt to add **New Sensitive File**, please complete the necessary configurations in the **Add New Sensitive File** pop\-up window on the right and click **Confirm** to proceed.

      * **Name**: A custom name to identify the current sensitive file.

      * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

      * **Rules**: Click **Add New** to configure rules in the following dimensions, with an AND relationship between multiple rules. SealSuite will subsequently match sent files based on the configured rules.

         * **File name** or **File content.** 

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">Note            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4"><strong>File name</strong> or <strong>File content</strong> rule configuration actions are consistent, this section takes <strong>File name</strong> as an example to introduce how to configure rules.            </div>
            

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c2e5d26737249f49d35675af7277051~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in area ① of the figure above, it supports choosing **Match any** or **Match all**.

   \* **Match any**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged if any one of those conditions is matched.

   \* **Match all**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged only if all conditions are matched.

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ③ as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured rules, you can click **Delete**.

   \* In the area ③ as shown above, click on the dropdown box to select from the options: **Identification Model**, **Built\-in Regular Expressions**, **Custom Regular Expressions**, **Keywords**, or **File Fingerprint**.

   \* **Identification Model**: Default provides multidimensional models such as function design scheme model, procurement contract model, cooperation agreement model, etc. You can choose one or more applicable models.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbccb37724db4215a6d3368b38ccb525~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Built\-in Regular Expressions:**  Default provides a variety of regular models, you can choose one or more options.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b59cc86676748fcae019bff7c36054e~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Custom Regular Expressions**: Configure your own regular expression settings. You can select or create one or more regular expressions, such as [a\-z], and press the Enter key to save them.

   \* **Keywords**: Enter your custom keywords here. You can select or create one or multiple keywords, and press the Enter key to save.

   \* **File fingerprint**: Implement custom file fingerprinting. You can select or create one or multiple file fingerprints.

   :::tip Note

   File fingerprint refers to information that can uniquely identify a digital file. File fingerprint matching protects key files in the system from being leaked by adopting a method of calculating the similarity of file fingerprints. File fingerprint is only applicable to **File content**.

   :::

   \* **File type**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac49053a32b54ed9893389f4212da47b~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area ① above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured rules, you can click **Delete**.

   \* As shown in the area ② above, click the dropdown box to select **Pre\-defined** or **Custom**.

   \* **Pre\-defined**: The SealSuite Admin Console includes a set of pre\-defined file types, including plain text files, formatted text, PDF documents, Office Word documents, and Office Excel spreadsheets, Office PPT PowerPoint, image files, compressed files, audio files, video files, and other file types.

   \* **Custom**: If the **Pre\-defined** file types do not meet your needs, you can specify your own file types using the format `.file suffix`. For example: `.psd`.

   As shown in the figure below, you can configure one or more **Pre\-defined** or **Custom** file types, where you need to press Enter to save when you add a **Custom** file type.

   :::tip Note

   Custom file types and some pre\-defined file types do not support parsing file content.

   :::

   \* **File size**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/754c26cee9fd4425aeae43b8f77bef5e~tplv-goo7wpa0wc-topic.webp) </span>

   It supports setting file size to be **greater than or equal to** or **less than or equal to** a specified value. The unit of file size supports **GB**, **MB**, **KB**, and **B**. For example, as shown in the figure above as default settings, it indicates the file size is greater than or equal to 100 MB.

   \* **File source**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09eec0d4b44346f9ac22df2a911c5518~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area marked ① in the figure above, you can choose one or more file sources, then use the search bar on the right to choose one or more source apps or websites.

   :::tip Note

   When you choose the option to download from a custom website, you can create a new website address. Other options do not support new creation.

   :::

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   After successfully adding sensitive data, you can view the data in the specified category of custom sensitive data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a85b836b622d48c1b0ad2090104e457f~tplv-goo7wpa0wc-topic.webp) </span>

   7. (Optional) If you choose to add **New Code Repository**, you need to complete the following configurations in the newly popped\-up **Add New Sensitive File** interface and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe694d70d294de8a767a8c169265555~tplv-goo7wpa0wc-topic.webp) </span>

   * **Name**: A custom name to identify the current sensitive file.

   * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

   * **Rules**: Click **Add New** to add rules and set the source domain of the Git code or SVN code repository. Supports the addition of multiple rules which operate based on an OR relationship.

2. **Configure audit policies**: Configure separate audit policies for each type of sensitive data to monitor all outgoing channels. For further information, please refer to [Configuring block policy for file-sharing behavior](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In web detection, we define recognition rules for Lark email addresses and set up an allowlist to exclude internal websites and Lark enterprise tenant URLs, thus ensuring the accuracy and focus of detection. Meanwhile, in instant messaging (IM) detection, by enabling exclusion rules, we effectively exclude Lark from being detected to avoid disturbing normal communication.   </div>
   

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, in the **File Transfer Control** tab, click the **Policy Management** tab.

   4. In the upper right corner of the **Policy Management** tab, click **New Policy** \> **Audit Policy**. You can choose to create a policy or choose a template to create a copy.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa1e1714912748fea666d4514223a7cc~tplv-goo7wpa0wc-topic.webp) </span>

      * Click **Create a policy**, on the **Add Audit Policy** page, complete the configuration according to the table below, and click **Confirm**.

      * Hover the mouse over a template card and click **Create a copy**, complete the suggested configuration according to the table below, and click **Confirm**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">Note         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can click on <strong>Preview</strong> to learn about the main purposes and recommended configurations of this template, and at the bottom of the preview page, click on <strong>Use this template</strong> to create a template copy.         </div>
         

&nbsp;

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy name** |Custom name, used to identify the policy. |
   |**Priority** |The priority of the current policy. The value range is from 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time.<br><br>If multiple policies are enabled, the final executed policy will assessed according to priority. If there are two policies have same priority, then the policy with the latest updated time will be executed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set to view by <strong>Last modified time</strong> in the Policy Management list to see the latest updated policies.</div><br> |
   |**Source channel** |You can choose one or several from **Removable storage devices**, **Desktop Apps**, **Websites**, and **Code Repository**. The specific configuration instructions are as follows:<br><br><br>* **Removable storage devices**: It detects the behavior of users sending files to USB and portable hard disk.<br><br>* **Desktop Apps**: It detects the behavior of users sending files to Messaging Apps, Cloud Storage Apps, Mailbox, and other desktop softwares. Click on the right to **Expand**, and choose the desktop software you need to monitor. Different applications are supported by different operating systems. SealSuite supports monitoring of messaging apps, cloud storage apps, mailbox, note\-taking apps, online collaboration tools, file transfer tool, command\-line tool, remote control tool, and others.<br><br>* **Websites**: It detects user's behavior of sending data to third\-party browsers. Click on the right to **Expand**, and finish the following configuration.<br><br>   1. Check the **Browser**, click on the right to **View** **all**, and filter by the browsers you need to monitor. Different browsers are supported by different operating systems.<br><br>   2. Choose **All** or **Selected Websites**.<br><br>      This configuration is currently enabled on Mac And Windows operating systems.<br><br>      * **All**: Indicates monitoring of file\-sharing behavior on all websites within the browser.<br><br>      * **Selected Websites**: Indicates detecting file\-sharing behavior from specified websites in the browser. When choosing **Selected Websites**, the following configurations need to be performed.<br><br>         * Select specific websites provided by SealSuite.<br><br>         * If you are to select any websites outside from the pre\-defined library, click **Select Websites** on the the right side of the **Custom** area, and then add and select your desired websites through the **Select custom Website** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Websites** area, click **Select Websites**, then manually add and select the websites you want to exclude from the audit through the **Select custom Website** interface.<br><br>* **Code Repository**: Its behavior of pushing data\-party code repositories via Git push. Click **Expand** on the right to complete the following configurations.<br><br>   1. Select **Code Version Control Tool**, click **View all** on the right, and filter by the code version control tools you need to check.<br><br>   2. Choose **All** or **Selected Code Repository**.<br><br>      This configuration currently supports being enabled on Mac, Windows, and Linux operating systems.<br><br>      * **All**: Indicates detecting outgoing behaviors on all hosting platforms.<br><br>      * **Selected Code Repository**: Indicates detecting the outgoing behavior within a browser on the specified hosting platform. When you choose **Selected Code Repository**, you need to perform the following configuration.<br><br>         * Check the specified code repositories provided by SealSuite.<br><br>         * If the websites provided by SealSuite are not suitable, you can also click on **Select Code Repository** on the right of the **Custom** area on the right, and add and select the platform to be checked in the **Select Custom Code Repository** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Code Repository** section, click **Select** **Code Repository**, then in the **Choose Custom Code Repository** interface, manually add and select platforms to exclude from the audit.<br><br>* **Copy to Clipboard**: It detects the behavior of copying or cutting text content to the clipboard from software. If the file content contains sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **Paste from Clipboard**: It detects the behavior of pasting text content from the clipboard into an application. If the file content includes sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **File printing**: It detects whether printing sensitive files or web pages contains sensitive information. If sensitive data is found in the "File name" or "File content" during printing, SealSuite will automatically record the behavior through an audit policy.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file printing feature is available exclusively for Windows 7 and later versions, as well as macOS 10.15 and later versions.   </div><br>    |
   |**Outgoing Content** |Click on **Add New Sensitive File**, and in the **Add New Sensitive File** interface, Choose **Predefined templates** or **Custom sensitive files**. In the **Add New Sensitive File** interface, the following operations are supported:<br><br><br>* Supports selecting multiple sensitive data classification checkboxes in the left navigation bar, and upon selecting, all sensitive data within that category will be included.<br><br>* Within a specified sensitive data classification, supports choosing one or more specified sensitive data.<br><br>* Every sensitive data entry supports a **Preview**, through which you can view the specific configuration of that sensitive data. For instance, previewing large images, you can see that large images refer to image files greater than or equal to 20 MB.<br><br>* Predefined sensitive data supports **Create** **a copy**, which can only be saved to the **Custom sensitive files** category, where you can modify the category's name, data classification, and rules as needed.<br><br>* The custom sensitive data supports **Edit**, and you can adjust the content of custom sensitive data according to actual needs.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a custom sensitive data item has been referenced by an audit policy, then when that custom sensitive data is edited, the corresponding sensitive data within the policy will also be updated synchronously.   </div><br>   <br><br>After adding sensitive data, you can view the name and data classification. Additionally, you can click **View** in the **Actions** column to inspect the specific configurations or click **Remove** to delete sensitive data that is no longer required. |
   |**Action** |The default is **Generate alert**, and additionally, you can choose one or more of the options. You can also choose **Take screenshot** and **File archive** according to actual needs.<br><br><br>* **Generate alert**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the alarm information will be uploaded by the SealSuite client to the SealSuite Admin Console.<br><br>* **Take screenshot**: You can choose one or more from **Windows**, **macOS**, and **Linux**. When a data breach incident occurs on a user's terminal within the workflow scope, the SealSuite client will take screenshot and upload it to the SealSuite Admin Console. The taken screenshot can be viewed in the specified user's **Risky Actions** and **Sent File Details**.<br><br>* **File archive**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the SealSuite client will save the leaked file and upload it to the SealSuite Admin Console. The file archive can be viewed within the designated user's **Risky Actions**. |
   |**Scope** |Supports restricting effective scope based on either **User** or **Device** dimensions.<br><br><br>* When choosing a **User**, you need to limit the scope through the **Department** or **Role** group.<br><br>* When choosing **Device**, you need to limit the scope through the **Device**, **OS**, **Group**. |
   


 &nbsp;

<span id="results"></span>
## Results

With the implementation of data classification, the research and development department has been able to successfully block most unauthorized transmission attempts of sensitive data, greatly enhancing the security and efficiency of our data protection measures.

 &nbsp;

<span id="scenario-two:-supply-chain-department-data-management-control"></span>
# Scenario Two: Supply chain department data management control

 &nbsp;

<span id="scenario-description-1"></span>
## Scenario description

The Supply Chain Department is responsible for coordinating procurement and logistics, and often needs to handle sensitive information such as BOMs. They share files with suppliers through channels like WeChat and Lark, but all file\-sharing behaviors must undergo an audit to ensure information security. Strategically, file sharing through Lark is encouraged, while strictly throttling outgoing permissions on other channels.

 &nbsp;

<span id="procedure-1"></span>
## Procedure


1. **Configure block policies**: Only allow personnel in the supply chain department to send out files via WeChat. For further information, please refer to [Configuring block policy for application](https://docs.byteplus.com/docs/sealsuite/Configuring_block_policy_for_application).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, click on the **Channel Block Control** tab.

   4. In the upper right corner of the **Channel Block Control** tab, click **New Policy**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you are configuring the blocking policy for the first time, click <strong>Policy Configuration</strong> in the lower part of the page.      </div>
      

   5. On the **Add Blocking Policy** page, complete the following configurations, and click **Confirm**.

&nbsp;

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Policy name** |Custom name used to identify the policy. |
      |**Priority** |The priority of the current policy. The value range is from 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time.<br><br>If multiple policies are enabled, the final executed policy will assessed according to priority. If there are two policies have same priority, then the policy with the latest updated time will be executed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set to view by <strong>Last modified time</strong> in the Policy Management list to see the latest updated policies.</div><br> |
      |**Blocking Scope** |Displays the block scope on Windows, Mac, and Linux. Supported applications for blocking include Messaging Apps (Desktop and web versions), Cloud Storage Apps (Desktop and web versions), and Online Collaboration Tools (Desktop version). |
      |**Application** |Based on actual needs, specify the required **Messaging Apps, Cloud Storage Apps** Or **Online Collaboration Tools**, supports multiple selections. |
      |**Notification** |Whether to enable notification messages. Once enabled, when blocking file\-sharing behavior on a user's devices, SealSuite Client will send notification messages to warn the user.<br><br>Click **Edit notification template** to view the default notification content and preview the effect. You can also modify the notification content yourself.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="danger">Notification content includes Chinese and English content. When modifying content, you need to refresh the multi\-language configuration to avoid inconsistency in content in a multilingual environment.</div><br> |
      |**Scope** |Supports restricting effective scope based on either **User** or **Device** dimensions.<br><br><br>* When choosing a **User**, you need to limit the scope through the **Department** or **Role** group.<br><br>* When selecting **Device**, you need to restrict device scope through **Device**, **OS**, and **Group**. |
      

2. **Audit file\-sharing behavior**: Notify the User about the audit requirements, and guide them to send files through compliant channels, such as Lark. For further information, please refer to [Configuring block policy for file-sharing behavior](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, in the **File Transfer Control** tab, click the **Policy Management** tab.

   4. In the upper right corner of the **Policy Management** tab, click **New Policy** \> **Audit Policy**. You can choose to create a policy or choose a template to create a copy.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa1e1714912748fea666d4514223a7cc~tplv-goo7wpa0wc-topic.webp) </span>

      * Click **Create a policy**, on the **Add Audit Policy** page, complete the configuration according to the table below, and click **Confirm**.

      * Hover the mouse over a template card and click **Create a copy**, complete the suggested configuration according to the table below, and click **Confirm**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">Note         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can click <strong>Preview</strong> to understand the main purposes and recommended settings for this template. At the bottom of the preview page, click <strong>Use this template</strong> to create a template copy.         </div>
         

&nbsp;

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy name** |Custom name, used to identify the policy. |
   |**Priority** |The priority of the current policy. The value range is from 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time.<br><br>If multiple policies are enabled, the final executed policy will assessed according to priority. If there are two policies have same priority, then the policy with the latest updated time will be executed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set to view by <strong>Last modified time</strong> in the Policy Management list to see the latest updated policies.</div><br> |
   |**Source channel** |You can choose one or several from **Removable storage devices**, **Desktop Apps**, **Websites**, and **Code Repository**. The specific configuration instructions are as follows:<br><br><br>* **Removable storage devices**: It detects the behavior of users sending files to USB and portable hard disk.<br><br>* **Desktop Apps**: It detects the behavior of users sending files to Messaging Apps, Cloud Storage Apps, Mailbox, and other desktop softwares. Click on the right to **Expand**, and choose the desktop software you need to monitor. Different applications are supported by different operating systems. SealSuite supports monitoring of messaging apps, cloud storage apps, mailbox, note\-taking apps, online collaboration tools, file transfer tool, command\-line tool, remote control tool, and others.<br><br>* **Websites**: It detects user's behavior of sending data to third\-party browsers. Click on the right to **Expand**, and finish the following configuration.<br><br>   1. Check the **Browser**, click on the right to **View** **all**, and filter by the browsers you need to monitor. Different browsers are supported by different operating systems.<br><br>   2. Choose **All** or **Selected Websites**.<br><br>      This configuration is currently enabled on Mac And Windows operating systems.<br><br>      * **All**: Indicates monitoring of file\-sharing behavior on all websites within the browser.<br><br>      * **Selected Websites**: Indicates detecting file\-sharing behavior from specified websites in the browser. When choosing **Selected Websites**, the following configurations need to be performed.<br><br>         * Select specific websites provided by SealSuite.<br><br>         * If you are to select any websites outside from the pre\-defined library, click **Select Websites** on the the right side of the **Custom** area, and then add and select your desired websites through the **Select custom Website** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Websites** area, click **Select Websites**, then manually add and select the websites you want to exclude from the audit through the **Select custom Website** interface.<br><br>* **Code Repository**: Itthe user's behavior of pushing data to third\-party code repositories via Git push. Click **Expand** on the right to complete the following configurations.<br><br>   1. Select **Code Version Control Tool**, click **View all** on the right, and filter by the code version control tools you need to check.<br><br>   2. Choose **All** or **Selected Code Repository**.<br><br>      This configuration currently supports being enabled on Mac, Windows, and Linux operating systems.<br><br>      * **All**: Indicates detecting outgoing behaviors on all hosting platforms.<br><br>      * **Selected Code Repository**: Indicates detecting the outgoing behavior within a browser on the specified hosting platform. When you choose **Selected Code Repository**, you need to perform the following configuration.<br><br>         * Check the specified code repositories provided by SealSuite.<br><br>         * If the websites provided by SealSuite are not suitable, you can also click on **Select Code Repository** on the right of the **Custom** area on the right, and add and select the platform to be checked in the **Select Custom Code Repository** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Code Repository** section, click **Select** **Code Repository**, then in the **Choose Custom Code Repository** interface, manually add and select platforms to exclude from the audit.<br><br>* **Copy to Clipboard**: It detects the behavior of copying or cutting text content to the clipboard from software. If the file content contains sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **Paste from Clipboard**: It detects the behavior ofpasting text content from the clipboard into an application. If the file content includes sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **File printing**: It detects whether printing sensitive files or web pages contains sensitive information. If sensitive data is found in the "File name" or "File content" during printing, SealSuite will automatically record the behavior through an audit policy.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file printing feature is available exclusively for Windows 7 and later versions, as well as macOS 10.15 and later versions.   </div><br>    |
   |**Outgoing Content** |Click on **Add New Sensitive File**, and in the **Add New Sensitive File** interface, Choose **Predefined templates** or **Custom sensitive files**. In the **Add New Sensitive File** interface, the following operations are supported:<br><br><br>* Supports selecting multiple sensitive data classification checkboxes in the left navigation bar, and upon selecting, all sensitive data within that category will be included.<br><br>* Within a specified sensitive data classification, supports choosing one or more specified sensitive data.<br><br>* Every sensitive data entry supports a **Preview**, through which you can view the specific configuration of that sensitive data. For instance, previewing large images, you can see that large images refer to image files greater than or equal to 20 MB.<br><br>* Predefined sensitive data supports **Create** **a copy**, which can only be saved to the **Custom sensitive files** category, where you can modify the category's name, data classification, and rules as needed.<br><br>* The custom sensitive data supports **Edit**, and you can adjust the content of custom sensitive data according to actual needs.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a custom sensitive data item has been referenced by an audit policy, then when that custom sensitive data is edited, the corresponding sensitive data within the policy will also be updated synchronously.   </div><br>   <br><br>After adding sensitive data, you can view the name and data classification. Additionally, you can click **View** in the **Actions** column to inspect the specific configurations or click **Remove** to delete sensitive data that is no longer required. |
   |**Action** |The default is **Generate alert**, and additionally, you can choose one or more of the options. You can also choose **Take screenshot** and **File archive** according to actual needs.<br><br><br>* **Generate alert**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the alarm information will be uploaded by the SealSuite client to the SealSuite Admin Console.<br><br>* **Take screenshot**: You can choose one or more from **Windows**, **macOS**, and **Linux**. When a data breach incident occurs on a user's terminal within the workflow scope, the SealSuite client will take screenshot and upload it to the SealSuite Admin Console. The taken screenshot can be viewed in the specified user's **Risky Actions** and **Sent File Details**.<br><br>* **File archive**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the SealSuite client will save the leaked file and upload it to the SealSuite Admin Console. The file archive can be viewed within the designated user's **Risky Actions**. |
   |**Scope** |Supports restricting effective scope based on either **User** or **Device** dimensions.<br><br><br>* When choosing a **User**, you need to limit the scope through the **Department** or **Role** group.<br><br>* When choosing **Device**, you need to limit the scope through the **Device**, **OS**, **Group**. |
   


 &nbsp;

<span id="results-1"></span>
## Results

Through the application of blocking strategy, the audit coverage of outgoing documents in the supply chain department is improved, effectively avoiding the unauthorized dissemination of sensitive information.

 &nbsp;

<span id="scenario-three:-data-management-in-the-manufacturing-industry's-hr-department"></span>
# Scenario Three: **Data management in the manufacturing industry's HR department**

 &nbsp;

<span id="scenario-description-2"></span>
## Scenario description

The HR Department is responsible for managing payroll data, which typically are highly sensitive and require special protection measures. Data concerning social security, housing provident fund details, and compensation plans are classified as Level Three sensitive materials. They must be accurately identified and safeguarded according to their file type and content.

 &nbsp;

<span id="procedure-2"></span>
## Procedure


1. **Define Sensitive Data**: Classify data pertaining to social security funds, compensation schemes, individual compensation details, and related statistics as Level 3 sensitive files. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, under the **File Transfer Control** tab, click **Go to manage sensitive documents**.

   4. In the list of all data on the left, select your target custom category.

      If no custom categories exist, you need to create a new custom category. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   5. In the specified custom category, click on **Add New Sensitive File**, and choose **New Sensitive File** or **New Code Repository**:

      * For guidance on adding **New Sensitive File**, please refer to step f.

      * For guidance on adding **New Code Repository**, please refer to step g.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f6da7f3f30345dabf7f5d769b3f0274~tplv-goo7wpa0wc-topic.webp) </span>

   6. (Optional) Should you opt to add **New Sensitive File**, please complete the necessary configurations in the **Add New Sensitive File** pop\-up window on the right and click **Confirm** to proceed.

      * **Name**: A custom name to identify the current sensitive file.

      * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

      * **Rules**: Click **Add New** to configure rules in the following dimensions, with an AND relationship between multiple rules. SealSuite will subsequently match sent files based on the configured rules.

         * **File name** or **File content**.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">Note            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4"><strong>File name</strong> or <strong>File content</strong> rule configuration actions are consistent, this section takes <strong>File name</strong> as an example to introduce how to configure rules.            </div>
            

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c2e5d26737249f49d35675af7277051~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in area ① of the figure above, it supports choosing **Match any** or **Match all**.

   \* **Match any**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged if any one of those conditions is matched.

   \* **Match all**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged only if all conditions are matched.

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ③ as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   \* In the area ③ as shown above, click on the dropdown box to select from the options: **Identification Model**, **Built\-in Regular Expressions**, **Custom Regular Expressions**, **Keywords**, or **File Fingerprint**.

   \* **Identification Model**: Default provides multidimensional models such as function design scheme model, procurement contract model, cooperation agreement model, etc. You can choose one or more applicable models.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3e4b1c5092245a6af52d76d63d712d3~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Built\-in Regular Expressions:**  Default provides a variety of regular models, you can choose one or more options.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b59cc86676748fcae019bff7c36054e~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Custom Regular Expressions**: Configure your own regular expression settings. You can select or create one or more regular expressions, such as [a\-z], and press the Enter key to save them.

   \* **Keywords**: Enter your custom keywords here. You can select or create one or multiple keywords, and press the Enter key to save.

   \* **File fingerprint**: Implement custom file fingerprinting.You can select or create one or multiple file fingerprints.

   :::tip Note

   File fingerprint refers to information that can uniquely identify a digital file. File fingerprint matching protects key files in the system from being leaked by adopting a method of calculating the similarity of file fingerprints. File fingerprint is only applicable to **File content**.

   :::

   \* **File type**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac49053a32b54ed9893389f4212da47b~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area ① above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   \* As shown in the area ② above, click the dropdown box to select **Pre\-defined** or **Custom**.

   \* **Pre\-defined**: The SealSuite Admin Console includes a set of pre\-defined file types, including plain text files, formatted text, PDF documents, Office Word documents, and Office Excel spreadsheets, Office PPT PowerPoint, image files, compressed files, audio files, video files, and other file types.

   \* **Custom**: If the **Pre\-defined** file types do not meet your needs, you can specify your own file types using the format `.file suffix`. For example: `.psd`.

   As shown in the figure below, you can configure one or more **Pre\-defined** or **Custom** file types, where you need to press Enter to save when you add a **Custom** file type.

   :::tip Note

   Custom file types and some pre\-defined file types do not support parsing file content.

   :::

   \* **File size**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/754c26cee9fd4425aeae43b8f77bef5e~tplv-goo7wpa0wc-topic.webp) </span>

   It supports setting file size to be **greater than or equal to** or **less than or equal to** a specified value. The unit of file size supports **GB**, **MB**, **KB**, and **B**. For example, as shown in the figure above as default settings, it indicates the file size is greater than or equal to 100 MB.

   \* **File source**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09eec0d4b44346f9ac22df2a911c5518~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area marked ① in the figure above, you can choose one or more file sources, then use the search bar on the right to choose one or more source apps or websites.

   :::tip Note

   When you choose the option to download from custom website, you can create a new website address. Other options do not support creating new ones.

   :::

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   After successfully adding sensitive data, you can view the data in the specified category of custom sensitive data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1dc22fcd7024e2e90029290d197120e~tplv-goo7wpa0wc-topic.webp) </span>

   7. (Optional) If you choose to add **New Code Repository**, you need to complete the following configurations in the newly popped\-up **Add New Sensitive File** interface and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe694d70d294de8a767a8c169265555~tplv-goo7wpa0wc-topic.webp) </span>

   * **Name**: A custom name to identify the current sensitive file.

   * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

   * **Rules**: Click **Add New** to add rules and set the source domain of the Git code or SVN code repository. Supports the addition of multiple rules which operate based on an OR relationship.

2. **Configure audit policies**: To exempt the auditing of actions like "HR User uploading social insurance and housing fund files to specific Website", for example, when configuring the channel, exclude the upload of social insurance and housing fundURL. For further information, please refer to [Configuring block policy for file-sharing behavior](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, in the **File Transfer Control** tab, click the **Policy Management** tab.

   4. In the upper right corner of the **Policy Management** tab, click **New Policy** \> **Audit Policy**. You can choose to create a policy or choose a template to create a copy.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa1e1714912748fea666d4514223a7cc~tplv-goo7wpa0wc-topic.webp) </span>

      * Click **Create a policy**, on the **Add Audit Policy** page, complete the configuration according to the table below, and click **Confirm**.

      * Hover the mouse over a template card and click **Create a copy**, complete the suggested configuration according to the table below, and click **Confirm**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">Note         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can click <strong>Preview</strong> to understand the main Purpose and recommended configuration of this template. At the bottom of the preview page, click <strong>Use this template</strong> to create a copy of the template.         </div>
         

&nbsp;

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy name** |Custom name, used to identify the policy. |
   |**Priority** |The priority of the current policy. The value range is from 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time.<br><br>If multiple policies are enabled, the final executed policy will assessed according to priority. If there are two policies have same priority, then the policy with the latest updated time will be executed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set to view by <strong>Last modified time</strong> in the Policy Management list to see the latest updated policies.</div><br> |
   |**Source channel** |You can choose one or several from **Removable storage devices**, **Desktop Apps**, **Websites**, and **Code Repository**. The specific configuration instructions are as follows:<br><br><br>* **Removable storage devices**: It detects the behavior of users sending files to USB and portable hard disk.<br><br>* **Desktop Apps**: It detects the behavior of users sending files to Messaging Apps, Cloud Storage Apps, Mailbox, and other desktop softwares. Click on the right to **Expand**, and choose the desktop software you need to monitor. Different applications are supported by different operating systems. SealSuite supports monitoring of messaging apps, cloud storage apps, mailbox, note\-taking apps, online collaboration tools, file transfer tool, command\-line tool, remote control tool, and others.<br><br>* **Websites**: It detects user's behavior of sending data to third\-party browsers. Click on the right to **Expand**, and finish the following configuration.<br><br>   1. Check the **Browser**, click on the right to **View** **all**, and filter by the browsers you need to monitor. Different browsers are supported by different operating systems.<br><br>   2. Choose **All** or **Selected Websites**.<br><br>      This configuration is currently enabled on Mac And Windows operating systems.<br><br>      * **All**: Indicates monitoring of file\-sharing behavior on all websites within the browser.<br><br>      * **Selected Websites**: Indicates detecting file\-sharing behavior from specified websites in the browser. When choosing **Selected Websites**, the following configurations need to be performed.<br><br>         * Select specific websites provided by SealSuite.<br><br>         * If you are to select any websites outside from the pre\-defined library, click **Select Websites** on the the right side of the **Custom** area, and then add and select your desired websites through the **Select custom Website** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Websites** area, click **Select Websites**, then manually add and select the websites you want to exclude from the audit through the **Select custom Website** interface.<br><br>* **Code Repository**: It detects the user's behavior of pushing data to third\-party code repositories via Git push. Click **Expand** on the right to complete the following configurations.<br><br>   1. Select **Code Version Control Tool**, click **View all** on the right, and filter by the code version control tools you need to check.<br><br>   2. Choose **All** or **Selected Code Repository**.<br><br>      This configuration currently supports being enabled on Mac, Windows, and Linux operating systems.<br><br>      * **All**: Indicates detecting outgoing behaviors on all hosting platforms.<br><br>      * **Selected Code Repository**: Indicates detecting the outgoing behavior within a browser on the specified hosting platform. When you choose **Selected Code Repository**, you need to perform the following configuration.<br><br>         * Check the specified code repositories provided by SealSuite.<br><br>         * If the websites provided by SealSuite are not suitable, you can also click on **Select Code Repository** on the right of the **Custom** area on the right, and add and select the platform to be checked in the **Select Custom Code Repository** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Code Repository** section, click **Select** **Code Repository**, then in the **Choose Custom Code Repository** interface, manually add and select platforms to exclude from the audit.<br><br>* **Copy to Clipboard**: It detects the behavior of copying or cutting text content to the clipboard from software. If the file content contains sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **Paste from Clipboard**: It detects the behavior of pasting text content from the clipboard into an application. If the file content includes sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **File printing**: It detects whether printing sensitive files or web pages contains sensitive information. If sensitive data is found in the "File name" or "File Content" during printing, SealSuite will automatically record the behavior through an audit policy.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file printing feature is available exclusively for Windows 7 and later versions, as well as macOS 10.15 and later versions.   </div><br>    |
   


 &nbsp;

<span id="results-2"></span>
## Results

After the implementation of the data audit strategy for the HR department's compensation data, the number of non\-essential audit activities was successfully reduced, while ensuring the security of all key payroll information.

 &nbsp;

<span id="scenario-four:-document-audit-in-the-cloud"></span>
# Scenario Four: Document audit in the cloud

 &nbsp;

<span id="scenario-description-3"></span>
## Scenario description

As enterprise documents transition to the Lark platform, the demands for security and auditability of cloud\-based documents are escalating. The audit feature within Lark must guarantee that the dissemination of downloaded documents is traceable, thereby averting the leakage of sensitive information.

 &nbsp;

<span id="procedure-3"></span>
## Procedure


1. **Define sensitive data**: Documents downloaded from Lark are categorized as sensitive files, assigned a security classification of L4. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, under the **File Transfer Control** tab, click **Go to manage sensitive documents**.

   4. In the list of all data on the left, select your target custom category.

      If no custom categories exist, you need to create a new custom category. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   5. In the specified custom category, click on **Add New Sensitive File**, and choose **New Sensitive File** or **New Code Repository**:

      * For guidance on adding **New Sensitive File**, please refer to step f.

      * For guidance on adding **New Code Repository**, please refer to step g.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f6da7f3f30345dabf7f5d769b3f0274~tplv-goo7wpa0wc-topic.webp) </span>

   6. (Optional) Should you opt to add **New Sensitive File**, please complete the necessary configurations in the **Add New Sensitive File** pop\-up window on the right and click **Confirm** to proceed.

      * **Name**: A custom name to identify the current sensitive file.

      * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

      * **Rules**: Click **Add New** to configure rules in the following dimensions, with an AND relationship between multiple rules. SealSuite will subsequently match sent files based on the configured rules.

         * **File name** or **File content**

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">Note            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4"><strong>File name</strong> or <strong>File content</strong> rule configuration actions are consistent, this section takes <strong>File name</strong> as an example to introduce how to configure rules.            </div>
            

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c2e5d26737249f49d35675af7277051~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in area ① of the figure above, it supports choosing **Match any** or **Match all**.

   \* **Match any**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged if any one of those conditions is matched.

   \* **Match all**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged only if all conditions are matched.

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ③ as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   \* In the area ③ as shown above, click on the dropdown box to select from the options: **Identification Model**, **Built\-in Regular Expressions**, **Custom Regular Expressions**, **Keywords**, or **File Fingerprint**.

   \* **Identification Model**: Default provides multidimensional models such as function design scheme model, procurement contract model, cooperation agreement model, etc. You can choose one or more applicable models.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3e4b1c5092245a6af52d76d63d712d3~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Built\-in Regular Expressions:**  Default provides a variety of regular models, you can choose one or more options.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b59cc86676748fcae019bff7c36054e~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Custom Regular Expressions**: Configure your own regular expression settings. You can select or create one or more regular expressions, such as [a\-z], and press the Enter key to save them.

   \* **Keywords**: Enter your custom keywords here. You can select or create one or multiple keywords, and press the Enter key to save.

   \* **File fingerprint**: Implement custom file fingerprinting. You can select or create one or multiple file fingerprints.

   :::tip Note

   File fingerprint refers to information that can uniquely identify a digital file. File fingerprint matching protects key files in the system from being leaked by adopting a method of calculating the similarity of file fingerprints. File fingerprint is only applicable to **File content**.

   :::

   \* **File type**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac49053a32b54ed9893389f4212da47b~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area ① above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   \* As shown in the area ② above, click the dropdown box to select **Pre\-defined** or **Custom**.

   \* **Pre\-defined**: The SealSuite Admin Console includes a set of pre\-defined file types. Including plain text files, formatted text, PDF documents, Office Word documents, Office Excel spreadsheets, Office PPT PowerPoint, image files, compressed files, audio files, video files, and other file types.

   \* **Custom**:If the **Pre\-defined** file types do not meet your needs, you can specify your own file types using the format `.file suffix`. For example: `.psd`.

   As shown in the figure below, you can configure one or more **Pre\-defined** or **Custom** file types, where you need to press Enter to save when you add a **Custom** file type.

   :::tip Note

   Custom file types and some pre\-defined file types do not support parsing file content.

   :::

   \* **File size**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/754c26cee9fd4425aeae43b8f77bef5e~tplv-goo7wpa0wc-topic.webp) </span>

   It supports setting file size to be **greater than or equal to** or **less than or equal to** a specified value. The unit of file size supports **GB**, **MB**, **KB**, and **B**. For example, as shown in the figure above as default settings, it indicates the file size is greater than or equal to 100 MB.

   \* **File source**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09eec0d4b44346f9ac22df2a911c5518~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area marked ① in the figure above, you can choose one or more file sources, then use the search bar on the right to choose one or more source apps or websites.

   :::tip Note

   When you choose the option to download from a custom website, you can create a new website address. Other options do not support new creation.

   :::

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   After successfully adding sensitive data, you can view the data in the specified category of custom sensitive data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c11e57f1c714f5da5899f158b846ef2~tplv-goo7wpa0wc-topic.webp) </span>

   6. (Optional) If you choose to add **New Code Repository**, you need to complete the following configurations in the newly popped\-up **Add New Sensitive File** interface and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe694d70d294de8a767a8c169265555~tplv-goo7wpa0wc-topic.webp) </span>

   * **Name**: A custom name to identify the current sensitive file.

   * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

   * **Rules**: Click **Add New** to add rules and set the source domain of the Git code or SVN code repository. Supports the addition of multiple rules which operate based on an OR relationship.

2. **Configure audit policies**: Configure separate audit policies for each type of sensitive data to monitor all outgoing channels. For further information, please refer to [Configuring block policy for application](https://docs.byteplus.com/docs/sealsuite/Configuring_block_policy_for_application).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, in the **File Transfer Control** tab, click the **Policy Management** tab.

   4. In the upper right corner of the **Policy Management** tab, click **New Policy** \> **Audit Policy**. You can choose to create a policy or choose a template to create a copy.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa1e1714912748fea666d4514223a7cc~tplv-goo7wpa0wc-topic.webp) </span>

      * Click **Create a policy**, on the **Add Audit Policy** page, complete the configuration according to the table below, and click **Confirm**.

      * Hover the mouse over a template card and click **Create a copy**, complete the suggested configuration according to the table below, and click **Confirm**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">Note         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can click on <strong>Preview</strong> to understand the main Scope and suggested Configuration of this template, and at the bottom of the preview page, click on <strong>Use this template</strong> to create a copy of the template.         </div>
         

&nbsp;

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy name** |Custom name, used to identify the policy. |
   |**Priority** |The priority of the current policy. The value range is from 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time.<br><br>If multiple policies are enabled, the final executed policy will assessed according to priority. If there are two policies have same priority, then the policy with the latest updated time will be executed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set to view by <strong>Last modified time</strong> in the Policy Management list to see the latest updated policies.</div><br> |
   |**Source channel** |You can choose one or several from **Removable storage devices**, **Desktop Apps**, **Websites**, and **Code Repository**. The specific configuration instructions are as follows:<br><br><br>* **Removable storage devices**: It detects the behavior of users sending files to USB and portable hard diskd disk.<br><br>* **Desktop Apps**: It detects the behavior of users sending files to Messaging Apps, Cloud Storage Apps, Mailbox, and other desktop softwares. Click on the right to **Expand**, and choose the desktop software you need to monitor. Different applications are supported by different operating systems. SealSuite supports monitoring of messaging apps, cloud storage apps, mailbox, note\-taking apps, online collaboration tools, file transfer tool, command\-line tool, remote control tool, and others.<br><br>* **Websites**: It detects user's behavior of sending data to third\-party browsers. Click on the right to **Expand**, and finish the following configuration.<br><br>   1. Check the **Browser**, click on the right to **View** **all**, and filter by the browsers you need to monitor. Different browsers are supported by different operating systems.<br><br>   2. Choose **All** or **Selected Websites**.<br><br>      This configuration is currently enabled on Mac And Windows operating systems.<br><br>      * **All**: Indicates monitoring of file\-sharing behavior on all websites within the browser.<br><br>      * **Selected Websites**: Indicates detecting file\-sharing behavior from specified websites in the browser. When choosing **Selected Websites**, the following configurations need to be performed.<br><br>         * Select specific websites provided by SealSuite.<br><br>         * If you are to select any websites outside from the pre\-defined library, click **Select Websites** on the the right side of the **Custom** area, and then add and select your desired websites through the **Select custom Website** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Websites** area, click **Select Websites**, then manually add and select the websites you want to exclude from the audit through the **Select custom Website** interface.<br><br>* **Code Repository**: It detects the user's behavior of pushing data to third\-party code repositories via Git push. Click **Expand** on the right to complete the following configurations.<br><br>   1. Select **Code Version Control Tool**, click **View all** on the right, and filter by the code version control tools you need to check.<br><br>   2. Choose **All** or **Selected Code Repository**.<br><br>      This configuration currently supports being enabled on Mac, Windows, and Linux operating systems.<br><br>      * **All**: Indicates detecting outgoing behaviors on all hosting platforms.<br><br>      * **Selected Code Repository**: Indicates detecting the outgoing behavior within a browser on the specified hosting platform. When you choose **Selected Code Repository**, you need to perform the following configuration.<br><br>         * Check the specified code repositories provided by SealSuite.<br><br>         * If the websites provided by SealSuite are not suitable, you can also click on **Select Code Repository** on the right of the **Custom** area on the right, and add and select the platform to be checked in the **Select Custom Code Repository** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Code Repository** section, click **Select** **Code Repository**, then in the **Choose Custom Code Repository** interface, manually add and select platforms to exclude from the audit.<br><br>* **Copy to Clipboard**: It detects the behavior of copying or cutting text content to the clipboard from software. If the file content contains sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **Paste from Clipboard**: It detects the behavior of pasting text content from the clipboard into an application. If the file content includes sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **File printing**: It detects whether printing sensitive files or web pages contains sensitive information. If sensitive data is found in the "File name" or "File Content" during printing, SealSuite will automatically record the behavior through an audit policy.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file printing feature is available exclusively for Windows 7 and later versions, as well as macOS 10.15 and later versions.   </div><br>    |
   |**Outgoing Content** |Click on **Add New Sensitive File**, and in the **Add New Sensitive File** interface, Choose **Predefined templates** or **Custom sensitive files**. In the **Add New Sensitive File** interface, the following operations are supported:<br><br><br>* Supports selecting multiple sensitive data classification checkboxes in the left navigation bar, and upon selecting, all sensitive data within that category will be included.<br><br>* Within a specified sensitive data classification, supports choosing one or more specified sensitive data.<br><br>* Every sensitive data entry supports a **Preview**, through which you can view the specific configuration of that sensitive data. For instance, previewing large images, you can see that large images refer to image files greater than or equal to 20 MB.<br><br>* Predefined sensitive data supports **Create** **a copy**, which can only be saved to the **Custom sensitive files** category, where you can modify the category's name, data classification, and rules as needed.<br><br>* The custom sensitive data supports **Edit**, and you can adjust the content of custom sensitive data according to actual needs.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a custom sensitive data item has been referenced by an audit policy, then when that custom sensitive data is edited, the corresponding sensitive data within the policy will also be updated synchronously.   </div><br>   <br><br>After adding sensitive data, you can view the name and data classification. Additionally, you can click **View** in the **Actions** column to inspect the specific configurations or click **Remove** to delete sensitive data that is no longer required. |
   |**Action** |The default is **Generate alert**, and additionally, you can choose one or more of the options. You can also choose **Take screenshot** and **File archive** according to actual needs.<br><br><br>* **Generate alert**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the alarm information will be uploaded by the SealSuite client to the SealSuite Admin Console.<br><br>* **Take screenshot**: You can choose one or more from **Windows**, **macOS**, and **Linux**. When a data breach incident occurs on a user's terminal within the workflow scope, the SealSuite client will take screenshot and upload it to the SealSuite Admin Console. The taken screenshot can be viewed in the specified user's **Risky Actions** and **Sent File Details**.<br><br>* **File archive**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the SealSuite client will save the leaked file and upload it to the SealSuite Admin Console. The file archive can be viewed within the designated user's **Risky Actions**. |
   |**Scope** |Supports restricting effective scope based on either **User** or **Device** dimensions.<br><br><br>* When choosing a **User**, you need to limit the scope through the **Department** or **Role** group.<br><br>* When choosing **Device**, you need to limit the scope through the **Device**, **OS**, **Group**. |
   


 &nbsp;

<span id="results-3"></span>
## Results

The implementation of the cloud document audit policy has decreased the frequency of sensitive documents being sent from the Lark platform, thereby increasing the opacity and controllability of document circulation.

 &nbsp;

<span id="scenario-five:-audit-operational-efficiency-improvement"></span>
# Scenario Five: Audit operational efficiency improvement

 &nbsp;

<span id="scenario-description-4"></span>
## Scenario description

In order to alleviate the audit workload for the operations team without compromising endpoint performance, the outbound audit of internal company documents is exempted under certain conditions. The outbound operations from Lark tenants and intranet websites are throttled by the DLP Policy Management to streamline the audit process.

 &nbsp;

<span id="procedure-4"></span>
## Procedure


1. **Define sensitive data**: When the administrator is defining sensitive documents, configurations should be differentiated based on file size; small files should be configured for detecting sensitive content, while large files should be configured for monitoring file size. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, under the **File Transfer Control** tab, click **Go to manage sensitive documents**.

   4. In the list of all data on the left, select your target custom category.

      If no custom categories exist, you need to create a new custom category. For further information, please refer to [Managing sensitive data](https://docs.byteplus.com/docs/sealsuite/docs-managing-sensitive-data).

   5. In the specified custom category, click on **Add New Sensitive File**, and choose **New Sensitive File** or **New Code Repository**:

      * For guidance on adding **New Sensitive File**, please refer to step f.

      * For guidance on adding **New Code Repository**, please refer to step g.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f6da7f3f30345dabf7f5d769b3f0274~tplv-goo7wpa0wc-topic.webp) </span>

   6. (Optional) Should you opt to add **New Sensitive File**, please complete the necessary configurations in the **Add New Sensitive File** pop\-up window on the right and click **Confirm** to proceed.

      * **Name**: A custom name to identify the current sensitive file.

      * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

      * **Rules**: Click **Add New** to configure rules in the following dimensions, with an AND relationship between multiple rules. SealSuite will subsequently match sent files based on the configured rules.

         * **File name** or **File content**.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">Note            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4"><strong>File name</strong> or <strong>File content</strong> rule configuration actions are consistent, this section takes <strong>File name</strong> as an example to introduce how to configure rules.            </div>
            

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c2e5d26737249f49d35675af7277051~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in area ① of the figure above, it supports choosing **Match any** or **Match all**.

   \* **Match any**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged if any one of those conditions is matched.

   \* **Match all**: When you have configured multiple conditions in the area ③ as shown above, a sensitive file will be flagged only if all conditions are matched.

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ③ as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   \* In the area ③ as shown above, click on the dropdown box to select from the options: **Identification Model**, **Built\-in Regular Expressions**, **Custom Regular Expressions**, **Keywords**, or **File Fingerprint**.

   \* **Identification Model**: Default provides multidimensional models such as function design scheme model, procurement contract model, cooperation agreement model, etc. You can choose one or more applicable models.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3e4b1c5092245a6af52d76d63d712d3~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Built\-in Regular Expressions:**  Default provides a variety of regular models, you can choose one or more options.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b59cc86676748fcae019bff7c36054e~tplv-goo7wpa0wc-topic.webp) </span>

   \* **Custom Regular Expressions**: Configure your own regular expression settings. You can select or create one or more regular expressions, such as [a\-z], and press the Enter key to save them.

   \* **Keywords**: Enter your custom keywords here. You can select or create one or multiple keywords, and press the Enter key to save.

   \* **File fingerprint**: Implement custom file fingerprinting. You can select or create one or multiple file fingerprints.

   :::tip Note

   File fingerprint refers to information that can uniquely identify a digital file. File fingerprint matching protects key files in the system from being leaked by adopting a method of calculating the similarity of file fingerprints. File fingerprint is only applicable to **File content**.

   :::

   \* **File type**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac49053a32b54ed9893389f4212da47b~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area ① above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   \* As shown in the area ② above, click the dropdown box to select **Pre\-defined** or **Custom**.

   \* **Pre\-defined**: The SealSuite Admin Console includes a set of pre\-defined file types. Including plain text files, formatted text, PDF documents, Office Word documents, Office Excel spreadsheets, Office PPT PowerPoint, image files, compressed files, audio files, video files, and other file types.

   \* **Custom**: If the **Pre\-defined** file types do not meet your needs, you can specify your own file types using the format `.file suffix`. For example: `.psd`.

   As shown in the figure below, you can configure one or more **Pre\-defined** or **Custom** file types, where you need to press Enter to save when you add a **Custom** file type.

   :::tip Note

   Custom file types and some pre\-defined file types do not support parsing file content.

   :::

   \* **File size**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/754c26cee9fd4425aeae43b8f77bef5e~tplv-goo7wpa0wc-topic.webp) </span>

   It supports setting file size to be **greater than or equal to** or **less than or equal to** a specified value. The Unit of file size supports **GB**, **MB**, **KB**, and **B**. For example, as shown in the figure above as default settings, it indicates the file size is greater than or equal to 100 MB.

   \* **File source**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09eec0d4b44346f9ac22df2a911c5518~tplv-goo7wpa0wc-topic.webp) </span>

   \* As shown in the area marked ① in the figure above, you can choose one or more file sources, then use the search bar on the right to choose one or more source apps or websites.

   :::tip Note

   When you choose the option to download from a custom website, you can create a new website address. Other options do not support new creation.

   :::

   \* In the area ② as shown above, it supports **Copy content** or **Delete**.

   \* **Copy content**: Click to copy the conditions configured in the area ② as shown above. You can then paste them into additional rules.

   \* **Delete**: If you no longer need the configured policies, you can click **Delete**.

   After successfully adding sensitive data, you can view the data in the specified category of custom sensitive data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8abab3d1691d46fc9cf54100b3a68005~tplv-goo7wpa0wc-topic.webp) </span>

   6. (Optional) If you choose to add **New Code Repository**, you need to complete the following configurations in the newly popped\-up **Add New Sensitive File** interface and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe694d70d294de8a767a8c169265555~tplv-goo7wpa0wc-topic.webp) </span>

   * **Name**: A custom name to identify the current sensitive file.

   * **Data classification**: Supports setting **Public** (L1), **Internal** (L2), **Confidential** (L3), **Restricted** (L4). You need to set the data classification level based on the sensitivity of the current data.

   * **Rules**: Click **Add New** to add rules and set the source domain of the Git code or SVN code repository. Supports the addition of multiple rules which operate based on an OR relationship.

2. **Configure audit policies**: Exclude the audit of the company's Lark tenant and company intranet websites when configuring the detection policy for various files. For further information, please refer to [Configuring block policy for file-sharing behavior](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule).

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **DLP** \> **Policy Management**.

   3. On the **Policy Management** page, in the **File Transfer Control** tab, click the **Policy Management** tab.

   4. In the upper right corner of the **Policy Management** tab, click **New Policy** \> **Audit Policy**. You can choose to create a policy or choose a template to create a copy.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa1e1714912748fea666d4514223a7cc~tplv-goo7wpa0wc-topic.webp) </span>

      * Click **Create a policy**, on the **Add Audit Policy** page, complete the configuration according to the table below, and click **Confirm**.

      * Hover the mouse over a template card and click **Create a copy**, complete the suggested configuration according to the table below, and click **Confirm**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">Note         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can click <strong>Preview</strong> to understand the main purpose and recommended configuration of the template, at the bottom of the preview page, click <strong>Use this template</strong> to create a template copy.         </div>
         

&nbsp;

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy name** |Custom name, used to identify the policy. |
   |**Priority** |The priority of the current policy. The value range is from 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time.<br><br>If multiple policies are enabled, the final executed policy will assessed according to priority. If there are two policies have same priority, then the policy with the latest updated time will be executed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set to view by <strong>Last modified time</strong> in the Policy Management list to see the latest updated policies.</div><br> |
   |**Source channel** |You can choose one or several from **Removable storage devices**, **Desktop Apps**, **Websites**, and **Code Repository**. The specific configuration instructions are as follows:<br><br><br>* **Removable storage devices**: It detects the behavior of users sending files to USB and portable hard disk.<br><br>* **Desktop Apps**: It detects the behavior of users sending files to Messaging Apps, Cloud Storage Apps, Mailbox, and other desktop softwares. Click on the right to **Expand**, and choose the desktop software you need to monitor. Different applications are supported by different operating systems. SealSuite supports monitoring of messaging apps, cloud storage apps, mailbox, note\-taking apps, online collaboration tools, file transfer tool, command\-line tool, remote control tool, and others.<br><br>* **Websites**: It detects user's behavior of sending data to third\-party browsers. Click on the right to **Expand**, and finish the following configuration.<br><br>   1. Check the **Browser**, click on the right to **View all**, and filter by the browsers you need to monitor. Different browsers support different operating systems.<br><br>   2. Choose **All** or **Selected Websites**.<br><br>      This configuration is currently enabled on Mac And Windows operating systems.<br><br>      * **All**: Indicates monitoring of file\-sharing behavior on all websites within the browser.<br><br>      * **Selected Websites**: Indicates detecting file\-sharing behavior from specified websites in the browser. When choosing **Selected Websites**, the following configurations need to be performed.<br><br>         * Select specific websites provided by SealSuite.<br><br>         * If you are to select any websites outside from the pre\-defined library, click **Select Websites** on the the right side of the **Custom** area, and then add and select your desired websites through the **Select custom Website** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Websites** area, click **Select Websites**, then manually add and select the websites you want to exclude from the audit through the **Select custom Website** interface.<br><br>* **Code Repository**: It detects the user's behavior of pushing data to third\-party code repositories via Git push. Click **Expand** on the right to complete the following configurations.<br><br>   1. Select **Code Version Control Tool**, click **View all** on the right, and filter by the code version control tools you need to check.<br><br>   2. Choose **All** or **Selected Code Repository**.<br><br>      This configuration currently supports being enabled on Mac, Windows, and Linux operating systems.<br><br>      * **All**: Indicates detecting outgoing behaviors on all hosting platforms.<br><br>      * **Selected Code Repository**: Indicates detecting the outgoing behavior within a browser on the specified hosting platform. When you choose **Selected Code Repository**, you need to perform the following configuration.<br><br>         * Check the specified code repositories provided by SealSuite.<br><br>         * If the websites provided by SealSuite are not suitable, you can also click on **Select Code Repository** on the right of the **Custom** area on the right, and add and select the platform to be checked in the **Select Custom Code Repository** interface.<br><br>   3. (Optional) On the right side of the **Out\-of\-Scope Code Repository** section, click **Select** **Code Repository**, then in the **Choose Custom Code Repository** interface, manually add and select platforms to exclude from the audit.<br><br>* **Copy to Clipboard**: It detects the behavior of copying or cutting text content to the clipboard from software. If the file content contains sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **Paste from Clipboard**: It detects the behavior of pasting text content from the clipboard into an application. If the file content includes sensitive data, SealSuite will perform an audit. Click **Expand** on the right to choose the software or website you need to monitor.<br><br>* **File printing**: It detects whether printing sensitive files or web pages contains sensitive information. If sensitive data is found in the "File name" or "File Content" during printing, SealSuite will automatically record the behavior through an audit policy.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file printing feature is available exclusively for Windows 7 and later versions, as well as macOS 10.15 and later versions.   </div><br>    |
   |**Outgoing Content** |Click on **Add New Sensitive File**, and in the **Add New Sensitive File** interface, Choose **Predefined templates** or **Custom sensitive files**. In the **Add New Sensitive File** interface, the following operations are supported:<br><br><br>* Supports selecting multiple sensitive data classification checkboxes in the left navigation bar, and upon selecting, all sensitive data within that category will be included.<br><br>* Within a specified sensitive data classification, supports choosing one or more specified sensitive data.<br><br>* Every sensitive data entry supports a **Preview**, through which you can view the specific configuration of that sensitive data. For instance, previewing large images, you can see that large images refer to image files greater than or equal to 20 MB.<br><br>* Predefined sensitive data supports **Create** **a copy**, which can only be saved to the **Custom sensitive files** category, where you can modify the category's name, data classification, and rules as needed.<br><br>* The custom sensitive data supports **Edit**, and you can adjust the content of custom sensitive data according to actual needs.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a custom sensitive data item has been referenced by an audit policy, then when that custom sensitive data is edited, the corresponding sensitive data within the policy will also be updated synchronously.   </div><br>   <br><br>After adding sensitive data, you can view the name and data classification. Additionally, you can click **View** in the **Actions** column to inspect the specific configurations or click **Remove** to delete sensitive data that is no longer required. |
   |**Action** |The default is **Generate alert**, and additionally, you can choose one or more of the options. You can also choose **Take screenshot** and **File archive** according to actual needs.<br><br><br>* **Generate alert**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the alarm information will be uploaded by the SealSuite client to the SealSuite Admin Console.<br><br>* **Take screenshot**: You can choose one or more from **Windows**, **macOS**, and **Linux**. When a data breach incident occurs on a user's terminal within the workflow scope, the SealSuite client will take screenshot and upload it to the SealSuite Admin Console. The taken screenshot can be viewed in the specified user's **Risky Actions** and **Sent File Details**.<br><br>* **File archive**: When an incident of data breach occurs on a user's terminal within the effective scope of the rule, the SealSuite client will save the leaked file and upload it to the SealSuite Admin Console. The file archive can be viewed within the designated user's **Risky Actions**. |
   |**Scope** |Supports restricting effective scope based on either **User** or **Device** dimensions.<br><br><br>* When choosing a **User**, you need to limit the scope through the **Department** or **Role** group.<br><br>* When choosing **Device**, you need to limit the scope through the **Device**, **OS**, **Group**. |
   


 &nbsp;

<span id="results-4"></span>
## Results

The optimized audit policy has alleviated the workload of the operations team's audit tasks, while preserving the security of corporate data and the stability of endpoint performance.
