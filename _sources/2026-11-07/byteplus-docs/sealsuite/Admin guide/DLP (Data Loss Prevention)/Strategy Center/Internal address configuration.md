---
title: "Internal address configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/internal-address-configuration"
---

To balance data security with workplace efficiency, SealSuite supports configuring granular "internal address" allowlist rules for different types of business channels. By configuring internal addresses, administrators can exclude normal internal business traffic from monitoring, enabling differentiated control over internal versus external data flows.

Internal address configuration applies to **document outgoing control policies** and **clipboard control policies**. When a policy is in effect, actions that match an internal address (allowlist) are neither logged nor blocked.

# Add internal addresses

Log in to the Admin Console and navigate to **DLP** \> **Strategy Center** \> **Internal address**. Manage each type of internal address under its corresponding tab.

## Configure internal website addresses

On the **Websites** tab, you can add your enterprise's trusted internal web applications or intranet sites to the allowlist. This configuration supports manual addition and batch import/export operations.

### Manually Add an Address

1. Click  **+ Add** in the upper\-right corner of the list.

2. Complete the following configuration on the configuration page that appears:

   |**Configuration Item** |**Description** |
   |---|---|
   |**Address Type** |Select the website address type as needed. The supported options are **URL**, **IP**, and **Domain**. |
   |**Website Name** |Enter the internal website name. Letters, special characters, and spaces are supported. The maximum length is 50 characters. |
   |**Address Information** |Complete the address information based on the selected address type.<br><br><br>* **URL**<br><br>   * **Contains matching**: If the website URL contains the string entered here, it is considered an internal website.<br><br>   * **Regular match**: Enter a regular expression for precise matching.<br><br>* **IP**<br><br>   * **Single IP**: Enter an exact IP address for matching, such as `192.168.1.1`.<br><br>   * **CIDR block**: Enter a CIDR block address, such as `192.168.1.0/24`. All IP addresses in this CIDR block are considered internal addresses.<br><br>   * **IP range**: Enter a continuous IP address range connected by a hyphen, such as `192.168.1.10-192.168.1.50`. The system matches all IP addresses in this range as internal addresses.<br><br>* **Domain**<br><br>   * **Exact domain**: Only the complete domain entered here is matched as an internal domain.<br><br>   * **Wildcard domain**: Use a wildcard to match all subdomains under a primary domain as internal domains.<br><br><br>> **警告**<br><br><br>> **IP** and **Domain** rules take effect only on SealSuite clients of version **3.3.16 or later**. If the client version is earlier than 3.3.16, these rules are not supported, and the corresponding allowlist does not take effect.<br> |
   |**Website Title** |**Optional** when the address type is **URL**. This field helps identify the website. If both Website URL and Website Title are configured, both must be matched before the website is reported. Configure this field as needed. |

3. Click **Confirm** to complete the addition. After the address is added, you can reference it when configuring control policies to allow it through the allowlist.

### Batch Import

1. Click **Batch import/export** \> **Import** in the upper\-right corner of the list.

2. Click **Download** to obtain the **Internal Web Website Batch Import Template** and fill in address records according to the template requirements.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f06de614d624809b03d9a665cc225b3~tplv-goo7wpa0wc-topic.webp)

3. After completing the template, click **Upload** or directly drag the completed file to import it.

   > **说明**

   1. > The file size must be no larger than **2 MB**, and up to **1,000 records** can be imported at a time.

   2. > After the file is uploaded, the system automatically validates whether the table content meets the requirements. If validation fails, modify the template content based on the error message and **upload it again**.

4. Click **Confirm** to complete the import.

5. **Optional**: You can export the currently configured internal Web website address table to a local file with one click. This can be used for offline security audits, batch adjustment of existing data (export, modify, and re\-import), and cross\-environment configuration migration.

   1. Select the target records, or leave all records unselected to export all records.

   2. Click **Batch import/export** \> **Export** in the upper\-right corner of the list.

   3. Click **Confirm** to save the address records as a local Excel file.

## Configure Instant Message internal addresses

On the **Instant Messaging** tab, you can configure allowlists for your enterprise's internal communication tools (currently supports Feishu and Lark). **Note**: This feature requires SealSuite client version 3.2.12 or later.

1. Click  **+ Add** in the upper\-right corner of the list.

2. Select the **IM Software Name** (**Feishu** or **Lark**).

3. Enter the corresponding **Enterprise name** and **Enterprise Tenant ID**.

   By configuring the enterprise name and Tenant ID, the system can identify internal enterprise accounts on the desktop client, enabling differentiated control between internal and external accounts. For instructions on obtaining the Tenant ID, see the appendix: [How to obtain your enterprise Tenant ID](https://docs.byteplus.com/docs/sealsuite/internal-address-configuration#c64e7475).

4. Click **Confirm** to save.

## Configure code repository internal addresses

On the **Code repository** tab, you can add your enterprise's internal code hosting platforms to the allowlist, allowing normal code commits and syncs to pass through. This configuration supports manual addition and batch import/export operations.

### Manually Add an Address

1. Click  **+ Add** in the upper\-right corner of the list.

2. Complete the following configuration on the configuration page that appears:

   |**Configuration Item** |**Description** |
   |---|---|
   |**Code Repository Name** |Enter the code repository name. Letters, special characters, and spaces are supported. The maximum length is 50 characters. |
   |**Address Type** |Select the code repository address type to add as needed. The supported options are **URL**, **IP**, and **Domain**. |
   |**Address Information** |Complete the address information based on the selected address type.<br><br><br>* **URL**<br><br>   * **Contains matching**: If the repository address contains the string entered here, it is considered an internal code repository.<br><br>   * **Regular match**: Enter a regular expression for precise matching.<br><br>* **IP**<br><br>   * **Single IP**: Enter an exact IP address for matching, such as `192.168.1.1`.<br><br>   * **CIDR block**: Enter a CIDR block address, such as `192.168.1.0/24`. All IP addresses in this CIDR block are considered internal addresses.<br><br>   * **IP range**: Enter a continuous IP address range connected by a hyphen, such as `192.168.1.10-192.168.1.50`. The system matches all IP addresses in this range as internal addresses.<br><br>* **Domain**<br><br>   * **Exact domain**: Only the complete domain entered here is matched as an internal domain.<br><br>   * **Wildcard domain**: Use a wildcard to match all subdomains under a primary domain as internal domains.<br><br><br>> **警告**<br><br><br>> **IP** and **Domain** rules take effect only on SealSuite clients of version **3.3.16 or later**. If the client version is earlier than 3.3.16, these rules are not supported, and the corresponding allowlist does not take effect.<br> |

3. Click **Confirm** to complete the addition. After the address is added, you can reference it when configuring control policies to allow it through the allowlist.

### Batch Import

1. Click **Batch import/export** \> **Import** in the upper\-right corner of the list.

2. Click **Download** to obtain the **Internal Code Repository Batch Import Template** and fill in address records according to the template requirements.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2de27d0c7f884d2e9aba919bad1039a2~tplv-goo7wpa0wc-topic.webp)

3. After completing the template, click **Upload** or directly drag the completed file to import it.

   > **说明**

   1. > The file size must be no larger than **2 MB**, and up to **1,000 records** can be imported at a time.

   2. > After the file is uploaded, the system automatically validates whether the table content meets the requirements. If validation fails, modify the template content based on the error message and **upload it again**.

4. Click **Confirm** to complete the import.

5. **Optional**: You can export the currently configured internal code repository table to a local file with one click. This can be used for offline security audits, batch adjustment of existing data (export, modify, and re\-import), and cross\-environment configuration migration.

   1. Select the target records, or leave all records unselected to export all records.

   2. Click **Batch import/export** \> **Export** in the upper\-right corner of the list.

   3. Click **Confirm** to save the address records as a local Excel file.

> **说明**

> **Upgrade note (for users on version 3.3.1 or earlier)**

> SealSuite has consolidated the standalone "Code repository upload" control capability into "Desktop applications." If you are upgrading from an earlier version, your existing file outbound policies that included code repositories, along with the code repository exclusion lists, will take effect automatically as follows:

* > **Policy configuration change**: Policies that previously included "Code repository upload" will have their outbound method automatically changed to "Desktop applications (Code repositories)".

* > **Allowlist preservation**: The allowlist platform resources previously configured for code repositories have been fully migrated to the current **Internal address** \> **Code Repository** tab and continue to function as exclusions in the original policies.

## Configure email internal addresses

On the **Email** tab, you can configure allowlists for your enterprise's internal email domains or trusted partner email domains. Email internal address configuration applies to both desktop email clients and webmail.

1. Click  **+ Add** in the upper\-right corner of the list.

2. In the configuration dialog box, enter the **Email name** and **Email address / suffix**.

   Internal email matching performs a 'contains' match. For example, entering only `outlook` will match `it@outlook.com`, `it@outlooksecurity.com`, and `it@outlook.security.com`.

3. Click **Confirm** to save.

> **注意**

> If any recipient, CC, or BCC address in an email is not covered by the internal addresses configured here, the system will still treat the action as an external transfer and may trigger an audit or block alert.

## Configure internal AI tools

On the **AI Tool** tab, you can configure allowlist entries for large language model service endpoints (BaseURL), model providers (Provider) or specific enterprise accounts that your enterprise has internally deployed or lawfully procured. After configuring the allowlist and excluding it in the relevant policies, the system will allow file transfers and interactions when employees use supported AI chat tools with these compliant models.

1. Click  **+ Add** in the upper\-right corner of the list.

2. In the configuration dialog box, fill in the following information:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55520f26c7da4f7c90178140d8d02595~tplv-goo7wpa0wc-topic.webp)

   * **Tool name**

      Enter a custom name that is easy to identify and remember, such as "Internal LLM".

   * **Identification Method**

      Select an appropriate identification method based on enterprise control requirements and the capabilities supported by the AI tool.

      * **BaseURL**: Select this option and enter the model service's API endpoint address in the input box below. Suitable for enterprises with privately deployed LLMs or services proxied through an internal API gateway.

      * **Enterprise account**: Identifies the account used by employees to log in to an AI tool. Use this option when the enterprise has centrally procured AI development tools and allows only enterprise\-authorized accounts, such as enterprise TRAE accounts, while auditing or blocking personal accounts. After selecting this option, select the **AI Application Type** first, and then enter the corresponding **Account Company Name**.

      * **Provider Name**: Select this option and enter the model provider name in the input box below. Suitable for public cloud LLM services that your enterprise has lawfully procured and allows employees to connect to directly.

   * **Supported tools**

      Read\-only area. The system dynamically displays the currently supported tools, operating system requirements, and client version requirements based on the selected **Identification Method**.

3. Click **Confirm** to save.

> **说明**

> **How the allowlist takes effect**

> Due to the working mechanism of some AI Agents, when employees use an AI Agent to call known transfer tools or software, such as WeChat or email, for file outbound, SealSuite applies the allowlist policy of the transfer tool itself. The internal AI tool allowlist configured here **does not take effect**. It applies only when an AI Agent directly reads local documents and interacts with an LLM, or when it uses an unknown tool.

## Configure CLI / remote control / file transfer tools

On the **Command line/Remote control/File transfer** tab, you can configure a unified destination address allowlist for specific operational tools, remote control software, or file transfer software. After configuring and excluding these addresses in a policy, the system will allow transfers when these tools connect to the specified internal servers (IP addresses or domains).

> **说明**

* > **Shared allowlist**: CLI tools, remote control software, and file transfer tools **share the same internal address allowlist pool**. Any IP address or domain you add here applies to all three control channels simultaneously.

* > **Backward compatibility (for users upgrading from version 3.3.1 or earlier)**: If you had already configured internal addresses for "File transfer tools" before upgrading, those historical addresses will automatically take effect for the newly controlled "CLI tools" and "Remote control software" after the upgrade. No reconfiguration is needed.

1. Click  **+ Add** in the upper\-right corner of the list.

2. In the configuration dialog box, complete the following settings:

   |**Field** |**Description** |
   |---|---|
   |**Address type** |Select **IP** or **Domain** based on how the destination server is identified. |
   |**Destination address information** |Enter the destination to allow. The system uses this configuration to identify trusted transfer paths.<br><br><br>* **IP format**: Supports a single IP (for example, `192.168.1.10`), a CIDR range (for example, `192.168.1.0/24`), or an IP range (for example, `192.168.1.1-192.168.1.254`).<br><br>* **Domain format**: Supports a main domain (for example, `example.com`) or a wildcard domain (for example, `*.example.com`). |
   |**Remarks** |Optionally enter the purpose or description of this address. |
   |**Supported tools** |Read\-only area. Displays the tools that currently support destination identification, including **Command\-line tool**, **Remote control software**, and **File transfer tool**, along with the minimum client version required for each operating system. |

3. Click **Confirm** to save.

# Exclude internal addresses in policies

On their own, internal addresses are just lists of entries. After configuring them, you must apply them to a specific outbound file control policy for them to take effect.

When configuring an outbound file control policy, after you select specific **Control channels** (such as a particular chat application, website, or code management tool), you can enable the corresponding channel type in the **Exclude internal address** section and import the internal addresses you have created.

Once the policy is in effect, when employees transfer files to these internal addresses, the policy's block or audit alerts will not be triggered. For detailed policy configuration instructions, see [Configuring document outgoing control policies](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule).

# Manage internal address records

After adding internal addresses, you can view and maintain them on the list page under each tab:

* **Search**: Each tab supports filtering through the search box at the top (for example, fuzzy search by enterprise name, website URL/title, hosting platform, or email address).

* **Edit**: Click **Edit** in the Action column to modify the configuration parameters of an internal address. After the address is edited, **policies that reference this internal address configuration are updated accordingly**.

* **Delete**: Click **Delete** in the Action column to remove a record. Internal addresses that are associated with control policies cannot be deleted. First remove the reference from the relevant policies.

# Appendix

## How to obtain your enterprise Tenant ID

To ensure SealSuite accurately identifies and integrates with your corporate Lark/Feishu environment, you must provide your unique **Tenant ID**.

Lark/Feishu assigns a unique technical identifier to every organization. Because this ID is primarily used for backend integrations, it is not displayed directly within the standard administrative user interface. You can retrieve it by inspecting network requests through your browser's developer tools.

1. Use a desktop browser (Google Chrome or Microsoft Edge recommended) to log in to your Lark/Feishu Admin Console.

2. Once the dashboard has loaded, open the browser's developer tools using the following keyboard shortcuts:

   * **Windows / Linux**: `Ctrl + Shift + I`

   * **macOS**: `Cmd + Option + I`

3. In the developer tools panel that appears (usually on the right or bottom of the screen), click the **Network** tab.

4. Filter Network Traffic:

   * Locate the **Filter** input box (the magnifying glass icon) and type the keyword `tenant`.

   * To further reduce clutter, click the **Fetch/XHR** sub\-tab. This ensures you only see data exchange requests rather than images or stylesheets.

> Note: If no requests appear in the list, refresh the Lark Admin Console page while keeping the developer tools open.

5. Locate the Tenant ID:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a709156a2234226ad2fae4644e04b5a~tplv-goo7wpa0wc-topic.webp)

   * In the filtered list of requests, look for an entry named `ping_tenant_restriction` or `tenantBaseInfo`.

   * Click on the request name to open its details.

   * Select the **Response** or **Preview** tab on the right side of the details panel.

   * You will see a block of code\-formatted text. Search for the field named `tenant_id`. The string of characters associated with this field is your **Enterprise Tenant ID**.

6. Copy the ID value and paste it into the corresponding field in the SealSuite Admin Console to complete your configuration.
