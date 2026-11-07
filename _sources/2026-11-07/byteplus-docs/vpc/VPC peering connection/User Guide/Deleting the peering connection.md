---
title: "Deleting the peering connection"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-the-peering-connection"
---

<span id="wchmo3V4"></span>
## Action notes


* Once deleted, a peering connection cannot be restored. Please operate with caution.

* After a peering connection is deleted, the route entry whose next hop is that peering connection is automatically deleted.

* After deleting a peering connection, please promptly handle the security group rules and network ACL rules configured for it.


<span id="BuIqkX4O"></span>
## Procedures


1. Log in to the [Peering Connection console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/peerConnection).

2. In the top menu bar, select the target region and project.

3. Click **Delete** to the right of the target peering connection.

4. Click **Delete** to complete the action.
