---
title: "Default Security Group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Default-Security-Group"
---

The default security group acts as a fallback configuration, ensuring that every ENI is associated with a security group.

## Action description

For convenience, the system automatically creates a default security group when a VPC is created:

* The default security group comes with several commonly used rules pre\-configured. For details, see the **Default security group rule** below.

* The Default security group cannot be manually deleted; it is deleted only when its associated VPC is deleted.

* Users can add, delete, and modify rules within the default security group.

## Default security group rules

Details of the default rules for the default security group are as follows:

* **Inbound rule**

   |Inbound |Priority |Strategy |Agreement |Port range |Source |Description |
   |---|---|---|---|---|---|---|
   |Inbound |100 |Allow |ALL |ALL |This security group |Allow ECSs within the same security group to communicate with each other |
   |Inbound |100 |Allow |ICMP |ALL |0.0.0.0/0 |Allows the use of the ping program to test the connectivity of ECSs |
   |Inbound |100 |Allow |ICMPV6 |ALL |::/0 |Allows the use of the ping program to test the connectivity of ECSs |
   |Inbound |100 |Allow |TCP |22 |0.0.0.0/0 |Allow SSH remote login to Linux servers |
   |Inbound |100 |Allow |TCP |80 |0.0.0.0/0 |Allow access to websites using the HTTP protocol |
   |Inbound |100 |Allow |TCP |443 |0.0.0.0/0 |Allow access to websites using the HTTPS protocol |
   |Inbound |100 |Allow |TCP |3389 |0.0.0.0/0 |Allows remote login to Windows ECS |

* **Outbound rule**

   |Outbound |Priority |Strategy |Agreement |Port range |Destination address |Description |
   |---|---|---|---|---|---|---|
   |Outbound |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow all IPv4 traffic |
   |Outbound |100 |Allow |ALL |ALL |::/0 |Allow all IPv6 traffic |
