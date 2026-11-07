---
title: "Managing the File Source Library"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-the-file-source-library"
---

The File Source Library is a centralized resource center for managing the channels through which files are generated. It aggregates various data origins—including corporate office applications, websites, and code repositories. By identifying where a file comes from, administrators can implement highly targeted data loss prevention (DLP) controls.

With this module, you can achieve the following objectives:


* **Source Traceability and Automated Grading**: Automatically determine a file's sensitivity level based on its origin (e.g., downloaded from an internal CRM or OA portal) without needing to parse the actual content.

* **Closed\-Loop Protection for Core Assets**: Bring internal code hosting platforms (e.g., GitLab, SVN) or proprietary business platforms under management, ensuring files from these high\-security sources remain controlled on the endpoint.

* **Flexible Business Boundary Expansion**: Manually add internal business URLs or code repository server addresses unique to your organization to ensure DLP rules cover all business scenarios.


<span id="0e543d11"></span>
## Use Cases

The File Source Library is designed for identification scenarios based on data generation channels. You should configure this library if you need to:


* **Protect Specific Business Data**: Audit all files downloaded from "Corporate Cloud Drives" or "Financial Reporting Systems" by adding their respective web origins.

* **Control Code and Development Assets**: Monitor the flow of files downloaded from internal repositories like Git, SVN, or Perforce (P4).

* **Monitor internal shared file circulation**: Configure the network identifiers (domain names or IPs) of intranet file servers to track files downloaded to local endpoints.

* **Inherit Feishu/Lark document confidentiality levels**: Configure Feishu as a source and use the SealSuite browser security plugin to intercept downloads and inherit labels. This ensures Feishu/Lark cloud documents downloaded to an employee's local computer retain their original confidentiality levels without requiring SealSuite to rescan the content.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Resources in this library apply only to <strong>File Source</strong> identification scenarios. Ensure you select the correct criteria when creating classification and grading rules.</div>


2. <div data-tips="true" data-tips-type="tip">Source identification relies on the SealSuite client's real\-time monitoring of processes and download behaviors. Ensure your endpoints are running a supported client version.</div>



<span id="df58ae4b"></span>
## Prerequisites

The administrator must have the following permissions. See [Configuring Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-adding-administrator_1) for details.


* **Menu Permissions**: **Security** \> **DLP** \> **Data Identification** \> **File Source Library**.

* **Operation Permissions**: **DLP** \> **Data Identification Related Permissions**.


<span id="cdfc38be"></span>
## Navigation Path


1. Log in to the Admin Console.

2. In the left navigation bar, choose **DLP** \> **Data Identification**.

3. Click the **File Source Library** tab at the top of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52979c8bb5944e9b91169e14189a74d4~tplv-goo7wpa0wc-image.image) </span>


<span id="10d8ff32"></span>
## Adding Custom File Sources

If your internal proprietary systems (e.g., OA, CRM), private code repositories, or specific production software are not in the built\-in library, you can add them manually.

**Recommendation**: SealSuite includes many built\-in sources for mainstream office apps and cloud drives. Before adding a custom one, search for it using the **Source name** filter at the top of the page.


1. On the **File Source Library** page, click  **+ Add File Source**.

2. Select a **Source Type** and configure the parameters:


<span id="6a6e3c56"></span>
### **Web Application**

Used for business systems accessed via browsers. Once configured, files downloaded or exported from these sites are tagged with this source. This configuration supports **manual addition** and **batch import**.

<span id="18051f0e"></span>
#### Manually Add a Source


1. In the **Add file source** window, select **Web application** as the source type and complete the following configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9875ec88384e40a694fa70c3c3cccd7c~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Item** |**Description and Business Logic** |**Configuration Suggestions and Examples** |
   |---|---|---|
   |**Source Name** |Customize an easily identifiable name. |You are advised to name it by business, such as "Core CRM System" or "Financial Report Portal". |
   |**Address Type** |Select the Web website address type to add as needed. The supported options are **URL**, **IP**, and **Domain**. |*  |
   |**Address Information** |Complete the address information based on the selected address type.<br><br><br>* **URL**<br><br>   * **Include match**: If the website URL contains the string entered here, the system determines that the file comes from this source.<br><br>   * **Regular match**: Enter a regular expression for precise matching.<br><br>* **IP**<br><br>   * **Single IP**: Enter an exact IP address for matching, such as `192.168.1.1`.<br><br>   * **CIDR block**: Enter a CIDR block address, such as `192.168.1.0/24`. All IP addresses in this CIDR block are considered file sources.<br><br>   * **IP range**: Enter a continuous IP address range connected by a hyphen, such as `192.168.1.10-192.168.1.50`. The system treats all IP addresses in this range as file sources.<br><br>* **Domain**<br><br>   * **Exact domain**: Only the complete domain entered here is matched as a file source.<br><br>   * **Wildcard domain**: Use a wildcard to match all subdomains under a primary domain as file sources.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>IP</strong> and <strong>Domain</strong> rules take effect only on SealSuite clients of version <strong>3.3.16 or later</strong>. If the client version is earlier than 3.3.16, such rules cannot be adapted, and the corresponding control policy does not take effect.</div><br> |* **Include match** is suitable for whole\-site control: For example, if you enter `crm.example.com`, files generated from all subpages under this domain, such as `/download` and `/index`, are marked as from the "CRM source". This is suitable for most standard business systems.<br><br>* **Regular** **match** is suitable for fine\-grained control: For example, if you only want to mark files under a specific path, enter `^https://hr\.com/salary/.*\.xlsx$`. The system marks only Excel files in the salary path under the HR domain, while allowing other ordinary web pages.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>1. <div data-tips="true" data-tips-type="warning"><strong>Regular syntax restrictions</strong>: The system does not currently support the following complex rules:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Assertions: <code>(?=</code>, <code>(?<=</code>, <code>(?!</code>, <code>(?<!</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Escape and reset classes: <code>\C</code>, <code>\R</code>, <code>\K</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Backreferences: <code>\number</code>, such as <code>\1</code></div><br><br><br>2. <div data-tips="true" data-tips-type="warning">Ensure that the syntax is standard. Incorrect regular logic may cause source identification to fail.</div><br> |
   |**Website Title** |**Optional** when the address type is **URL**. This field helps identify the website. If both Website URL and Website Title are configured, both must be matched before the file source is reported. Configure this field as needed. |When the website URL is not sufficiently distinguishable, such as when multiple systems share the same intranet IP address or domain, you are advised to configure this item. For example, set URL to `10.1.2.3` and Website Title to "Human Resource Management System" to improve identification accuracy. |
   

2. Click **Confirm** to complete the addition.


<span id="098971de"></span>
#### Batch Import


1. On the **File Source Library** list page, click **Batch import web applications** in the upper\-right corner of the list.

2. Click **Download** to obtain the **Data recognition \- File source \- Web application batch import template**, and fill in address records according to the template requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4adb50e1fd36486eb3036c5b66bd1421~tplv-goo7wpa0wc-image.image) </span>

3. After completing the template, click **Upload** or directly drag the completed file to import it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file size must be no larger than <strong>2 MB</strong>, and up to <strong>1,000 records</strong> can be imported at a time.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the file is uploaded, the system automatically validates whether the table content meets the requirements. If validation fails, modify the template content based on the error message and <strong>upload it again</strong>.   </div>
   

4. Click **Confirm** to complete the import.


<span id="3f889f20"></span>
### **Code Repository**

Used for platforms like Git, SVN, and Perforce (P4).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/521917e97bb7425dab2cb165a96aeb97~tplv-goo7wpa0wc-image.image) </span>


|**Setting** |**Description & Logic** |**Best Practices & Examples** |
|---|---|---|
|**Source name** |A clear identifier for the source. |e.g., "R&D GitLab" or "Proprietary SVN Repo." |
|**Repository domain or address** |The domain, IP, or connection string. |* **Git/SVN**: Enter the domain or IP, e.g., `git.example.com`.<br><br>* **P4**: Enter the address and port in the `IP:PORT` format, e.g., `10.0.0.1:1666`. |


<span id="9f5d80cd"></span>
### **File server**

This type applies to shared folders or file transfer servers (such as NAS or shared drives) on the enterprise intranet. Files downloaded or copied from these network paths using the OS file explorer (or Finder) receive this source tag.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c115a9d4b7e437ba489ed97351385c9~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Prerequisites</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>Supported protocols</strong>:</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Windows</strong>: Intercepts file transfers via FTP and SMB.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>macOS</strong>: Intercepts file transfers via AFP, NFS, WebDAV, FTP, and SMB.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Version requirements</strong>: Requires SealSuite client version <strong>3.3.13</strong> or later.</div>




|**Configuration item** |**Description and business logic** |**Configuration suggestions and examples** |
|---|---|---|
|**File source name** |A custom, easily identifiable name. |Name the source based on its business function or department, such as "Design Department Public Material Drive" or "R&D Department FTP Server". |
|**File source type** |The network identification method for the file server. Select **Domain name** or **IP**, and enter the address. |Select the type based on how employees mount the shared drive.<br><br><br>* **Domain name**: Enter the main domain (e.g., `example.com`) or a wildcard domain (e.g., `*.example.com`).<br><br>* **IP**: Enter a single IP (e.g., `192.168.1.10`), a CIDR block (e.g., `192.168.1.0/24`), or an IP range (e.g., `192.168.1.10-192.168.1.50`). |
|**Source path** |The specific shared directory path on the file server. |Supports the `*` wildcard. Enter a detailed path to control a specific directory rather than the entire drive. |


<span id="e5ea4e94"></span>
### **Feishu/Lark cloud documents**

Use the SealSuite browser security plugin to deeply control browser behaviors. This automatically identifies and inherits original confidentiality levels when users download Feishu/Lark cloud documents.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60311b3f92e2460eab2d894580376e8c~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Prerequisites</strong></div>



* <div data-tips="true" data-tips-type="tip"><strong>Environment requirements</strong>: The extension supports Chrome and Edge on Windows 10+ and macOS 11+.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Version requirements</strong>: Requires SealSuite client version 3.3.12 or later.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Prerequisite configuration</strong>: To enable this capability, go to <strong>DLP</strong> \> <strong>Strategy Center</strong> \> <strong>System Configuration</strong> and enable <strong>Browser plug\-in</strong>. The plugin runs silently in the background.</div>




|**Configuration item** |**Description and business logic** |**Configuration suggestions and examples** |
|---|---|---|
|**Source name** |(Required) A custom, easily identifiable name. |Name the source based on its business function, such as "Group Core Feishu/Lark Cloud Documents". |
|**Match type** |The mapping between enterprise domain names and document confidentiality levels. Click  **+ Add** to configure multiple rule sets. |We recommend creating separate match types for domains with different confidentiality requirements. |
|**Enterprise domain name** |(Required) The enterprise domain name for the Feishu/Lark cloud documents. |Enter the enterprise's exclusive Feishu/Lark domain name to identify downloads from that domain. |
|**Document confidentiality level** |(Required) The corresponding Feishu/Lark document confidentiality level for the domain. Click  **+ Create classification** in the drop\-down list to add a new level. |The system matches based on this level. Inheritance triggers only if the file originates from the specified domain and its Feishu/Lark confidentiality level matches this setting. |


**Working principle and control effects**:

After mapping the Feishu/Lark domain and confidentiality level here, go to **Classification and grading rules** to create a rule with the "File/Lark source" dimension that references this source. When the **Document outgoing control policy** in the Policy center references this rule, you gain efficient control over the download, local storage, and secondary outbound transfer of highly confidential Feishu documents.


* **Working principle**: When an employee downloads a file from the configured `Enterprise domain name`, the SealSuite browser plugin silently identifies the download and reads the document's confidentiality level in Feishu. If the level matches the `Document confidentiality level` configured here, SealSuite inherits it directly instead of rescanning the file.

* **Control effect**: Even if an employee renames the file or it contains an unscannable image, SealSuite reads the inherited confidentiality label during any subsequent outbound transfer attempts via controlled channels. This triggers the alarm or block actions configured in the Policy center, ensuring consistent protection from the cloud to the local endpoint.

5. Click **Confirm**.


<span id="0a1e2c7d"></span>
## Viewing and Managing the File Source List

You can search and manage all existing sources from the list page.


|**Field** |**Description** |
|---|---|
|**Source name** |The identifier for the file source. |
|**Source type** |The category of the source. |
|**Minimum client version** |The minimum SealSuite version required for the identification logic. Ensure endpoints are updated to at least this version to guarantee accurate tagging. |
|**Supported OS** |Supported platforms: Windows, macOS, and Linux. |
|**Creation type** |* **Pre\-defined**: Pre\-defined by SealSuite.<br><br>* **Custom**: Manually added by an administrator. |
|**Action** |* **Pre\-defined Sources**: Cannot be viewed, edited, or deleted.<br><br>* **Custom Sources**: Support full lifecycle management.<br><br><br>*Note: Sources referenced by a classification and grading rule cannot be deleted until the association is removed.*  |


<span id="8889faa9"></span>
## Next Steps

After configuring the File Source Library, you must link the sources to a **Classification and Grading Rule**. Refer to [Managing classification and grading rules](https://docs.byteplus.com/docs/sealsuite/managing-classification-and-grading-rules) for details on using "File Source" as a detection criterion to enable targeted auditing or blocking.
