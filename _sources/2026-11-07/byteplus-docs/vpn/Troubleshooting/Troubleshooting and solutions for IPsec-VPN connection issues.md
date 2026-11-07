---
title: "Troubleshooting and solutions for IPsec-VPN connection issues"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Troubleshooting-and-solutions-for-IPsec-VPN-connection-issues"
---

This topic describes how to troubleshoot issues for IPsec\-VPN connections between a virtual private cloud (VPC) and a data center or another VPC. In the examples below, IPsec\-VPN connections between a VPC and a data center are used.

<span id=".5LiA44CBSVBzZWPov57mjqXnirbmgIHkuLrigJznrKzkuIDpmLbmrrXljY_llYbmnKrmiJDlip_igJ0="></span>
## 1. Phase 1 negotiations failed

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible causes


* IKE negotiations are in progress. Please wait.

* IKE negotiations failed. Refer to the solutions for troubleshooting.


<span id=".6Kej5Yaz5pa55qGI"></span>
#### Solution

A failure in the IKE negotiations typically results from inconsistencies between the configurations of the on\-premises VPN gateway and those on the IPsec\-VPN connection page in the Virtual Private Network console. Follow the steps below for troubleshooting:


1. On the VPN \> IPsec\-VPN Connection page, review the configurations of the following parameters.

   * Verify that the configurations of the VPN gateway in the data center are consistent with those for the IPsec\-VPN connection. If inconsistent configurations exist, modify them to be consistent.

   * Verify that the IKE protocol version in "aggressive" negotiation mode is set to "IKEv2". If the negotiation mode is set to "aggressive" and the IKE protocol version is set to "IKEv1", the local side rejects connection requests for security reasons when the peer initiates a negotiation. If the peer also rejects negotiations initiated from the local side, Phase 1 negotiations fail.

2. On the VPN \> Customer Gateway page, verify that the IP address of the customer gateway associated with the IPsec\-VPN connection is the public IP address of the data center gateway.

   If the configuration is incorrect, recreate a customer gateway with the correct IP address and recreate an IPsec\-VPN connection that is associated with the newly created customer gateway.

3. Verify the status of the VPN gateway in the data center to see if it is functioning normally.

   Verify the status of the VPN gateway in the data center to see if it is functioning normally. If the VPN gateway is in an abnormal status and cannot respond, conduct an inspection or consult the device vendor to restore the functionality of the VPN gateway.


<span id=".5LqM44CBSVBzZWPov57mjqXnirbmgIHkuLrigJznrKzkuozpmLbmrrXljY_llYbmnKrmiJDlip_igJ0="></span>
## 2. Phase 2 negotiations failed

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible causes


* IPsec\-VPN negotiations have not been initiated.

* IPsec\-VPN negotiations are in progress. Please wait.

* IPsec\-VPN negotiations failed. Refer to the solutions for troubleshooting.


<span id=".6Kej5Yaz5pa55qGI"></span>
#### Solution

A failure in the IPsec\-VPN negotiations typically results from inconsistencies between the configurations of the on\-premises VPN gateway and those on the IPsec\-VPN Connection page in the Virtual Private Network console. Follow the steps below for troubleshooting:


1. After an IPsec\-VPN connection is created, the VPN connection tunnel is not established instantly. The Phase 2 negotiation process is activated to establish the communication tunnel only when traffic is detected or after the `ping` command is executed.

2. On the VPN \> VPN Connection page, click Modify for the target IPsec\-VPN connection. On the modification page, review the following configurations:

   1. Check the connection information. In the "interested traffic" mode, ensure that the private CIDR blocks of the gateways at both ends of the IPsec\-VPN connection are correct and consistent.

      If the private CIDR blocks of the gateways at both ends are incorrect, please modify them to the correct private CIDR blocks. If the private CIDR blocks of the gateways at both ends are not consistent, modify them to be consistent.

   2. Check the IPsec Config, ensuring that the authentication algorithm, encryption algorithm, and DH algorithm configurations in the IPsec negotiation phase of the VPN gateway at the data center are consistent with those in the IPsec\-VPN connection.

      If there are inconsistent parameter configurations, please modify them to be consistent.

   3. In Protected Data Flows mode, if multiple IPsec\-VPN connections are created using varying CIDR block sizes, review the IPsec\-VPN connection configurations to ensure that the IKE configurations across the IPsec\-VPN connections with different\-sized CIDR blocks are identical. After an IPsec\-VPN connection is established, if the CIDR blocks of the routes overlap with those for other IPsec\-VPN connections, multiple IPsec\-VPN connections share the same security association (SA). This requires identical IKE configurations among these connections.

      For example, assume that a data center (private CIDR block: 10.0.0.0/8) interconnects with two CIDR blocks of a VPC (private CIDR blocks: 192.168.0.0/24 and 192.168.0.0/26) over IPsec\-VPN Connection A and IPsec\-VPN Connection B, respectively. In this case, the IKE configurations of IPsec\-VPN Connection A and IPsec\-VPN Connection B must be the same.


<span id=".5LiJ44CBSVBzZWPov57mjqXnirbmgIHkuLrigJznrKzkuozpmLbmrrXljY_llYbmiJDlip_igJ3vvIzkvYbku43ml6Dms5Xorr_pl64="></span>
## 3. Unable to access although Phase 2 negotiations succeeded

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible causes


* **Scenario 1: The data center cannot access an Elastic Compute Service instance within the VPC**

   * Route tables of the data center do not contain route entries that forward traffic accessing the VPC to the IPsec\-VPN tunnel, or the ACL configurations of the data center deny VPC access traffic into the IPsec\-VPN tunnel.

   * Security groups of the Elastic Compute Service instance do not contain rules that allow access from the private CIDR blocks of the data center.

* **Scenario 2: The Elastic Compute Service instance within the VPC cannot access the data center**

   * The VPC route tables lack the necessary route entries.

   * Security settings of the data center do not allow access traffic from the VPC.

* **Scenario 3: The data center and the Elastic Compute Service instance within the VPC are both inaccessible.** 

   The public IP address of the VPN gateway in the data center is mapped from a private IP address through NAT. However, NAT traversal was not enabled during the IPsec\-VPN connection setup.


<span id=".6Kej5Yaz5pa55qGI"></span>
#### Solution


* **Scenario 1: The data center cannot access an Elastic Compute Service instance within the VPC**

   * Review the route entries and ACL configurations of the data center. Make sure that traffic from the data center to the VPC is allowed into the IPsec\-VPN tunnel. If the configurations do not allow traffic into the IPsec\-VPN tunnel, modify the configurations as needed.

   * Check the security group of the Elastic Compute Service instance to confirm that there are security group rules allowing access from the data center's private CIDR block. If there are no relevant security group rules, manually add the relevant security group rules. For more information, refer to [Adding Security Group Access Rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

* **Scenario 2: The Elastic Compute Service instance within the VPC cannot access the data center**

   * Verify that the VPC route tables contain route entries whose next hop is the VPN gateway that is used for the IPsec\-VPN connection.

      The routing information in the VPC route table implements communication between the local VPC and the VPN gateway. After a VPN gateway route is configured, the system automatically advertises this route to the system route table of the VPC associated with the VPN gateway, routing traffic from the VPC to the VPN gateway. If the VPC is using a custom route table, manually add the VPN gateway route to the custom route table. For more information, refer to [Adding a Route Entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

   * Review the firewall/iptables configurations of the peer VPN gateway to confirm that access from the private CIDR blocks of the VPC is allowed.

      Make sure that the VPN gateway is interconnected with the VPC in terms of route configurations. In Protected Data Flows mode, the Local Subnet and Remote Subnet of the IPsec\-VPN connection must be consistent with the source and destination CIDR blocks to be accessed.

* **Scenario 3: The data center and the Elastic Compute Service instance within the VPC cannot access each other**

   If the IP address you configured when creating the customer gateway is obtained through NAT, you must enable NAT traversal and configure NAT traversal on the on\-premises VPN gateway device. Refer to [Modifying IPsec-VPN connection configurations](https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations) to toggle on the NAT Traversal switch under Advanced Configurations. Additionally, make sure that the NAT traversal feature is enabled on the VPN gateway device in the data center.


<span id=".5Zub44CBSVBzZWPov57mjqXnirbmgIHkuLrigJznrKzkuozpmLbmrrXljY_llYbmiJDlip_igJ3vvIzkvYblpJrnvZHmrrXlnLrmma_kuIvpg6jliIbpgJrkv6HkuI3mraPluLg="></span>
## 4. Communication is successful only to some CIDR blocks although Phase 2 negotiations succeeded

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible causes


* The IKE protocol version is incorrectly configured. We recommend that you use IKEv2.

* In scenarios where an IPsec\-VPN connection is created to connect to multiple CIDR blocks, the recommended mode is a single connection with a single SA. In other modes, multiple SAs may exist under a single connection, which can result in abnormal communication.


<span id=".6Kej5Yaz5pa55qGI"></span>
#### Solution


1. In the "VPN connection console \> IPsec\-VPN connection" page, click the target IPsec\-VPN connection name to enter the "Overview" page. Check whether the IKE protocol version is "IKEv2".

   If not, please modify it to "IKEv2". For specific [actions](https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations), please refer to modifying IPsec\-VPN connection configurations. Because when the routing mode is "Protected Data Flows", the IKE protocol version must be "IKEv2".

2. If the IKE protocol version is correct but communication to some CIDR blocks still fails, review the SA status of the VPN gateway in the data center.

   * Single SA: indicates a normal status. In this case, verify whether other configurations are correct.

   * Multiple SAs: indicates that the VPN gateway in the data center is using a non\-standard IKEv2 protocol. In this case, use multiple IPsec\-VPN connections to interconnect with various CIDR blocks.

      For example, assume that the data center originally used a single IPsec\-VPN connection to connect two CIDR blocks (192.168.0.0/24 and 10.0.0.0/8) to the VPC (private CIDR block: 172.16.0.0/24). To ensure successful communication, use two separate IPsec\-VPN connections (A and B): Use Connection A and Connection B to connect the 192.168.0.0/24 and 10.0.0.0/8 CIDR blocks of the data center to the VPC, respectively. Additionally, make sure that the IKE configurations for Connection A and Connection B are identical.


<span id=".5LqU44CBSVBzZWPov57mjqXmiJDlip_vvIxWUE7kuKTnq6_pgJrkv6HmraPluLjvvIzkvYblgbblsJTlh7rnjrDkuKLljIXnjrDosaE="></span>
## 5. The IPsec\-VPN connection is established and communication is normal between both sides, but packet loss occurs occasionally

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible causes


* The IKE configurations and IPsec configurations for the IPsec\-VPN connection use less secure authentication algorithms, encryption algorithms, or DH algorithms.

* The actual traffic exceeds the maximum bandwidth of either the local or peer VPN gateway.


<span id=".6Kej5Yaz5pa55qGI"></span>
#### Solution

Modify the IPsec\-VPN connection configuration to set authentication algorithms, encryption algorithms, and DH algorithms with higher security. Refer to [modifying the configurations of an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations) for specific modification actions.


|Name |**Description** |
|---|---|
|Authentication algorithm |Exercise caution when using sha1 and md5, because they are less secure. It is recommended to use the more secure sha256, sha384, and sha512. |
|Encryption algorithm |Exercise caution when using des and 3des, because they are less secure. It is recommended to use the more secure aes, aes192, and aes256. |
|DH Algorithm |Exercise caution when using groups such as group1, group2, and group5, because they are less secure. We recommend that you use group14 for higher security. |
