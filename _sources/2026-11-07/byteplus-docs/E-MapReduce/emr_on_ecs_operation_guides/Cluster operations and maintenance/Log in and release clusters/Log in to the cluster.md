---
title: "Log in to the cluster"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_log_in_to_the_cluster"
---

This article describes how to log in to an EMR cluster using the Volcano Engine E\-MapReduce (EMR) console and SSH.

<span id="_1-前提条件"></span>
# **Prerequisites**


1. The EMR cluster has been successfully created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. To log in to the cluster via SSH, ensure that both the local server and the ECS instance ID of the primary node in the EMR cluster are bound to an elastic public IP. For details, see [Bind public IP](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP).

3. Access [http://myip.ipip.net/](http://myip.ipip.net/) from your local machine to obtain your local IP address, and add it to the allowlist in **Security Group \> Access Rules** of the EMR cluster. For details, see [Security group access rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).


<span id="_2-登陆主节点"></span>
# **Log in to the primary node**

<span id="_2-1-emr-控制台登录"></span>
## Obtain primary node information


1. Log in to[E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)

2. In the top menu bar, select the region and project space from the drop\-down list as needed.

3. Click Resources \> on ECS \> Cluster name \> Nodes \> MasterGroup to view the details of the primary node, including the IP address and more.


<span id="61c537f3"></span>
## Log in to the primary node

The procedure for logging in to the EMR primary node is identical to that for logging in to an ECS server. Multiple login methods are supported, such as via the console and SSH. For details, see the [Log in to ECS instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance) documentation.

The following highlights the key points for logging in via the console. For more configuration details, see [Log in to Linux instance via ECS console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).


1. Click `master-1-1 ID` under the primary node to enter the ECS instance page, then click the **Remote connection** button in the upper right corner of the ECS instance page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The domain name conventions for nodes may vary across different EMR versions, so the "emr\-master\-1\-1 address" above can be adjusted accordingly by referring to EMR's <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5648539066d84e54adc0edede7936a32~tplv-goo7wpa0wc-image.image) </span>

2. Select a remote connection method (ECS Terminal is recommended), and click the **Log in now** button to enter the login page.

3. Enter the cluster authentication information. You can choose one of the following two authentication methods to log in:

   * Password authentication: If you selected **Password** authentication when creating the cluster, enter the password set during cluster creation here.

   * Certificate authentication: If you selected **Key pair**certificate authentication when creating the cluster, upload the key authentication file here.


<span id="_3-登录其他节点"></span>
# **Log in to other nodes**

After logging in to the primary node using either of the above methods, you can log in to other nodes by using the hostnames of the remaining nodes, as shown below:

```Bash
#Enter the master node
ssh [主节点的公网IP地址] -i  emr-key.pem -l root
#Log in to the core node using the hostnames of the other nodes
ssh emr-core-1
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2263b4c7828dd1e3f8f5adebe206233.png) </span>
