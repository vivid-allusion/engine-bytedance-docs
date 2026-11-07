---
title: "Managing address resources (domains and IPs)"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-address-resources"
---

In addition to bulk importing new domain and IP resources, the Admin Console provides a comprehensive set of tools for managing your existing network resources efficiently.

<span id="fe440875"></span>
# How It Works

The Address Management page is a centralized hub for managing all your network address resources. From here, you can add, edit, delete, and perform bulk operations on your domains and IPs to ensure optimal resource allocation and network security.

<span id="7c5c47e3"></span>
# **How to add address resources**

<span id="922eafd1"></span>
## **Adding a domain resource**

Use this task to add specific domain names to SealSuite, which can then be used in DNS configurations and other network policies.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Settings** \> **Resource** \> **Address Management**.

3. Click the **Domain Name** tab.

4. In the top\-right corner, click  **+ Add Domain Name**. Fill in the following and click **Confirm**.

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |Domain resource name |Yes |A user\-friendly name to identify this resource. |
   |Domain resource tag |No |Apply tags to categorize resources. You can select an existing tag or create a new one. |
   |Domain address |Yes |Enter the specific domain (e.g., `example.com`) or wildcard domain (e.g., `*.example.com`). Use commas or spaces to separate multiple entries. |
   


<span id="9f6d6ded"></span>
## **Adding an IP address resource**

Use this task to define static IP addresses or IP ranges for your network services.


1. Log in to the Admin Console.

2. Go to **Settings** \> **Resource** \> **Address Management**.

3. Click the **IP Address** tab.

4. In the top\-right corner, click  **+ Add IP Address**. Fill in the following and click **Confirm**.

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |IP resource name |Yes |A user\-friendly name to identify this resource. |
   |IP resource tag |No |Apply tags to categorize resources. You can select an existing tag or create a new one. |
   |IP address |Yes |Enter the specific IP address or CIDR range. Use commas or spaces to separate multiple entries. |
   


<span id="5b0fef17"></span>
## **Importing resources in bulk**

This feature allows you to add a large number of domain or IP resources at once from a template file, which is ideal for complex network environments.


1. Log in to the Admin Console.

2. Go to **Settings** \> **Resource** \> **Address Management**.

3. Select either the **Domain Address** or **IP Address** tab.

4. In the top\-right corner, click **Import**.

5. On the **Batch Resource Import** page, download the template file.

6. Open the template, fill it in with your resource information, and save it.

7. Return to the **Batch Resource Import** page, upload your completed template.


<span id="74dd0926"></span>
# **How to manage existing resources**

This section covers the day\-to\-day management of your domain and IP resources.


1. Log in to the Admin Console.

2. Go to **Settings** \> **Resource** \> **Address Management**.

3. Select either the **Domain Address** or **IP Address** tab.

4. Use the search bar at the top to find a specific resource by name or tag.

5. In the resource list, find the item you want to manage and use the **Action** column:

   * **Edit:**  Modify the resource's name, tags, or addresses.

   * **Delete:**  Permanently remove the resource.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You cannot delete a resource if it is currently being used by an active policy.      </div>
      

<span id="ce5c071c"></span>
# **How to export resources**

You can export your current list of domain or IP resources to a file for backup, auditing, or migration purposes.


1. Log in to the Admin Console.

2. Go to **Settings** \> **Resource** \> **Address Management**.

3. Select either the **Domain Address** or **IP Address** tab.

4. (Optional) Use the search bar to filter the list to the specific resources you want to export.

5. In the top\-right corner, click **Export**. The system will generate a file containing the current (or filtered) list of resources for you to download.
