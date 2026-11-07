---
title: "Creating a custom image based on Docker"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-custom-image-based-on-Docker"
---

Vital Kubernetes Engine (VKE) allows you to install operating systems on cluster nodes by using veLinux\-based custom images. This topic describes how to create a custom image by using the `docker run` command.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Image creation described in this topic is a VKE\-specific encapsulation of custom image packaging. The` docker run` command automatically performs the following steps to package necessary contents as a custom image:


1. Create an Elastic Compute Service (ECS) that runs the veLinux operating system, an Elastic IP (EIP) address, a Virtual Private Cloud (VPC), and a subnet of the VPC according to the selected specification. The ECS instance and EIP address are billed using the pay\-as\-you\-go billing method.

2. Package contents as a custom image and check its availability.

3. Import the ready\-to\-use image into the image center in ECS.

4. Delete all resources created temporarily in the process, and settle the costs for the pay\-as\-you\-go ECS and EIP usage.


<span id="lr9aQ8D8"></span>
## Usage limits

For custom and shared images based on ‌Linux 2.0 and later or Ubuntu 22.x and later, cgroupv2 is enabled by default in Kubernetes v1.30 and later. To use cgroupv1, [submit a ticket](https://console.byteplus.com/workorder/create).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Docker has already been installed on an Internet\-connected on\-premises machine or ECS instance. For details, see [Get Docker](https://docs.docker.com/get-docker/).

* The snapshot feature has been enabled. For details, see [Snapshots](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots).

* The access key ID and secret access key of your account have been obtained. If you have not obtained these credentials, you can get them at [Access Key Management](https://console.byteplus.com/iam/keymanage).

* (Optional) If you use a Container Registry Standard Edition instance, ensure that you have prepared the image to be packaged, and obtained the image address, Container Registry username, and Container Registry password.

* (Optional) If you use a Container Registry Standard Edition instance, ensure that the ECS instance used to create the custom image can communicate with the Container Registry instance over the public network or through a VPC.

   * If you use a public network, public network access has been enabled for the Container Registry instance. For details, see [Enabling public network access](https://docs.byteplus.com/en/docs/cr/enable-public-network-access). Also note that traffic over the public network is billed using the pay\-as\-you\-go billing method.

   * If you want to specify a VPC, ensure that the VPC has been added to the access control allowlist of the Container Registry instance. For details, see [Connecting to the VPCs within the account](https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account).

* (Optional) If you use an Identity and Access Management (IAM) user to create a custom image, ensure that the IAM user has been granted permission to perform the following actions:

   ```Bash
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "ecs:RunInstances",
                   "ecs:StopInstance",
                   "ecs:DeleteInstance",
                   "ecs:DescribeInstances",
                   "ecs:CreateImage",
                   "ecs:PreheatImage",
                   "ecs:DescribeImages",
                   "ecs:DescribeTasks",
                   "vpc:CreateVpc",
                   "vpc:DeleteVpc",
                   "vpc:DescribeVpcs",
                   "vpc:CreateSubnet",
                   "vpc:DeleteSubnet",
                   "vpc:DescribeSubnets",
                   "vpc:DescribeSecurityGroups",
                   "vpc:AllocateEipAddress",
                   "vpc:AssociateEipAddress",
                   "vpc:DescribeEipAddresses",
                   "vpc:DisassociateEipAddress",
                   "vpc:ReleaseEipAddress"
               ],
               "Resource": [
                   "*"
               ]
           }
       ]
   }
   ```
   


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* **Disclaimer: Custom images are non\-standard environments for which  does not provide official support or ongoing maintenance**. For detailed disclaimer statements regarding custom images, see [Disclaimers](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).

* You can create Docker\-based custom images only by using the VKE base image veLinux.

* During image creation, the system creates an ECS instance and EIP address, which are billed by using pay\-as\-you\-go and automatically deleted when the process ends. Make sure that your account balance is sufficient for the operation to complete successfully.


<span id=".5pON5L2c6K-05piO"></span>
## Procedure

On the on\-premises server or ECS instance where Docker is installed, use the `docker run` command to create a custom image. Note that you need to provide all parameters through environment variables (ENV).

<span id=".5L2_55So56S65L6L"></span>
### Examples


* **Example 1**: Only includes required parameters

   ```Bash
   docker run --rm \
           -e VOLC_AK="<AK>" \ 
           -e VOLC_SK="<SK>" \ 
           -e TAILOR_SPEC="ecs.xxx.large" \ 
           vke-cn-beijing.cr.volces.com/vke/private-image-packer:v1.0.9
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The backslash (<code>\</code>) character at the end of the previous command indicates line continuation in Shell. If your client cannot correctly recognize the character, delete it and format the command as a single line.   </div>
   

* **Example 2**: Includes all parameters

   ```Bash
   docker run --rm \
           -e VOLC_AK="<AK>" \ 
           -e VOLC_SK="<SK>" \ 
           -e REGION="cn-shanghai" \
           -e ZONE="cn-shanghai-a" \
           -e TAILOR_IMAGE_NAME="my-image-name" \
           -e TAILOR_SPEC="ecs.xxx.large" \ 
           -e TAILOR_DISK_SIZE="60" \
           -e TAILOR_COMPAT="false"  \
           -e IMAGES="cr-helm2-cn-beijing.cr.volces.com/****/busyxxx:latest,cr-helm2-cn-beijing.cr.volces.com/****/3gixxx:latest" \
           -e REGISTRY_USERNAME="paas2b_prod@2100****" \
           -e REGISTRY_PASSWORD="password123" \
           -e TAILOR_PASSWORD="password"\
           -e TAILOR_VPC="vpc-13fawddpwxxxxxx6nu4g2y8bt"\
           -e TAILOR_SUBNET="subnet-mj92ij8xxxxxxsmt1arvwrtw"\
           -e TAILOR_KERNEL="5.4"\
           vke-cn-beijing.cr.volces.com/vke/private-image-packer:v1.0.9
   ```
   


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description


|**ENV name** |**Required** |**Description** |**Sample value** |
|---|---|---|---|
|VOLC_AK |Yes |The access key ID of your account. You can get the access key ID at [Access Key Management](https://console.byteplus.com/iam/keymanage). |AKLTN2M1NTRjODNkYmI2NGEzNWFiYTk3ZTZhY\*\*\*\*\*\*\*\* |
|VOLC_SK |Yes |The secret access key for the account. You can get the secret access key at [Access Key Management](https://console.byteplus.com/iam/keymanage). |WkRVek5EWmtaalU0Wm1RMU5ETTJOamcyWlRoaU5EaGlObVJq\*\*\*\* |
|REGION |No |Region. If you leave this parameter empty, it defaults to `cn-beijing`. For a list of regions and availability zones supported by VKE, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |cn\-beijing |
|ZONE |No |Availability zone. If you leave this parameter empty, it defaults to `{REGION}-a`. |cn\-beijing\-a |
|TAILOR_SPEC |Yes |The instance specification from which you want to create a custom image. All instance specifications available in the console can be used. For a complete list, see [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You should select an ECS instance specification that suits your application requirements. For example, if you want to create a custom image for GPU scenarios, you must use a GPU Accelerated instance specification to prevent the resulting ECS instance from failing your application requirements due to a lack of a required driver.</div><br> |ecs.xxx.large |
|TAILOR_DISK_SIZE |No |The capacity of the system volume to be used for creating a custom image. If you do not specify a value, it defaults to `40`, which indicates 40 GiB. |100 |
|TAILOR_IMAGE_NAME |No |Name of the custom image. If you leave this parameter empty, a name starting with `velinux` will be generated automatically. |velinux\-example |
|TAILOR_COMPAT |No |Whether to use a CentOS\-compatible veLinux version.<br><br><br>* `false`:  a CentOS\-compatible veLinux version is not used.  This is the default value.<br><br>* `true`: a CentOS\-compatible veLinux version is used. |false |
|REGISTRY_USERNAME |No |The username for the private Container Registry instance from which images are pulled. The username is typically in the `BytePlus account@Account ID` format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you leave this parameter empty, you pull an image as an anonymous user. This parameter must be used together with <code>REGISTRY_PASSWORD</code>.</div><br> |user@2100\*\*\*\*\*\* |
|REGISTRY_PASSWORD |No |The password for the username of the private Container Registry instance from which images are pulled.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you leave this parameter empty, you pull an image as an anonymous user. This parameter must be used together with <code>REGISTRY_USERNAME</code>.</div><br> |password@123 |
|IMAGES |No |Images to be pulled. If you leave this parameter empty, the system does not pull container images of the user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you specify multiple images, separate them with commas (,).</div><br> |cr\-helm2\-cn\-beijing.cr.volces.com/\*\*\*\*/busy\*\*\*\*\*:latest,cr\-helm2\-cn\-beijing.cr.volces.com/\*\*\*\*\*/3gixxx:latest |
|TAILOR_PASSWORD |No |The password used when you create an ECS instance. |Password |
|TAILOR_VPC |No |The VPC where you want to create the ECS instance. This parameter must be used together with the TAILOR_SUBNET parameter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you specify a VPC and its subnet, ensure that the security group for the subnet includes an inbound rule that opens port 22.</div><br> |vpc\-13fawddpwxxxxxx6nu4g2y8bt |
|TAILOR_SUBNET |No |The subnet where you want to create the ECS instance. This parameter must be used together with the TAILOR_VPC parameter. |subnet\-mj92ij8xxxxxxsmt1arvwrtw |
|TAILOR_KERNEL |No |The kernel version to be used by the image. Available values are 5.4 and 5.10. The default value is 5.4. |5.4 |


<span id=".cHJpdmF0ZS1pbWFnZS1wYWNrZXIt5pu05paw6K6w5b2V"></span>
### private\-image\-packer versions


|Version |Version status |Update in |Change log |Impact |
|---|---|---|---|---|
|v1.0.9 |Being maintained |August 2024 |Fixed the issue where the image cannot be found when the kernel version is set to 5.10. |No |
|v1.0.8 |Being maintained |June 2024 |Fixed the issue where multiple ECS instances created by using a custom image have the same machine\-id value. |No |
|v1.0.7 |No longer maintained |October 2023 |Optimized the logic for image preheating to support both ECS image preheating and Elastic Block Service (EBS) snapshot preheating. The default retention period for snapshot preheating is 365 days. |No |
|v1.0.6 |No longer maintained |September 2023 |* [Incompatible] Renamed environment variable `PREHEATING_DISABLED` to `PREHEAT_DISABLED` and changed its default value from `false` to `true`.<br><br>* Changed the method of pulling container images from ECS from crictl to ctr. |An incompatible change that requires you to switch from `PREHEATING_DISABLED` to `PREHEAT_DISABLED`. |
|v1.0.5 |No longer maintained |August 2023 |* Added environment variable `TAILOR_KERNEL` for specifying a kernel version.<br><br>* Added environment variable `TAILOR_PASSWORD` for specifying a password for an ECS instance.<br><br>* Add environment variables `TAILOR_VPC` and `TAILOR_SUBNET` for specifying a VPC and subnet for an ECS instance.<br><br>* Added environment variable `PREHEATING_DISABLED` for creating a custom image without preheating. |No |
|v1.0.4 |No longer maintained |June 2023 |Added the `TAILOR_COMPAT` environment variable to provide veLinux compatibility with CentOS. |No |
|v1.0.3 |No longer maintained |April 2023 |[Incompatible] Changed the format of the environment variable `Zone` from `a` to `{REGION}-a`, such as `cn-beijing-a`. For a list of regions and availability zones, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |An incompatible change that requires you to modify environment variable `Zone`. |
|v1.0.2 |No longer maintained |April 2023 |Fixed the issue with execution errors in the China (Guangzhou) region. |No |
|v1.0.1 |No longer maintained |April 2023 |Added availability zone check during image preheating. |No |
|v1.0.0 |No longer maintained |March 2023 |Released private\-image\-packer v1.0.0. |No |


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

<span id=".5omT5YyF6L-H56iL5pWF6Zqc5aSE55CG"></span>
### Troubleshooting errors

If the `docker run` command returns an error, you need to fix the error and run the command again to complete image creation. Possible errors include:


* **docker run command errors**, such as syntax errors or missing parameters.

* **Failures in custom image checks**, such as the operating system, kernel version, basic components (for example, systemd), cloud\-init status, DNS settings, Network Time Protocol (NTP) status, add\-ons (for example, atop, proxima, and unscd), filesystem mount status, network interface card, and system boot parameters.


<span id=".5p-l55yL6Ieq5a6a5LmJ6ZWc5YOP"></span>
### View the custom image

After the `docker run` command finishes successfully, the created custom image is automatically uploaded to the ECS image center.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c5bbea7bda0e395d2f6d0e5e3095968.png) </span>

<span id=".5L2_55So6Ieq5a6a5LmJ6ZWc5YOP"></span>
### Use the custom image

When you create a cluster, create a node pool, or add existing nodes, you can select the created custom image. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster), [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes), and [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb1560eb969099847f212e24bbdeaf6d.png) </span>

&nbsp;

&nbsp;

&nbsp;
