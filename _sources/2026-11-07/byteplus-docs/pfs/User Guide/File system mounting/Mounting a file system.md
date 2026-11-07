---
title: "Mounting a file system"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Mounting-a-file-system"
---

This topic introduces the prerequisites and operation steps for mounting the PFS file system.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Before mounting PFS, please make sure you have completed the following steps:


* You have created a file system.For specific steps, please refer to [Creating a file system](https://docs.byteplus.com/docs/pfs/Creating-a-file-system).

* You have created the mount service and bound the file system. For specific steps, please refer to [Creating a mount service](https://docs.byteplus.com/docs/pfs/Creating-a-mount-service) and [Binding a file system](https://docs.byteplus.com/docs/pfs/Binding-a-file-system).

* The nodes for mounting PFS file system have been created within the VPC.For specific steps, please refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">PFS only supports mounting to nodes in the same region.   </div>
   

* Cross\-service authorization has been completed. For specific steps, please refer to [Cross-service authorization](https://docs.byteplus.com/docs/pfs/Cross-service-authorization).


<span id=".77yI5LuF5pm6566X54mI6ZyA6KaB77yJ5q2l6aqk5LiA77ya5Li66auY5oCn6IO96ZuG576k57uR5a6aLXZlcGZzLeaWh-S7tuezu-e7nw=="></span>
## Step 1: Add a security group to the ECS instance

Before mounting the PFS file system, you need to associate the same security group with the ECS instance as the PFS management node.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="warning">After creating the mount service, ECS will automatically create three PFS management nodes. You can log in to the <a href="https://console.byteplus.com/vepfs">PFS console</a> to view the corresponding management node information.</div>


* <div data-tips="true" data-tips-type="warning">The security group of the PFS management node mainly opens the relevant IP ports in the same VPC network segment and the 100.64.0.0/10 cloud service network segment in the inbound direction. If your client node has other network requirements and needs to open additional network segments and ports, please bind other security groups by yourself, as long as they do not conflict with the current security group rules.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top navigation bar, select the region of the target instance.

3. In the left navigation bar, select **Instances & Images** \> **Instances**.

4. View the security group information of the PFS management node.

   1. On the **Instances** page, locate the management node instance of PFS and click its name.

   2. On the instance details page, you can view the security group name associated with the network card.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also obtain security group information based on the mounted service ID. The naming format for security groups is <code>sg-<mounted service ID></code> or <code>sg-<file system ID>-<mounted service ID></code>.      </div>
      

5. Add security group information to the mounted ECS instance.

   1. On the **Instances** page, locate the ECS instance where PFS needs to be mounted, and click the instance name.

   2. On the instance details page, click **Network Interface** tab.

   3. On the **Network Interface** tab, click network interface that needs to be associated with a security group.

   4. In the network interface details panel, click **Associated Security Groups** tab.

   5. On the **Associated Security Groups** tab, click **Change**.

   6. In the **Change Security Group** panel, select the confirmed security group information in step 4 and click **Confirm.** 

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If your ECS instance has multiple network interfaces, please make sure to associate the security group with the network interface where the mounted IP is located.      </div>
      

<span id=".5q2l6aqk5LiJ77ya5oyC6L295paH5Lu257O757uf"></span>
## Step 2: Mounting a file system.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">Before mounting the file system, please make sure that your instance has been properly associated with the corresponding security group. After associating the security group, you can log in to the PFS management node to mount the PFS file system.</div>



1. Log in to the PFS management node. For specific steps, please refer to [Using the console to log on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you create the mount service, ECS will automatically create three PFS management nodes. You can log in to the <a href="https://console.byteplus.com/vepfs">PFS console</a> to view the corresponding management node IP and login password.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The format of the PFS management node name is <code>client-{mount service ID}-{number}</code> or <code>client-{PFS file system ID}-{mount service ID}-{number}</code>.   </div>
   

2. According to the login method of the instance, execute the corresponding command to mount the PFS file system.

   
   <Tabs>
   <Tab zoneid="ZhvHAnzPFx" title="Password login">
   <TabTitle>Password login</TabTitle>
   
   ```JSON
   vepfs add password {ECS IP address}
   ```
   
   
   Parameter description is as follows:
   
   
   * You need to replace {ECS IP address} with the private IP address of the ECS instance you want to mount.
   
   * You can add multiple mount addresses, separated by spaces. Up to 50 nodes can be mounted simultaneously. If you need to mount a large number of nodes, it is recommended to use this method for batch mounting.
   
   * After executing the mount command, you need to manually enter the password for the mount node, and then the system will automatically mount the PFS file system.
   
   * When mounting multiple instances simultaneously, you can add the \-p option in the command to use the default password. For example, you can use `vepfs -p xxx add password xxx xxx xxx` to add the default password.
   
   
   </Tab>
   <Tab zoneid="qv6FcDG4JB" title="Certificate login">
   <TabTitle>Certificate login</TabTitle>
   
   <div data-tips="true" data-tips-type="warning">Note</div>
   
   
   <div data-tips="true" data-tips-type="warning">If your instance is logged in using a certificate, before executing the mount command, you need to copy the key file to the PFS management node.</div>
   
   
   ```JSON
   vepfs -r add key {key_path} {ECS IP address}
   ```
   
   
   Parameter description is as follows:
   
   
   * You need to replace `{key_path}` with the key file path of the ECS instance.
   
   * You need to replace `{ECS IP address}` with the private IP address of the ECS instance you want to mount.
   
   * You can add multiple mount addresses, separated by spaces; if you need to mount multiple nodes at the same time, all nodes must use the same key file.
   
   
   </Tab>
   </Tabs>
   


<span id=".5q2l6aqk5Zub77ya5p-l55yL5oyC6L295oOF5Ya1"></span>
## Step 3: Check the mounting status.


1. Log in to the ECS instance mounting the PFS file system. For specific steps, please refer to [Using the console to log on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run `df -h` to check the mount situation.

   If the Filesystem column in the echo information displays `vepfs` or `fs_instance ID`, it indicates that the mounting is successful. In this article, displaying vepfs is used as an example.

   ```JSON
   Filesystem      Size  Used Avail Use% Mounted on
   devtmpfs        3.8G     0  3.8G   0% /dev
   tmpfs           3.8G     0  3.8G   0% /dev/shm
   tmpfs           3.8G  8.6M  3.8G   1% /run
   tmpfs           3.8G     0  3.8G   0% /sys/fs/cgroup
   /dev/vda1        50G  3.7G   44G   8% /
   vepfs           6.0T   12G  6.0T   1% /mnt/vepfs
   tmpfs           777M     0  777M   0% /run/user/0
   ```
   


<span id=".5YW25LuW5pON5L2c"></span>
## Other operations


* View mount node status

   You can log in to the management node and execute the following command to check the PFS mounting node status.

   ```Plain
   mmgetstate -N  {IP address}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Support adding multiple IP addresses, separated by commas.   </div>
   

   The returned information is as follows, and the Node name returned is the ID of the mounting node.

   ```Plain
   Node number  Node name                GPFS state  
   ---------------------------------------------------
              4  iv-ybqk7fafww8rx7p8****  active  
   ```
   

* View all node statuses

   You can log in to the management node and execute the following command to check the status of all PFS nodes.

   ```Plain
   mmgetstate -a
   ```
   

   The return information is as follows.

   ```Plain
   Node number  Node name                                       GPFS state  
   ------------------------------------------------------------------------
              1  client-vepfs-cnbj83050aae****-mount-b990****-1  active
              2  client-vepfs-cnbj83050aae****-mount-b990****-2  active
              3  client-vepfs-cnbj83050aae****-mount-b990****-3  active
              4  iv-ybqk7fafww8rx7p8****                         active
   ```
   

* View the IP address corresponding to Node

   You can check the IP address corresponding to the node name in`/etc/hosts` file.
