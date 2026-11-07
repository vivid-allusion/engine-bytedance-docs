---
title: "Managing dumb terminals"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-dumb-terminals"
---

You can onboard and manage dumb terminals (such as printers, cameras, or IoT devices) to allow them to securely connect to your corporate wired network. Once a terminal is added, you can view its information and manage its access permissions from the Admin Console.

<span id="5c07a63d"></span>
# Prerequisite

You must have already configured a wired network in the Admin Console. For details, see [Adding a switch](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-switch).

<span id="49286aba"></span>
# **Adding a dumb terminal**


1. Log in to the Admin Console.

2. From the left navigation bar, go to **NAC** \> **Dumb Terminals**.

3. On the **Devices** tab, you can add terminals individually or in bulk.

   * **Option A: Add a Single Terminal**

      1. Click  **+ Add Device** in the top right corner.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d81d9c7c84b44658be5b3d75acf1331c~tplv-goo7wpa0wc-image.image) </span>

      2. In the dialog, fill in the following details and click **Confirm**.

         
         |**Parmeter** |**Description** |
         |---|---|
         |**Device Name** |A user\-friendly name to identify the dumb terminal. |
         |**Device Group** |Assign the terminal to a group for easier management. |
         |**MAC Address** |The dumb terminal's MAC address. You can enter a single address, a range (e.g., `aa:bb:cc:00:00:00-aa:bb:cc:ff:ff:ff`), or use a wildcard (e.g., `aa:bb:cc*`). |
         |**Effective Time Range** |Set a validity period for the terminal. It will be automatically deactivated upon expiration. You can also configure expiration reminder workflows. For details, see [Creating workflows](https://docs.byteplus.com/docs/sealsuite/creating-workflows). |
         |**Applicant** |The employee who owns or is responsible for this dumb terminal. |
         |**Remarks** |Any additional notes for identification. |
         

   * **Option B: Import Terminals in Bulk**

      1. Click **Batch Device Operations** \> **Device Batch Import**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de6ce73029a24c58b622bc0aed583e05~tplv-goo7wpa0wc-image.image) </span>

      2. Download the **Device import template**.

      3. Fill in the template with your dumb terminal information and save the file.

      4. Return to the Admin Console and upload the completed file.


<span id="cfdff178"></span>
# **Configuring access permissions**


1. Log in to the Admin Console.

2. Go to **NAC** \> **Dumb Terminals**.

3. Click the **Authorization** tab.

4. Choose a default mode:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f995fba651174c96890610605e8f475a~tplv-goo7wpa0wc-image.image) </span>

   * **Full:**  All registered dumb terminals can connect to the network by default.

   * **Restricted:**  Only dumb terminals matching a specific permission group can connect. **You must create at least one permission group in this mode.** 

5. (Optional) Click  **+ Add New Policy** to create a new permission group. Fill in the details and click **Confirm**.

   
   |**Section** |**Parameter** |**Description** |
   |---|---|---|
   |**General** |Policy name |A user\-friendly name for this permission group. |
   ||Priority |Determines the policy's execution order, from 0 to 100. **Higher numbers have higher priority.**  When a device connects, policies are evaluated in descending order of priority. The first policy that matches the device is applied, and no further policies are checked. If two policies have the same priority, the one that was most recently modified takes precedence. |
   |**Permission Group Policy** |Network permission |The RADIUS attributes to be returned to the network device upon successful authentication.<br><br><br>* **Web\-Based:**  Assign a VLAN using **Tunnel\-Pvt\-Group\-ID** (VLAN ID) or **VLAN Pool**.<br><br>* **Role\-Based:**  Assign a network role or ACL using **Filter\-ID**.<br><br>* **Custom\-Based:**  Define your own vendor\-specific attributes (VSAs). |
   |**Scope** |Scope |The **Device** or **Device Group** that this permission group applies to. |
   |**Advanced settings** |/ |(Optional) Restrict this permission group to specific RADIUS servers, network devices, or SSIDs. |
   


<span id="dc1197dd"></span>
# **Managing dumb terminals**


* **Enabling or disabling a terminal**

   On the **Device List** tab, you can use the **Enable** or **Disable** buttons in the **Action** column to control a dumb terminal's network access. A disabled terminal cannot connect to the network.

* **Editing or deleting a terminal**

   * To edit or delete a single terminal:

      On the **Devices** tab, click **More** in the dumb terminal's row and select **Edit** or **Delete**.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><em>Deleting a dumb terminal will immediately disconnect it from the network. This action cannot be undone.</em>      </div>
      

   * To delete terminals in bulk:

      1. Click **Batch Device Operations** \> **Batch Device Deletion**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33f9e73f5ef1442689cfc23bb6e61e3c~tplv-goo7wpa0wc-image.image) </span>

      2. Download the **Dumb terminals delete template**.

      3. Fill in the template with the MAC addresses of the dumb terminals you want to delete.

      4. Upload the completed file. The system will validate the MAC addresses.

      5. Review the validation results and click **Delete** to confirm. You can monitor the task's progress in the top\-right corner of the page.
