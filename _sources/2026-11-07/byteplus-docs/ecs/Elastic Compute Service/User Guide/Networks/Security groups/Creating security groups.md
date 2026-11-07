---
title: "Creating security groups"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-security-groups"
---

A security group offers access policies for Elastic Compute Service (ECS) instances within the same virtual private cloud (VPC) that have similar security requirements and trust each other. It serves as an important means of network security isolation. This topic describes how to create a security group in the ECS console.

<span id="operation-scenario"></span>
## Operation scenario

By creating security groups, you can segregate ECS instances into different security domains, enhancing the overall security of instance access.

<span id="precautions"></span>
## Precautions


* We recommend that you assign ECS instances with different public network access policies to separate security groups.

* Every ECS instance must be associated with at least one security group. When creating an ECS instance, if you have not created a security group, the system will automatically generate a default security group for the instance.

* If you prefer not to include the ECS instance in the default security group, you can refer to this section to create your own custom security group and define the access policies.


<span id="procedure"></span>
## Procedure


1. Log on to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the Region.

3. Choose **Security group** \> **Creat security group**. The security group creation page appears.

4. The following table describes the parameters for a security group.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |Specify a security group name. |sg\-01 |
   |VPC |Select the VPC where the security group resides. If no VPC exists, click **Create VPC** to create one. |vpc\-01 |
   |Access rules |Configure inbound and outbound rules for the security group. |\-\- |
   |Project |Select the project to which the security group belongs.<br><br><br>* The default value is empty, which indicates that the security group does not belong to any project.<br><br>* Once a project is selected, the security group you create is available only to users who have permission on that project.<br><br><br>If no options are available in the drop\-down menu, click **Create project** on the right to create one. |default |
   |Tags |A tag is a key\-value pair used for classifying and searching for resources.<br><br>Click **Add tag** to add tags to the security group. |* Tag key：sg\-key<br><br>* Tag value：sg\-tes |
   

5. Click **OK**.


<span id="results"></span>
## Results

Once the security group is created, navigate to the **Security Group** tab on the instance details page to view the associated security groups. From that page, you can also [modify the security group](https://docs.byteplus.com/en/docs/ecs/Changing-security-groups) for the target instance.
