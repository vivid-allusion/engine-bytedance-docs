---
title: "Customizing client interface and feature visibility"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/customizing-client-interface-and-feature-visibility"
---

SealSuite allows organizations to deeply customize the interface layout, menu names, and feature visibility of the desktop clients (Windows, macOS, and Linux). Administrators can hide redundant modules or rename menu items to align with corporate culture and specific usage scenarios, creating a tailored workspace experience for employees.

<span id="91830798"></span>
## Prerequisites

This feature is primarily used to hide specific modules or adjust their display names and order based on existing permissions.

**Important**: The final interface displayed to an employee is determined by both the organization's subscription plan and the individual's assigned permissions. For example, if the "Endpoint Security" module is not purchased or if an employee is not granted "Wi\-Fi Connection" permissions, the corresponding entries **will not appear** on their client, even if the administrator sets the "Security" or "Wi\-Fi" toggles to "ON" in this configuration.

<span id="aa919056"></span>
## Procedure


1. Log in to the Admin Console.

2. In the left navigation pane, select **Branding**.

3. Locate the **Client Function Display Settings** card under the **Feature Configuration** section.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86234541f2b74754a359d1f7070338a3~tplv-goo7wpa0wc-image.image) </span>

4. In the top right corner of the card, you can toggle the **Global Configuration** switch:

   * **ON**: All configurations are immediately deployed to the clients.

   * **OFF**: All configurations are saved as drafts, and the client interface reverts to the system default.

5. Click the card to enter the detailed settings page.


<span id="70654460"></span>
## I. Sidebar Navigation Configuration

This section controls the layout of the primary navigation bar on the left side of the client.

<span id="fd1f527d"></span>
### Adjusting Navigation Structure


* **Show/Hide Modules**: Use the checkboxes next to the module names to control whether a specific module is visible to users.

* **Reorder Menus**: Use the **drag handles** on the left of each module to adjust their vertical order in the client sidebar.

* **Select Module for Editing**: Click any module name to switch the right\-hand panel to that module's specific settings.


*Note: The* ***Overview*** *and* ***Settings*** *modules are foundational and cannot be hidden or reordered.* 

<span id="a9af7ce8"></span>
### Modifying Module Names

Select a module and click the edit icon next to the title in the right panel to configure display names and multi\-language settings.


* **Rename**: Change the display name (e.g., rename "Overview" to "Workspace").

* **Multi\-language Support**: Click  **+ Add Language** to define specific names for Chinese, English, or Japanese environments.


<span id="25e9bb68"></span>
## II. Page Content Details

You can perform granular control over the layout and information displayed within specific secondary pages.

<span id="53292d2a"></span>
### Overview Page


1. **Account Information**: Customize the fields displayed in the account section at the top of the page.

2. **Function Card Management**: Control the visibility and names of the core cards on the Overview page.

   * **VPN Connectivity**: Toggle visibility of the VPN connection card and rename its title.

   * **Toolbox**: Toggle visibility and rename the toolbox. Click **Expand** to manage the visibility and order of specific tools (e.g., Network Diagnostics, Security Detection).

   * **Application Management**: Toggle the visibility of the recommended apps card.

      * Note: To configure the actual app list and groupings, click the **Configure** link to navigate to **Identity** \> **SSO** \> **Application Group Management**.


<span id="44b2c2e3"></span>
### Network Page

Manage the five core network modules: **VPN**, **SWG** (Secure Web Gateway), **Wi\-Fi**, **Wired Network**, and **Proxy Server**.


* **Show/Hide**: Control the visibility of each sub\-item.

* **Reorder**: Drag the handle to adjust the horizontal order of these modules in the client.

* **Rename**: Customize multi\-language titles for each network service.


<span id="634a867a"></span>
### Security Page

The visibility of content on this page is determined by your **Endpoint Security Policies** rather than manual toggles here.


* **Device Baseline & Running Processes**: Visibility depends on whether Baseline Detection policies are enabled. (Path: **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**).

* **Viruses & Trojans**: Visibility depends on whether Antivirus policies are active. (Path: **Endpoint Security** \> **Anti\-Virus** \> **Policy Management**).


<span id="2963e3a7"></span>
### Lab Page

Manage system diagnostics and maintenance tools integrated into the **Lab** module.


1. **Tool List Management**: Arrange tools such as **Network Diagnostics**, **DNS Reset**, **Device Info**, and **Remote Control**.

   * **Show/Hide**: Control tool visibility via checkboxes.

   * **Reorder**: Drag to adjust the sequence of tools.

2. **Custom Descriptions**: Edit both the **Title** and **Description** for each tool to help employees understand their purpose.

* *Note: Network Diagnostics supports deep customization of detection items. See* [Network diagnosis](https://docs.byteplus.com/docs/sealsuite/docs-managing-network-diagnosis) *for details.* 


<span id="0b4726cd"></span>
### Software Page

Visibility is controlled via **Software Management Policies**. Click **Configure** to navigate to **Endpoint** \> **Software** \> **Library** to upload enterprise software, define categories, and set target scopes.

<span id="26c78d63"></span>
### Help Page

Visibility is determined by the configuration of the respective business modules:


* **Help**: Displays internal FAQs. Configure this in **Enterprise** **Settings** \> **Admin Center** \> **Help Center**.

* **IT Assistant**: Provides a direct line to IT support. Configure this in **Settings** \> **IT Tools** \> **IT Assistant**.

* **Feedback**: Collects user issues. Enable/disable this in **Settings** \> **IT Tools** \> **Feedback**.


<span id="d5b14b24"></span>
### Settings Page


* **General Settings**: Control the visibility and naming of startup options like **Auto\-connect to VPN** and **Go to Network tab**.

* **Shortcuts**: Toggle the visibility of the entire hotkey settings module.


<span id="ffb0b0a7"></span>
## III. Target Scope

After finalizing the UI customizations, define which users or devices will receive this specific interface scheme.


1. Scroll to the **Scope** section at the bottom of the page.

2. Select the application range:

   * **All Employees**: Applies the UI scheme to every desktop client in the organization.

   * **Selected Employees**: Assign the scheme by **Department** or **Role**. This allows different departments to have distinct client interfaces.


<span id="0f067e64"></span>
## IV. Deployment and Maintenance

<span id="006d17ce"></span>
### Saving and Publishing


* **Save as Draft**: Saves all customizations as a draft without deploying them.

* **Save and Publish**: Saves the configuration and immediately pushes update instructions to the target scope. The UI changes will take effect after the next login or client heartbeat sync.


<span id="a2511e74"></span>
### Restoring Defaults

To discard customizations and return to the standard SealSuite interface, click **Restore Default Settings** in the top right corner. This action clears all custom names, reordering, and visibility settings, reverting the client to its original state.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f58d9ceb78b044578e251a6e25610294~tplv-goo7wpa0wc-image.image) </span>
