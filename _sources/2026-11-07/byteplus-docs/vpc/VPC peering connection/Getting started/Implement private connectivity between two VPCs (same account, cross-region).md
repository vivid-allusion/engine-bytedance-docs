---
title: "Implement private connectivity between two VPCs (same account, cross-region)"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Implement-private-connectivity-same-account-cross-region"
---

You can refer to this document to achieve private connectivity between private network instances in the same account and region through peering connections.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51345a1b82f15c5c4b25461235d589ae.png)

## Preparations

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:

1. Register account A and complete real name verification.

2. Recharge account.

3. In China (Beijing) region, [Create 2 VPCs with their subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Create 2 ECSs](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). The required information is as follows:

   * VPC\-A (172.16.0.0/16), subnet A (172.16.1.0/24), ECS\-A (172.16.1.11).

   * VPC\-B (192.168.0.0/16), subnet B (192.168.1.0/24), ECS\-B (192.168.1.22).

## Procedures

Explanation

The following describes only the required parameters and their values. For other parameters not mentioned, retain the default values.

### Step one: configure the initiating VPC

#### (1) create a peering connection

   1. Log in to the peering connection console.

   2. In the top navigation bar, select the target project.

   3. Click the **Create Peering Connection** button.

   4. configure relevant parameters based on the table below.

      |Parameters |Explanation |Sample value |
      |---|---|---|
      |Name |Enter the name of CEN instance. |Peering\-X |
      |Originating VPC instance |Select the source VPC. |VPC\-Source |
      |Account type of recipient |Select the receiver account type. Select same account. |Same account |
      |Receiver region type |Select the receiver region type. Select Across Regions. |Inter\-region |
      |Receiver region |If the receiver region type is Across Regions, select the region. |China (Shanghai) |
      |Destination VPC ID |Select the receiver VPC. |VPC\-Destination |

   5. Click **Migrate** to complete the action.

#### (2) Configure the initiator VPC route

   6. Log in to VPC console.

   7. In the left\-side navigation pane, select **Route Table**.

   8. In the top menu bar, select the project and region.

   9. Click the route table name of the initiator VPC.

   10. On the **Route Entry \> Custom route** tab, click **Add route**.

   11. configure relevant parameters based on the table below.

      |Parameters |Explanation |Sample value |
      |---|---|---|
      |Destination CIDR |Set the destination CIDR block for traffic routing. |0.0.0.0/0 |
      |Next Hop type |Select a resource type for the next hop of the route entry. Subnet route tables support the following next hop types: |Peering connection |
      |Next Hop |Select resources from the drop\-down menu based on the next hop type. |Peering\-X |

   12. Click **Create** to complete configuration.

#### (3) Configure security group and network ACL

Security groups and network ACLs for resources that require communication between the initiating VPC and the receiving VPC:

   * Security Group configuration example:

      |Rule direction |Priority |Strategy |Protocol type |Destination port |Source/destination address |Description |
      |---|---|---|---|---|---|---|
      |Inbound |100 |Permit |ALL |ALL |Source address: 192.168.1.0/24 |Allow VPC\-B’s inbound traffic to VPC\-A |
      |Outbound |100 |Permit |ALL |ALL |Destination address: 192.168.1.0/24 |Allow traffic from VPC\-A to access VPC\-B |

   * Network ACL configuration example:

      |Direction |Priority |Strategy |Protocol type |Destination port |Source/destination address | |
      |---|---|---|---|---|---|---|
      |Inbound |Set priority (e.g. 1) |Permit |ALL |ALL |Source address: 192.168.1.0/24 |Allow traffic from VPC\-B to enter VPC\-A |
      |Outbound |Set priority (e.g. 1) |Permit |ALL |ALL |Destination address: 192.168.1.0/24 |Allow traffic from VPC\-A to VPC\-B outbound |

   Refer to [Adding security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) and [Adding network ACL rules](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules) for instructions.

### Step two: Configure the receiving VPC

#### (1) Accept connection

Connections are accepted by default within the same account.

#### (2) Configure receiving VPC routing

   1. Log in to VPC console.

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

####  **(3) configure security groups and network ACLs**

The security groups and network ACLs for resources in the receiver VPC that need to connect with the initiator VPC:

   * Security Group configuration example:

      |Rule direction |Priority |Strategy |Protocol type |Destination port |Source/destination address |Description |
      |---|---|---|---|---|---|---|
      |Inbound |100 |Permit |ALL |ALL |Source address: 172.16.1.0/24 |Allow VPC\-A's incoming traffic to enter VPC\-B |
      |Outbound |100 |Permit |ALL |ALL |Destination address: 162.16.1.0/24 |Allow traffic from VPC\-B to access VPC\-A |

   * Network ACL configuration example:

      |Direction |Priority |Strategy |Protocol type |Destination port |Source/destination address |Description |
      |---|---|---|---|---|---|---|
      |Inbound |Set priority (e.g. 1) |Permit |ALL |ALL |Source address: 192.168.1.0/24 |Allow traffic from VPC\-A to enter VPC\-B |
      |Outbound |Set priority (e.g. 1) |Permit |ALL |ALL |Destination address: 192.168.1.0/24 |Allow traffic from VPC\-B to go to VPC\-A |

   For specific steps, see [Adding Security Group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) and [Adding Acl Entries](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules).

## Verification

1. Remotely log in to ECS\-A.

2. On the command line, execute `ping <IP address of ECS-B, using 192.168.1.22 as an example>` to test network connectivity.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_177a7daa6fc6a6a2276e68b3e28111d7.png)

3. Similarly, verify that ECS\-B can access ECS\-A.
