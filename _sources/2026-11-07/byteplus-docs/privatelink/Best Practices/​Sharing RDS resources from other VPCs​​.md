---
title: "​Sharing RDS resources from other VPCs​​"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Sharing-RDS-resources-in-a-VPC-with-another-VPC"
---

This topic explains how to share the RDS database service within a Virtual Private Cloud (VPC) with other VPCs using PrivateLink.

## Scenarios

PrivateLink enables the sharing of service resources within a VPC to other VPCs via a private network, ensuring business security and helping to reduce costs.

This topic describes how to share RDS\-type service resources within a VPC for use by other VPCs. The specific network scenario is illustrated in the figure below.

> The RDS\-type service resource uses Cloud Database MySQL Edition as an example.

## Prerequisites

* The required VPC and subnets have been created. For detailed actions, see [Building an IPv4 Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

* Creation of the required Elastic Compute Service (ECS) instances has been completed. For detailed operations, see [Purchasing an Elastic Compute Service instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* The cloud database service has been deployed, and the PrivateLink deployment network segment 100.64.0.0/10 has been added to the cloud database allowlist. For detailed operations, see [Cloud Database Getting Started](https://docs.byteplus.com/en/docs/RDS_for_MySQL/use_process).

   > **tip**

   > After deployment is complete, see [Viewing Cloud Database details](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_address_and_port) to obtain in advance the **ID of the Cloud Database instance**, **ID of the connection endpoint**, and **Port of the Cloud Database service**.

## Configuration procedures

1. [(Optional) Complete cross-account authorization](https://docs.byteplus.com/en/docs/privatelink/Sharing-RDS-resources-in-a-VPC-with-another-VPC#.5q2l6aqk5LiA77ya5a6M5oiQ6Leo6LSm5Y-35o6I5p2D77yI5Y-v6YCJ77yJ): Authorize Account A to manage the endpoint services within the VPC in Account B.

2. [Configure Endpoint Service](https://docs.byteplus.com/en/docs/privatelink/Sharing-RDS-resources-in-a-VPC-with-another-VPC#.5q2l6aqk5LqM77ya6YWN572u57uI56uv6IqC54K55pyN5Yqh): Create an endpoint service associated with the RDS\-type service resource. This serves as the instance carrier for the shared service resource and authorizes the endpoint in Account A to access the endpoint service in Account B.

3. [Create Interface Endpoint](https://docs.byteplus.com/en/docs/privatelink/Sharing-RDS-resources-in-a-VPC-with-another-VPC#.5q2l6aqk5LiJ77ya5Yib5bu65o6l5Y-j57uI56uv6IqC54K5): Create an interface endpoint, which serves as the access point for the VPC in Account A to access shared service resources within other VPCs.

4. [Configure Endpoint Security Group](https://docs.byteplus.com/en/docs/privatelink/Sharing-RDS-resources-in-a-VPC-with-another-VPC#.5q2l6aqk5Zub77ya6YWN572u57uI56uv6IqC54K55a6J5YWo57uE): Allow the RDS service resource port in the inbound rules of the endpoint's security group.

5. [Result Verification](https://docs.byteplus.com/en/docs/privatelink/Sharing-RDS-resources-in-a-VPC-with-another-VPC#.5q2l6aqk5LqU77ya57uT5p6c6aqM6K-B): Use the `mysql` command to connect to the endpoint domain name and verify that vpc\-01 can normally access the shared RDS service resource via PrivateLink.

## Configuration procedures

### Step 1: Complete cross\-account authorization (optional)

When Account A needs to create and manage an endpoint service on behalf of Account B to automate the establishment of network connectivity, the following steps can be completed for cross\-account IAM authorization on BytePlus.

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) using account B.

2. In the left\-side navigation pane, select **Role** and click **Create Role** to configure the following parameters.

   1. Trusted identity type: Select account

   2. Trusted identity: Select other accounts

   3. Account ID: Enter account A's ID

   4. Role name: User\-defined, for example: forRDS

   5. Policy: Select PrivateLinkEndpointServiceFullAccess

3. Click **Submit** to complete role creation and authorization.

### Step 2: Configure endpoint service

1. Use the temporary AK/SK obtained from Account B to call the [CreateUniqueResourceTypeVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateUniqueResourceTypeVpcEndpointService) API, create the endpoint service, and record the returned **ServiceId**. A sample request is as follows:

   > **tip**

   > In the following examples: Replace the value of **Resource.InstanceId** with the **Instance ID of the cloud database service**. Replace the value of **Resource.ResourceId** with the **ID of the connection endpoint**.

   ```Plain Text
   GET /?Action=CreateUniqueResourceTypeVpcEndpointService&Version=2020-04-01&Resource.ResourceType=RDSMySQL&Resource.InstanceId=mysql-53b1f339****&Resource.ResourceId=mysql-53b1f339****-cluster-2ghyj78f****&ZoneIds.1=cn-guangzhou-a HTTP/1.1
   Host: open.volcengineapi.com
   Service: privatelink
   Region: cn-guangzhou
   ```

2. Use the temporary AK/SK obtained from Account B to call the [DescribeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes) API, query the name (**ServiceName**) of the endpoint service, and record it.

3. Use the temporary AK/SK obtained from Account B to call the [AddPermissionToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AddPermissionToVpcEndpointService) API to add an allowlist to the endpoint service. Sample request:

   > **tip**

   > In the following examples: Replace the value of **ServiceId** with the **ID of the endpoint service**. Replace the value of **PermitAccountId** with the **ID of Account A**.

   ```Plain Text
   GET /?Action=AddPermissionToVpcEndpointService&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&PermitAccountId=210005**** HTTP/1.1
   Host: open.volcengineapi.com
   Service: privatelink
   Region: cn-guangzhou
   ```

### Step 3: Create interface endpoint

1. Log in to the Endpoint console using Account A.

   > **tip**

   > If cross\-service role authorization has not been performed, please complete the authorization first according to the prompts on the page.

2. Click **Create Endpoint** and see the table below to configure the relevant parameters.

   |Parameter |Value |
   |---|---|
   |**Basic information** ||
   |Regions |China (Guangzhou） |
   |Name |endpoint\-01 |
   |Topic |Interface |
   |**Endpoint service resources** ||
   |Add method |Search by service name |
   |Endpoint Service |com.volces.privatelink.cn\-guangzhou.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
   |**Network Configuration** ||
   |VPC |vpc\-01 |
   |AZs and Subnets |Availability Zone A, subnet\-01 \| Auto\-assign IP, 192.168.1.0/24 |
   |Security group |Default\-sg |

3. Click **Confirm order** according to the console instructions to review and confirm the Legal.

4. Click **Buy now** to complete the purchase.

5. Click **Go to console** to view and record the domain name of the created endpoint instance, which will be needed during [Verification](https://docs.byteplus.com/en/docs/privatelink/Sharing-RDS-resources-in-a-VPC-with-another-VPC#.5q2l6aqk5LqU77ya57uT5p6c6aqM6K-B).

### Step 4: Configure endpoint security group

1. Click the name of the target endpoint and select the **Security Group** tab.

2. Click the name of the security group and select the **Access rules** tab.

3. Click **Add rule** and see the table below to configure the endpoint security group.

   |No. |Priority |Strategy |Protocol type |Port range |Source |Description |
   |---|---|---|---|---|---|---|
   |1 |100 |Allow |TCP |3306<br><br>> **tip**<br><br><br>> Configure this parameter as the **Port of the cloud database service** and modify it according to your actual configuration.​​<br> |0.0.0.0/0 |Allow all clients to access the cloud database service through this endpoint |
   |2 |100 |Allow |ICMP |ALL |100.64.0.0/10 |Allow the PrivateLink service to access the cloud database service |

   > **tip**

   > If the endpoint security group already contains an inbound rule with the protocol type set to ICMP and the source address set to 0.0.0.0/0, there is no need to configure the second rule.

4. Click **Confirm** to complete the action.

### Step 5: Verification

1. Log in to the Elastic Compute Service (ECS) instance ecs\-01. For details, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. See [Connecting to a cloud database instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/connect_instance) to verify that ecs\-01 in Account A can normally access the cloud database service.

   In the final command, replace  *<connection_address\>*  with the **Endpoint domain name**.​​
