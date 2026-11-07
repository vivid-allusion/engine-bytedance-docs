---
title: "Creating a CLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-01"
---

## Scenarios

This topic describes how to create a Classic Load Balancer (CLB) instance. Before creation, confirm that you have completed the relevant planning and preparation. For more information, see [Planning and Preparation](https://docs.byteplus.com/en/docs/clb/Planning-and-preparation).

## Action description

The maximum number of CLB instances created per account per region is 60. If the default quota does not meet your needs, please go to Quota Center to increase the corresponding quota.

## Procedures

1. Log in to the [CLB Console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Create CLB.

4. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Example |
   |---|---|---|
   |**Basic information** || |
   |Billing method |Select a billing method for the CLB instance.<br><br><br>* Pay\-as\-you\-go: a postpaid method charging by usage duration.<br><br>* Subscription: A prepaid metering method that charges based on your purchased duration. |Subscription |
   |Regions |Select the region where the CLB instance is located. |China (Shanghai) |
   |Availability zone |Select the availability zone where the CLB instance is located. Availability Zones supported by each Region can be queried through the DescribeZones API.<br><br><br>* When a region supports primary and secondary availability zones, the CLB instance deploys across two availability zones.<br><br>   * By default, the primary availability zone is enabled and the secondary availability zone does not carry traffic under normal conditions.<br><br>   * When the primary Availability Zone fails, the system automatically switches to the secondary Availability Zone to ensure continuous CLB service.<br><br>* If a region does not support primary and secondary availability zones, the CLB instance deploys in only one availability zone, which is the primary availability zone by default. |* Primary: Availability Zone A<br><br>* Secondary: Availability Zone B |
   |Name |Enter the name of CLB instance. |clb\-1 |
   |**Network Configuration** |||
   |IP version |Select the IP version of the CLB instance.<br><br><br>* IPv4: Only IPv4 is supported.<br><br>* Dual\-stack: supports both IPv4 and IPv6. |IPv4 |
   |Network type |Select the network type of the CLB instance. For details, see [Product type and specification](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).<br><br><br>* Public network: public CLB applies for a public IP simultaneously when created and binds it, both having the same lifecycle.<br><br>* Private network: private CLB can bind a public IP independently if public service is needed.<br><br><br>> **tip**<br><br><br>> When the IP version is set to Dual\-stack, only private networks are supported. Both IPv4 and IPv6 private network accesses are enabled by default.<br><br><br><br>* > To access the IPv4 network, either configure the parameter Access to Internet when creating the CLB instance, or Associate an Elastic IP (EIP) after the CLB instance is successfully created.<br><br><br>* > To access the IPv6 internet, enable IPv6 Internet bandwidth for the CLB instance.<br> |Public |
   |VPC |Select the private network where the CLB instance belongs. |VPC01 |
   |Subnet |Select the subnet to which the CLB instance belongs. |subnet01 \| 192.168.3.0/24 |
   |IPv4 address |Set the CLB instance IPv4 address; modification is not supported after creation.<br><br><br>* Auto\-assign IP: the system automatically assigns an available IPv4 address from the selected subnet.<br><br>* Manual IP assignment: Manually assign an available IPv4 address from the selected subnet. Batch creation of CLB instances is not supported. |Automatic IP assignment |
   |IPv6 address |For Dual\-stack IP versions, configure the IPv6 address for the CLB instance.<br><br><br>* Auto\-assign IP: The system automatically assigns an available IPv6 address from the selected subnet.<br><br>* Manual IP assignment: Manually assign an available IPv6 address from the selected subnet. Batch creation of CLB instances is not supported. |Automatic IP assignment |
   |Allowing backend security group |Enable the **Allow backend security group** feature. After enabling, the security groups of backend servers in the backend server group (server type only) no longer verify CLB traffic and allow it by default. |Check |
   |Internet Access |This parameter appears only when the CLB network type is private. You can bind an existing public IP to the private CLB instance as needed. |Checked, eip\-h1wgehsn23s\*\*\*\* |
   |**Associate EIP (only available when CLB network type is internet)**  || |
   |ISP |The ISP of the EIP. Only supports BGP (multi\-line) by default. |BGP (multi\-line)  |
   |Metering method |When the CLB instance billing method is pay\-as\-you\-go, you can select the EIP billing method.<br><br><br>* Pay\-by\-bandwidth: after specifying a bandwidth limit, fees are based on usage duration and unrelated to actual traffic.<br><br>* Pay\-by\-data\-transfer: after specifying a bandwidth limit, fees are based on the actual outbound public traffic and unrelated to usage duration.<br><br><br>> **tip**<br><br><br>> When the public CLB instance billing method is subscription, its EIP billing method is also subscription.<br> |\- |
   |Bandwidth cap |Maximum bandwidth of the EIP. Unit: Mbps.<br><br><br>* Subscription: Range is 1–500 Mbps.<br><br>* Pay\-by\-bandwidth: Range is 1–500 Mbps.<br><br>* Pay\-by\-data\-transfer: Range is 1–200 Mbps. |20Mbps |
   |Bandwidth Package |When the EIP billing method is pay\-by\-bandwidth or pay\-by\-data\-transfer, select Add to [the Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package) as needed.<br><br><br>* If left unchecked, you can [add the EIP to a Bandwidth Package](https://docs.byteplus.com/en/docs/clb/CLB-instances-08) as needed in the next step.<br><br>* If checked, you can select an IPv4 Bandwidth Package in the current region that has the same security protection as your EIP.<br><br>   After being added to the Bandwidth Package, the traffic fee or bandwidth fee and bandwidth limit of the above billing method become invalid, and the EIP shares the bandwidth of the Bandwidth Package. If you remove the EIP from the Bandwidth Package, EIP's original billing method and maximum bandwidth restore valid. |No |
   |**Instance type** |||
   |Specification |Different specifications correspond to varying Max Connection, New Connections Per Second, Queries Per Second (QPS), bandwidth. Select the specification that best fits your performance requirements and business scenarios. For detailed specifications, see Product types and specifications. |Small I |
   |**More information** |||
   |Duration |When the CLB billing method is Subscription, enter the purchase duration for the CLB instance. |1 month |
   |Automatic renewal |When the CLB billing method is Subscription, select whether to enable auto\-renewal. This feature is disabled by default. After selecting automatic renewal, the default renewal period is 1 month; if the account balance is sufficient, renewal continues automatically without limit. |Not selected |
   |Instance count |Enter the number of CLB instances to create.<br><br>> **tip**<br><br><br>> When the CLB instance is of enhanced protection internet type, the maximum number of CLB instances created at one time cannot exceed the remaining number of internet IPs available in the associated safety package.<br> |2 |
   |Ordered suffix |When creating multiple CLB instances, you can add numeric suffixes to the instance names. The starting number defaults to 1, meaning suffixes like \-1, \-2 will be sequentially appended to the CLB instance. |Checked, 1 |
   |Affiliated Project |Select the project to which the CLB instance belongs. After a public CLB instance is added to a project, the public IP created simultaneously will also join the same project. For more information, see [Project management](https://docs.byteplus.com/en/docs/clb/Project-management). |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources. For more information, see [Tag management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the add icon, enter the tag key and tag value, and add tags to the CLB instance. |* Tag key: clb\-key<br><br>* Tag value: clb\-test |

5. Follow the console guidance to review and accept Legal.

6. Click **Buy now** to complete the action.

## What to do next

After the CLB instance is created successfully, you need to configure the listener and backend server group for it to function properly. For detailed steps, see [Creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-a-TCP-listener) and [Creating a backend server group](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group).

## Related documents

[CreateLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateLoadBalancer)
