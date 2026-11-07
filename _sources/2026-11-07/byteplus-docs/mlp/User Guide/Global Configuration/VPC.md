---
title: "VPC"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/VPC"
---

Before using the private network login of Dev boxes, mounting NAS/PFS shared file system and other functions in the Machine Learning Platform, you need to complete the global VPC configuration, which involves the configuration of VPC, subnet, SecurityGroup and routing.

<span id="使用前提"></span>
# premise of use


1. The current user has `MLPlatformAdminAccess`IAM policies .

2. The current account has \> = 1 VPC.

   * If you have not created a VPC in advance, you need to go to the corresponding [console ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc?)to create it.


<span id="使用步骤"></span>
# Procedure


1. Log in to the Machine Learning Platform and click [global configuration] in the left navigation bar to enter the corresponding page.

2. Click [Configure Private Network] in [VPC] to enter the relevant page and select the eligible VPC, subnet, SecurityGroup and route.

   * To avoid conflicts between users' network segments and the Machine Learning Platform, the platform will automatically filter out available VPCs.

   * Each Availability Zone supports the selection of only one subnet.

3. Submit the form to complete the global VPC configuration. At this time, the private network login function of Dev boxes can be used. Machines under this VPC can connect to Dev boxes through ssh but cannot use PFS\-related functions.

4. To use PFS, you need to create a PFS instance in advance and create a mount point under that VPC. Complete the binding of PFS in [global configuration]. After binding PFS, the VPC cannot be replaced freely. You need to unbind the PFS before replacing the new VPC.

   * When binding the PFS, an additional SecurityGroup will be added to the global VPC configuration, and the corresponding SecurityGroup will also be deleted after unbinding.
