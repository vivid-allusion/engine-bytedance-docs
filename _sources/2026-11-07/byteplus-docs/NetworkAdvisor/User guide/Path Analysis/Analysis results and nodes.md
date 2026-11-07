---
title: "Analysis results and nodes"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Analysis-result-and-node"
---

## Analysis nodes

Currently supported nodes: Currently supported nodes: Elastic IP Adress (EIP), [Route table](https://docs.byteplus.com/en/docs/vpc/Route-table-overview), [Subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), [Network interface](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview), [BytePlus EIP](https://docs.byteplus.com/en/docs/eip/What-is-EIP), [Elastic Compute Service (ECS)](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service), [Internet NAT gateway](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway), [Classic Load Balancer (CLB)](https://docs.byteplus.com/en/docs/clb/Product-Overview-01), [VPN connection](https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network), [Direct Connect (DC)](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect), [Transit Router (TR)](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01), [Cloud Enterprise Network (CEN)](https://docs.byteplus.com/en/docs/cen/Product-Overview-01), [PrivateLink (PL)](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01).

Based on the supported nodes, the following scenarios are supported for path analysis:

* On\-Cloud Private Network

   * Private network communication between ECS instances within the same VPC.

   * Communication between ECS instances via TR, CEN, or VPN Connection.

   * ECS instances accessing a private CLB.

   * ECS instances access CLB or cloud services through PrivateLink.

* On\-Cloud Public Network

   * An Internet EIP on the Internet accessing a cloud EIP (including EIPs bound to an ECS instance, network interface, Internet NAT Gateway, or CLB).

   * An EIP (including EIPs bound to an ECS instance, network interface, or Internet NAT Gateway) accessing an Internet IP or another cloud\-based EIP.

* Hybrid Cloud

   * Communication between a server in an on\-premises IDC and a cloud\-based ECS instance via Direct Connect or VPN Connection.

   * A server in an on\-premises IDC accessing a cloud\-based Internet NAT Gateway or CLB via Direct Connect or VPN Connection.

   * Communication between a server in an on\-premises IDC and a server in another IDC via Direct Connect or VPN Connection.

## Analysis results

After the path analysis between the source and destination is completed, a path analysis report is automatically generated. Click on a node to view its details.

The path analysis may return the following results:

|Analysis results |Cause and advice |Related documents |
|---|---|---|
|Path reachable |\-\- |\- |
|Path unreachable |Resource status is abnormal; please check the resource's operational status |\- |
||Route unreachable. Check route configurations. |[Adding a route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry) |
||No matching security group rule found; traffic denied by default rule |[Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) |
||Traffic matches a security group deny rule |[Modifying a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing_a_security_group_rule) |
||No matching Network ACL rule found; traffic denied by default rule |[Adding a network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules) |
||Traffic matches a Network ACL deny entry |[Editing a Network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules) |
||Unable to interconnect with the internet. Please bind an EIP |[Applying for EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP), [Associating an EIP](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP) |
||No listener matching the CLB port was found |[Creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener) |
||Traffic matches the CLB access control denylist policy |[Adding or removing the IP entries in the policy group](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups) |
||No match found for the CLB access control allowlist policy; traffic dropped by the default rule |[Adding or removing the IP entries in the policy group](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups) |
||Internet NAT Gateway mismatch. Please check the NAT gateway configuration |[Creating the SNAT rule](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules), [Creating the DNAT rule](https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules) |
||Matches a Cloud Firewall block rule |[Internet Border Firewall](https://docs.byteplus.com/en/docs/cloud_firewall/Configuring_policies_for_internet_firewall) |
|Unknown |Intermediate nodes exist that are not currently supported |\- |
||Neither the source nor destination is a BytePlus EIP. Path analysis does not currently support this scenario |\- |
||Internal exception |\- |
