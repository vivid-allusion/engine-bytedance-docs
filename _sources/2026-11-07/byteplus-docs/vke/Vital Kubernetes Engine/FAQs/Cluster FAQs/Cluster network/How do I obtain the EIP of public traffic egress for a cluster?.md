---
title: "How do I obtain the EIP of public traffic egress for a cluster?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-get-the-egress-EIP-for-forwarding-internet-traffic-out-of-a-cluster"
---

VKE supports public access for nodes and applications within clusters by using NAT Gateway of BytePlus.

The EIP of public traffic egress for a cluster can be obtained only if the public access feature is enabled for the cluster.


* Enable public access when creating a cluster. For detailed information, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Enable public access for an existing cluster. For detailed information, see [How do I manually enable Public NAT for Internet endpoint for a cluster?](https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster)


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, find the target cluster and click the name of the cluster.

3. On the **Overview** tab of the **Overview** page, click the name of the VPC to which the cluster belongs to go to the [VPC console](https://console.byteplus.com/vpc).

4. On the **Overview** page of the VPC, click **NAT Gateway**.

5. The address displayed in the **EIP addresses** column on the **NAT Gateway** page is the EIP of public traffic egress for a cluster.
