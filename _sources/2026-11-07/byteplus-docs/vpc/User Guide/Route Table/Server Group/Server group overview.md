---
title: "Server group overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Server-Group-Overview"
---

## Introduction​

Within a Virtual Private Cloud (VPC), to achieve traffic forwarding to ECSs via ECMP (Equal\-Cost Multi\-Path Routing), you can create a server group and set it as the route's next hop. Then, add the target servers to this group to complete the ECMP routing configuration.

> **tip**

> The server group is currently in Beta. For trial requests, please contact your account manager.

## Composition

* **Elastic Compute Service**

   After an ECS is added to a server group, the specified traffic is forwarded to each server within the group via ECMP routing.

* **Path policy**

   After an ECS is added to a server group, connections are evenly distributed to each ECS.

* **Health check**

   The server group is configured with health checks by default, which use ICMP packets to probe server availability. Therefore, for each ECS in the server group, please ensure that the security group associated with its primary network interface allows inbound ICMP traffic from the destination CIDR block 100.64.0.0/10. This traffic is used for health checks.

   * Check interval: 2 seconds.

   * Check timeout period: 2 seconds.

   * The status is considered normal after three consecutive successful probes, and abnormal after three consecutive failed probes. Traffic is not routed to abnormal servers.

## Limitations

* **Quota limitations**

   |Limit item |Maximum |Support adjustment |
   |---|---|---|
   |Maximum number of ECSs per server group |32 |No |
   |Maximum number of server groups per account per region |10 |Yes. If the default quota does not meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota. |

* **Feature limitations**

   * Shared VPC is not supported.

   * The server group has a default health check configured and does not support adjusting the health check.

   * The server group is configured with health checks by default, which currently cannot be modified. Server groups only support adding ECSs that reside in the same VPC.

   * Since the system\-defined policies `VPCFullAccess` and `VPCReadOnlyAccess` do not include permissions for server groups, an IAM user granted `VPCFullAccess` or `VPCReadOnlyAccess` policy must be additionally granted specific permissions for server groups in order to use them. An example permission policy is provided below:

      ```json
      {
          "Statement":[
              {
                  "Effect":"Allow",
                  "Action":[
                      "vpc:*InstanceGroup*"                                                   
                  ],
                  "Resource":[
                      "*"
                  ]
              }
          ]
      }
      ```

## Configuration procedures

1. [Create Server Group](https://docs.byteplus.com/en/docs/vpc/Creating-or-deleting-a-server-group#.5Yib5bu65pyN5Yqh5Zmo57uE): Create a server group.

2. [Add Server](https://docs.byteplus.com/en/docs/vpc/Adding-or-Removing-servers#.5re75Yqg5pyN5Yqh5Zmo): Add multiple ECS instances.

3. [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry): Add a route entry with the next hop pointing to a server group to route traffic within the specified destination CIDR block to the server group.
