---
title: "Purchasing and using ECS instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances"
---

This topic introduces how to build an Elastic Compute Service (ECS) instance from scratch in the simplest way, including purchasing, connecting, deploying, and releasing the instance.

<span id=".5q2l6aqk5LqM77ya6LSt5Lmw5a6e5L6L"></span>
## Step 1: Purchase an instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. (Optional) If you have completed cross\-service access authorization, skip this step. Otherwise, perform the authorization first to allow the ECS instance to access other services. For details, see [Cross-service authorization](https://docs.byteplus.com/en/docs/ecs/Cross-service_authorization).

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. Click "Create instance" to purchase an ECS instance.

   The configuration listed in the table below is used in this topic. For parameters not covered, please use the default configuration.

   
   |Configuration page |Parameter​ |Recommended configuration |Details |
   |---|---|---|---|
   |Basic configuration |Billing method |Pay\-as\-you\-go |Pay\-as\-you\-go is a billing method where payment is made after usage. It is available for use immediately after activation. It can be stopped at any time, which is flexible. [Learn more](https://docs.byteplus.com/en/docs/ecs/Billing-overview) |
   ||Region and AZ |China (Beijing) A |Select a region closest to your service location.<br><br>Once the instance is created, you can not change the region. Please set it with caution. |
   ||Instance type |Instance type family: General\-purpose ecs.g1ie<br><br>Instance type: ecs.g1ie.large |Different vCPUs and memory ratios are applicable for different business scenarios. The g1ie specification provides balanced vCPU, memory, and network capabilities. It can meet the service needs in most scenarios. [Learn more](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) |
   ||Image |Type: Public Images<br><br>Edition: CentOS 7.9 |The platform provides multiple public images that include operating systems and essential application data. They are accessible to all users. [Learn more](https://docs.byteplus.com/en/docs/ecs/Image-overview) |
   ||Storage |Default configuration<br><br>System volume: ESSD 40 GiB<br><br>Data volume: ESSD 20 GiB |After the instance starts, the system volume fully replicates the operating system and application data from the image. The data volume stores business application data. [Learn more](https://docs.byteplus.com/en/docs/ecs/Overview-of-elastic-block-storage) |
   |Network configuration |Virtual Private Cloud |Default VPC |An isolated, customizable, and manageable virtual network environment for the ECS instance. [Learn more](https://docs.byteplus.com/en/docs/ecs/VPC-overview) |
   ||Subnet |Default subnet |A private IP address of the ECS instance for private network access. [Learn more](https://docs.byteplus.com/en/docs/ecs/VPC-overview) |
   ||Security group |Default security group |A security group is composed of multiple security group rules. It is used to control the outbound and inbound traffic at the ECS network interface. [Learn more](https://docs.byteplus.com/en/docs/ecs/Security-group-overview)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Security groups are designed based on the allowlist principle. By default, security groups deny the inbound and outbound traffic of network interfaces. Ensure that the required port, such as port 22 for remote login to the ECS instance, is allowed.</div><br> |
   ||EIP |Select the EIP option |An EIP address of the ECS instance for Internet access. [Learn more](https://docs.byteplus.com/en/docs/ecs/EIP-overview) |
   |Custom configuration |Login credentials |Key Pair |The credentials used for instance login. The "Key Pair" method is recommended, which provides high security. [Learn more](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview) |
   ||Key pair |key01 |Click "Create key pair". Enter a key pair name and quickly create a key pair used for instance login. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After the creation, the private key file is automatically downloaded to your local machine. The default file name is key_name.pem. You have only one chance to download the private key. The platform does not save your private key. Please keep it secure.</div><br> |
   ||Instance name |ECS\-Instance01 |You can customize an instance name. |
   

5. Click "Next" and follow the console instructions to read and confirm the agreement.

6. Click "Buy now". A page with that prompts submission success appears. On this page, you can view whether the ECS instance is created.

7. Click the "Go to console" button to go to the Instances page and view the newly created instance and its public and private IP addresses.


<span id=".5q2l6aqk5LiJ77ya55m75b2V5a6e5L6L"></span>
## Step 2: Log in to the instance


1. On the Instances page, find the instance ECS\-Instance01 you created. Click "Connect" in the "Actions" column.

2. In the dialog box that appears, click "Log in now" in the **ECS Terminal** section.

3. On the login page, configure the following login settings and click "Login".

   * Port and username: For Linux operating systems, the username is root, and the port is 22 by default.

   * Authentication method: Select "Key".

   * Key: Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ffce6f4de4ea9336a70362a8d9af5e69.png) </span> to upload the key that you have created during custom configuration when [purchasing the instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances#.5q2l6aqk5LqM77ya6LSt5Lmw5a6e5L6L). This is the key that was automatically downloaded to your local machine.


For more instance login methods, refer to [Logging in to instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

<span id=".5q2l6aqk5Zub77ya5YiG5Yy65Y-K5qC85byP5YyW5pWw5o2u55uY"></span>
## Step 3: Partition and format the data volume

If you purchase a data volume when you create the instance, partition and format the data volume after you log in to the instance. After doing this, you can use the data volume. Follow the appropriate document based on the capacity of your data volume and the image type.


* [Partitioning and formatting volumes (less than or equal to 2 TiB)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-larger-than-2-TiB)

* [Partitioning and formatting volumes (larger than 2 TiB)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB)


<span id=".5q2l6aqk5LqU77ya6YOo572y5Lia5Yqh"></span>
## Step 4: Deploy business operations


* Upload local data to the ECS instance. For details, refer to [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

* For how to deploy business environments within the instance, refer to:

   * [Set up environments](https://docs.byteplus.com/en/docs/ecs/Building-environments)

   * [Set up applications](https://docs.byteplus.com/en/docs/ecs/Building-applications)

   * [Set up websites](https://docs.byteplus.com/en/docs/ecs/Building-websites)


<span id=".5q2l6aqk5YWt77ya5pS-6YCa5Lia5Yqh56uv5Y-j5bm26K6_6Zeu5Lia5Yqh77yI6YeN6KaB77yJ"></span>
## Step 5: Enable business port access and access the business (important)

Enable the business ports provided externally by the ECS, allowing the port to be accessed. Otherwise, third parties are not able to access the ECS instance.


1. Click the name of the purchased instance. Then, click the "Security Group" tab.

2. In the Actions column of the security group, click "Edit rule". You are redirected to the "Access rules" tab.

3. You can add a rule. Select the "Inbound rules" tab and click "Add rule" to add an inbound rule. For example, the business port is 1122, the following configuration allows access from any address to the business on 1122 port of the ECS instance:

4. Click "Add". The action is complete.

5. Access your business via the following methods:

   1. Access via private network: Any ECS instance in the VPC where the purchased instance resides can access the business through `http://<instance private IP address>:1122`.

   2. Access via Internet: Any server on Internet can access the business through `http://<instance Elastic IP (EIP)>:1122`.


<span id=".5q2l6aqk5LiD77ya566h55CGL-mHiuaUvuWunuS-iw=="></span>
## Step 6: Manage/Release the instance


* To learn more about and use ECS instances, see [Instructions on common console operations](https://docs.byteplus.com/en/docs/ecs/Using-the-console).

* If you no longer need an ECS instance, you can refer to [Deleting instances](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances) to delete it. After the deletion, the data can not be recovered.


&nbsp;

&nbsp;
