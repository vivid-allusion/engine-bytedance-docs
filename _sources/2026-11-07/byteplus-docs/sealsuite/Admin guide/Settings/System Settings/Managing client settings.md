---
title: "Managing client settings"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-client-configuration"
---

This guide explains how to configure key security and operational policies for the SealSuite client. By managing settings like anti\-tampering, auto\-start, and network awareness, you can enhance the security and stability of your digital work environment.

<span id="4751fbad"></span>
# Key Features


* **Anti\-Tampering:**  Protects the client from unauthorized sign\-outs or uninstalls by requiring a password. This is critical for ensuring that security policies remain active and corporate data stays protected.

* **Windows Driver Master Switch:**  Provides an administrator\-level kill switch for the client drivers on Windows devices. This can be used to troubleshoot system stability issues without needing to uninstall the client.

* **Boot Up Configuration:**  Ensures the **SealSuit Client** launches automatically when a device starts up, guaranteeing that employees are connected and protected from the beginning of their session.

* **Intranet Detection:**  Allows the client to automatically detect its network environment (e.g., corporate intranet vs. external network) and adapt its behavior accordingly.

* **Anonymous Mode:**  Enables security policies (like DLP and Antivirus) to remain active even when an employee is not signed into the client. This maximizes security policy coverage across all devices.


<span id="1bf9b17d"></span>
# Common Use Cases


* **Protecting Sensitive Data:**  In regulated industries like finance or legal, configuring **Anti\-Tampering** is essential. It prevents users or malware from disabling the client, ensuring that data protection policies are always enforced.

* **Ensuring Continuous Connectivity:**  For critical operations, such as in healthcare, **Boot Up Configuration** and **Anti\-Tampering** guarantee that the client is always running, so staff can receive important communications without interruption.

* **Maintaining System Stability:**  In large\-scale deployments like schools or corporations, **Boot Up Configuration** and **Intranet Detection** ensure a consistent and stable user experience, regardless of the network environment.


<span id="14d7911b"></span>
# How to Configure Anti\-Tampering


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Client Settings**.

3. Click the **Logout Password**/**Anti\-Tampering** tab.

   * The **Configuration Version** at the top of the tab is a timestamp that updates when you save changes. You can compare this to the version on a client to verify if its policies are up\-to\-date.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a316723100b34ee8b190ac45cc4adbdc~tplv-goo7wpa0wc-image.image) </span>

4. Enable the **Logout Password** or **Anti\-Tampering**toggles:

   * **Logout Password:**  Requires users to enter the universal password to sign out of their account. It also prevents account switching if a user's session expires. This feature cannot be enabled if "Anonymous Mode" is active.

   * **Anti\-Tampering:**  Requires users to enter the universal password to uninstall the client. On Windows, this also prevents the SealSuite process from being terminated. On Linux, it disables command\-line uninstallation.

5. After enabling either feature, configure the following:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Password type (Same password will be used for logout and uninstallation)**  |* **Universal password**: SealSuite automatically generates a universal exit/uninstall password, and displays it under the **Universal password** option. You can view and copy the password.<br><br>* **One password per User**: In this option, all devices that belong to a single user have the same exit/uninstall password. To view the password, you need to navigate to the **General** tab of the relevant device in the Device List module.<br><br>* **One password per device**: In this option, the exit/uninstall password for each device varies. To view the password, you need to navigate to the **General** tab of the relevant device in the Device List module. |
   |**Password for logout and uninstallation** |The system\-generated password (for the Universal option). |
   |**Expiration period**  **(Same password will be used for logout and uninstallation)**  |In this option, you can set the corresponding validity period of the exit/uninstall password according to the effective scope that you have selected. Detailed descriptions are as follows:<br><br><br>* **Universal password**: The universal password is unmodifiable and will be refreshed every 15 minutes.<br><br>* **One password per User**: The password will be refreshed every 15 minutes by default. You can also modify the default time period and set it to **1 day**, **3 days**, or **7 days**.<br><br>* **One password per device**: The password will be refreshed every 15 minutes by default. You can also modify the default time period and set it to **1 day**, **3 days**, or **7 days**. |
   |**Password contact** |Click **Edit** to designate an administrator as the point of contact for passwords. Employees can contact this admin to request the password when needed. |
   |**Scope for enabling logout password and anti\-tampering** |By default, this policy applies to everyone. You can enable this to restrict the policy to a specific scope of users or devices. (Does not apply to users in the global allowlist). |
   


<span id="571b1a84"></span>
# How to Configure the Global Driver Control (Windows)


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Client Settings**.

3. Click the **Windows Driver Master Switch** tab.

4. Enable or disable the toggle switch:

   * **Enabled (Default):**  The SealSuite client drivers are active.

   * **Disabled:**  Disables the drivers. Use this for troubleshooting widespread blue screen issues. When disabled, self\-protection and peripheral control features will not function.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The switch will automatically re\-enable itself after 15 minutes.      </div>
      

<span id="b7c1f485"></span>
# How to Configure Auto\-Start


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Client Settings**.

3. Click the **Boot Up Configuration** tab.

4. Enable or disable the main toggle:

   * **Enabled:**  The SealSuite will launch automatically when the device starts up.

   * **Disabled:**  The client will not launch automatically.

5. (Optional) Click **Edit** to define the startup behavior.


<span id="87a6aab7"></span>
# How to Configure Intranet Detection


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Client Settings**.

3. Click the **Intranet Detection** tab.

4. Enable or disable the main toggle:

   * **Enabled:**  The client will periodically check its network environment based on your configuration.

   * **Disabled:**  Network\-aware policies will not function.

5. If enabled, configure the following:

   
   |**Parameter** |**Description** |
   |---|---|
   |Detection scheme |Choose when to check the network.<br><br><br>* **Real time**: The check runs automatically whenever a change in the network adapter is detected. Ideal for mobile users.<br><br>* **Scheduled:**  The check runs at a fixed interval (in minutes). |
   |Detection method |Choose how to identify the corporate network.<br><br><br>* **Based on internal IP of FQDN:**  Provide a list of internal server hostnames (e.g., `intranet.example.com`). If the client can connect to any of them, it is considered on the intranet.<br><br>* **Based on internal IP:**  Provide one or more IP ranges. If the client's IP address falls within one of these ranges, it is considered on the intranet.<br><br>* **Based on DNS address:**  Provide the IP address(es) of your internal DNS servers. If the client is using one of these DNS servers, it is considered on the intranet. |
   


<span id="d23bb2f1"></span>
# How to Configure the Client to Run Without Login

This feature allows critical security policies to run even when a user is not signed into the SealSuite client, maximizing your security coverage.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Client Settings**.

3. Click the **Anonymous Mode** tab.

4. Enable the **The policy will still take effect even if the client has not logged in with real\-name authentication.**  toggle.

   * **When Enabled:**  The client runs in a low\-privilege, unauthenticated state. Security features like DLP, Anti\-virus, and Dynamic Control remain active. Users can still sign in if they need to access features like VPN. Click **Enabled Features** to see a full list.

      * Note: This feature is incompatible with the **Anti\-Tampering** setting.

   * **Account Association Priority:**  When the client is running without a login, SealSuite needs to associate the device with a user account to apply the correct policies. Drag and drop to set the priority for how this is determined (e.g., Last Logged\-in User, AD Domain Account). If a device has never been logged into, a **Fallback Account** is used.

   * **Scope:**  Define which users, roles or departments this feature applies to.

   * **When Disabled:**  The client must be logged in to function.
