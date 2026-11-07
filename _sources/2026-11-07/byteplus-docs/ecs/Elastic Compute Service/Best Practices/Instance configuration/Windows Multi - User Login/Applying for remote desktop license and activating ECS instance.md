---
title: "Applying for remote desktop license and activating ECS instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Apply_for_Remote_Desktop_authorization_licenses_and_activate_the_Elastic_Compute_Service"
---

The grace period for remote desktop authorization is 120 days. If you do not activate the ECS instance with a license within this period, the multi\-user login feature will be unavailable. This topic describes the procedure for applying for a remote desktop license and activating the corresponding ECS instance.

<span id="YL6za7QS"></span>
## Prerequisites

You have [enabled the multi-user login feature](https://docs.byteplus.com/en/docs/ecs/Configure_multi-user_log_in_in_Windows_2019_operating_system_instance) in an ECS instance.

<span id="rIEI4EEy"></span>
## Procedure

This section uses Windows Server 2019 as an example. The actual paths may vary depending on your operating system.

<span id="SCXQT7Z6"></span>
### Step 1: Obtain the product ID


1.  [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon and select "Server Manager."

3. In the left navigation tree, select "All Servers", right\-click the target server, and select "RD Licensing Manager".

4. Right\-click the target server and select "Properties".

5. Configure the properties.

   1. Set "Connection Method" to "Web browser", and record the "Product ID" value.

   2. Select the "Required Information" tab, fill in the required information, and click "OK".


<span id="xrKDA3g8"></span>
### Step 2: Apply for a Remote Desktop license


1. Use any PC with internet access to visit the[ Microsoft Remote Desktop Licensing website](https://activate.microsoft.com/).

2. Select "Activate a license server" and then click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a8330902a3da2e9b2a9fc61e31cd359.png) </span>

3. In the "Product ID" field, enter the product ID you obtained in Step 1 along with other required information, and then click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_95291f51e6abdff6b89e70140714b6c7.png) </span>

4. After verifying the information, click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_af7c3ffbccca204539c0e42f730fd774.png) </span>

5. Record the server ID indicated in the red box, and then click "YES".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e44efae6f60ac78973ce086b5ebd2122.png) </span>

6. In the "License Program" field, select "Enterprise agreement". After verifying the other information, click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_230f4836e27fe9892aa07c8818563c78.png) </span>

7. After filling in the configuration information, click "Next".

   * Product Type: Product type. Please select the corresponding license based on the actual operating system platform version of the server. This document uses "Windows Server 2019 Remote Desktop Services Per User client access license" as an example.

   * Quantity: The maximum number of users that can log in simultaneously. This document uses "99" as an example.

   * Agreement Number: The agreement number. Enter the registration number of the Remote Desktop Services Client Access Licenses (RDS CALs) that you purchased from [Microsoft](https://www.microsoftstore.com.cn/software/software).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84068d9aaa85e1a6c4c624c2649a4589.png) </span>

8. After confirming the information is correct, click "Next".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_742fb4d34d535f204e9343f31b4d9eeb.png) </span>

9. Record the License Server ID and the License Key Pack ID, and then click "Finish" to complete the operation.


<span id="gJmrXi0b"></span>
### Step 3: Activate the ECS instance


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon and select "Server Manager."

3. In the directory tree on the left, select "All Servers," right\-click the target server, and select "RD Authorization Manager."

4. Right\-click the target server and select "Properties \> Activate Server".

5. Follow the wizard and click the "Next" button.

6. Select "Connection Method" as "Web Browser," and click the "Next Step" button.

7. Enter the License Server ID obtained in Step 2, and then click "Next".

8. Check the "Enable the License Installation Wizard immediately" option, and click the "Next Step" button.

9. Enter the License Key Pack ID obtained in Step 2, and then click "Next".

10. Click "Finish" to complete the configuration.


<span id="7gHN4cQQ"></span>
### Step 4: Configure the Remote Desktop Session Host authorization server.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows picture, and select "Server Manager".

3. In the directory tree on the left, select "All Servers", right\-click the target server, and choose "RD Licensing Diagnosis".

4. If the diagnosis result contains "Remote Desktop Session Host server licensing mode is not configured", follow the steps below to complete the configuration.

5. Click the Windows icon, and then select "Windows System \> Run".

6. In the dialog box, input `gpedit.msc` and press Enter to open the Local Group Policy Editor.

7. In the directory tree on the left, select "Computer Configuration \> Administrative Templates \> Windows Components \> Remote Desktop Services \> Remote Desktop Session Host \> Licensing", and complete the following configuration.

   * **Use the specified Remote Desktop license server.** 

      1. Right\-click "Use the specified Remote Desktop license servers", and select "Edit".

      2. Select "Enabled", and in the "License Server to Use" field, enter the private IP address or hostname of the current ECS instance.

      3. Click the "Apply" button, then click "OK" to complete the configuration.

   * **Set the Remote Desktop licensing mode**

      4. Right\-click "Set the Remote Desktop licensing mode" and select "Edit".

      5. Select "Enabled", and in the "Specify RD Session Host server authorization mode", set it to "Per User".

      6. Click the "Apply" button, then click "OK" to complete the configuration.

8. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to make the policy take effect.
