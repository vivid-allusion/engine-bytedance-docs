---
title: "Channel lookup and custom configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/channel-lookup-and-custom-configuration"
---

SealSuite DLP provides a **Channel list** that serves as a unified entry point for viewing and querying channel capabilities. Through this feature, administrators can:


* View a centralized list of all outbound channels that SealSuite supports for control.

* Drill down into each channel to see its security control capabilities across different operating systems — including outbound file audit, outbound file blocking, channel blocking, and internal address configuration — along with the minimum client version required.

* Create custom channels to fill gaps not covered by built\-in channels, tailored to your enterprise's business needs.


<span id="0f0772a8"></span>
# View the channel list

Log in to the Admin Console and navigate to **DLP** \> **Strategy Center** \> **Channel list** to view all supported channels and their capability overview.

The left side of the page provides a category directory tree, and the right side displays the corresponding channel list. Click a category on the left to filter quickly, or enter a channel name in the search box for a fuzzy search. The number next to each category in the directory tree indicates the total number of channels in that category (both built\-in and custom).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf55388524b64931be8649911e6454ba~tplv-goo7wpa0wc-image.image) </span>

<span id="1fcca1ce"></span>
## Desktop applications & Websites

In the **Update Version** filter above the list, you can select a client version to quickly view the channel capability changes in that version, including newly added control channels and the coverage of newly added control capabilities. Click **Details** in the **Action** column to further view the control policies supported by the channel.

Click **Export List** in the upper\-right corner of the list, you can export the desktop application and Web website channel lists for offline management.


|**Field** |**Description** |
|---|---|
|**Channel name** |Displays the channel's icon and name (for example, Feishu, WeCom, Baidu Netdisk). |
|**Channel type** |The category the channel belongs to, corresponding to the categories in the left directory tree. |
|**URL**<br><br>(Websites only) |The URL address of the website channel. |
|**Creation category** |Indicates whether the channel is **Pre\-defined** or **Custom**. |
|**Number of app rules** |The number of policies currently referencing this channel. Hover over the number to see the policy types and counts. Click the number to jump directly to the corresponding policy page, filtered to show only policies that reference this channel. |
|**Update Version** |Displays the client version corresponding to the latest update of the channel capability. |
|**Supported OS** |The operating systems supported by this channel's capabilities. |
|**Action** |Click **Details** to view the channel's control capability details. For custom channels, you can also **Edit** or **Delete**. |


<span id="79b7ef1e"></span>
## Computer peripherals

On the **Computer peripherals** tab, supported peripheral channels are displayed as cards. Currently, two types are available: **Storage peripherals** and **Printers**. Each card shows the current **Applied policies** count and **Supported OS** for that peripheral channel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f77db1e6d7744260a4f888c2c35d390d~tplv-goo7wpa0wc-image.image) </span>

<span id="8db6e347"></span>
# View channel capability details

In the channel list, click **Details** in the Action column to open the details page and review the channel's specific capability matrix.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e361d2aa1a0f458693d90515ec098a84~tplv-goo7wpa0wc-image.image) </span>


* **Basic information**

   Displays the channel name, channel type, and creation type (built\-in/custom).

* **Control policy support**

   Provides a detailed table of security control capabilities supported by the channel across different operating systems (Windows, macOS, and Linux), along with the minimum required client version. Depending on the channel type (Desktop application or Websites), the capability items include:

   * **File sending audit**: Records file outbound activities through this channel.

   * **File sending blocking**: Intercepts unauthorized file outbound through this channel.

   * **Channel blocking**: Directly blocks the use of the desktop application.

   * **Internet address**: Configures internal address whitelists for the desktop application (e.g., excluding specific tenants or internal domains).

   * **Text Audit/Block**: Audits and intercepts interactive text sent via web pages. To control web\-based text transfers (e.g., preventing code snippets from being pasted into ChatGPT), you must first enable the **Browser Plugin** in **System Configuration**. For more information, see [Browser plug-in control configuration](https://docs.byteplus.com/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies#645581b7).


<span id="c4e3b7cd"></span>
# Manage custom channels

If the built\-in channels do not meet your control requirements, you can add custom channels.

<span id="954a297d"></span>
## Add a custom channel

<span id="f6f9639d"></span>
### Add a custom desktop application


1. On the **Channel list** page, switch to the **Desktop application** tab.

2. Click  **+ Custom channel** in the upper\-right corner of the list.

3. In the **Add New Application** dialog box, complete the following configuration and click **Confirm** to save.

   * **General**

      * **Name**: Enter the application name. Supports Chinese, English, special characters, and spaces, up to 64 characters.

      * **Application icon**: Upload an identifiable icon for the software. Maximum size: 500 KB. A 1:1 aspect ratio is recommended to prevent distortion.

   * **Custom Application Configuration**

      * **Category**: Select the software category from the drop\-down list.

      * **OS**: Custom desktop applications only support control on Windows or macOS. You can select Windows, macOS, or both. Based on your selection, provide the identification information for the software.

         * **Windows**: Enter the **Process name** (required) and **Process signature** (optional). You can add up to 10 processes. For details, see [Customizing Windows process configuration](https://docs.byteplus.com/docs/sealsuite/customizing-windows-process-configuration).

         * **macOS**: Enter the **Signing ID**. A Signing ID consists of a certificate and private key generated from a developer account, used to sign macOS applications. You can add up to 10 Signing IDs. For details, see [Customizing macOS process configuration](https://docs.byteplus.com/docs/sealsuite/customizing-macOS-process-configuration).

      * **Functional application range**: Select the security capabilities this custom channel supports, including **Outbound file audit**, **File\-level blocking**, and **Channel blocking**.


<span id="3774821c"></span>
### Add a custom website

On the **Channel list** page, switch to the **Websites** tab. You can **manually add** or **batch import** custom Web website channels.

<span id="b1ae74da"></span>
#### Manually Add a Channel


1. Click  **+ Custom channel** in the upper\-right corner of the list.

2. In the **Custom Channel** dialog box, complete the following configuration and click **Confirm** to save.

   * **General**

      * **Channel name**: Enter the website name. Supports Chinese, English, special characters, and spaces, up to 64 characters.

      * **Channel type**: Select the website category from the drop\-down list.

      * **Manage labels**: Associate the current website resource with specific tags (optional). The drop\-down list only displays tags that the current administrator has been granted. By associating tags, you can enforce policy and resource management permission isolation between administrators of different regions or business lines. To add or adjust the visible tag options in the drop\-down list, a super administrator must modify the **Managed tag scope** for your administrator role under **Settings** \> **Admin Access**.

      * **Channel icon**: Upload an identifiable icon for the website. Maximum size: 500 KB. A 1:1 aspect ratio is recommended to prevent distortion.

   * **Website configuration**

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Address Type** |Select the Web website address type to add as needed. The supported options are **URL**, **IP**, and **Domain**. |
      |**Address Information** |Complete the address information based on the selected address type.<br><br><br>* **URL**<br><br>   * **Include match**: If the website URL contains the string entered here, it is considered a target controlled website.<br><br>   * **Regular match**: Enter a regular expression for precise matching.<br><br>* **IP**<br><br>   * **Single IP**: Enter an exact IP address for matching.<br><br>   * **CIDR block**: Enter a CIDR block address. All IP addresses in this CIDR block are considered target controlled websites.<br><br>   * **IP range**: Enter a continuous IP address range connected by a hyphen. The system matches all IP addresses in this range as target controlled websites.<br><br>* **Domain**<br><br>   * **Exact domain**: Only the complete domain entered here is matched.<br><br>   * **Wildcard domain**: Use a wildcard to match all subdomains under a primary domain.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>IP</strong> and <strong>Domain</strong> rules take effect only on SealSuite clients of version <strong>3.3.16 or later</strong>. If the client version is earlier than 3.3.16, such rules cannot be adapted, and the corresponding outbound control policy does not take effect.</div><br> |
      |**Website Title** |**Optional** when the address type is **URL**. This field helps identify the website. If both Website URL and Website Title are configured, both must be matched before the website is reported. Configure this field as needed. |
      

3. Click **Confirm** to complete the addition. After the address is added, you can select it when configuring a control policy to implement control.


<span id="6a444a6b"></span>
#### Batch Import


1. Click **Import** in the upper\-right corner of the channel list page.

2. Click **Download** to obtain the **Channel List \- Web website batch import template**, and fill in address records according to the template requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b24874b185ab4b9491805c5fe2d589bf~tplv-goo7wpa0wc-image.image) </span>

3. After completing the template, click **Upload** or directly drag the completed file to import it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The file size must be no larger than <strong>2 MB</strong>, and up to <strong>1,000 records</strong> can be imported at a time.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the file is uploaded, the system automatically validates whether the table content meets the requirements. If validation fails, modify the template content based on the error message and <strong>upload it again</strong>.   </div>
   

4. Click **Confirm** to complete the import.


<span id="83c4ca2c"></span>
## Manage custom channels

You can maintain and manage custom channels on the **Channel list** page.


* **Edit a channel**

   Locate the custom channel you want to modify in the list and click **Edit** in the Action column to update its basic information, identification criteria, and supported capability scope. After you save your changes, they are automatically synced to all policies that reference this channel.

* **Delete a channel**

   If you no longer need to control a custom channel, click **Delete** in the Action column to remove it from the list. You can also select the check boxes on the left side of the list for **bulk deletion**.

   **Note**: Custom channels that are bound to security policies cannot be deleted. First remove the channel reference from the relevant policies, then delete the channel. You can click the **Applied policies** number in the list to quickly jump to the policies that reference the channel.
