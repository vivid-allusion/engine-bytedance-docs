---
title: "Establish private connectivity between two VPCs (cross-account, cross-region)"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Implement-private-connectivity-cross-account-cross-region"
---

This topic explains how to use Cloud Enterprise Network (CEN) to establish private network connectivity between cross\-account, cross\-region Virtual Private Cloud (VPC) instances.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4f58e2ff65ae1a8455254c9320f7532.png)

## Preparations

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:

1. Register Account A, Account B, and complete real name verification.

2. Recharge account.

3. Create 1 VPC and subnet in China (Beijing) and China (Shanghai) respectively, and [create 1 ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). The details are as follows:

   * China (Beijing): VPC\-A (172.16.0.0/16), Subnet\-A (172.16.1.0/24), ECS\-A (172.16.1.11).

   * China (Shanghai): VPC\-B (192.168.0.0/16), Subnet\-B (192.168.1.0/24), ECS\-B (192.168.1.22).

## Procedures

> **tip**

> The following describes only the required parameters and their values. For other parameters not mentioned, retain the default values.

### Step one: configure the initiator

#### (1) Create a peering connection

   1. Log in to the peering connection console using account A.

   2. In the top navigation bar, select the target project.

   3. Click the **Create peering connection** button.

   4. configure relevant parameters based on the table below.

      |Parameters |Explanation |Sample value |
      |---|---|---|
      |Name |Enter the name of CEN instance. |Peering\-X |
      |Initiating VPC instance |Select the initiator VPC. |VPC\-Source |
      |Receiver account type |Select the account type of the receiver.<br><br><br>* **Cross\-account**: the receiver's VPC is in a different account than the initiator's VPC. |Cross\-account |
      |Recipient main account UID |If cross\-account is selected, enter the main account ID. |210005XXXX |
      |receiver region type |Select the receiver region type.<br><br><br>* **Across Regions**: the receiver VPC and the initiator VPC are in different regions. |Inter\-region |
      |receiver region |If the receiver region type is set to Across Regions, select a region. |China (Shanghai) |
      |Receiver VPC ID |Select the receiving VPC. |VPC\-Destination |

   5. Click **Migrate** to complete the action.

#### (2) Configure the initiator VPC route

   6. Use account A to log in to the [VPC console](https://console.byteplus.com/vpc/vpc)

   7. In the left\-side navigation pane, select **Route Table**.

   8. In the top menu bar, select the project and region.

   9. Click the route table name of the initiating VPC

   10. On the **Route Entry \> Custom route** tab, click **Add route**.

   11. configure relevant parameters based on the table below.

      |Parameters |Explanation |Sample value |
      |---|---|---|
      |Destination CIDR |Set the destination CIDR block for traffic routing. |0.0.0.0/0 |
      |Next Hop type |Select a resource type for the next hop of the route entry. Subnet route tables support the following next hop types: |peering connection |
      |Next Hop |Select resources from the drop\-down menu based on the next hop type. |Peering\-X |

   12. Click **Create** to complete configuration.

#### (3) Configure security groups and network ACLs

The security groups and network ACLs of resources in the initiating VPC that need to communicate with the receiving VPC:

   * Security Group configuration example:

      |Rule direction |Priority |Strategy |Protocol type |Destination port |Source/destination address |Description |
      |---|---|---|---|---|---|---|
      |Inbound |100 |Permit |ALL |ALL |Source address: 192.168.1.0/24 |Allow VPC\-B's traffic to enter VPC\-A |
      |Outbound |100 |Permit |ALL |ALL |Destination address: 192.168.1.0/24 |Allow traffic from VPC\-A to access VPC\-B |

   * Network ACL configuration example:

      |Direction |Priority |Strategy |Protocol type |Destination port |Source/destination address | |
      |---|---|---|---|---|---|---|
      |Inbound |Set priority (e.g. 1) |Permit |ALL |ALL |Source address: 192.168.1.0/24 |Allow traffic from VPC\-B into VPC\-A |
      |Outbound |Set priority (e.g. 1) |Permit |ALL |ALL |Destination address: 192.168.1.0/24 |Allow traffic from VPC\-A to VPC\-B |

   For actions, see [Adding security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) and [Adding network ACL rules](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules).

### Step two: configure the receiver

#### one, accept connection

   1. Log in to the peering connection console with account B.

   2. In the top navigation bar, select the target project.

   3. Click the **Accept connection** button on the right side of the target peering connection.

   4. Click Migrate to complete the action.

#### 2. configure the receiver VPC route

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc) using account B.

   2. In the left\-side navigation pane, select **Route Table**.

   3. In the top menu bar, select the project and region.

   4. Click the route table name of the receiver VPC.

   5. On the **Route Entry \> Custom route** tab, click **Add route**.

   6. configure relevant parameters based on the table below.

      |Parameters |Explanation |Sample value |
      |---|---|---|
      |Destination CIDR |Set the destination CIDR block for traffic routing. |0.0.0.0/0 |
      |Next Hop type |Select a resource type for the next hop of the route entry. Subnet route tables support the following next hop types: |Peering connection |
      |Next Hop |Select resources from the drop\-down menu based on the next hop type. |Peering\-X |

   7. Click **Create** to complete configuration.

#### **3. Configure security group and network ACL**

The security groups and network ACLs of resources in the receiving VPC that need to communicate with the initiating VPC:

   * Security Group configuration example:

      |Rule direction |Priority |Strategy |Protocol type |Destination port |Source/destination address |Description |
      |---|---|---|---|---|---|---|
      |Inbound |100 |Permit |ALL |ALL |Source address: 172.16.1.0/24 |Allow traffic from VPC\-A to enter VPC\-B |
      |Outbound |100 |Permit |ALL |ALL |Destination address: 162.16.1.0/24 |Allow traffic from VPC\-B to access VPC\-A |

   * Network ACL configuration example:

      |Direction |Priority |Strategy |Protocol type |Destination port |Source/destination address |Description |
      |---|---|---|---|---|---|---|
      |Inbound |Set priority (e.g. 1) |Permit |ALL |ALL |Source address: 192.168.1.0/24 |Allow traffic from VPC\-A to enter VPC\-B |
      |Outbound |Set priority (e.g. 1) |Permit |ALL |ALL |Destination address: 192.168.1.0/24 |Allow traffic from VPC\-B to go to VPC\-A |

   Refer to [Add security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) and [Add network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules) for the operation.

### Verification

1. Remotely log in to ECS\-A.

2. On the command line, execute `ping <IP address of ECS-B, using 192.168.1.22 as an example>` to test network connectivity.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_177a7daa6fc6a6a2276e68b3e28111d7.png)

3. Similarly, verify that ECS\-B can access ECS\-A.
