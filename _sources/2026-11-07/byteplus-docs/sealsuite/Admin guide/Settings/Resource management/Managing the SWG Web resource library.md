---
title: "Managing the SWG Web resource library"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/swg-web-resource-library-management"
---

The **Resource library** is a standardized component provided by the SealSuite Resource Management Center. It uses fingerprint identification and attribute classification on massive internet traffic to transform fragmented network connections into named resource objects. Administrators do not need to maintain cumbersome IP or domain lists — they can simply reference preset resource categories to quickly build granular web access control policies.

This document describes how to manage and maintain the web resource library, and how each resource library is used across different policy modules.

## How to access

1. Log in to the SealSuite Admin Console.

2. Go to **Settings** \> **Resources** \> **Resource Library** in the left navigation pane.

## Cloud Applications library

The Cloud Applications library identifies cloud applications and services accessed by employees, including personal cloud drives, collaboration tools, AI applications, AI model relay services, and more. Administrators can view built\-in applications or maintain custom applications, then use these resources in cloud application control and SSL decryption policies to configure access and decryption requirements.

### View built\-in applications

SealSuite provides built\-in application resources across categories such as enterprise management, marketing, development tools, security, e\-commerce, IT, and generative AI. Administrators can browse by category or search by application name or address to verify whether a service is already included.

1. In **Settings** \> **Resources** \> **Resource Library**, select **Cloud Applications**.

2. Expand **Built\-in app categories** and select the category to view.

3. In the list on the right, view the application names and their categories. To find a specific application, enter keywords in **Application name** or **Application address**.

For example, to view AI model relay services, select the **AI Model Relay Services** category. This category includes relay services included in SealSuite. Each relay service corresponds to one application. Multiple model addresses associated with the same relay service are merged into that application by domain name. Administrators can select the target relay service in a cloud application control policy to disable access or enable access auditing for specified employees or devices. For more information, see [Configure cloud application control policies](https://docs.byteplus.com/docs/sealsuite/configure-cloud-application-control-policies).

Built\-in resources are updated regularly by SealSuite. Built\-in relay service resources are also regularly synchronized to the Cloud Applications library. Administrators can view the latest update time and synchronization status in the upper\-right corner of the page.

### Add custom applications

If an internally developed system or specific business application is not covered by the built\-in library, administrators can manually add rules. Custom applications follow the same category management logic.

#### Step 1: Create a custom category

1. At the bottom of the left directory tree, click  **+ Create a custom category**.

2. Enter a category name and confirm. All custom applications must belong to a specific custom category.

#### Step 2: Add application entries

1. Select the target custom category in the left directory.

2. Click  **+ Add application** on the right side of the page.

3. In the popup, configure the following parameters:

   * **Application name**: The display name for the custom application.

   * **Classification**: Select the custom business category this application belongs to from the dropdown.

   * **Application address**: Enter the domain addresses or specific URL patterns associated with the application. You can enter multiple addresses. Press Enter after each entry, or separate them with commas.

4. Click **Confirm** to complete the creation.

### Manage resources

* **Edit and delete**: Administrators can **edit** or **delete** custom applications. Before deleting a custom application entry, ensure that all associated policy references have been removed — otherwise, the corresponding control logic will lose its matching target and become ineffective.

* **Use resources in policies**:

   * Associate with **cloud application control** policies: Configure access blocking or auditing for specified employees or devices to manage their use of personal cloud drives, collaboration tools, AI applications, and AI model relay services. For details, see [Configure cloud application control policies](https://docs.byteplus.com/docs/sealsuite/configure-cloud-application-control-policies).

   * Associate with **SSL decryption** policies: Used to define whether the system performs SSL/TLS decryption for specific applications. For details, see [Configure SSL decryption policies](https://docs.byteplus.com/docs/sealsuite/configure-ssl-decryption-policies).

## Web URL category library

The Web URL category library is the foundational resource for SSL decryption policies, web content filtering, and for configuring threat protection domains. The system classifies URLs into named categories based on site business attributes, industry affiliation, and security reputation.

### View built\-in categories

SealSuite provides a standard category library covering dozens of categories — including job search, online gaming, illegal content, and adult content.

* **Quick search**: Supports fuzzy search by **Category name** or **Website address** to check whether a specific address is already included in the system.

* **Why it matters**: When configuring control policies, administrators can simply select website categories to manage millions of similar sites, without needing to collect individual domain names.

* **Automatic updates**: Built\-in resource libraries are periodically updated by SealSuite. Administrators can view the "Last updated" time and sync status in the upper\-right corner of the page.

### Add custom website categories

Administrators can create proprietary URL collections based on organizational management needs (such as "Business partners" or "Company\-owned sites"). Custom categories follow the same category management logic.

#### Step 1: Create a custom category

1. At the bottom of the left directory tree, click  **+ Create a custom category**.

2. Enter a category name and confirm. All custom websites must belong to a specific custom category.

#### Step 2: Add addresses

1. Select the target custom category in the left directory.

2. Click  **+ Add address** on the right side of the page. The system supports the following two entry methods:

   * **Exact entry**: Enter domains (such as `example.com`) or wildcard domains (such as `*.example.com`) directly. Separate multiple addresses with commas.

   * **Regex entry**: Enter regular expression strings to match URLs with specific patterns. Separate multiple regex entries with line breaks.

      * **Regex testing**: Enter a specific URL in the **Test URL** field and click **Test** to verify that the regular expression accurately matches the target address and ensure the rule is valid.

3. Click **Confirm** to complete the addition.

### Manage resources

* **Edit all addresses**: Administrators can **edit** custom addresses. Click the **Edit all addresses** button to adjust all exact addresses and regex rules under a category in a single popup, which allows for quick deletion or addition of entries.

* **Delete addresses**: Only custom categories and addresses support deletion. Before deleting, ensure that all policy module references have been removed — otherwise, the related policies will lose their evaluation targets and become ineffective.

* **Use resources in policies**:

   * Associate with **web content filtering**: Enforce domain\-level access control, such as blocking or warning on "Entertainment" category websites. For details, see [Configure web content filtering policies](https://docs.byteplus.com/docs/sealsuite/configure-web-content-filtering-policies).

   * Associate with **SSL decryption** policies: Used to define whether the system performs SSL/TLS decryption for specific addresses. For details, see [Configure SSL decryption policies](https://docs.byteplus.com/docs/sealsuite/configure-ssl-decryption-policies).

   * Associate with **threat protection**: Reference categories within the "Threat protection domains" configuration to define the scope of advanced threat scanning. For details, see [Configure threat protection](https://docs.byteplus.com/docs/sealsuite/configure-threat-protection).
