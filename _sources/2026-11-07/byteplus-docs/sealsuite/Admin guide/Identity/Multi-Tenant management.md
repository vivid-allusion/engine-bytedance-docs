---
title: "Multi-Tenant management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-multi-tenant_configurations"
---

Multi\-tenant Management is a powerful multi\-organization feature that enables you to centrally manage multiple, distinct organizations from a single platform, even when each has its own independent identity and data sources.

Within this feature, your primary corporate entity is referred to as the **Primary Tenant**, while each independent organization you create is known as a **Sub\-tenant**.

The key benefit of this feature is the ability to configure dedicated, independent authentication sources (such as different AD domains, LDAP, Lark, or DingTalk instances) and data synchronization sources for each Sub\-tenant.

<span id="96640f48"></span>
# Use Cases

We recommend using the Multi\-tenant Management feature if your organization fits any of the following profiles:


* **Conglomerates with Multiple Subsidiaries:**  A parent company needs to centrally manage subsidiaries that each maintain their own independent IT identity systems (e.g., Subsidiary A uses WeChat Work, while Subsidiary B uses Active Directory).

* **Multinational Corporations:**  A company's headquarters in one region uses a different identity service than its international branches (e.g., Lark in the main office, Azure AD for international branches).

* **Partner and Ecosystem Management:**  You need to onboard external vendors or partners as distinct organizational units, allowing them to use their own account systems to access authorized resources.

* **Business Isolation Requirements:**  Different business lines within the same enterprise must use logically or physically isolated identity data sources for security or compliance reasons.

> If all employees in your organization use a single, unified identity system, this feature is not necessary. Standard **Department Management** will be sufficient for your organizational structure needs.


<span id="20ea6eef"></span>
# Configuration Workflow

<span id="81ac0a86"></span>
## Step 1: Create a Sub\-tenant

Creating a Sub\-tenant is the first step in establishing a management framework for a separate organization.


1. Log in to the Admin Console.

2. In the left navigation bar, navigate to **Identity** \> **Multi\-tenant**.

3. Click **Add New Tenant** in the upper\-right corner of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bad30fe1c40f4649a2ccf6cb3880fa0e~tplv-goo7wpa0wc-image.image) </span>

4. In the **Create New Tenant** dialog, configure the following parameters and then click **Confirm**.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Tenant ID** |A globally unique identifier for the Sub\-tenant. It can only contain lowercase letters, numbers, and underscores (`_`).<br><br>The Tenant ID cannot be changed after the Sub\-tenant is created. |
   |**Tenant Name** |A user\-friendly name for easy identification, such as "Overseas Division" or "Subsidiary Branch". |
   |**Tenant Description** |(Optional) A brief description of the tenant's business purpose or function. |
   


<span id="9ff3e4df"></span>
## Step 2: Configure Independent Authentication and Data Sources

After creating a sub\-tenant, you must configure its independent authentication and data sources to enable multi\-organization identity management.


* **Configure Authentication Sources**

   1. Select the sub\-tenant you just created and click **Details** in the **Operation** column.

   2. In the **Tenant Association** section at the bottom of the page, click **Third\-Party Login** to configure a dedicated authentication method for this tenant. For detailed instructions, see [Configuring third-party authentication source](https://docs.byteplus.com/en/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-_1).

* **Configure Synchronization Sources**

   1. Select the Sub\-tenant you just created and click **Details** in the **Operation** column.

   2. In the **Tenant Association** section at the bottom of the page, click **Directory Synchronization** to configure how personnel and organizational data are synced for this tenant. For detailed instructions, see [Integrating third-party data sources](https://docs.byteplus.com/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-).


<span id="627ff9ee"></span>
## Step 3: Manage the Sub\-tenant's Org Chart and Employees

When you create a Sub\-tenant, the system automatically generates a top\-level department with the same name, which serves as the root of its organizational hierarchy.


1. In the left navigation bar, navigate to **Identity** \> **Directory**.

2. In the department list on the left, select the Sub\-tenant you created in Step 1.

3. From here, you can manage the Sub\-tenant's organizational structure and employee information.

   * To manually add departments and employees, refer to [Managing departments](https://docs.byteplus.com/docs/sealsuite/docs-managing-departments) and [Managing users](https://docs.byteplus.com/docs/sealsuite/docs-managing-members).

   * If you configured data source synchronization in Step 2, the tenant's org chart and employee data will be synced automatically from the source.


<span id="52228a7a"></span>
# Ongoing Management

<span id="87f35b3a"></span>
## View or Edit Tenant Details


1. Log in to the Admin Console.

2. In the left navigation bar, navigate to **Identity** \> **Multi\-tenant**.

3. In the tenant list, find the tenant you want to manage and click **Details** in its **Operation** column.

4. On the details page, manage tenant information on the following tabs.

   * **Unit information**: View basic tenant information, associated login authentication sources, and data synchronization sources.

   * **Agreement Management**: Manage the agreement policies that employees must accept when logging in to SealSuite.

      * **Primary**: If your enterprise has purchased the **Multi Tenant** license, you can centrally configure agreements for the Primary Tenant on this tab, including user agreements, privacy policies, and custom agreements. If the license has not been purchased, go to **Enterprise Settings** \> **Company General** to manage the global agreements. For details, see [Configuring and viewing enterprise information](https://docs.byteplus.com/docs/sealsuite/docs-configuring-and-viewing-enterprise-information).

      * **Sub\-tenant**: Uses the Primary Tenant’s agreements by default. After you enable the switch, you can configure agreements independently for the Sub\-tenant. For details, see [Manage Sub-tenant Agreements](https://docs.byteplus.com/docs/sealsuite/managing-multi-tenant_configurations#65cdd6f7).

5. (Optional) Click the **Edit** button in the upper\-right corner to modify the tenant's name and description.

   * The Tenant ID of the Primary Tenant can be modified.

   * The Tenant ID of a Sub\-tenant cannot be modified.


<span id="65cdd6f7"></span>
## Manage Sub\-tenant Agreements

For multi\-region compliance or cross\-business requirements, you can configure independent login agreements for specific Sub\-tenants, including user agreements, privacy policies, and other custom compliance agreements.


1. On the **Multi\-Tenant** page, find the target Sub\-tenant and click **Details** in the **Operation** column.

2. At the top of the details page, switch to the **Agreement Management** tab.

3. Enable **Separate Protocol Configuration**.

   * **Disabled (default)** : The Sub\-tenant uses the privacy agreements of the Primary Tenant.

   * **Enabled**: The Sub\-tenant can use independent agreement policies.

4. Manage agreement content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48f07963b5954bb09dfd6be6c2a44f61~tplv-goo7wpa0wc-image.image) </span>

   * **Enable or disable built\-in agreements**: Enable or disable built\-in agreements as needed.

   * **Create an agreement**: Click  **+ Create New Agreement** to add custom agreements for specific compliance requirements. English and Chinese are supported.

   * **Edit an agreement**: Click **Edit** on the right side of a custom agreement to modify its English and Chinese content.

   * **Adjust the order**: Drag the sorting handle on the left side of an agreement to customize the display order on the client login page.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">SealSuite client version <strong>2.2.12 and later</strong> supports reading custom agreement policies for Sub\-tenants. Earlier client versions read the original built\-in SealSuite agreements by default. We recommend guiding employees to upgrade their clients.</div>


* <div data-tips="true" data-tips-type="warning">If you enable <strong>Separate Protocol Configuration</strong> but disable all agreements and create no new ones, employees in this tenant cannot view or accept any agreements during login, which may pose legal compliance risks.</div>



<span id="92802112"></span>
## Delete a Sub\-tenant


1. Log in to the Admin Console.

2. In the left navigation bar, navigate to **Identity** \> **Multi\-tenant**.

3. In the tenant list, find the Sub\-tenant you wish to delete and click **Delete** in its **Operation** column.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The Primary Tenant cannot be deleted.</strong>   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before deleting a Sub\-tenant, you must first remove all departments and employees associated with it. The deletion will be blocked if any members or departments still exist within the tenant.   </div>
