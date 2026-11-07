---
title: "Configuring IPv4/IPv6 dual-stack networks"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-IPv4_IPv6-dual-stack-networking"
---

VCI supports IPv4 and IPv6 dual\-stack networking. Compared with IPv4, IPv6 drastically expands the available address space.  This topic describes how to configure IPv4/IPv6 dual\-stack networking for VCIs.

Both the primary and secondary NICs of VCI pods support IPv4 and IPv6 dual\-stack networking. The addition of IPv6 support enables pods to run in dual\-stack mode.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: The dual\-stack networking feature is in the beta stage. To use this feature, submit an application.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

IPv6 is in the beta stage for other BytePlus products (such as VPC, VKE, CLB, and ALB). To use IPv6 networking in these products, submit an application for this feature in **individual products**. The following products are used in the examples in this topic. Please submit an IPv6 beta application in advance for each relevant product:


* [VPC](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-IPv6-for-a-VPC)

* [Vital Kubernetes Engine](https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE)

* [IPv6 gateway](https://docs.byteplus.com/en/docs/IPv6/What-New)


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An IPv4/IPv6 dual\-stack cluster has been created. For detailed steps, see [Creating IPv4/IPv6 dual-stack clusters with VKE](https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE).

* A container image has been created. You can use images from BytePlus CR as well as images from third\-party container registries. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use images uploaded to CR, ensure that the CR instance has been granted access to the VPC used by the dual\-stack cluster. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account">Connecting to the VPC of the current account</a>.   </div>
   

<span id=".6YWN572u6K-05piO"></span>
## Configuration description

Configure IPv4/IPv6 dual\-stack networking for VCIs by adding pod annotations.

The following table describes the annotations.


|Annotation key |Annotation sample value |Description |Required |
|---|---|---|---|
|vci.vke.volcengine.com/pod\-ip\-family |ipv4 |Protocol stack used by the primary NIC of the VCI pod. Valid values:<br><br><br>* **ipv4**: (Default) Use the IPv4 stack.<br><br>* **dualstack**: Use IPv4/IPv6 dual\-stack networking. |Required for this scenario |
|vke.volcengine.com/preferred\-network\-interface |Object type |Secondary NIC configuration of the VCI pod. The value is an array, with each object in the array representing the configuration of a NIC. For details, see the [Secondary NIC configuration](https://docs.byteplus.com/en/docs/vke/Configuring-IPv4_IPv6-dual-stack-networking#.6L6F5Yqp572R5Y2h6YWN572u5L-h5oGv6KGo) table below.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: Secondary NIC configuration for VCI pods is in the beta stage. To use it, please submit an application.</div><br> |Optional |


<span id=".6L6F5Yqp572R5Y2h6YWN572u5L-h5oGv6KGo"></span>
### Secondary NIC configuration


|Key |Sample value |Description |Required |
|---|---|---|---|
|Type |"Secondary" |ENI type. For a secondary NIC, it must be set to `"Secondary"`. |Required |
|AccountId |21000\*\*\*\* |The ID of the BytePlus root user to which the NIC belongs (tenant ID). Secondary NICs can belong to the same\-tenant or a different tenant. |Required |
|VpcId |vpc\-2d6px\*\*\*\*\*\* |The ID of the VPC to which the NIC belongs. |Required |
|SubnetIds |["subnet\-os74b\*\*\*\*\*\*"] |The ID of the subnet.<br><br><br>* The subnet must belong to the same VPC as the primary NIC of the current VCI pod.<br><br>* The secondary NIC and the primary NIC can belong to the same or different subnets, and the VPC CIDR blocks can overlap. |Required |
|SecurityGroupIds |["sg\-123edf\*\*\*\*\*\*"] |List of security groups to which the ENI is added.<br><br><br>* The specified security groups must be in the same VPC as the ENI.<br><br>* The number of security groups must be equal to or greater than 1. |Required |
|SecondaryPrivateIpAddressCount |1 |Number of secondary private IP addresses for the secondary NIC. Value range: 1–2.<br><br>A secondary NIC must have at least one primary private IP address and can have zero or more secondary private IP addresses.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the secondary NIC uses only the primary private IP addresses, do not specify this parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The total number of EIP addresses that can be bound to a secondary NIC is <code>SecondaryPrivateIpAddressCount + 1</code>.</div><br> |Optional |
|Ipv6AddressCount |1 |Number of IPv6 addresses for the secondary NIC of the VCI pod. Value range: 1–2.<br><br>After you specify this parameter, the system automatically allocates the corresponding number of available IP addresses from the subnet to which the NIC belongs as secondary private IP addresses for the NIC. |Optional |


<span id=".6YWN572u56S65L6L"></span>
## Configuration examples

This topic uses the example of creating a VCI with subnets specified and IPv4/IPv6 dual\-stack networking configured. For detailed steps to create a VCI, see [Creating VCI instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

<span id=".a3ViZXJuZXRlcy3mlrnlvI8="></span>
### Using the Kubernetes approach

The following example demonstrates how to create a Deployment in an IPv4/IPv6 dual\-stack cluster.


1. Connect to the dual\-stack cluster by using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the Deployment. The following `nginx-deployment.yaml` file serves as an example:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following is sample code. In your actual scenario, update the parameter values as needed and delete the comments in the <strong>secondary NIC configuration information</strong> section.   </div>
   

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name:  # Deployment name.
   spec:
     replicas: 2  # Number of Deployment replicas.
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         annotations:
           vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
           vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1nai****  # Subnet ID.
           vci.vke.volcengine.com/pod-ip-family: dualstack  # Protocol stack used by the primary NIC.
           vke.volcengine.com/preferred-network-interface:  # Secondary NIC configuration information.
               '[{
                  "Type":"Secondary",  # Network card type; must be set to "Secondary", which stands for the secondary network card.
                  "AccountId": 21000****, # Tenant ID.
                  "VpcId": "vpc-2d6px******", # VPC ID that the network card belongs to.
                  "SubnetIds":["subnet-os74b94e***"],  # Subnet ID of the secondary network card.
                  "SecurityGroupIds":["sg-123edfgt8***"],  # Security group ID of the secondary network card.
                  "SecondaryPrivateIpAddressCount": 1,  # Number of secondary private IP addresses for the secondary network card.
                  "Ipv6AddressCount": 1  # Number of IPv6 addresses for the secondary network card.
                 }]'
         labels:
           app: nginx
       spec:
         containers:
         - name: nginx
           image: cr-cn-beijing.volces.com/tw/nginx:1.0  # The address and version of the container image. Replace the value with your actual information.
           ports:
           - containerPort: 80
   ```
   

3. Run the following command to create the Deployment.

   ```bash
   kubectl create -f nginx-deployment.yaml
   ```
   

4. Run the following command to query pod information.

   ```bash
   kubectl get pods -o wide
   ```
   

   The expected result is as follows:

   ```bash
   NAME                                READY   STATUS    RESTARTS   AGE   IP            NODE                      NOMINATED NODE   READINESS GATES
   nginx-deployment-6b9cd76fb8-ht2z2   1/1     Running   0          24m   192.168.0.2   vci-node1-cn-shanghai-a   <none>           <none>
   nginx-deployment-6b9cd76fb8-m7krc   1/1     Running   0          24m   192.168.0.3   vci-node1-cn-shanghai-a   <none>           <none>    
   ```
   

5. Run the following command to obtain the IPv4/IPv6 address of the pod.

   ```bash
   kubectl describe pod <your_pod_name>
   ```
   

   The expected output is as follows. The IPv4 and IPv6 addresses of the pod can be found in the `IPs` field:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd3a89467d99fc71b7cebaf5e02d6bd8.png) </span>


<span id=".5o6n5Yi25Y-w5pa55byP"></span>
### Console

This example shows how to create a stateless workload (Deployment). The procedure for creating other workloads is similar. For a detailed description of the procedure and parameter configuration, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VCI does not support DaemonSets. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-limits">Limits</a>.</div>



1. Create a Deployment for **VCI** deployment.

2. Specify the **Instance annotation** parameter during Deployment creation.

3. On the **List of instances** tab of the **Deployment list page**, obtain the IPv4/IPv6 addresses allocated to the VCI.


<span id=".5L2_55SoLWlwdjYt5Zyw5Z2A6L-b6KGM5YWs572R6YCa5L-h"></span>
## Using an IPv6 address for communication over the Internet

After configuring an IPv4/IPv6 dual\-stack network for the VCI pod, the VCI will be automatically allocated an IPv6 address, which can be used directly for network communication within the VPC. To use this IPv6 address for public network communication, use BytePlus IPv6 Gateway.


1. Create an IPv6 gateway. For details, see [Creating IPv6 Gateway instances](https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the VPC where the IPv6 gateway is located is the same as the VPC of the dual\-stack VKE cluster.   </div>
   

2. Enable public bandwidth for the IPv6 address used by the VCI (pod). For details, see [Enabling IPv6 public bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth).

   After public bandwidth is enabled, the VCI can communicate over the Internet by using the IPv6 address.

3. (Optional) You can use the following settings to implement access control and cost management of IPv6 traffic over the Internet.

   * To prevent the IPv6 address from being accessed by public IPv6 endpoints, create an **Egress Only rule**. For details, see [Creating an Egress Only rule](https://docs.byteplus.com/en/docs/IPv6/Create_only_active_outgoing_rules).

   * To share the IPv6 public bandwidth of multiple pods for cost optimization, you can create a shared bandwidth package to share the IPv6 public network bandwidth of these pods. For details, see [Managing shared bandwidth packages](https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package).
