---
title: "Deploying Ceph"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-Ceph"
---

Ceph is an open\-source distributed file system with high reliability, automatic rebalancing, and flexible scalability. It supports object storage, block storage, and file storage. This topic describes how to deploy Ceph.

## Ceph components

RADOS (Reliable Autonomic Distributed Object Store), known as the Ceph storage cluster, is the core component of the Ceph storage system. ​It features high availability, self\-healing, and self\-management, and consists of two core components: Ceph Monitor and Ceph OSD.

* **Ceph Monitor**: Monitors the cluster running status via maps, including the monitor map, OSD map, Placement Group (PG) map, and CRUSH map.

* **Ceph OSD**: Stores data and handles data replication, recovery, backfilling, and rebalancing. Ceph OSD also provides monitoring information to Ceph Monitors by checking the heartbeats of other OSD daemons. Typically, at least three Ceph OSDs are needed to achieve redundancy and high availability.

For more information, refer to [Ceph documentation](http://docs.ceph.org.cn/start/intro/).

## Prerequisites

* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [associated an EIP with it](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* The ECS instance status is **Running**.

## Practice planning

In this best practice, Ceph is deployed with products of the BytePlus platform, specifically ECS instances, VPC, and a public NAT gateway. Below is the planning for these relevant products.

|Product/Service |Provided sample in this topic |Other information |
|---|---|---|
|VPC |* Name: ceph\-vpc<br><br>* IPv4: 172.16.0.0/12 |* Region: Asia Pacific (Johor)<br><br>* Availability zone: ap\-southeast\-1a<br><br>* Subnet name: ceph\-cluster\-subnet<br><br>* IPv4: 172.16.3.0/24 |
|ECS instance |* Name: ceph\-node1<br><br>* Instance type: ecs.g1.xlarge (vCPU: 4, memory: 16 GiB)<br><br>* System volume: 100 GiB<br><br>* Data volume: 200 GiB \* 3 |* Operating system: CentOS 7.6<br><br>* Region: Asia Pacific (Johor)<br><br>* Availability zone: ap\-southeast\-1a<br><br>* Private network address: 172.16.3.76 |
||* Name: ceph\-node2<br><br>* Instance type: ecs.g1.xlarge (vCPU: 4, memory: 16 GiB)<br><br>* System volume: 100 GiB<br><br>* Data volume: 200 GiB \* 3 |* Operating system: CentOS 7.6<br><br>* Region: Asia Pacific (Johor)<br><br>* Availability zone: ap\-southeast\-1a<br><br>* Private network address: 172.16.3.237 |
||* Name: ceph\-node3<br><br>* Instance type: ecs.g1.xlarge (vCPU: 4, memory: 16 GiB)<br><br>* System volume: 100 GiB<br><br>* Data volume: 200 GiB \* 3 |* Operating system: CentOS 7.6<br><br>* Region: Asia Pacific (Johor)<br><br>* Availability zone: ap\-southeast\-1a<br><br>* Private network address: 172.16.3.223 |
||* Name: ceph\-client<br><br>* Instance type: ecs.g1.xlarge (vCPU: 4, memory: 16 GiB)<br><br>* System volume: 40 GiB |* Operating system: CentOS 7.6<br><br>* Region: Asia Pacific (Johor)<br><br>* Availability zone: ap\-southeast\-1a<br><br>* Private network address: 172.16.3.211 |
|NAT Gateway |* Name: ceph\-nat<br><br>* Specification: Small |* Region: Asia Pacific (Johor)<br><br>* Availability zone: ap\-southeast\-1a<br><br>* Public address: 180.184.xx.xx |

## Environment setup

Before deploying Ceph, you need to first set up​ an environment on the BytePlus platform, including creating a VPC, ECS instances, and a public NAT gateway. These are the prerequisites for starting your Ceph installation.

### Create a VPC and subnet

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Product and Services \> VPC".

3. In the top menu bar, select Asia Pacific (Johor).

4. On the Virtual Private Cloud page, click "Create VPC".

5. On the Create VPC page, configure the parameters of the VPC and subnet. For configuration details, see the table below.

   |Category |Configuration item |Description |
   |---|---|---|
   |Virtual Private Cloud |Region |Asia Pacific (Johor) |
   ||Name |ceph\-vpc |
   ||IPv4 CIDR |172.16.0.0/12 |
   |Subnet |Name |ceph\-cluster\-subnet |
   ||Availability zone |ap\-southeast\-1a |
   ||IPv4 CIDR |172.16.3.0/24 |

6. After the configuration is completed, click "Confirm".

### Create an ECS instance

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Product & Services \> ECS".

3. In the left navigation bar, select "Instances", set the region to Asia Pacific (Johor), and click "Create instance".

4. On the Create Instances page, configure parameters as specified in the following table.

   |Configuration item |Description |
   |---|---|
   |Billing method |Pay\-as\-you\-go |
   |Region and AZ |* Region: Asia Pacific (Johor)<br><br>* Availability zone: ap\-southeast\-1a |
   |Instance |Instance type: General\-purpose,<br><br> ecs.g1.xlarge (vCPU: 4, memory: 16 GiB) |
   |Image |Public image: CentOS 7.6<br><br>No mandatory requirement for the operating system type. Any Linux operating system can be used. In the example provided in this topic, CentOS 7.6 is used. |
   |Storage |System volume 40 GiB \* 1<br><br>Data volume 200 GiB \* 3 |

5. After the basic configuration is completed, click "Next" for network and security configuration.

   |Configuration item |Description |
   |---|---|
   |Network |VPC: Select the existing VPC (ceph\-vpc)<br><br>Subnet: Select the existing subnet (ceph\-cluster\-subnet) |
   |Security group |Select the default security group. |
   |EIP |Unselect "Assign Elastic IP (EIP)". |

6. Click "Next".

7. On the Confirm page, confirm the parameter information. After the information is confirmed, follow the console guidance to review and confirm the agreement, and then click the "Buy now" button to create the instance.

   To deploy Ceph as described in this topic, you need to create four ECS instances. You can follow the guidance in the **Practice planning** to create them.

### Create an EIP

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Product and Service \> EIP".

3. On the Elastic IP page, click "Apply for EIP".

4. Configure EIP parameters as specified below. After configuration, click "Agree and buy" to complete the creation process.

   |Configuration item |Description |
   |---|---|
   |Name |ceph\-nat\-eip |
   |ISP |Select "BGP (multi\-line)". |
   |Billing method |Select "Pay\-by\-bandwidth". |

### Create a public NAT gateway

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Products and Services \> Internet NAT Gateway".

3. On the Internet NAT Gateway page, click "Create NAT Gateway". Configure parameters as specified below. After configuration, click "Confirm order".

4. After the details are confirmed, follow the console guidance to review and confirm the agreements, and then click the "Buy now" button to complete creating the public NAT gateway.

   |Configuration item |Description |
   |---|---|
   |Billing method |Pay\-as\-you\-go |
   |Region |Asia Pacific (Johor) |
   |Types |Small |
   |Virtual Private Cloud |ceph\-vpc |

5. In the Internet NAT Gateway console, click the created "ceph\-nat" to enter the public NAT gateway details page. Click "EIPs" and "Associate EIP" in sequence to associate the EIP **ceph\-eip**.

6. On the public NAT gateway details page, click "SNAT rules" and "Create SNAT rule" in sequence to add an SNAT entry.

## Prepare for Ceph cluster installation

To speed up Ceph cluster deployment, we use Ansible for batch operations for most tasks in this practice. This helps reduce the time spent switching between nodes.

> **tip**

> Among the following operations, only the step **"Change hostnames"** requires you to log in to each node. All other can be performed on the deployment node ceph\-node1.

### Plan the hosts

|Host |IP |Feature |
|---|---|---|
|ceph\-node1 |172.16.3.76 |mon, osd, mgr, deploy |
|ceph\-node2 |172.16.3.237 |mon, osd, mgr |
|ceph\-node3 |172.16.3.223 |mon, osd, mgr |
|ceph\-client |172.16.3.211 |\- |

### Prepare the installation environment

#### Change hostnames

Use ECS Terminal or a remote connection tool to [log in to the command line interface of each of the four ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance), respectively. Then, change instance hostnames in sequence.

```Plain Text
hostnamectl set-hostname ceph-node1
hostnamectl set-hostname ceph-node2
hostnamectl set-hostname ceph-node3
hostnamectl set-hostname ceph-client
```

#### Configure the environment on ceph\-node1

1. Configure the file used for domain name resolution.

   1. Execute the `vim /etc/hosts` command to open the /etc/hosts file.

   2. Press `i` to enter the edit mode.

   3. Add the following content to the end of the /etc/hosts file, and replace the sample private IP address with your own private IP address.

      ```Plain Text
      172.16.3.76   ceph-node1
      172.16.3.237  ceph-node2
      172.16.3.223  ceph-node3
      172.16.3.211  ceph-client
      ```

   4. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

2. Configure password\-free login.

   SSH keys are stored in the `~/.ssh` directory by default. You can specify a storage location for SSH keys as needed when configuring SSH keys. If you do not specify the storage location, press Enter when prompted for the storage location.

   ```Plain Text
   ssh-keygen -t rsa -P ''
   ssh-copy-id ceph-node1
   ssh-copy-id ceph-node2
   ssh-copy-id ceph-node3
   ssh-copy-id ceph-client
   ```

3. Install Ansible.

   1. Execute the following commands to install Ansible.

      ```Plain Text
       yum install epel-release -y
       yum install ansible -y
      ```

   2. Execute the `vim /etc/ansible/hosts` command to open the /etc/ansible/hosts file.

   3. Press `i` to enter the edit mode.

   4. Add the following content to the end of the /etc/ansible/hosts file.

      ```Plain Text
      [ceph]
      ceph-node1 ansible_ssh_user=root
      ceph-node2 ansible_ssh_user=root
      ceph-node3 ansible_ssh_user=root
      ```

   5. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

   6. Execute the following command to check whether all nodes support a password\-free login.

      ```Plain Text
      ansible ceph -m ping
      ```

      If the following output is displayed, the configuration succeeds.

      ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_804046e85c1aecb6006c5063f8c37843)

4. Execute the following command to copy the hosts file from the management machine to other remote hosts.

   ```Plain Text
   ansible ceph -m copy -a 'src=/etc/hosts dest=/etc/'
   ```

   If the following output is displayed on ceph\-node1, ceph\-node2, and ceph\-node3, the configuration succeeds.

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_dda802be5a48cc5d46d1882e5298b1a5)

5. Configure the Ceph package repository.

   1. Execute the vim `/etc/yum.repos.d/ceph.repo` command to open the /etc/yum.repos.d/ceph.repo file.

   2. Press `i` to enter the edit mode.

   3. Add the following content to the /etc/yum.repos.d/ceph.repo file.

      ```Plain Text
      [ceph]
      name = ceph
      gpgcheck = 0
      baseurl = https://mirrors.volces.com/ceph/rpm-luminous/el7/x86_64/
      
      [ceph-deploy]
      name = ceph-deploy
      gpgcheck = 0
      baseurl = https://mirrors.volces.com/ceph/rpm-luminous/el7/noarch/
      ```

   4. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

   5. Execute the following commands to copy the configuration changes to other nodes.

      ```Plain Text
      ansible ceph -m copy -a 'src=/etc/yum.repos.d/ceph.repo dest=/etc/yum.repos.d/'
      ```

      If the following output is displayed on ceph\-node1, ceph\-node2, and ceph\-node3, the configuration succeeds.

      ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_70d1146a0f7d67f3866f2ae07e05cc78)

6. Configure the /etc/yum.conf file to restrict the installable version of Ceph.

   1. Execute the `vim /etc/yum.conf` command to open the /etc/yum.conf file.

   2. Press `i` to enter the edit mode.

   3. Add the following content to the end of the /etc/yum.conf file.

      `exclude=*12.2.13*`

   4. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

   5. Execute the following commands to copy the modified yum configuration to the other nodes.

      ```Plain Text
      ansible ceph -m copy -a 'src=/etc/yum.conf dest=/etc/yum.conf'
      ```

## Install and configure a Ceph cluster

1. Execute the following command to install ceph\-deploy.

   ```Plain Text
   yum install ceph-deploy -y
   ceph-deploy --version
   ```

   If the version information is displayed, the installation succeeds.

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5c6b9098a64fbdee64d3db7cf231ff86)

2. Use ceph\-deploy to install Ceph.

   > **Note**

   > Before this operation, make sure the EPEL repository is installed. Otherwise, an error occurs.

   1. Execute the following commands to install Ceph.

      ```Bash
      ansible ceph -m yum -a 'name=epel-release state=latest'
      ceph-deploy install --no-adjust-repos ceph-node1 ceph-node2 ceph-node3
      ```

      If the following output is displayed, the installation succeeds.

      ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6d9c7acc7bd4e8678cd0923921be9dc0)

   2. Execute the following command to view the Ceph version.

      ```Plain Text
      ansible ceph -m shell -a 'ceph -v'
      ```

      The output is returned as follows:

      ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f2e26d250b18aad750f774e91f962459)

3. Deploy a RADOS storage cluster.

   1. Execute the following command to initialize the cluster.

      ```Plain Text
      mkdir ceph-cluster
      cd ceph-cluster/
      ceph-deploy new ceph-node1 ceph-node2 ceph-node3
      ls
      ```

      The output is returned as follows:

      ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_cb2ec5f6a019d7aaea5c2bb6d2e54166)

   2. Execute the `cat ceph.conf` command to view the configuration, as shown in the picture below:

      ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_494d416fdc3ff23740f41ca1a1dceb4a)

4. Execute the following commands to deploy mon nodes.

   ```Plain Text
   ceph-deploy mon create-initial
   ls
   ```

   The output is returned as follows:

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8072d7886329a76afd121c8675373cc2)

5. Execute the following commands to copy the admin configuration to other nodes.

   ```Plain Text
   ceph-deploy admin ceph-node1 ceph-node2 ceph-node3
   ceph -s
   ```

   The output is returned as follows:

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3c0adb3664a7e851041283225c65edeb)

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_fa424538b93abcbcf805d8744cef0488)

6. Deploy ceph\-mgr.

   ceph\-mgr is a key feature mainly promoted in Ceph 12.2 and a component responsible for Ceph cluster management. Its goal is to achieve Ceph cluster management and provide a unified entry point for external systems.

   Execute the following commands to deploy ceph\-mgr.

   ```Plain Text
   ceph-deploy mgr create ceph-node1 ceph-node2 ceph-node3
   ceph -s
   ```

   The output is returned as follows:

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9b0ac2cfac76b57e62c967eeb2781cd0)

7. Start Ceph Dashboard.

   Ceph includes a native Dashboard feature, which allows you to view information about various basic statuses of a Ceph cluster.

   1. Execute the following commands to enable Dashboard.

      ```Plain Text
        ceph mgr module enable dashboard
        #Check the current dashboard location
        ceph mgr services
      ```

   2. [Associate an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP) with the node where the Ceph Dashboard is located.

   3. After the installation is completed, open a browser and in the address bar, input: `http://<the EIP of the node where the Dashboard is located>:7000`

      > **tip**

      > Before you access the Dashboard, follow the guidance of [changing security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules) to allow port `7000`.

      ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_549ffbdb9c52b0a2e4ca1de371612dbe)

8. Create OSDs.

   1. Execute the following commands to create OSDs on each node.

      ```Plain Text
      ceph-deploy disk zap ceph-node1 /dev/vdb
      ceph-deploy disk zap ceph-node1 /dev/vdc
      ceph-deploy osd create ceph-node1 --data /dev/vdb
      ceph-deploy osd create ceph-node2 --data /dev/vdb
      ceph-deploy osd create ceph-node3 --data /dev/vdb
      ceph-deploy osd create ceph-node1 --data /dev/vdc
      ceph-deploy osd create ceph-node2 --data /dev/vdc
      ceph-deploy osd create ceph-node3 --data /dev/vdc
      ```

   2. Execute the `ceph -s` command to query the cluster status.

      ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_da77e79dc7e9525dd4e525505168cae2)

## Create RBD

RBD (RADOS Block Device), a block storage, is the most stable and widely used storage type. An RBD can be mounted as a disk. It offers features including snapshots, multiple replicas, cloning, and consistency, with data stored in a striped manner across multiple OSDs in a Ceph cluster.

1. Execute the following command to create a Ceph pool.

   ```Plain Text
   rados mkpool <poolname>
   rados lspools
   ```

   If the following output is displayed, the creation succeeds.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f67282d32ae007970ec6f774e5f58461)

2. Execute the following commands to create image1 in the Ceph pool.

   ```Plain Text
   rbd create <poolname>/image1 --size 20480 --image-format 2
   rbd info <poolname>/image1
   ```

   If the following output is displayed, the creation succeeds.

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_997284b1df4d44ec0ff8a56f2d374d12)

3. Execute the command `rbd list <poolname>` to view the image information in the Ceph pool.

   The output is returned as follows:

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_229c411064d0de4ec27e13d662226ade)

## Use a client to mount the RBD to the local node

1. Execute the following commands on ceph\-node1 to install ceph\-client.

   ```Plain Text
   ceph-deploy install ceph-client
   ceph-deploy admin ceph-client
   ```

2. Execute the following commands in the ceph\-client environment to mount the RBD to the local node.

   ```Plain Text
   rbd create <poolname>/test2 --size 20G --image-format 2
   rbd feature disable <poolname>/test2 object-map fast-diff deep-flatten
   rbd map --pool <poolname> --image test2
   mkfs.ext4 -m0 /dev/rbd0
   mkdir /mnt/ceph-block-devicesudo
   mount -t ext4 /dev/rbd0  /mnt/ceph-block-devicesudo
   df -h
   ```

   If the following output is displayed, the RBD is mounted.

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a16dd3a83a75277a2b44ef7a34dad903)

## Uninstall the cluster

Execute the following commands to uninstall the cluster.

```Plain Text
# Uninstall the ceph software package
ceph-deploy purge {ceph-node} [{ceph-node} ...]

# Delete various configuration files and generated data files
ceph-deploy purgedata {ceph-node} [{ceph-node} ...]

# Remove the authentication key of the uninstalled node from the local directory
ceph-deploy forgetkeys
```

##
