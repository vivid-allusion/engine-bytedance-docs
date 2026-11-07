---
title: "Configuring the peering connection routes"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-VPC-peering-connection-routes"
---

After creating a peering connection, to enable communication between the two Virtual Private Clouds (VPCs), both the requester and acceptor VPCs need to configure routes: enter the CIDR block of the peer VPC in the destination CIDR (if you only need specific subnets to communicate, enter the subnet CIDR block), and set the next hop to the peering connection.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff4574ae169ad7281f97d7bc6a115a92.png) </span>

<span id="rbUdAIip"></span>
## Procedures


1. Log in to the [Peering Connection console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/peerConnection).

2. In the top menu bar, select the target region and project.

3. Click **Configure route** in the **Requester** or **Acceptor** column of the target peering connection.

4. Configure parameters based on the table below.

   
   |Parameters |Notes |Example |
   |---|---|---|
   |Route entry name |Enter the route entry name. |PeerConnection\-A |
   |Requester route table/Acceptor route table |* Requester route table: Select a subnet route table of the requester VPC.<br><br>* Acceptor route table: Select a subnet route table of the acceptor VPC.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the requester VPC or acceptor VPC has multiple subnet route tables, you can repeat this operation to configure routes for multiple subnet route tables.</div><br> |Default |
   |Destination CIDR |* Requester route table: Enter the CIDR block of the acceptor VPC (if only specific subnets need to communicate, enter the subnet CIDR block).<br><br>* Acceptor route table: Enter the CIDR block of the requester VPC (if only specific subnets need to communicate, enter the subnet CIDR block). |192.168.0.0/16 |
   |Next Hop |The name of the peering connection is fixed. |Peering Connection\-X |
   

5. Click **Create** to complete the action.


&nbsp;

&nbsp;

&nbsp;

&nbsp;
