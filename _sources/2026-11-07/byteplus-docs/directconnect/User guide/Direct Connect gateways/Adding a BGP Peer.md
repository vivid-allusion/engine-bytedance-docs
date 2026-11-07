---
title: "Adding a BGP Peer"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If a Virtual Interface associated with a Direct Connect (DC) Gateway uses **BGP** routes without configuring BGP parameters at the creation of the interface, see this topic. You can add a BGP Peer at your on\-premises data center (IDC) for the DC Gateway to interconnect networks between the IDC and the gateway.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a DC Gateway with basic features and a Virtual Interface using **BGP**.


<span id=".6ZmQ5Yi25p2h5Lu2"></span>
## Limits

DC Gateways with the status of **Suspended** do not support adding BGP Peers.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target Region.

3. Click the name of the target DC Gateway to enter the DC Gateway details page.

4. Select the **BGP Peer** tab, click **Add BGP Peer**, and then configure the BGP Peer based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Network type |Select the network type of the BGP Peer. IPv4 is supported by default. If you enable IPv6 for DC Gateway, you can add BGP Peers of both IPv4 and IPv6 types separately. |IPv4 |
   |DC Virtual Interface |Select the Virtual Interface to add the BGP Peer. Only Virtual Interfaces with "BGP" are selectable. |VIF\-ad3hu |
   |Peer ASN |Type the ASN of the BGP Peer. In the BGP protocol, each independent AS has a globally unique Autonomous System Number (ASN).<br><br><br>* The valid range for the Peer ASN is 1 to 4294960000.<br><br>* The ASN of the BGP Peer can neither be the same as that of the DC Gateway, nor be the BytePlus ASN (137718).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the DC Gateway uses the BytePlus ASN (137718), confirm the Peer ASN is different from 137718.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the DC Gateway ASN is custom, the Peer ASN must be different from both the custom ASN of DC Gateway and 137718.</div><br> |46000 |
   |BGP key |Type the BGP key accurately. |123456 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once a BGP peer is added, the BGP information (Peer ASN and BGP key) cannot be modified.   </div>
   

5. Click **Add** to complete adding the BGP Peer.


<span id=".5pON5L2c57uT5p6c"></span>
## Results

After you add a BGP Peer, a neighbor relationship is established between the Autonomous Systems (ASes). The DC Gateway then automatically learns the on\-premises data center routes from this peer and propagates them into its routing table.

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateBgpPeer](https://docs.byteplus.com/en/docs/directconnect/CreateBgpPeer): Create a BGP Peer.
