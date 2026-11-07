---
title: "Billing"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/VPC-peering-connection-billing-instruction"
---

## Billing rules

Creating VPC peering connections between two ends in the same region does not incur a fee; for VPC peering connections across regions, all communication traffic is billed based on data transfer uniformly by [Cloud data transfer](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/What_is_Cloud_Data_Transfer).

## Traffic description

In cross\-region scenarios, the billing traffic is as follows:

* **Same account**: The total outbound traffic from both the sending and receiving VPC ends is combined and billed together.

* **Cross\-account**: Each account independently counts the outbound traffic of its local VPC, and fees are settled separately.

##
