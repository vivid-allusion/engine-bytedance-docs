---
title: "Important Notice: 2025 Product Upgrade Announcement"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/2025-upgrade"
---

Dear SealSuite Users,

The SealSuite Admin Console has been upgraded with a redesigned navigation structure and homepage UI to enhance your management efficiency. This guide details the key changes, including a streamlined navigation menu, a new management\-focused homepage, and the rationale behind the restructuring, ensuring you can quickly adapt to the more intuitive layout.

**Please rest assured that this upgrade will not impact your business operations. All your existing configurations, account data, and security policies will be seamlessly migrated automatically.** 

<span id="9e71a2c8"></span>
## **Background and Goals**

We initiated this upgrade based on extensive user feedback and industry best practices. As our product features have rapidly evolved, the previous Admin Console design presented challenges, such as scattered information on the homepage, the lack of an effective global overview, and deep navigation hierarchies that made key features difficult to locate.

This upgrade is designed to systematically address these issues with the following core objectives:


* **Providing a Management\-Focused Homepage**: We have completely redesigned the homepage, transforming it from a simple information display into a comprehensive management homepage. It provides a clear, focused, at\-a\-glance view to help you quickly assess your core operational status.

* **Enhancing Navigation Efficiency**: We have systematically restructured the navigation, streamlining the number of top\-level menus from 31 to 16 and reducing the overall depth from three levels to two. This will significantly reduce mouse clicks and page jumps, allowing you to locate features much faster.

* **Aligning with Industry Standards**: We have aligned the naming and categorization of certain features (such as "Zero Trust Access") with prevailing industry security concepts, making the navigation more consistent with your expertise and workflows.


<span id="c0c502a3"></span>
## **Key Changes**

This upgrade focuses on two main areas: the **Admin Console Homepage** and the **Navigation Menu**.

<span id="a69998b4"></span>
### **Admin Console Homepage**

The homepage has been completely redesigned to provide a clear, focused, single\-screen overview. In\-depth data analysis has been consolidated into the dedicated **Dashboard** page, resulting in a more streamlined and organized layout. Upon logging in, you can now instantly assess core operational data and your overall security posture.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/935a7d29141645e3b3806d71d93fbe9c~tplv-goo7wpa0wc-image.image" width="850px" /></div>


The new homepage consists of the following core modules:


1. **Basic Information Overview**


Located at the top of the page, this section centralizes essential information such as company details, key asset counts, and the status of your service subscription.


2. **Quick Access Shortcuts**


To streamline your daily workflow, we have added a shortcuts module based on user frequency. You can now get one\-click access to the most commonly used pages, including Directory, Asset List, Dashboard, Branding, and Audit Logs.


3. **Key Data Statistics**


The lower half of the homepage features two new core statistical charts of company members and devices. These charts dynamically display key operational metrics to support data\-driven management decisions. For details on where data from the old homepage has been moved, please refer to [Appendix I](https://docs.byteplus.com/docs/sealsuite/2025-upgrade#b310f97b).

<span id="0aa270a7"></span>
### **Navigation Menu**

To improve logic and usability, we have systematically reorganized and optimized the navigation menu. Below is a summary of the key changes:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d7e62e178094d0ca5f636f1744d77e2~tplv-goo7wpa0wc-image.image" width="400px" /></div>



1. **Restructuring Core Security Scenarios**

   We have re\-categorized core security capabilities to better align with mainstream security frameworks.

   * **Segregating Security Functions:**  The former `Security` module has been split into two distinct top\-level menus, **`Endpoint Security`** and **`DLP`** ** (Data Loss Prevention)** , to provide more precise, scenario\-based management.

   * **Consolidating "Zero Trust" Capabilities:**  Features previously under `VPN` and `App Gateway` have been unified under the new **`Zero Trust Access`** menu. This aligns with the industry\-standard "Zero Trust" model and provides a single entry point for managing access to internal applications.

2. **Grouping Related Features to Streamline Workflows**

   We have grouped related but previously scattered functions to streamline your configuration and management processes.

   * **Centralizing Identity Capabilities:**  The formerly separate `SSO` feature is now part of the **`Identity`** menu, centralizing identity and access management functions.

3. **Promoting Frequently Used Features**

   For your convenience, we have elevated several frequently used modules to the top\-level navigation.

   * **`Dynamic Control`** is now a top\-level menu, highlighting its role as the core engine for continuous verification in the Zero Trust framework.

   * **`Audit Logs`** and **`Enterprise Settings`** are now top\-level menus. **`Enterprise Settings`** has become a unified hub for managing company information, admin permissions, version releases, and more.

4. **Optimizing Naming and Categorization**

   We have updated the names of some features to more accurately reflect their scope.

   * `Wi-Fi Management` has been renamed to **`NAC`** ** (Network Access Control)**  to better cover both wired and wireless scenarios.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">For a detailed mapping of every feature's new location, please refer to the complete new vs. old navigation table organized by module in <a href="https://docs.byteplus.com/docs/sealsuite/2025-upgrade#12dc7711">Appendix II</a>.</div>


2. <div data-tips="true" data-tips-type="tip">For instructions on using the new Admin Console, please refer to the <a href="https://docs.byteplus.com/docs/sealsuite/docs-operation-instructions">Using the Admin Console</a>.</div>



<span id="704a9ba3"></span>
### **Application Configuration and Management**

A core part of this upgrade is the separation of **Single Sign\-On (SSO)**  and **Application Gateway** functionalities. This change creates a clearer division of responsibilities between identity authentication and secure access, resulting in a more logical and intuitive configuration workflow. This section explains the new locations for application settings and how to configure them going forward.


* **Core Concept: Decoupling Features**

   * **Identity \> SSO:**  This module is now exclusively focused on **identity authentication**. Use this module to manage all applications that require user authentication, including those using protocols like CAS/SAML/OIDC, Password Vaulting apps, and simple bookmark links.

   * **Zero Trust Access \> Application:**  This module is now focused on **secure access**. Use this module to securely publish internal web applications to the internet for remote access.

* **Historical Data Migration**

   All of your existing application configurations have been automatically migrated to their new locations based on this updated logic. **Your current services are not affected.**  The migration rules are as follows:

   
   |**Original Configuration** |**New Location** |**Notes** |
   |---|---|---|
   |**Single Sign\-On Apps** (CAS, SAML, OIDC, Password Vaulting, etc.) |**Identity \> SSO** |All protocol settings, application information, and authorization rules have been fully preserved. |
   |**Quick Access & Wildcard Gateway Apps** |**Zero Trust Access \> Application \> Web** **App** |The primary function of these apps is secure access, so they are now managed as Web Applications. |
   |**Apps with both SSO and Gateway configured** |**Data is preserved in both locations** |We have processed this data to ensure these applications continue to function correctly under both the **Single Sign\-On** and **Zero Trust Access** modules. |
   |**Gateway Nodes, Logs, and Certificates** |**Zero Trust Access \> Gateway** **Config** |Only the management location has changed; all configuration data remains unchanged. |
   

* **Guide to Configuring New Applications**

   Use the appropriate module for your needs:

   * To configure **identity authentication** for an application, go to **Identity \> SSO**.

   * To securely **publish an internal application** via the gateway, go to **Zero Trust Access \> Application \> Web App**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Special Scenario:</strong> If you want to add a gateway\-published Web Application to a client's app group, simply copy its public URL and add it as a new link in the app group under <strong>Identity \> SSO</strong>.   </div>
   

* **Feature Licensing and Permissions**

   This restructuring does not affect your existing feature licenses or service scope. Feature permissions in the new console are aligned with the new module structure:

   * Under **Identity \> SSO:** 

      * Adding "Quick Access" is a **base feature** available to all users.

      * Configuring other SSO types (SAML, OIDC, Password Vaulting, etc.) is a **paid subscription**. Your existing licenses and billing remain unchanged.

   * **Under Zero Trust Access \> Application:** 

      * Publishing Web Applications via the Application Gateway is part of the "Application Gateway" feature module. Your existing licenses and billing for this feature also remain unchanged.


<span id="b04e3cc7"></span>
## **Contact Us**

If you encounter any issues while exploring the new Admin Console, please feel free to [submit a ticket](https://console-stable.volcadocean.com/workorder/list/). Our technical support team will respond promptly to provide assistance.

Thank you for your continued support of SealSuite. We are confident that this upgrade will bring you a more efficient and convenient management experience.

<span id="b310f97b"></span>
## **Appendix I**

The locations for data dashboards from the previous homepage overview are as follows:


|Previous Location |New Location |
|---|---|
|Homepage \-\> VPN Daily Peak |Dashboard \-\> Network \-\> VPN \-\> VPN Daily Peak |
|Homepage \-\> Office Network Peak |Dashboard \-\> Network \-\> Network admission status \-\> Office Network Peak |
|Homepage \-\> Endpoint Security \-\> DLP alerts |Dashboard \-\> Security \-\> DLP \-\> Top 10 Risky Employees |
|Homepage \-\> Endpoint Security \-\> Risk alerts |Dashboard \-\> Security \-\> Other Data \-\> Endpoint Security \-\> Risk alerts |
|Homepage \-\> Warning |Dashboard \-\> Endpoints \-\> Hardware Occupancy \-\> Warning |


<span id="12dc7711"></span>
## **Appendix II**

**Complete New vs. Old Navigation Mapping**

<span id="426d7aaf"></span>
### **Homepage & Dashboard**


|New Navigation Path |Old Navigation Path |
|---|---|
|Home |Home |
|Dashboard |Home \-\> "Device" tab, "Security" tab, "VPN" tab |


<span id="e70d9641"></span>
### **Identity**


|New Navigation Path |Old Navigation Path |
|---|---|
|Identity \-\> Directory |Identity \-\> User Directory |
|Identity \-\> Roles |Identity \-\> User Roles |
|Identity \-\> Account Setup |Identity \-\> Settings |
|Identity \-\> Multi\-Tenant |Identity \-\> Multi\-Tenant |
|Identity \-\> SSO |Application \-\> App Gateway |


<span id="e23dd203"></span>
### **Endpoint**


|New Navigation Path |Old Navigation Path |
|---|---|
|Endpoint \-\> Assets \-\> Asset List |Device \-\> Device Assets \-\> Asset List |
|Endpoint \-\> Assets \-\> Security Posture |Security \-\> Dynamic Control \-\> Risk Events |
|Endpoint \-\> Assets \-\> Enrollment |Device \-\> Device Assets \-\> Asset Enrollment |
|Endpoint \-\> Endpoint Control \-\> Endpoint Baseline |Device \-\> Device Control \-\> Device Baseline |
|Endpoint \-\> Endpoint Control \-\> Patch Management |Device \-\> Device Control \-\> Patch Management |
|Endpoint \-\> Endpoint Control \-\> Endpoint Network Control |Device \-\> Device Control \-\> Endpoint Network Control |
|Endpoint \-\> Software \-\> (All tabs) |Device \-\> Software \-\> (All tabs) |
|Endpoint \-\> MDM \-\> (All tabs) |Devce \-\> MDM \-\> (All tabs) |


<span id="8058bafe"></span>
### **Endpoint Security**


|New Navigation Path |Old Navigation Path |
|---|---|
|Endpoint Security \-\> Anti\-Virus \-\> Audit Logs |Security \-\> Anti\-Virus \-\> Audit Logs |
|Endpoint Security \-\> Anti\-Virus \-\> Policy Management |Security \-\> Anti\-Virus \-\> Control Policy |
|Endpoint Security \-\> Endpoint Firewall \-\> Audit Logs |Device \-\> Device Control \-\> Endpoint Firewall ("Audit Logs" tab) |
|Endpoint Security \-\> Endpoint Firewall \-\> Policy Management |Device \-\> Device Control \-\> Endpoint Firewall ("Policy Management" tab) |
|Endpoint Security \-\> Threat Intelligence |Security \-\> Threat Intelligence |


<span id="9b7710b8"></span>
### **DLP**


|New Navigation Path |Old Navigation Path |
|---|---|
|DLP \-\> Risk Employee |Security \-\> DLP \-\> Insider Risk |
|DLP \-\> eDiscovery |Security \-\> DLP \-\> eDiscovery |
|DLP \-\> File Transfer Control |Security \-\> DLP \-\> The "File"\-related sections from "DLP Alerts" and "Control Policy" |
|DLP \-\> Channel Block Control |Security \-\> DLP \-\> The "Channel"\-related sections from "DLP Alerts" and "Control Policy" |
|DLP \-\> Watermark |Security \-\> DLP \-\> Watermark |
|DLP \-\> Removable Endpoint |Security \-\> DLP \-\> Removable Device |


<span id="e0f9f4c5"></span>
### **NAC**


|New Navigation Path |Old Navigation Path |
|---|---|
|NAC \-\> (All tabs) |Network \-\> Wi\-Fi \-\> (All tabs) |


<span id="d182016b"></span>
### **Zero Trust Access**


|New Navigation Path |Old Navigation Path |
|---|---|
|Zero Trust Access \-\> Gateway Config \-\> Online Endpoints |Network \-\> VPN \-\> Online Devices |
|Zero Trust Access \-\> Gateway Config \-\> VPN Gateway |Network \-\> VPN Management \-\> VPN Gateway |
|Zero Trust Access \-\> Gateway Config \-\> App Gateway |Application \-\> App Gateway ("Gateway" tab) |
|Zero Trust Access \-\> Gateway Config \-\> Access Logs |Application \-\> App Gateway ("Access Log" tab) |
|Zero Trust Access \-\> Gateway Config \-\> Certificate |Application \-\> App Gateway ("Certificate" tab) |
|Zero Trust Access \-\> Application \-\> VPN App |Network \-\> VPN \-\> ACL Policy ("Network Resources" tab) |
|Zero Trust Access \-\> Application \-\> Web App |Applications published via App Gateway in `Application` \-\> `SSO` |
|Zero Trust Access \-\> VPN \-\> ACL Policy |Network \-\> VPN \-\> Access Policy |
|Zero Trust Access \-\> VPN \-\> Access Policy |Network \-\> VPN \-\> ACL Policy ("Access Policy" tab) |
|Zero Trust Access \-\> VPN \-\> Settings |Network \-\> VPN \-\> Settings |


<span id="63562a0e"></span>
### **SD\-WAN, Dynamic Control & Agent Release**


|New Navigation Path |Old Navigation Path |
|---|---|
|SD\-WAN \-\> (All tabs) |Network \-\> SD\-WAN \-\> (All tabs) |
|Dynamic Control \-\> (All tabs) |Security \-\> Dynamic Control \-\> (All tabs) |
|Agent Release \-\> (All tabs) |Agent \-\> (All tabs) |


<span id="558e4ce9"></span>
### **Enterprise Settings, Branding & Audit Logs**


|New Navigation Path |Old Navigation Path |
|---|---|
|Enterprise Settings \-\> Company General |Settings \-\> System Settings \-\> System Settings |
|Enterprise Settings \-\> Admin Access |Settings \-\> System Settings \-\> Admin Access |
|Enterprise Settings \-\> Admin Center |* Settings \-\> IT Application (User Feedback & Help Center)<br><br>* Admin Center ("Approval Center" tab) |
|Enterprise Settings \-\> Workflow |Workflow \-\> Workflow |
|Enterprise Settings \-\> Versions |Versions |
|Branding |Settings \-\> System Settings \-\> Branding |
|Audit Logs |Settings \-\> System Settings \-\> Audit Logs |


<span id="8c94bc14"></span>
### **Settings**


|New Navigation Path |Old Navigation Path |
|---|---|
|Settings \-\> Integration |Settings \-\> Integration |
|Settings \-\> System Settings |Settings \-\> General Settings |
|Settings \-\> Resources |Settings \-\> Resources |
|Settings \-\> IT Tools |Settings \-\> IT Application \-\> Quick Tools |
