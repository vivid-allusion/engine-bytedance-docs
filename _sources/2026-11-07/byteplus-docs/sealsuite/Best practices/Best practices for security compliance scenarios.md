---
title: "Best practices for security compliance scenarios"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-best-practices-for-dynamic-control"
---

This document offers a comprehensive overview of how Dynamic Control can be pragmatically utilized to enforce a comprehensive zero\-trust solution. SealSuite's Dynamic Control lets you tailor a dynamic security policy to meet your business's unique needs and specific security concerns.

<span id="38bc4037"></span>
# **Feature Overview**

SealSuite's Dynamic Control and its integrated features ensure real\-time monitoring of device security posture and swift adjustments to access control policies when security events occur. You can customize dynamic control policies to align with security policies and administrative needs, effectively centralizing control and consistently monitoring baseline data across more than 150 parameters, such as account information, device information, behavior information, risk events, operational data, and temporal parameters. For more information, please refer to [Dynamic control overview](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-dynamic-control).

Once SealSuite detects behavior or risks matching set policies, it will immediately take predefined responsive actions, such as degrading network access permissions, prohibiting specific operations, or sending alert notifications. This series of features establishes a detailed, continuous authentication and dynamic disposition system, ensuring the security of users, devices, and behaviors while enhancing the flexibility and diversity of network access control.

<span id="14637ab6"></span>
# Scenario one: **Restricting non\-compliant devices from accessing the office network**

<span id="0900b4c1"></span>
## **Scenario introduction**

In this scenario, we've established a device baseline scanning policy that routinely scans to identify security risks, such as insecured Wi\-Fi connection is detected or non\-compliant applications like personal dropbox or telegram is installed on corporate devices. At the same time, we configured a dynamic control policy group to automatically lower the network permission of non\-compliant devices when security risks are detected, preventing them from accessing the office network.

<span id="972d7e31"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. (Optional) In the left sidebar, select **Device Control** \> **Device Baseline**.

   On the Policy Management page, build a detection policy based on corporate security standards for your enterprise's office security baseline. For specific operations, please refer to [Configuring endpoint control policy](https://docs.byteplus.com/docs/sealsuite/docs-control-rules). You may skip this step if you have already configured the device baseline scanning policy.

3. In the left navigation bar, select **Dynamic Control** \> **Policy Management**.

4. To create a new policy, go to the **Policy Management** page and select **Create New Policy**.

5. On the **Add New Policy** page, complete the following configurations in sequence and click **Confirm**.

   At the bottom of the page, next to the **Confirm** button, you can uncheck the **Enable immediately after creation** option. After unchecking, you need to manually enable the policy in the policy list.

   
   |**Configuration area** |**Configuration item description** |
   |---|---|
   |**General** |**Policy name**: Enter a custom name that identifies the policy group. For example, “Office Security Baseline Detection”. |
   |**Trigger Condition** |* **Condition**: Select **Event Trigger**, SealSuite will provide protection when the device status changes due to risk events, viruses, or DLP.<br><br>* **Trigger event**: Select [Device Risk Detection/Device Baseline]+[Device Risk Detection/Application Risk]+[Device Risk Detection/Process Risk], the decision will be triggered when the client reports the status of security detection.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/851a14ef94e2407982c8a4724c0fa4b1~tplv-goo7wpa0wc-image.image) </span><br><br>* **Parameters**: Select [Device security status/Risk status/Device security baseline risk level]\>[Belong to]\>[Low Risk]+[Medium Risk][High Risk].<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a24a70e3fcdf4e5cac5cbbcce9c0bf8b~tplv-goo7wpa0wc-image.image) </span> |
   |<br>---<br><br><br><br><br>---<br><br><br><br>**Policy** |**Logical expression**: Set to **A**. |
   ||**Action**: Choose **Network Restriction triggered** \> [Limit device VPN usage] + [Limit device Wi\-Fi usage] + [Limit device to wired connection]. When selecting a downgraded mitigation method, it is also necessary to specify the downgrading policy (restricted access to resources or restrictions on Not accessible resources).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f8a64cb49ab45b7b06c32121d3050ba~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If your staff network auth protocol is Portal, then the following four actions cannot be used.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Restrict wired\-connection by device using Wi\-Fi</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Account prohibited from using Wi\-Fi.</strong></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Restrict wired\-connection by device.</strong></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Account prohibited from using wired functions</strong>.</div><br> |
   


<span id="25cf12fa"></span>
## Results

Employees from department A of the company attempted to connect to the company's office network through their personal laptops. Since the laptop failed the device baseline scanning, it triggered a dynamic control policy, resulting in an automatic reduction of its internet access control policies. Therefore, the employee's laptop access to the office network was restricted until their device met the security standards.

<span id="00c355ae"></span>
# Scenario two: Suspending **network access for employees intending to leave the company**

<span id="fee296b2"></span>
## **Scenario introduction**

If an employee exhibits signs of a data breach within a month of departure, the system will immediately restrict their VPN and Wi\-Fi access permission and promptly alert the administrator. This policy requires the pre\-configuration of a DLP policy. For specific operations, please refer to [Configuring file outbound control policies](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule).

<span id="3db123f8"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Dynamic Control** \> **Policy Management**.

3. To create a new policy, go to the **Policy Management** page and select **Create New Policy**.

4. On the **Add New Policy** page, complete the following configurations in sequence, and click **Confirm**.

   At the bottom of the page, next to the **Confirm** button, you can uncheck the **Enable immediately after creation** option. After unchecking, you need to manually enable the policy in the policy list.

   
   |**Configuration area** |**Configuration item description** |
   |---|---|
   |**General** |**Policy name**: Enter a custom name that identifies the policy group. For example, "Limiting the use of the corporate network for employees with an intent to resign and notify the Administrator". |
   |**Trigger Condition** |* **Condition**: Select **Event Trigger**, SealSuite will provide protection when the device status changes due to risk events, viruses, or DLP.<br><br>* **Trigger event:**  Choose **DLP Alert**.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce4ed1a145c84ee88065a4c982787068~tplv-goo7wpa0wc-image.image) </span><br><br>* **Parameters**: Add the following three parameters:<br><br>   * [Account info/Account expiration time] \> value.<br><br>   * [predefined functions/System Time].<br><br>   * [Device security status/DLP Events[Within 1 Month]/Number of alert] \> Greater than or equal to \> 1.<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3c9ed0dace74002ae10cd0181eb6a2a~tplv-goo7wpa0wc-image.image) </span> |
   |<br>---<br><br><br><br>**Policy** |**Logical expression**: Set to `((A-B)<2592000)&&C`. |
   ||**Action**:<br><br><br>* Select **Network Restriction triggered** \> **Restrict device from VPN usage** + **Limit device Wi\-Fi usage**. When selecting a downgrade remediation approach, it is also necessary to specify the downgrade policy (limited access to resources or restricting non\-accessible resources). For information on how to set up network resources for VPN access, please refer to [Configuring VPN access control policies](https://docs.byteplus.com/docs/sealsuite/docs-managing-access-control-rules_2); for information on how to set up an authorization policy, please refer to [Managing staff network](https://docs.byteplus.com/docs/sealsuite/docs-managing-staff-wi-fi).<br><br>* Select **Notification triggered** \> **Send notification via third party app**. Admin can configure the end\-user notification to alert the behaviours. Admin can also configure notifications to end users after the service is restored. Associate third\-party robots are required for notification, with support for multiple selections. For management operations of third\-party robots, please refer to [Manage third-party IM](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#7e2d6168).<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cd8adec547b49899931ca8bfdc4b54f~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="a3d1407d"></span>
## Results

An employee from Department A was discovered to have engaged in a data breach after filing a resignation application. According to the policy, the employee's network permission was immediately reduced, and VPN and Wi\-Fi Access permissions were restricted. At the same time, the user received an instant notification about the incident through a third\-party notification platform.

<span id="10679734"></span>
# Scenario three: Restricting the number of devices an **employee** can connect to the network

<span id="94b407a2"></span>
## **Scenario introduction**

To optimize device access management within the corporate intranet, it is advised to implement a policy to limit the number of devices that employees can connect to the corporate network. This policy effectively controlled the excessive bandwidth occupation by individual employee devices, enhancing the overall network bandwidth availability and user experience within the company.

<span id="4fb21ff7"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Dynamic Control** \> **Policy Management**.

3. To create a new policy, go to the **Policy Management** page and select **Create New Policy**.

4. On the **Add New Policy** page, complete the following configurations in sequence, and click **Confirm**.

   At the bottom of the page, next to the **Confirm** button, you can uncheck the **Enable immediately after creation** option. After unchecking, you need to manually enable the policy in the policy list.

   
   |**Configuration area** |**Configuration item description** |
   |---|---|
   |**General** |**Policy name**: Enter a custom name that identifies the policy group. For example, "Limiting employee access to devices". |
   |**Trigger Condition** |* **Condition**: Select **Event Trigger**, SealSuite will provide protection when the device status changes due to risk events, viruses, or DLP.<br><br>* **Trigger event:**  Select **Period (5 min)** .<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7275e6e3ae9744f081a1706eef52f915~tplv-goo7wpa0wc-image.image) </span><br><br>* **Parameters**: Choose [Behavior info/Account behavior/Number of Wi\-Fi connected devices] \- [Greater than] \- [{Enter the number that the enterprise wishes to restrict here, for example, 100}].<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60ae48ac3b2944c6ba2b21ded8276617~tplv-goo7wpa0wc-image.image) </span> |
   |<br>---<br><br><br><br>**Policy** |**Logical expression**: Set to `A`. |
   ||**Action**: [Limit device Wi\-Fi usage] \- [Downgrade to authorization rule] \- [{Select the corresponding authorization policy here}].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Different authorization policies will be associated with different VLANs, which allows network speed limits to be set on network switches for different VLANs to restrict bandwidth usage.</div><br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20cd7a6cad194e95addf7e6d3b93bec9~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="531882f7"></span>
## Results

An employee from Department A tried to connect a fourth device to the company's network. As the connection exceeded the corporate level device access limit, the policy was triggered, resulting in the downgrade of Wi\-Fi access for the device. It was only permitted to access limited network resources until the number of devices connected was reduced.

<span id="2e4e71ff"></span>
# Scenario four: Restricting access to sensitive resources for teleworking

<span id="fc2cc07a"></span>
## **Scenario introduction**

To ensure the data security, it is recommended to establish a policy that limits the remote access permissions of non\-company assets or BYOD devices. Only company\-owned devices can access specific sensitive resources by using their in\-built security protections and traceability to reduce the security risks associated with remote access.

<span id="ee6381de"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. (Optional) In the left navigation bar, select **Device Assets** \> **Asset Enrollment**.

   In the Device Management module, based on the company's asset inventory, categorize the **company assets** and **non\-company assets**. For specific operations, please refer to [Adding device registration policies](https://docs.byteplus.com/docs/sealsuite/docs-adding-device-registration-rules).

3. In the left navigation bar, select **Dynamic Control** \> **Policy Management**.

4. To create a new policy, go to the **Policy Management** page and select **Create New Policy**.

5. On the **Add New Policy** page, complete the following configurations in sequence, and click **Confirm**.

   At the bottom of the page, next to the **Confirm** button, you can uncheck the **Enable immediately after creation** option. After unchecking, you need to manually enable the policy in the policy list.

   
   |**Configuration area** |**Configuration item description** |
   |---|---|
   |**General** |**Policy name**: Enter a custom name that identifies the policy group. For example, "Restricting access to non\-company assets". |
   |**Trigger Condition** |* **Conditions**: Choose **Action Trigger**, which triggers when an employee performs specified operations on the device, and SealSuite will provide protection for the current policy.<br><br>* **Trigger event**: Select **VPN** \> **VPN Connection**.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9795f28fce5346feabaafce48040c1fb~tplv-goo7wpa0wc-image.image) </span><br><br>* **Parameters**: Choose [Device Info/Device group] \- [Does not include any] \- [{Select the group name of company assets here}].<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b60dc4724e134421b1eb797037bf3c67~tplv-goo7wpa0wc-image.image) </span> |
   |**Policy** |**Logical expression**: Set to `A`. |
   ||**Action**: Choose [Limit device VPN usage] \> [Restrict resources] \> [{Restrict resources}]. For information on how to set up VPN access to network resources, please refer to [Configuring VPN access control policies](https://docs.byteplus.com/docs/sealsuite/docs-managing-access-control-rules_2).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8a7456757fa400bba8049256893b06d~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="6818ff41"></span>
## Results

Remote employees from Department A attempted to access the company's sensitive resources using a computer that is not a company asset. Since the device was not recognized in the company device group, it triggered the policies, resulting in restricted VPN connection and preventing access to the designated sensitive resources.

<span id="3691f02c"></span>
# Scenario five: Employee account r**emote login notification**

<span id="14d26c08"></span>
## **Scenario introduction**

In this scenario, it is recommended to automatically detect and compare the current and recent login locations when an employee logs in. If remote login is detected, the system will send a reminder message to the employee through a third\-party robot platform to enhance account security and promptly notify potential account security events.

<span id="d443c186"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Dynamic Control** \> **Policy Management**.

3. To create a new policy, go to the **Policy Management** page and select **Create New Policy**.

4. On the **Add New Policy** page, complete the following configurations in sequence, and click **Confirm**.

   At the bottom of the page, next to the **Confirm** button, you can uncheck the **Enable immediately after creation** option. After unchecking, you need to manually enable the policy in the policy list.

   
   |**Configuration area** |**Configuration item description** |
   |---|---|
   |**General** |**Policy name**: Enter a custom name that identifies the policy group. For example, "Notification of account login from a different location to the user." |
   |**Trigger Condition** |* **Conditions**: Choose **Action Trigger**, which triggers when an employee performs specified operations on the device, and SealSuite will provide protection for the current policy.<br><br>* **Trigger event:**  Select **Client Operation** \> **Client Login (Try)** .<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7992f559a2754027a31cb7400900f189~tplv-goo7wpa0wc-image.image) </span><br><br>* **Parameters**: Add the following two parameters:<br><br>   * [Operation Info/Request geolocation/City] \> [Low risk locations]<br><br>   * [Behavior info/Account behavior/Geolocation of latest user login/City] \> [Sanctioned locations or any high risk locations]<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b480f4de2fe74b3ea5846dcfc7923ccb~tplv-goo7wpa0wc-image.image) </span> |
   |<br>---<br><br><br><br>**Policy** |**Logical expression**: Set to `A!=B`. |
   ||**Action**: Choose **Notification after service recovery** \> **Third Party Notification**. Associate third\-party robots for notification, and support multi\-selection. For management operations of third\-party robots, please refer to [Manage third-party IM](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#7e2d6168).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/375dd08549174172b7fdcbaf6ea6ba89~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="77aed6f9"></span>
## Results

An employee of Department A logged into the company's SealSuite client while on a business trip using their personal device. The system detected that the login location was inconsistent with low risk locations that users frequently visited, triggering the policy, and sent a message alert about the remote login to the employee through a third\-party robot platform.
