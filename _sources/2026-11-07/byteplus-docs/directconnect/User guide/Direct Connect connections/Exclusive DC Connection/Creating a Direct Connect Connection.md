---
title: "Creating a Direct Connect Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1"
---

This topic describes how to create a dedicated Direct Connect (DC) Connection. To create a dedicated DC Connection, you need to apply for a DC Connection port yourself. After approval, contact the line operator to establish the DC Connection, finalize completion acceptance and reporting, and handle payment.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Complete the access point selection, onsite survey and other preparations. For procedure, see [Preparations before access](https://docs.byteplus.com/en/docs/directconnect/Preparation-for-access).

* You have completed real\-name authentication for your account before purchasing Direct Connect\-related resources.


<span id=".5q2l6aqk5LiA77ya55Sz6K-35o6l5YWl54mp55CG5LiT57q_"></span>
## Step 1: Create DC Connection


1. Log in to [the DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select a project and region for the DC Connection to be deployed.

3. Click **Create DC Connection**.

4. Configure the DC Connection port based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Access point mode |Select an access point mode for the DC Connection:<br><br><br>* High reliability mode: Create multiple access points in a single request, providing disaster recovery capabilities. Suitable for new sites.<br><br>* Classic mode: Create a single access point in a single request. Suitable for expanding existing connections. |High reliability mode |
   |Combination type |When selecting High reliability mode for the access point mode, you need to configure the access combination type for the DC Connection. It supports three options: "Optimal Disaster Recovery", "Powerful Disaster Recovery", and "Development and Testing". Select based on your actual business needs:<br><br><br>* Optimal Disaster Recovery: You apply for resources in 2 access points and establish 4 independent DC Connections. A [service level agreement (SLA)](https://docs.byteplus.com/en/docs/6407/102215) can be guaranteed in this mode. This mode provides recovery capabilities during device failure, connection failure, and full site failure. Combining with [dual-line access best practices](https://docs.byteplus.com/en/docs/6407/159228), it minimizes the risk of a single\-site failure caused by a single device failure.<br><br>* Powerful Disaster Recovery: You apply for resources in 2 access points and establish 2 independent DC Connections. An [SLA](https://docs.byteplus.com/en/docs/6407/102215) can be guaranteed in this mode. This mode provides recovery capability when connection fails due to line interruption or device failure, preventing full site failure. Combining with [dual-line access best practices](https://docs.byteplus.com/en/docs/6407/159228), it largely avoids single\-site failures caused by a single device failure.<br><br>* Development and Testing: You apply for resources within 1 access point to establish 2 DC Connections. This mode provides recovery capability in case of device failure, but does not provide recovery capability for site failure. |Development and testing |
   |Region |Select the access point region of the DC Connection. |China (Beijing) |
   |Name |Enter a name for the DC Connection. No special requirements for the DC Connection name format. You may define it yourself. "DAS\-246\-3_port10\-conn" is just a sample name without practical meaning. |DAS\-246\-3_port1\*\*0\-conn |
   |Access point |Select an access point for the DC Connection. You should confirm the DC access point during the [Preparations before access](https://docs.byteplus.com/en/docs/directconnect/Preparation-for-access) stage.<br><br><br>* We recommend choosing the access point nearest to your on\-premises data center (IDC). For details of the access point, see [Direct Connect access points](https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-access-point).<br><br>* When you deploy multiple DC Connections, we recommend selecting different access points to ensure high reliability. |Beijing\-Chaoyang\-A |
   |line operator |Select the type of line operator who constructs your DC Connection. Different access points support different line operators. Confirm in advance the line operator type supported by the target access point.<br><br><br>* China Mobile<br><br>* China Unicom<br><br>* China Telecom<br><br>* Other Chinese line operators<br><br>* International line operator |China Mobile |
   |Port speed |Select a port specification. Different specifications charge different port occupancy fees. Apply based on actual needs. |1G |
   |Port type |Port Type includes the optical port. Port Spec determines the port rate. BytePlus access point devices support single\-mode optical ports with specifications of 1Gbps, 10Gbps, 40Gbps, 100Gbps, and 400Gbps.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, 40G and 100G optical ports are not available. If needed, please contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only Beijing\-Langfang\-C access point supports the 400Gbps optical port in DC Connections with classic mode. If needed, please contact your account manager.</div><br><br><br>* Different types of ports support different lines and bandwidths. Select the port type that matches the port type of your IDC.<br><br>* BytePlus defaults to providing single\-mode optical ports of 1Gbps and 10Gbps with a data transmission distance of 10 kilometers.<br><br>* If you need single\-mode optical ports with a data transmission distance over 10 kilometers or specifications of 40Gbps or 100Gbps, please prepare them in advance.<br><br>* If you need to use optical ports, first confirm that your line operator can provide fiber lines to connect to BytePlus devices.<br><br>* BytePlus does not support hosting any optoelectronic conversion devices. You should communicate with your line operator in advance to ensure they deploy the proper type of line for connecting to BytePlus devices. |1G optical port |
   |Affiliated project |Select a project to which the new DC Connection belongs. A project refers to a task in your daily work. You can create multiple projects under the same account and create or purchase cloud resources for each project. Cloud resources cannot be shared between different projects.<br><br><br>* After selecting the project, the DC Connection you create can only be used by users with permission over that project.<br><br>* If you selected **All Resources** in the top menu bar before entering the creation page, the new DC Connection belongs to the default project. You can reselect a project on the Create DC Connection page.<br><br>* If you select a specific project in the top menu bar before entering the creation page, the new DC Connection belongs to that specific project. You cannot reselect a project on the Create DC Connection page. To reselect, exit the creation page, select another project, and then create.<br><br>* If no projects are available, click **Create Project** on the left to create a new project.<br><br>* After adding a DC Connection to a project, you can transfer the DC Connection out of the project based on actual business needs. For details, see [Project resource management](https://docs.byteplus.com/en/docs/6649/94337). |default |
   |Billing rules |View and confirm the DC Connection billing rules. This option needs to be checked during configuration only for the DC Connection in classic mode. |Check |
   |**Advanced options** |||
   |Tags |A tag consists of a tag key (Key) and a tag value (Value). It can be used to classify and search for DC Connections.<br><br><br>* Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_004141eef23f0c9ac0f05517c9e79040.png) </span> icon to add multiple tags. You can add up to 20 tags per action, and up to 50 tags for a single DC Gateway.<br><br>* The keys of multiple tags for the same DC Connection must be unique. Each key has only one value.<br><br>* The key and the value are case\-sensitive. For example, the key=tag and the key=tag are two different keys. For more information, see [Tag management](https://docs.byteplus.com/en/docs/directconnect/Tag-management). |key:test |
   |MACsec |Specify whether to enable Media Access Control Security (MACsec). When checked, a DC Connection with MACsec support will be created. After creation, the encryption mode defaults to **No encryption**. You can [change the encryption mode](https://docs.byteplus.com/en/docs/directconnect/Managing_encryption_mode) on the instance details page.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Due to access point resource support for MACsec, a MACsec\-enabled DC Connection may fail to provision. Monitor the application result.</div><br> |Not check |
   

5. After configuration:

   * DC Connection with high reliability mode: Click **Buy now**, view and confirm the DC Connection billing rules, and then click **Submit**.

   * DC Connection with classic mode: Click **Buy now** to submit the request.


Upon receiving the port application, BytePlus staff will approve it as soon as possible. Once approved, BytePlus will notify you via onsite message and SMS. You can check the DC status on the DC Connection console. At this point, the status of the DC Connection is **LOA pending**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Complete the construction and pay the port fee within 45 days after approval. Otherwise, the assigned port will be released.</div>


<span id=".5q2l6aqk5LqM77ya55Sz6K-3TE9B"></span>
## Step 2: Apply for LOA

LOA is a letter of authorization for the DC Connection construction in the BytePlus access point data center. After the DC Connection application is approved, the status of DC Connection becomes **LOA pending**. Go to the BytePlus DC Connection console to apply for a LOA.


1. Log in to [the Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the project and region of the DC Connection to be applied for the LOA.

3. In the DC Connection list, click **Apply for LOA** in the **Actions** column to the right of the target DC Connection, and configure the LOA application based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Company name |Enter the name of the company who uses the DC Connection. |ByteDance |
   |Construction Company entering BytePlus Data Center |Enter the name of the construction company. |BytePlus |
   |Construction Company email |Enter the email address of the construction company to notify them to complete the relevant access application. |user@mail.server.name |
   |Line type |Select a type for the DC Connection.<br><br><br>* MSTP: MSTP DC Connection<br><br>* MPLSVPN: MPLS VPN DC Connection<br><br>* FIBRE: Fiber DC Connection<br><br>* Other: Other types of DC Connections |MSTP |
   |Construction schedule |Select the expected time when the line operator will enter the BytePlus data center for construction. After the LOA is approved, relevant construction personnel must strictly follow the specified time; otherwise, entry will be denied. |2023\-06\-30 |
   |IDC location |Enter the detailed address of your data center in the format: [country]\-[province]\-[city]\-[district/county/town]\-[street]\-[building]\-[data center]. |XX data center, XX Building, No. XX, XX Road, Chaoyang District, Beijing, China |
   |Bandwidth |Enter the bandwidth of the DC Connection purchased from the line operator. |1000Mbps |
   |Field Engineer |When the DC Connection region is within China, provide the construction engineer’s name, contact information, and ID number. You can fill contact information of up to 16 construction engineers. |Wang \*\*, 151\*\*\*\*0086, China Mainland ID, 22222219990101\*\*\*\* |
   

4. Click **Submit** to complete the application. At this point, the status of the DC Connection is **LOA reviewing**.


<span id=".5q2l6aqk5LiJ77ya54mp55CG5LiT57q_5pa95bel"></span>
## Step 3: Construction by line operator


1. After the LOA application is approved, BytePlus will notify you via onsite message and SMS. At this time, the status of the DC Connection changes to L**ine operator construction**.

2. Log in to [the DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

3. In the top menu bar, select the project and region of the DC Connection to be constructed.

4. In the DC Connection list, click **Download LOA** in the **Actions** column to the right of the target DC Connection to obtain the LOA for on\-site construction.

5. You should take the LOA with you and contact the line operator to construct the DC Connection.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The DC Connection construction requires a certain lead time. Confirm the specific schedule with the line operator and reserve sufficient time.</div>


<span id="1LyyJusS"></span>
## Step 4: Report completion

After the line operator completes the construction and you finalize the completion by testing the DC Connection link connectivity, you need to access the BytePlus DC Connection console to report the completion.


1. Log in to [the DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the project and region of the DC Connection to be reported.

3. In the DC Connection list, click **Completion report** in the **Actions** column to the right of the target DC Connection.

4. After confirming the information about the DC Connection to report, enter the Building Cable ID of the DC access point's data center.

5. Click **Submit**.


After the completion report is submitted, the status of the DC Connection changes to **BytePlus construction**.

<span id="ZGnA6PaM"></span>
## Step 5: Construction by BytePlus

After the completion report is submitted, BytePlus engineers will perform patch cord installation and check optical attenuation for your DC Connection. You will receive a notification via onsite message and SMS once the construction is complete. Wait patiently.

<span id=".5q2l6aqk5LqU77ya5pSv5LuY56uv5Y-j5Y2g55So6LS5"></span>
## Step 6: Pay port occupancy fee

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the project and region of the DC Connection to be paid.

3. In the DC Connection list, click **Pay now** in the **Actions** column to the right of the target DC Connection to enter the Payment page.

4. Configure parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Billing method of DC port resources. Currently supports only Subscription. |Subscription |
   |Purchase time |Usage duration of DC port resources. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. If automatic renewal is enabled, the renewal length is one month and the number of renewals is unlimited. You can manually disable automatic renewal or visit the Billing center to modify the number of renewals. For detailed actions, see [Automatic renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). For DC port resources used long\-term, to avoid business impact due to expiration, we recommend checking Automatic renewal. |Disable |
   

5. Follow the console guidance to review and accept the legal terms, and click **Pay now**.

6. Click **Next**, select a payment method, and then click **Pay**.

7. Make the payment by the selected method. After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.

8. Once the payment is complete, the DC Connection status becomes **Opened**. The DC Connection is available for use.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create a DC Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1): After enabling the DC Connection, you also need to create a DC Gateway for your on\-premises data center to access the cloud.

* (Optional) [Associate a QoS policy](https://docs.byteplus.com/en/docs/directconnect/Attaching_and_detaching_DC_Connection): You can associate a QoS policy with the DC Connection to ensure stable operation of critical services during bandwidth congestion.

* (Optional) [Create an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy): You can create CloudMonitor alarm strategies to monitor the DC Connection status. When alert trigger conditions are met, the system will push alarm notifications through the methods you specified. When creating an alarm strategy for the DC Connection, we recommend monitoring DC Connections in **Opened** status only. This excludes DC Connections under construction, preventing false alarms.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectConnection): Create a dedicated DC Connection.

* [CreateDirectConnectConnectionOrder](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectConnectionOrder): Create a payment order for a Direct Connect resource.

* [DescribeDirectConnectAccessPoints](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectAccessPoints): Query the information about Direct Connect access points.
