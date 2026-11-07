---
title: "Implement load balancing using CLB"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Implement_load_balancing_using_CLB"
---

This article describes how to implement load balancing and high availability for StarRocks based on the Volcano Engine CLB service.

<span id="_1-使用限制"></span>
## **Limits**

The CLB load balancer and the StarRocks cluster must be in the same VPC and security group.

StarRocks must be a high\-availability cluster. Non\-high\-availability clusters have only a single FE and do not require CLB for load balancing.

<span id="_2-操作步骤"></span>
## **Procedure**


1. Click the "Cluster Management" tab of the EMR cluster, expand the node list of "MasterGroup", and click one of the nodes to obtain the name and ID of the "VPC" and "security group".

2. Go to the CLB[ service page](https://console.volcengine.com/clb/region:clb+cn-beijing/LoadBalancer) and select the "Create Load Balancer" button.

3. Select the CLB according to the actual environment information. For example, the region, availability zone, VPC, and subnet must be the same as those of the EMR cluster. If all network access is internal, select "Private network"; if public access is required, select "Public network" here. You can select the corresponding specification according to the specification limit.

4. Create a server group and associate the ECS instances of the three FEs, binding port 9030, which is the default query port for FE.

5. Add a listener and associate it with the server group created above. Set the listening port to 9030 as well. The remaining parameters can be left as default.

6. On the CLB overview page, find the corresponding IP and access the FE through CLB.


```sql
mysql -h <CLB_IP> -P 9030 -u root
```
