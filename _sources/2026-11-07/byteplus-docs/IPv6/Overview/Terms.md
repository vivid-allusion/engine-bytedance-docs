---
title: "Terms"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Basic_concept"
---


|Term |Description |
|---|---|
|IPv6 address |IPv6 addresses allocated by the system to instances in the VPC. The IPv6 address is 128 bits in binary, generally grouped in 16 bits separated by colons (:). Each group is typically represented by 4 hexadecimal digits, e.g., 2001:xxx:0102::0304. |
|IPv6 gateway instance |The operating carrier of the IPv6 gateway service. Creating an IPv6 gateway instance is a prerequisite for IPv6 internet configurations. |
|IPv6 Internet bandwidth |The bandwidth for IPv6 internet traffic, which determines the internet communication capacity of the IPv6 address. |
|Egress Only rule |A management rule for IPv6 Internet traffic, which restricts IPv6 traffic from the Internet accessing the Virtual Private Cloud (VPC). |
|VPC IPv6 CIDR block |IPv6 CIDR blocks for the VPC. After enabling IPv6 for the VPC, the system automatically allocates an IPv6 CIDR block with a subnet mask of `/56` to the VPC. |
|Subnet IPv6 CIDR block |IPv6 CIDR blocks for subnets in the VPC. After enabling IPv6 for the VPC, you can enable IPv6 CIDR for subnets. After enabling IPv6 for the subnet, the default allocated subnet mask is `/64`. You can customize the last 8 bits of the subnet IPv6 CIDR block by typing in decimal numbers from 0 to 255. |
