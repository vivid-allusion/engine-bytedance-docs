---
title: "Best practices for Wi-Fi management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Best-practices-for-Wi-Fi-management"
---

This article is designed to provide IT administrators with a series of tutorials on office network configuration. Enterprise administrators can refer to the content of this article to customize and implement the SealSuite Wi\-Fi feature according to the specific needs of their enterprise.

<span id="b95e960b"></span>
# Feature overview

SealSuite provides its self\-developed RADIUS component for network access authentication and billing integration, supporting 802.1X authentication protocol\-compliant network services, ensuring network access security. Furthermore, to enhance the convenience of network access, SealSuite offers Portal authentication protocol\-compliant network services, freeing users from dependence on the SealSuite client and enabling one\-click network access.

The Admin Console's Wi\-Fi management function supports configuring corporate Wi\-Fi networks and wired networks and managing all employees' office network access rights. Once you have configured the Wi\-Fi or wired network in SealSuite according to the actual office environment, employees can connect to the office network with one click through the SealSuite client within the coverage area of the office network.

<span id="d51fb844"></span>
# Scenario One: Employees connect to the internet with one click (802.1X authentication)

<span id="c306b4e3"></span>
## Solution One: Configure staff Wi\-Fi (Wireless controller taking H3C as an example)

<span id="50b9856a"></span>
### **Scenario introduction**

In a digital office environment, the demands for network security and convenience are growing for enterprises. SealSuite's 802.1X authentication solution ensures the security of network access and enhances employees' work efficiency through a simplified one\-click connection. Employees can quickly and securely access the corporate network from any location covered by the office network through the SealSuite client.

This scenario introduces the configuration of 802.1X authentication access for Wi\-Fi networks, where you need to configure both on the SealSuite Admin Console and on the local wireless controller device.

<span id="1e50bd53"></span>
### **Procedure**


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. In the Wi\-Fi management module, add a RADIUS server, wireless router, and SSID.

   For specific operations, please refer to [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

3. Enter the management interface of the local wireless controller device (taking H3C as an example) and configure the RADIUS scheme.

   1. In the left navigation bar, select **Network Security** \> **Authentication**.

   2. Click on the RADIUS tab, and click on the plus sign (+).

   3. Add a RADIUS scheme.

      * The configured ports 1812 and 1813 must be consistent with the Staff Wi\-Fi ports set in the SealSuite Admin Console's RADIUS gateway configuration.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33e5f52d7a1b41749c114efdeb6adb1f~tplv-goo7wpa0wc-image.image) </span>

      * The shared key that is configured must be obtained from the wireless router settings in the SealSuite Admin Console.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/751e0c26f38046949efeb29ac07e0076~tplv-goo7wpa0wc-image.image) </span>

4. In the wireless controller, configure the ISP domain name and bind the RADIUS scheme.

   1. On the **Network Security** \> A**uthentication** page, click on the **ISP Domain** tab.

   2. Click on the plus (+) sign to configure the ISP domain name.

   3. In the **Actions** column of the specified domain name, click the edit icon and then bind the RADIUS scheme.

5. In the wireless controller, turn on 802.1X authentication and set the authentication method to EAP.

   1. In the left navigation bar, select **Network Security** \> **Access Control**, and click **Enable 802.1X**.

   2. Click the settings icon at the top right of the page.

   3. In the **Authentication Method** area, set it to **EAP**.

6. (Optional) Configure dynamic authorization in the wireless controller.

   If you've added the Dynamic Control feature to your SealSuite for Wi\-Fi management and created a policy group with specific trigger conditions and rules in client\-side management, you should then finalize the dynamic authorization setup on your local wireless controller.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have not configured dynamic authorization in the wireless controller, then when SealSuite downgrades Wi\-Fi for a specified terminal, re\-authentication needs to be carried out in the wireless controller, or the SealSuite client needs to actively disconnect the Wi\-Fi connection and reconnect.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If dynamic authorization is configured in the wireless controller, it is possible for SealSuite to proactively inform the wireless controller to adjust its privileges when a terminal triggers a policy group for Dynamic Control.   </div>
   

   1. Use SSH to log in to the wireless controller.

   2. Run the following commands in the command line to configure.

      ```Bash
      system-view
      radius dynamic-author server
      client ip <RADIUS server IP address> key simple <shared key>
      port 3799
      ```
      

      * The `RADIUS Server IP address` can be obtained from the corresponding RADIUS gateway in the SealSuite Admin Console.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dff142f3a5e1497d8e5c720ee846c936~tplv-goo7wpa0wc-image.image) </span>

      * The `Shared key` can be obtained from the corresponding wireless router in the SealSuite Admin Console.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/751e0c26f38046949efeb29ac07e0076~tplv-goo7wpa0wc-image.image) </span>

7. Create a Wi\-Fi service in the wireless controller and bind the corresponding access point devices.

   1. In the left navigation bar, select **Wireless Settings** \> **Wi\-Fi Networks**.

   2. On the **Wi\-Fi Networks** tab, click on the plus sign (+).

   3. Add a new Wi\-Fi service.

   4. In the Advanced Settings, bind the access point device.


<span id="25a3d8a8"></span>
### Results

After configuration, employees can simply open the SealSuite client and connect to the corporate Wi\-Fi with a single click without the need for complicated authentication steps.

<span id="802fe139"></span>
## Solution Two: Configure the wired network (Taking the H3C network switch as an example)

<span id="5446fca0"></span>
### **Scenario introduction**

Configuring wired network access with 802.1x authentication to achieve network admission control effects requires configuration in both the Admin Console and the local switches.

In the Admin Console, you need to add a RADIUS node, switches, and an SSID.

On the local switch, you should sequentially configure the RADIUS server, set up the ISP domain, enable 802.1x, configure port\-based 802.1x, configure MAC address\-based access control for ports, enable escape VLAN for ports, enable Guest VLAN for ports, and enable COA (Change of Authorization).

<span id="dcca5f48"></span>
### **Procedure**


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. In the Wi\-Fi management module, add a RADIUS server, wireless router, and SSID.

   For specific operations, please refer to [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

3. Log in to the local Network switch through SSH.

4. In the command line of the network switch, execute the following commands in sequence to complete the configuration.

   1. Configure the network switch's RADIUS server.

      ```Bash
      [H3C]radius scheme feilian_rd        #Create a RADIUS scheme and enter its view.
      [H3C-radius-feilian_rd]primary authentication 127.0.0.1 2812 #Configure the IP address and port of the primary authentication server.
      [H3C-radius-feilian_rd]key authentication admin@123          #Configure the authentication shared secret key.
      [H3C-radius-feilian_rd]primary accounting 127.0.0.1 2813     #Configure the IP and port of the primary accounting server.
      [H3C-radius-feilian_rd]key accounting admin@123              #Set the accounting shared secret key.
      [H3C-radius-feilian_rd]timer realtime-accounting 5           #Configure the accounting period.
      [H3C-radius-feilian_rd]user-name-format without-domain       #The username sent to the server does not include the domain name.
      [H3C-radius-feilian_rd]quit
      ```
      

   2. Configure the ISP domain.

      ```Bash
      [H3C]domain feilian_ad             #Create a domain and enter its view.
      [H3C-isp-feilian_ad]authentication lan-access radius-scheme feilian_rd  #Configure 802.1x to use the RADIUS scheme for authentication and authorization.
      [H3C-isp-feilian_ad]authorization lan-access radius-scheme feilian_rd
      [H3C-isp-feilian_ad]accounting lan-access radius-scheme feilian_rd    #Configure the billing plan as feilian_radius.
      [H3C-isp-feilian_ad]quit                        
      ```
      

   3. Globally enable 802.1x.

      ```Bash
      [H3C]dot1x                              #Enable the global 802.1X feature.
      [H3C]dot1x authentication-method eap    #Enable EAP relay mode.
      ```
      

   4. Configure ports with 802.1x.

      ```Bash
      [H3C]interface Ethernet 1/0/1                        #Enter the specified port view.
      [H3C-Ethernet1/0/1]port link-type hybrid             #It is recommended to use the hybrid port type to support dynamic VLANs.
      [H3C-Ethernet1/0/1]mac-vlan enable
      [H3C-Ethernet1/0/1]dot1x                             #Port enables 1x authentication.
      [H3C-Ethernet1/0/1]dot1x port-method macbased        #Use the MAC-based port mode to support multi-terminal access.
      [H3C-Ethernet1/0/1]undo dot1x handshake              #It is recommended to enable this to prevent frequent terminal handshakes and reconnections.
      [H3C-Ethernet1/0/1]undo dot1x multicast-trigger      #Enable this feature to prevent frequent re-authentication of terminals.
      [H3C-Ethernet1/0/1]dot1x unicast-trigger             #Enable this feature to shorten the 1x authentication trigger time.
      [H3C-Ethernet1/0/1]dot1x mandatory-domain feilian_ad #Configure the authentication domain that the port is forced to use; if not configured, the global default domain will be used.
      [H3C-Ethernet1/0/1]quit
      ```
      

   5. Configure access control based on the MAC address on the port.

      ```Bash
      [H3C]mac-authentication                        #Enable the global MAC authentication feature.
      [H3C]interface Ethernet 1/0/1
      [H3C-Ethernet1/0/1]mac-authentication          #Enable MAC address authentication for this port.
      [H3C-Ethernet1/0/1]mac-authentication domain feilian_ad   #Configure the authentication domain that is forced to be used for MAC authentication; if not configured, the global default domain will be used.
      [H3C-Ethernet1/0/1]quit
      [H3C]dot1x timer supp-timeout 30 #Set the 802.1x authentication timeout period, which is the time from when the M wireless controller starts the authentication process.
      ```
      

   6. Activate the escape VLAN on the port.

      ```Bash
      [H3C]interface Ethernet 1/0/1
      [H3C-Ethernet1/0/1]port hybrid vlan 100 untagged  #For example, VLAN 100 is set as the escape VLAN.
      [H3C-Ethernet1/0/1]dot1x critical vlan 100
      [H3C-Ethernet1/0/1]quit
      ```
      

   7. Activate the Guest VLAN on the port.

      ```Bash
      [H3C]interface Ethernet 1/0/1
      [H3C-Ethernet1/0/1]port hybrid vlan 0 untagged
      [H3C-Ethernet1/0/1]dot1x guest-vlan 0
      [H3C-Ethernet1/0/1]quit
      ```
      

   8. Enable COA.

      ```Bash
      [H3C]radius dynamic-author server
      [H3C]client ip 127.0.0.1  key simple admin@123
      ```
      


<span id="939bcf9d"></span>
### Results

After the configuration is completed, employees can use the company's wired network without going through cumbersome authentication steps.

<span id="ae2d52b0"></span>
# Scenario Two: Employee quick internet access (Portal authentication)

<span id="eafd21cd"></span>
## Scenario introduction

To meet the diverse network type needs of different enterprises, SealSuite offers a Portal\-based network access solution. This solution is suitable for enterprises that want to retain traditional login habits while enhancing the convenience of logging in. Through Portal authentication, employees can connect to Wi\-Fi and complete authentication through a simple web interface to access network services.

<span id="e2114ff5"></span>
## Procedure


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Wi\-Fi Management** \> **Staff Network**.

3. On the **Staff Network** page, click the **General Settings** tab.

4. In the top right corner of the **General Settings** page, you can click **Select Authentication Method** to add Portal authentication or switch to Portal authentication.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">SealSuite supports enabling both 802.1X authentication protocol and Portal authentication protocol simultaneously.   </div>
   

5. Next to authentication protocol, click **Expand,**  and in the top right corner of the expanded page, click **Edit,**  where you can adjust the following settings and click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e17b2b763be4ea3a1369c393fe29322~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Authentication method** |After clicking **Modify**, the page will automatically redirect to the **Authentication** tab in **Account Settings**. For specific configuration methods, see [Setting up account systems and identity authentication](https://docs.byteplus.com/docs/sealsuite/docs-managing-account-settings).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the Portal authentication protocol supports the configuration of employee network access authentication methods.</div><br> |
   |**Requires 2FA when employees log in to the corporate network** |After clicking **Modify**, the page will automatically redirect to the **MFA Setup** tab in **Account Settings**. For specific operations, please refer to [Configuring multi-factor authentication (MFA)](https://docs.byteplus.com/docs/sealsuite/docs-configuring-multi-factor-authentication-mfa-). |
   |**Detect SealSuite desktop client login using portal authentication** |* Enable feature: After enabling, before employees perform Portal authentication, the system will check if they have installed or logged into the SealSuite desktop. If it is detected that the employee has not installed or logged into the SealSuite desktop, the employee can contact the designated administrator.<br><br>* Administrator: Enter the name of the administrator, only one person can be added. After setting, when the system detects that an employee has not installed or logged into the SealSuite desktop, it will prompt the employee to contact this administrator; if not set, this prompt will not be displayed. |
   |**Device authentication expiration**<br><br>(You need to click on **Advanced Settings** to view this Configuration item.) |Select the validity period for device authentication, with a default of 7 days, options include **1 day**, **3 days**, and **7 days**. |
   


<span id="235f361b"></span>
## Results

After deploying the Portal network access solution, employees will automatically be prompted with the login page when connecting to Wi\-Fi. They can use the account information provided by the company, or log in quickly through methods like SMS verification code without the need to download any client.

<span id="51e613c2"></span>
# Scenario Three: Guest temporary internet access

<span id="b9cf873c"></span>
## Scenario introduction

SealSuite provides enterprises with a secure and convenient Guest Wi\-Fi solution, distinguishing between SSIDs for staff and guests to ensure corporate network security while optimizing the guest internet experience. SealSuite supports the simultaneous configuration of Guest Wi\-Fi and Staff Wi\-Fi, requiring only different SSID setups and backend integration settings. When guests connect to the SealSuite Guest Wi\-Fi, multiple login methods are supported:


* Short Messaging Service: send account details, liberating guests from manually entering complex credentials.

* QR code scanning: guests simply need to display the QR code to complete the login.

* SMS Self\-authentication: guests can enter their phone number to perform self\-authentication.


<span id="76d18f04"></span>
## Procedure


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Wi\-Fi** \> **Guest Wi\-Fi**.

3. On the **Guest Wi\-Fi** page, click the **General Settings** tab.

4. In the upper right corner of the page, click **Edit**, and complete the following settings, and click **Save**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Guest Wi\-Fi Name** |Custom name, used to identify the current guest Wi\-Fi. |
   |**Applicant scope** |Set the scope of employees who can apply for or authenticate guest access, options include **All** or **Selected** members. If **Selected** members are chosen, it is necessary to manage the scope by adding **Department**, **User**, or **Role** parameters. |
   |**Guest authentication type (apply to all devices)**  |Options include **Portal** or **PEAP**, where **Portal authentication** supports QR code and SMS Self\-Authentication. |
   |**Guest authentication method** |Upon selecting **Portal authentication**, the guest authentication method supports username & password, QR code, and SMS self\-authentication. After selecting **PEAP**, the guest authentication method only supports username & password:<br><br><br>* **Username & password**: The method where guests connect to Wi\-Fi by entering an account password. After setting this method, you will also need to specify the notification method for the account password, options include:<br><br>   * **SMS**: Send an SMS to inform the guest of the account and password.<br><br>   * **Notification from corporate employee**: After an employee requests guest Wi\-Fi access, they will notify the guest of the account and password.<br><br>* **QR code**: After an employee requests guest Wi\-Fi access, they can help guests connect to Wi\-Fi by scanning a code through the SealSuite mobile app.<br><br>* **SMS Self\-Authentication**: Upon arrival, guests authenticate independently by entering their mobile number to receive a verification code. This method requires no employee intervention. |
   |**Guest Information Record** |After enabling this feature, options such as **Phone number**, **Visit time**, and **Reason** are available for multi\-selection. Once selected, SealSuite will record the guest information when guests connect to Wi\-Fi, which will be displayed on the **Guest Wi\-Fi** \> **Request Records** page. |
   


<span id="ecc9cabb"></span>
## Results

Through SealSuite's Guest Wi\-Fi configuration, guests can quickly gain network access rights through simple SMS verification, QR code scanning, or self\-service authentication and other methods.

<span id="e7e44b9c"></span>
# Scenario Four: AD domain authentication access

<span id="42402a5f"></span>
## Scenario introduction

For enterprises that have deployed Microsoft AD, SealSuite provides a seamless network access solution. Employees can access the corporate network using their AD domain account and password through a single SSID. This solution utilizes Windows authentication components and protocols, forwarding authentication requests to the AD domain for validation, ensuring that only accounts with an exact match can successfully authenticate.

<span id="dee429e2"></span>
## Procedure


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Wi\-Fi Management** \> **Staff Network**.

3. On the **Staff Network** page, click the **General Settings** tab.

4. To the right of **802.1X Authentication Protocol**, click **Expand,**  and in the upper right corner of the expanded page, click **Edit**, where you can adjust the following settings and click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/405e0ad2d1c44a00baae11fada127f15~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration item** |**Description** |
   |---|---|
   |authentication method |* **Primary method**: Options include **User ID**, **Phone Number**, or **Email**. Only one option can be selected, by default, and the primary method is displayed to all employees.<br><br>* **Secondary method**: In addition to the primary method, you can select the remaining two alternatives. If the employee has not set a primary method, secondary method 1 and secondary method 2 will be displayed in sequence by priority.<br><br>* **WindowsAD Account**:<br><br>   * Activate feature: Once activated, SealSuite will add a WindowsAD account as an authentication method for network access, allowing employees to use both a SealSuite account and a WindowsAD account to connect to the network.<br><br>   * User Scope: You can click **Set** to adjust the scope of users for whom the WindowsAD account is effective.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To enable WindowsAD as the Staff Wi\-Fi verification method, you need to complete the synchronization settings of your Windows AD account first. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-">Integrating third\-party data sources</a>.</div><br><br><br>When employees use the SealSuite client login session timeout period for one\-click network authentication, the user ID, mobile, or Email address will be displayed as the Wi\-Fi account name. Here, User ID refers to the user's unique identifier, under the SealSuite account source, SealSuite will, by default, generate a user ID, which you can edit. For detailed information, please refer to [Managing users](https://docs.byteplus.com/docs/sealsuite/docs-managing-members). |
   |**Employee Wi\-Fi Configuration Guide** |If you are setting up the Employee Wi\-Fi feature for the first time, click on **Advanced Settings** below the section and then on **Configure** to understand the full network access process and complete configuration following the guidance in the popup. |
   |**Hide Password**<br><br>(This configuration item can be viewed only after clicking **Advanced Settings**.) |After enabling this feature, employees will not be able to retrieve the password of the account through the SealSuite client, they can only view the account, and support one\-click connection to the network through the client. In addition, you can set an **Administrator**. Administrator settings effect description:<br><br><br>* After setting the **Administrator**, the information will be displayed on the SealSuite client, and employees can contact the administrator to request the password.<br><br>* If an **Administrator** is not set, the administrator information will not be displayed in the SealSuite client. |
   |**Windows wired network identification method**<br><br>(This configuration item can be viewed only after clicking **Advanced Settings**.) |Configure the effective account after connecting to a wired network in Windows OS.<br><br><br>* If you select **All system accounts**, network permission is identified based on connected devices, and switching system accounts does not affect the network connection status.<br><br>* If you select **Current system account**, network permission is identified based on the system account, and switching system accounts requires reconnection to the network. |
   |**Forget guest Wi\-Fi SSID after employee network connection**<br><br>(This configuration item can be viewed only after clicking **Advanced Settings**.) |Upon enabling this feature, you must add a designated guest Wi\-Fi SSID. When employees connect to the corporate employee network with one click, the guest Wi\-Fi SSID will be automatically forgotten. Once forgotten, it will no longer connect to that Wi\-Fi automatically. |
   |**Require 2FA for network access**<br><br>(This configuration item can be viewed only after clicking **Advanced Settings**.) |Clicking **Modify** will automatically redirect you to the **Account Settings** under the **MFA Setup** tab, for detailed setup methods, please refer to [Configuring multi-factor authentication (MFA)](https://docs.byteplus.com/docs/sealsuite/docs-configuring-multi-factor-authentication-mfa-). |
   |**Customize employee network access page**<br><br>(This configuration item can be viewed only after clicking **Advanced Settings**.) |After clicking **Configure**, the page will automatically redirect to the **Customize employee network access page**, for the specific configuration method, please refer to [Customizing employee Wi-Fi page content](https://docs.byteplus.com/docs/sealsuite/docs-customizing-employee-wi-fi-page). |
   


<span id="80d0f002"></span>
## Results

After completing the AD domain account network access configuration, employees can use their familiar AD account and password to authenticate the network through the SealSuite system.

<span id="ca8c400f"></span>
# Scenario Five: Unified network access authentication for multi\-location offices

<span id="9c4e6a64"></span>
## Solution One: Deploy the RADIUS service in the public cloud, exposing the authentication and accounting ports

<span id="1c211de9"></span>
### **Scenario introduction**

For enterprises with multiple office locations, achieving unified network access management and authentication is a challenge. SealSuite's unified network access authentication solution, whether it is deployed through the public cloud RADIUS service, and opens up external network open certification and accounting port, or configuring wireless controller devices or network switches separately in each office area, and associating them with the open authentication and billing ports of the RADIUS server, can achieve unified network access management.

<span id="b5a219b0"></span>
### **Procedure**


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. In the Wi\-Fi Management module, configure the RADIUS Gateway.

3. Configure wireless routers (or network switches) and SSIDs separately in different office areas.

   The configuration methods for Wi\-Fi networks and wired networks are different:

   * Under RADIUS Gateway, configure wireless routers and SSIDs that match the number of office areas, and configure device information according to the actual conditions of each office area. For specific configuration operations of RADIUS gateway, wireless routers, and SSIDs, please refer to [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router) and [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

   * Configure network switches and SSIDs under the RADIUS gateway to match the number of office areas and configure peripheral information according to the actual situation of each office area. For detailed configuration operations regarding RADIUS gateways, Network switches, and SSIDs, please refer to [Adding a switch](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-switch) and [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring a network switch for a wired network, 802.1X authentication should be set up at the access layer rather than at the aggregation layer or core layer, to ensure the switch can communicate properly with SealSuite's RADIUS gateway.   </div>
   

<span id="4dd37081"></span>
### Results

After deployment, the company will have a centralized network authentication system. Whether through cloud deployment or on\-site deployment of RADIUS service, employees can access the network with one click through the client login session timeout period at any office location.

<span id="8d380bcf"></span>
## Solution Two: Deploy the RADIUS service in each office

<span id="192779c4"></span>
### **Scenario introduction**

In a multi\-site office corporate environment, ensuring the consistency and security of the network is crucial. SealSuite's solution allows companies to deploy local RADIUS service nodes independently at each office location, realizing localized network authentication and management. This distributed deployment strategy not only reduces dependence on the central server but also improves the network's response speed and reliability, ensuring that, even in the event of network segmentation or failure, the network services in each office area can operate independently and ensure business continuity.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This solution requires your SealSuite to support the creation of multiple RADIUS gateways. If your current gateway quota is insufficient for the actual configuration needs, additional gateways can be allocated.</div>


<span id="0878ada5"></span>
### **Procedure**


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. Configure RADIUS Gateway, wireless routers (or network switch), and SSID.

   1. Configure the corresponding RADIUS Gateway in each office area.

   2. In the RADIUS Gateway of each office area, configure the Wi\-Fi networks (or network switch), and the SSID.

      The configuration method for Wi\-Fi network and wired network is different:

      * Under the RADIUS gateway, configure wireless routers and SSID, and configure device information according to the actual situation of each office area. For specific configuration operations of RADIUS Gateway, wireless routers, and SSID, please refer to [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router) and [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">When configuring the RADIUS service in local wireless controller devices within each office area, it is necessary to fill in the relevant information of the local office area's RADIUS gateway.         </div>
         

      * Under the RADIUS gateway, configure network switch and SSID, and configure device information according to the actual situation of each office area. For detailed configuration operations on the RADIUS gateway, Network switch, and SSID, please refer to [Adding a switch](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-switch) and [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).


<span id="5a5c379e"></span>
### Results

After deployment, each office area will have its own RADIUS service node responsible for handling authentication requests from all devices within the area. Employees use the SealSuite client to initiate one\-click network access at their respective office locations, and authentication requests are directly sent to the local RADIUS service node, thus achieving quick authentication and network access.

<span id="aa7fc2a7"></span>
## Solution Three: Deploy the RADIUS service in one of the offices (when the internal networks are not interconnected)

<span id="05033df8"></span>
### **Scenario introduction**

In some enterprises, due to security policies or network architecture constraints, the networks between different office areas are not interconnected. In response to this situation, SealSuite's solution is to deploy a RADIUS service node in one central office area and expose its authentication and accounting port to the external network, allowing for remote access and authentication from other office areas. In this way, even if the internal networks are not interconnected, unified network authentication and management can be achieved.

<span id="664efb0d"></span>
### **Procedure**


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. Configure RADIUS Gateway in the designated office area.

3. Configure wireless routers (or network switches) and SSIDs in different office areas respectively.

   The configuration methods for Wi\-Fi networks and wired networks are different:

   * Under the RADIUS gateway, configure wireless routers and SSIDs equal to the number of offices, and configure the device information according to the actual conditions of each office. For detailed configuration operations of RADIUS gateway, wireless routers, and SSIDs, please refer to [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router) and [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

   * Configure network switches and SSIDs under the RADIUS gateway to match the number of offices and configure peripheral information according to the actual situation of each office. For detailed configuration operations of RADIUS gateway, network switches, and SSIDs, please refer to [Adding a switch](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-switch) and [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring a network switch for a wired network, 802.1X authentication should be set up at the access layer rather than at the aggregation layer or core layer, to ensure the switch can communicate properly with SealSuite's RADIUS gateway.   </div>
   

<span id="a876cd77"></span>
### Results

Through this configuration, all network devices in the remote working area will send authentication requests to the RADIUS service node in the central office area through a secure VPN connection or other encrypted channels. Once authenticated successfully, employees will be able to obtain access control rules to the network.

<span id="ee6c47c2"></span>
# Scenario Six: Configure the primary and backup RADIUS servers

<span id="d8b4e343"></span>
## Scenario introduction

To enhance the stability and reliability of the corporate network, configure two RADIUS nodes in the SealSuite Admin Console and correspondingly add a server template on the local wireless controller device (taking Huawei AP3050DE as an example) and configure the primary and backup mode. This configuration allows automatic switching to the backup server in case the primary RADIUS server fails, ensuring the continuity of network authentication services, thus enhancing the stability of the corporate Wi\-Fi network.

<span id="2e28e428"></span>
## Procedure


1. Log in to the SealSuite Admin Console.

   You need to log in to the SealSuite Admin Console with an administrator account.

2. In the Wi\-Fi Management module, configure two RADIUS nodes.

   Two RADIUS gateways correspond to the primary and secondary RADIUS of your local routing device. For detailed operations on adding RADIUS gateways, please refer to [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

3. Log in to the Web page of your local routing device and configure RADIUS.

   1. On the **Create RADIUS Server Template** page, complete the following configurations.

      * Select **Mode** as **Primary\-Secondary mode**.

      * Click **Create New Server** to add two RADIUS servers and enable billing and authentication port.

      * Fill in other configuration items as per the actual situation.

   2. Create an authorization server and associate it with the RADIUS server template.

      * Authorization Server **IP Address**: Refers to the corresponding RADIUS server IP Address.

      * **Template Name**: Select the appropriate RADIUS server template.

      * **Key**: Refers to the wireless router's corresponding **Shared key** in the SealSuite Admin Console.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59b1e92063ce4ef6be9abf4c98f40f4b~tplv-goo7wpa0wc-image.image) </span>


<span id="2a9fe364"></span>
## Results

After configuring the main and backup RADIUS service, enterprises will have a more stable and reliable network authentication service. Even in the event of a main server failure, the backup server can take over quickly, ensuring that the network connection of employees is not affected.
