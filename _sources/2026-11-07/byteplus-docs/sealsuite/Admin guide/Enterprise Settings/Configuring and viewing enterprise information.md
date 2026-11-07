---
title: "Configuring and viewing enterprise information"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-and-viewing-enterprise-information"
---

The Corporate General page allows you to manage your company profile, self\-signed root certificate, client installer packages, user agreements, and system time.

<span id="5fff560c"></span>
# How to Configure Enterprise Information


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Company General**.

3. On the **Company General** page, follow the instructions below to configure each section.


<span id="9a712882"></span>
## **Setting Your Company's Basic Profile**

Click **Edit** in the top\-right corner to modify your company's icon, full name, and short name. Click **Save** to apply your changes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c8dfb1875f94ff18d285290addbfee1~tplv-goo7wpa0wc-image.image) </span>

You can provide multi\-language versions for each field by selecting the language option to the right of the input box.

<span id="0e703ad7"></span>
## **Managing the Corporate Root Certificate**

Configuring your self\-signed root certificate involves two steps: creating the certificate and defining its automatic installation scope.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae8520add52b4d998b02f685f719a7f1~tplv-goo7wpa0wc-image.image) </span>


1. In section  **① Root Certificate**, click **Configure**. Enter a name for the root certificate and click **OK**.

   * **Root Certificate Name:**  We recommend using the format `EnterpriseID + Corp Root CA` (e.g., `Exampleid Corp Root CA`). The name can be up to 20 characters and supports uppercase/lowercase letters, numbers, and underscores.

2. In section  **② Certificate Auto\-Installation Scope**, click **Configure**.

3. Define the scope for automatic installation by choosing **Members** or **Devices**.

   * **For Members:**  Click **Add Member** and scope the policy by **Department** or **Role**.

   * **For Devices:**  Click **Add Device** and scope the policy by **Device**, **Operating System**, or **Group**.

   * Once configured, the system will automatically distribute and install the certificate on all in\-scope desktop clients (PC only).

   * **Troubleshooting:**  If automatic installation fails, you can install it manually. In section  **①** , click **Download Public Key** and distribute the file to employees for manual installation.

   * After installation, the **SealSuite Client** will report the certificate's status (e.g., **Installed**, **Not Installed**) back to the Admin Console, which you can view in the Endpoint Asset list. For details, see [Manage Endpoint Devices](https://www.google.com/url?sa=E&q=%2F4q5lwbix%2F3o3qvusk).


<span id="bdda6105"></span>
## **Managing Client Installation** Instructions

This section provides links and status information for your corporate portal and client installers.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df9627d8976c4c058549364f0c962b4c~tplv-goo7wpa0wc-image.image) </span>


* **Corporate Portal Domain:**  This status will show as **Configured** after you set your portal domain in **Operations Platform** \> **System Configuration** \> **Corporate Settings**.

* **Publish the installation package**: This status will show as **Configured** after you upload and publish a client installer package on the **Version Release** page.

* **Client Download Link:**  Copy and distribute this link to your employees. They can use it to download the appropriate SealSuite client for their device. Click **Reset** to generate a new download link if needed.


<span id="29756547"></span>
## **Managing the User Agreement and Privacy Policy**

<span id="7fc13af1"></span>
### Agreement Management

When employees log in to the SealSuite client, they must confirm that they have read and agreed to the **User Agreement** and **Privacy Policy**. Enterprises can customize the configuration based on their own business requirements after consulting their legal team to ensure compliance.

SealSuite supports delivering login agreements by tenant. By default, all tenants use the agreements of the Primary (Global) Tenant.


* **General Configuration**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/390a92231ffd4aa9b9b1d1954e3b59af~tplv-goo7wpa0wc-image.image) </span>

   * Click **Edit** to configure the Chinese and English versions of the enterprise **User Agreement** and **Privacy Policy** in the dialog box that appears. After completing the configuration, click **Confirm**.

   * Click **Delete** to delete the current agreement. Note that built\-in SealSuite agreements cannot be deleted.

   * Click  **+ Add** to add Chinese and English agreements. After editing, click **Confirm**.

* **Configure by Tenant**

   To configure tenant\-specific agreements, first purchase the **Multi Tenant** license. Then, click **Configure by Unit Management Agreement** to go to **Multi\-Tenant** page for configuration. For details, see [Multi-Tenant management](https://docs.byteplus.com/docs/sealsuite/managing-multi-tenant_configurations).


<span id="cbd6493b"></span>
### **Privacy Policy for Guest Wi\-Fi**

You can require guests to accept a privacy policy before connecting to your guest Wi\-Fi.

Enable the Privacy Policy for Guest Wi\-Fi feature and add your custom agreement. The policy takes effect immediately. Guests will be prompted to accept it before they can connect. You can **Edit**, **Delete**, or **Add** new agreements for the guest network here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a33a15aa5f5e430a87a911eed68b172a~tplv-goo7wpa0wc-image.image) </span>

You can disable this feature at any time using the toggle switch in the top\-right corner.

<span id="53daa43b"></span>
## **Managing System Time**

This section displays the current system time of the SealSuite Admin Console. It is critical that the server time and client time are synchronized for features like OTP (One\-Time Password) to work correctly. If the server time is incorrect, log in to the system console via SSH, configure an NTP server, and then restart the machine or all services.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf7a7bc4eb4b426eaf28b0cc68433854~tplv-goo7wpa0wc-image.image) </span>
