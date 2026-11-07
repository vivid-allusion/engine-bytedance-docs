---
title: "Adding access entrance"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Adding_access_entrance"
---

The system uses a LoadBalancer (CLB) as the network entrance for the APIG instance. This article explains how to bind a custom CLB instance to an APIG instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When creating an APIG instance, the system automatically creates and binds a managed LoadBalancer (CLB) instance to provide a network entrance for the APIG instance. Additionally, to enhance the availability of your APIG instance, you can also bind your own CLB instance. The descriptions and differences of different CLB instance types are shown in the table below.


|Type of instance |Instance name |Manage mode |Optional |Description of differences |
|---|---|---|---|---|
|Managed LoadBalancer instance |Default(Public/Private) |Managed |Mandatory |* When creating an APIG instance, a LoadBalancer instance is created simultaneously.<br><br>* When creating an APIG instance, the network type and specifications of the managed LoadBalancer instance are configured simultaneously. For more details refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance). |
|Custom CLB instance |User\-defined |User managed maintenance |Optional |* When creating an APIG instance, binding a custom LoadBalancer instance is not supported. Binding is only supported after the APIG instance has been created.<br><br>* The network type and specifications of the custom LoadBalancer instance are configured at the time of create LoadBalancer instance, for more details refer to [Creating a LoadBalancer instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-01).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The custom LoadBalancer instance must be in the same VPC as the APIG instance.</div><br> |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An APIG instance has been created. For details refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A custom CLB instance has been created. For details refer to [Creating a LoadBalancer instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-01).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya57uR5a6a6Ieq5a6a5LmJIENMQiDlrp7kvos="></span>
### Step 1: Bind a custom CLB instance


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Instances Management**, in the Instances list, select the target instance, click the instance name, and enter the details page of the instance.

4. Select the **Overview** tab, click **Add Access**, and bind a new CLB instance to the current instance.

5. In the existing LoadBalancer instance list, select the CLB instance bound to the current APIG.

6. Click **confirm** to complete the configuration.


<span id=".5q2l6aqk5LqM77ya6YWN572u5a6J5YWo57uE"></span>
### Step 2: Configure Security groups


1. Log in to the [VPC console](https://console.byteplus.com/vpc).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, select **Security groups**, and find the APIG\-created security group in the list, formatted as `apig-sg-xxx`. Click on the security group name to enter the details page of the security group.

4. Select **Access rules** \> **Inbound rules** tab, click **add rules**, and configure the rules for this security group.

   * If Public NAT for internet endpoint is needed, then allow the segment `0.0.0.0/0`, with the port range of `1-65535`.

   * If only intranet access is needed, then allow the segment `100.64.0.0/10` and VPC subnet, with the port range of `1-65535`.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

<span id=".6I635Y-W572R5YWz5Zyw5Z2A"></span>
### Obtain the API gateway address


1. In the left navigation bar select **Instances Management**, in the Instances list, select the target instance, click the instance name, and enter the details page of the instance.

2. Select the **Overview** tab, in the **Access Entry** list, view the LoadBalancer instance information bound to the current APIG instance. In the **Type of network**, the IP address of the APIG instance is displayed.


<span id=".6K6_6Zeu5Lia5Yqh"></span>
### Access service

Create a Service, bind the Domain name to a custom CLB address, and configure Upstream and routing. After that, you can access the business through the custom CLB.
