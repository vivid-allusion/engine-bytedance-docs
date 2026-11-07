---
title: "On-premises data center Internet connectivity"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Interconnection-between-a-data-center-and-the-internet"
---

Internet Tunnel allows an on\-premises data center to access the internet through a Direct Connect (DC) Connection without relying on the cloud. This article describes how to quickly configure an Internet Tunnel (IT).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The Internet Tunnel feature has been enabled for you.

* After completing [account registration](https://docs.byteplus.com/en/docs/6261/64925) and real\-name authentication on BytePlus, you can purchase resources related to Direct Connect.

* The [available balance](https://docs.byteplus.com/en/docs/6269/100429) of the account should be no less than USD 0. If the balance is insufficient, please recharge before creating IT Bandwidth. For procedure, see [Recharge](https://docs.byteplus.com/en/docs/6269/100434).

* You have completed all the necessary procedures required to establish the DC Connections or have obtained the names of the DC Connections to be reused, ensuring that they are not in use.

   In this case, the DC Connection to be used is DAS123_port503_conn. For more information about how to apply for a DC Connection, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65LqS6IGU572R6YCa6YGT572R5YWz"></span>
### Step 1: Create an IT Gateway


1. Log in to [Internet Tunnel Gateway console](https://console.byteplus.com/dc/InternetTunnelGateway).

2. From the top menu bar, select the target region. In this case, **China (Beijing)**  is selected.

3. Click **Create IT Gateway**, and configure the IT Gateway parameters in the pop\-up dialog box.

   
   |Name |Description |Sample values |
   |---|---|---|
   |Region  |Select the region of the IT Gateway. |China (Beijing) |
   |Name |Name the IT Gateway. |Gateway\-Internet_example |
   |IPv6 |This parameter is displayed only after enabling the IT IPv6 capability. Whether to enable the IPv6 feature, it currently does not support Disable after enabling the IPv6 feature.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Internet Tunnel feature by default only supports IPv4 functionality. IPv6 functionality can only be used after being enabled. If needed, please contact the account manager to apply.</div><br> |Disabled |
   

4. Click **Create** to complete the creation.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65YWs572R5bim5a69"></span>
### Step 2: Create an IT Bandwidth


1. On the IT Gateway list page, click the name of the target IT Gateway **Channel\-Internet_example**.

2. Select the **IT Bandwidth** tab, then click **Create IT Bandwidth**, and configure the parameters on the Create IT Bandwidth page as follows.

   
   |Name |Description |Sample values |
   |---|---|---|
   |**Basic information **  |||
   |Billing method |The billing method for the IT Bandwidth. Currently, only Pay\-as\-you\-go is supported. |Pay\-as\-you\-go |
   |Region  |The region of the IT Bandwidth. It defaults to the region of the IT Gateway to which the current IT Bandwidth belongs. You can leave it as it is. |China (Beijing) |
   |IT Gateway |The IT Gateway to which the IT Bandwidth belongs. Defaults to the ID of the selected IT Gateway. You can leave it as it is. |itg\-12ajc0ris7egw17q7y2p9\*\*\*\* |
   |Name  |Name the IT Bandwidth. |Bandwidth\-Internet_example |
   |**Public network information** |||
   |ISP |Select the ISP for the IT Bandwidth. The IT Bandwidth's ISP must match the ISP of the IT Public IP Address created in [Step 4: Create an IT Public IP Address and add to an IT Bandwidth](https://docs.byteplus.com/en/docs/directconnect/Interconnection-between-a-data-center-and-the-internet). |China Unicom |
   |Metering mehtod |Select the metering method for the IT bandwidth. Currently, only Pay\-by\-95th\-percentile is supported. |Pay\-by\-95th\-percentile |
   |Bandwidth limit |Set the maximum bandwidth of the Internet Tunnel. |300 |
   |Agreement |Please refer to the console guidance to review and Confirm the related Legal. |Checked |
   |**Advanced option** |||
   |Affiliated project |Set the project to which the IT Bandwidth belongs. |default |
   |Tags |Set the tag for IT Bandwidth. |* Tag key: ITBandwidth\-key<br><br>* Tag value: ITBandwidth\-v1 |
   

3. Click **Submit** to complete the creation of the IT Bandwidth.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65LqS6IGU572R6YCa6YGT6Jma5ouf5o6l5Y-j"></span>
### Step 3: Create an IT Virtual Interface


1. On the details page of the IT Gateway page, select the **IT Virtual Interface** tab.

2. Click **Create IT Virtual Interface**, and refer to the following table to configure the IT Virtual Interface.

   
   |Name |Description |Sample values |
   |---|---|---|
   |**Basic information **  |||
   |Region  |The region of the IT Virtual Interface. Fixed to the region of the current IT Gateway. |China (Beijing) |
   |Name  |Name the IT Virtual Interface. |Interfaces\-Internet_example |
   |DC Connection |Filter Direct Connect connections by project and select the one to be associated with the IT Virtual Interface. |Project\-01\|DAS123_port503_conn |
   |IT Gateway |Defaults to the selected target IT Gatewayve it as it is. |Gateway\-Internet_example |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Enter an IPv4 address.<br><br><br>* **Cloud gateway IP**: Set the IT Gateway IPv4 Type IP and mask. You can customize the IP address based on your network planning, but you must ensure that the IP address of the local gateway and that of the peer gateway are in the same CIDR block and are not duplicated.<br><br>* **Your gateway IP**: Set the IP address and mask of the gateway on the data center side off the cloud for IPv4 type. You can customize the IP address based on your network planning, but you must ensure that the IP address of the local gateway and that of the peer gateway are in the same CIDR block and are not duplicated. Please use the private IP address of a Virtual Private Cloud, and the address does not conflict with the IP addresses both on the cloud and on\-premises. |* Cloud gateway IP: 10.0.0.1/30<br><br>* Your gateway IP: 10.0.0.2/30 |
   |IPv6 interconnect IP |This parameter is displayed only after enabling the IPv6 capability of the Internet Tunnel. It specifies whether to enable the IPv6 type of interconnect IP. The currently attached IT Gateway has not enabled the IPv6 feature, so it is fixed as not enabled and cannot be modified. |Disabled |
   |VLAN ID |Set the VLAN ID that is to be used to connect to the on\-premises data center. Make sure this VLAN ID is not in use. Valid range: 0\-2999. For a Shared Line, leave the VLAN ID as it is. |233 |
   |**Routing Information** |||
   |Route type  |Select the route type of the IT Virtual Interface. Currently, only BGP is supported. |BGP route |
   |BGP ASN |Enter the ASN of the BGP peer, ensuring that it is different from the ASN of BytePlus. |439001 |
   |BGP key |Enter the password of the BGP peer. |m9D0g1o1d8g\*\*\*\* |
   |Detection mode |Select the mode for connection health detection.<br><br><br>* **Disable**: Health detection is disabled.<br><br>* [BFD](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface): Enable BFD as the detection mode. |Disable |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Sample values are only provided for the necessary parameters here. For more information about the parameters, see <a href="https://docs.byteplus.com/en/docs/directconnect/Creating-an-Internet-Tunnel-virtual-interface">Creating an IT Virtual Interface</a>.   </div>
   

3. Click **Create** to complete the creation and association of the IT Virtual Interface.


<span id=".5q2l6aqk5Zub77ya5Yib5bu65LqS6IGU572R6YCa6YGT5YWs572RSVDlubbliqDlhaXlhaznvZHluKblrr0="></span>
### Step 4: Create an IT Public IP Address and add to an IT Bandwidth


1. In the left\-side navigation pane, select **Public IP Address**.

2. Click **Apply for IT Public IP Address** and configure the IT Public IP Address parameters in the pop\-up dialog box.

   
   |Name |Description |Sample values |
   |---|---|---|
   |Billing method |The billing type for IT Public IP Address is set to Pay\-as\-you\-go by default and does not require modification. |Pay\-as\-you\-go (Monthly) |
   |Region  |Select the region of the Internet Tunnel address. The region cannot be changed after the application is successful. |China (Beijing) |
   |Name |Name of the Internet Tunnel address. |IP\-Internet_example |
   |Protocol type |The IP type of the Internet Tunnel address. Currently, only IPv4 is supported. |IPv4 |
   |ISP |The line type of the IT Public IP Address must be consistent with the [Step 2: Create an IT Bandwidth](https://docs.byteplus.com/en/docs/directconnect/Interconnection-between-a-data-center-and-the-internet#.5q2l6aqk5LqM77ya5Yib5bu65YWs572R5bim5a69). |China Unicom |
   |Number of IPs |Select the number of Internet Tunnel addresses to be applied for. Only 4, 8, 16, 32, 64, 128 and 256 can be applied for in a single application. |4 |
   |IT Gateway |Select the IT Gateway Internet Tunnel bandwidth to which the Internet Tunnel address to be added belongs. |Gateway\-Internet_example |
   |IT Bandwidth |Select the IT Bandwidth to which the Internet Tunnel address to be added. You can select the IT Bandwidth instance only after an IT Gateway is selected. |Bandwidth\-Internet_example |
   |Affiliated project |Set the project to which the the IT Public IP belongs. |default |
   |Tags |Set the IT Public IP Address tag. |* Tag key: Internetip\-key<br><br>* Tag value: Internetip\-v1 |
   |Agreement |Follow the console guidance to review and confirm the related Legal. |Checked |
   

3. Click **Buy now** to complete the application.


<span id=".5q2l6aqk5LqU77ya6L-e6YCa5oCn5rWL6K-V"></span>
### Step 5: Test connectivity 


1. Log in to any server of the on\-premises data center.

2. Open the terminal interface of the server and execute the command `ping 114.114.114.114` or `ping 8.8.8.8`. If the response is something like the content below, it indicates that the on\-premises data center can access the internet.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d522c960416513138087097a194d2c95.png) </span>
