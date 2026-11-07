---
title: "Access control of API server"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Can-I-configure-access-control-for-the-CLB-instance-used-by-the-API-server"
---

To prevent unauthorized access to the API server of a cluster, it is recommended that you set up access control on the CLB instance working for the API server. The following content will introduce how to set up access control on a CLB.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Generally, API servers need to be accessible on the Internet to allow clients to operate clusters remotely. The VKE now can provide Internet access to API servers through CLB or by allocating public IP addresses. However, exposing the API server directly to the Internet without any restrictions poses significant security risks. By configuring source IP\-based access control on the CLB, you can restrict access to the API server to only specific clients instead of exposing the EIP to all addresses.

The CLB instance is able to filter requests from certain source IPs based on an allowlist or blocklist, which is created by binding access control policy groups to listeners. An access control policy group contains a set of IP addresses or CIDR blocks. Once a policy group is bound to a CLB listener, the listener matches the source IPs of incoming requests against the entries in the group. Two matching methods are supported: There are two comparison methods:


* Allowlist: Only source IP addresses matching the policy group will be allowed to access the API server of the cluster.

* Blocklist: The source IP addresses matching the policy group will be denied access to the API server of the cluster.


The following figure shows how a listener of a CLB instance works to control access:

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Apart from ensuring specified client IPs are able to access API servers when configuring policy groups for access control, the IPs of the cluster control plane and the console need to be taken into consideration as well. Otherwise, the cluster will not work properly. These IPs include:

   * IP addresses in subnet `100.64.0.0/10`: Health checks will be sent by the control plane to the cluster from these IPs.

   * The VPC subnets where nodes are running: The nodes in the cluster will send requests to API servers from these subnets.

* Enter the correct source IPs of the client requests, and make sure that no Source Network Address Translation (SNAT) is performed along the access path.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

The following section describes how to configure a CLB to allow access only from specific clients by using an allowlist.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**. On the page that appears, find the target cluster and click its name.

3. On the **Overview** tab, find **Cluster API Server configuration** and click the Load Balancer instance name.

4. In the **Overview** tab of the CLB instance page, disable **Modification Protection**.

5. Click the **Listener** tab and click **Edit listener** in the **Actions** column to enable **Access control** for the CLB instance. Then, configure the allowlist for access control of the CLB instance. For details, see [Access control](https://docs.byteplus.com/en/docs/clb/Access-control-list-01) .

6. To prevent subsequent misoperations, we recommend that you enable **Modification Protection** again on the **Overview** tab of the CLB instance.
