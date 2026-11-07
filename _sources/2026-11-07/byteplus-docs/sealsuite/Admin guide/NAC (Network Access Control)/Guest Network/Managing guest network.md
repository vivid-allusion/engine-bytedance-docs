---
title: "Managing guest network"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-guest-wi-fi"
---

After setting up a guest Wi\-Fi network, you can manage access requests and configure the network's general settings from the Admin Console.

<span id="2d24fee4"></span>
# Prerequisite

You must have already created a guest Wi\-Fi network in the Admin Console. For details, see [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router).

<span id="e055d1b7"></span>
# Configuring general guest Wi\-Fi settings


1. Log in to the Admin Console.

2. From the left navigation bar, go to **NAC** \> **Guest Network**.

3. Click the **General Settings** tab.

4. In the top\-right corner, click **Edit**, complete the following configurations and click **Save**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Guest Wi\-Fi Name |A custom name to identify the current guest Wi\-Fi network. This name must be the same as the guest SSID in **NAC** \> **Config** \> **SSID**. It appears on the guest network access page and in SMS notifications, but does not affect authentication. |
   |Applicant scope |Define which employees can request or approve guest Wi\-Fi access. You can select **All** or scope it to **Selected** members by Department, User, or Role. |
   |Guest authentication type (apply to all devices) |Choose between **Portal** or **PEAP**.<br><br><br>* **Portal authentication**: After a guest connects to Wi\-Fi, the phone or computer automatically opens a browser\-based authentication page. This protocol supports flexible access methods such as employee\-assisted QR code scanning and guest SMS self\-service. It is suitable for temporary visitors, meeting attendees, or for QR code scanning at the front desk.<br><br>* **PEAP authentication**: When a guest connects to Wi\-Fi, the operating system directly opens its native account and password prompt, without requiring a browser. PEAP authentication provides physical\-layer blocking based on the 802.1X protocol (Layer 2 authentication) and offers stronger security. It is suitable for long\-term on\-site partners, outsourced staff, or specific office areas with strict security requirements. |
   |Guest authentication method |Manage the authentication methods displayed on the Portal authentication page and their order. You can drag the icon at the beginning of each row to reorder the methods.<br><br><br>* **Account password**: Guests authenticate by entering their account or phone number and password. Additional settings are supported.<br><br>   * **Select account type**: Select **Account**, **Phone number**, or both. You can set one option to **Priority display** so that it appears first in the input box.<br><br>   * **Select notification method**: Select **SMS** or **Notification from corporate employee**.<br><br>* **SMS verification code**: Visitors apply for guest Wi\-Fi by using a mobile number verification code.<br><br>* **Scan the Code**: After an employee applies, visitors can quickly connect to the network by scanning a QR code. For **Placement**, select **Main Authentication Area** or **Backup Authentication Area**. |
   |General Settings |Configure **Mobile Phone Number Area Code Settings** for the country/region codes available when guests enter a mobile number on the Portal authentication page.<br><br><br>* **Select network devices**: Select **All network devices** or **Some Network Devices**. If you select **Some Network Devices**, select authentication devices that have been connected to SealSuite from the drop\-down list. For details, see [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router). You can configure separate area code rules for devices in different office locations.<br><br>* **Default area code**: After this option is enabled, visitors can select the area code and enter their phone number. After this option is disabled, the area code option is hidden, and the system uses the selected default country/region code for verification.<br><br>* **Select country/region**: Set the country/region code that is selected by default or automatically used when the option is hidden.<br><br>* **Alternative Mobile Phone Number Area Code**: Select one or more alternative area codes and sort them. The visitor\-side drop\-down list displays area codes in the order configured here. |
   |Guest Information Record |Enable this to require guests to provide additional information during login, such as their **Phone number**, **Visit time**, or **Reason** for visit. This data is logged in the request history. |
   |Verify inviter information |When enabled for **Account password** or **SMS verification code** methods, guests must provide information about their employee host (e.g., name, employee ID, or email) to connect. |
   |Expiration |Set the default duration for guest access. The actual session lifetime is determined by the shortest of this value, the guest account's validity, and the network device's session timeout. |
   |Concurrent device limit |The maximum number of devices a single guest account can connect simultaneously (up to 10). |
   


<span id="855d55d2"></span>
# Create a Visitor Account in the Admin Console

In addition to employee\-submitted applications and visitor self\-service applications, administrators can proactively pre\-create visitor accounts in the Admin Console. This feature is suitable for scenarios such as centralized onboarding of a large number of visitors or partners. It helps IT personnel prepare network access credentials in advance, reducing visitor waiting time after they arrive on site and improving office operations efficiency.


1. Log in to the Admin Console.

2. In the left navigation pane, choose **NAC** \> **Guest Network**.

3. On the **Request Records** tab, click  **+ Create New Account** in the upper\-right corner.

4. In the **1 Account Settings** step of the **Create New Account** pop\-up window, complete the following settings and click **Next Step**.

   
   |Configuration Item |Description |
   |---|---|
   |**Guest Wi\-Fi account / password** |1. **Select a format**: Use a custom **Account** or **Phone number** as the network access identifier.<br><br>2. **Enter the account and password**: Manually enter them or click the refresh icon to generate them randomly. The account supports a combination of numbers and English letters, with 2 to 15 characters. If you customize the account, make sure it is globally unique. The password is a 6\-digit number by default.<br><br>3. **Add credentials**: Click  **+**  **Add Credentials** to create multiple accounts in one task, up to 5 accounts. |
   |**Valid period** |Set the effective start and end time of the account. Custom date and time settings and quick options are supported. |
   |**Limit the number of terminals** |After this is enabled, you can separately limit the number of terminals that can connect using this account, from 1 to 10. If this is disabled, the configuration in **Execute per global configuration, without time limits** is applied. |
   |**Applicant** |Search for and select the internal responsible employee corresponding to this account. |
   |**Purpose** |Select a preset purpose from the drop\-down list, such as meeting or customer reception. |
   |**Remarks** |Enter any additional information to note for this account. |
   

5. In the **2 Preview** step, verify the account information. You can click the copy icon on the right of each information item to manually distribute it to visitors.

6. Click **Save** to complete the creation.


<span id="38393f6c"></span>
# Viewing and managing

guest network request logs

Administrators can centrally manage created visitor accounts on the **Request Records** page, audit visitor access behaviors in real time, and perform batch operations or emergency interventions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/993dc459f3bc4fa5b484df4593a819a4~tplv-goo7wpa0wc-image.image) </span>


* **Audit records**: Filter and view guest application details, including request time, applicants (employees), methods, assigned passwords, mobile numbers, and arrival times.

* **Edit**: Modify the configurations of the guest account. Accounts in the **Expired** status cannot be edited.

* **Delete**: Permanently removes guest accounts that are no longer needed. This operation cannot be undone. Proceed with caution.

* **Disable (Forced Offline)** : For visitor accounts in the **Active** status, click **Disable** in the **Action** column to immediately disconnect the specified device. The account status changes to **Expired**. This feature requires the CoA port (Huawei default: 3799; Cisco default: 1700) to be correctly configured on the network device.

* **Change expiration dates in bulk**: Click **Change expiration dates in bulk** in the lower\-left corner of the list to change the validity periods of multiple accounts. The system automatically changes account statuses based on the configured time. For example, after you extend the validity period of an expired account, its status changes from **Expired** back to **Active**. Avoid setting an overly long validity period to reduce the risk of malicious use.
