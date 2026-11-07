---
title: "Manually releasing temporary resources"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Manually-release-temporary-resources"
---

Migration may fail due to causes such as network issues, changes to the source server, or other failures. In this case, SMC does not automatically release the temporary cloud resources it creates for data migration (for example, EIPs, security groups, and volumes). You need to manually release these resources to prevent incurring unnecessary charges.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Manual release of temporary resources is required only when migration fails during the process of migrating to ECS instances or custom images.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6L-B56e76Iez54Gr5bGx5byV5pOO5a6e5L6L5aSx6LSl"></span>
### Migration failure to ECS instance


1. Log in to the [Server Migration Center console](https://console.byteplus.com/ecs/migrationTask). 

2. In the left directory tree, select "Server Migration Center \> Migration Job".

3. Select the "Migrate to server" tab.

4. Click the "Logs" button in the Actions column on the right side of the target migration task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1e225c8b440c2a0b94da98b2afa24aa.png) </span>

   Resource description:

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Temporary SecurityGroup |Temporary security group ID. |sg\-miqmwast7xxxxx4ye |
   |Instance |ID of the destination instance for migration. |i\-ycswsqhurk5xxxxxzda |
   |KeyPair |Temporary key pair ID. |kp\-ycswszszxxxxxj2a |
   |Transition Data Volume |Temporary data volume ID. |vol\-99t2xxxxxcpc |
   

5. Manually release the corresponding resources based on the resource IDs displayed in the log information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Additionally, you can check the Agent logs located in the migration Agent directory on your source server.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Linux operating system: Execute the <code>cat smc.log</code> command.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Windows operating system: View the smc.txt file.   </div>
   

   * Release temporary key pair

      1. Log in to [the Key Pair console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/keyPair). 

      2. In the top menu bar, select the region where the target instance resides.

      3. In the search box at the top right, select "ID" from the dropdown, and enter the value of `KeyPair` in the log information to search for the target key pair.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7459f0e6669f022643f9074c3ea977a9.png) </span>

      4. Click the "Unbind instances" button in the Actions column to the right of the target key pair, and in the pop\-up window, check the instance corresponding to the `Instance` parameter.

      5. Click the "Confirm" button to complete disassociation.

      6. Click the "Delete" button in the Actions column to the right of the target key pair, and confirm the key pair information in the pop\-up window.

      7. Click the "Delete" button to complete deletion.

   * Release temporary security group

      1. Log in to [the Security Group console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/securityGroup). 

      2. In the top menu bar, select the region where the target instance resides.

      3. In the search box at the top right, select "ID" from the dropdown, and enter the value of `Temporary SecurityGroup` in the log information to search for the target security group.

      4. Click the "Associate ENI" button in the Actions column to the right of the target security group. On the "Associate ENI" tab, select the network interface associated with the instance corresponding to the `Instance` parameter.

      5. Click the "Disassociate" button in the Actions column to the right of the target network interface, confirm the network interface information in the pop\-up window, and click the "Disassociate" button to complete the disassociation.

      6. Switch back to the security group list page, click the "... \> Delete" button in the Actions column to the right of the target security group, and confirm the security group information in the pop\-up window.

      7. Click the "Delete" button to complete deletion.

   * Release temporary data volume

      1. Log in to the [Volumes console](https://console.byteplus.com/ebs/region:ebs+cn-beijing/volume). 

      2. In the top menu bar, select the region where the target instance resides.

      3. In the search box at the top right, select "Volume ID" from the dropdown, and enter the value of `Transition Data Volume` in the log information to search for the target volume.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a7974d0ccfb835be064f4d03c8b06d08.png) </span>

      4. Click the "... \> Detach" button in the Actions column to the right of the target volume, and confirm the volume and target instance information in the pop\-up window.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_87669085360a195d225f884f0f4c99ef.png) </span>

      5. Click the "Confirm" button to complete detachment.

      6. After detachment is complete, click the "... \> Delete" button in the Actions column to the right of the target volume, and confirm the volume information in the pop\-up window.

      7. Click the "Confirm" button to complete the operation.

   * Reset target instance login credentials

      Since SMC replaces the login credentials of the target instance with a temporary key pair during migration, if migration fails, you need to reset the login credentials of the target instance to avoid login failure to the target instance. For operation details, see [Resetting login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords).

6. Afterwards, you can use SMC to migrate source server data to the BytePlus. For details, see [Getting started](https://docs.byteplus.com/en/docs/smc/Getting-Started).


<span id=".6L-B56e76Iez54Gr5bGx5byV5pOO6Ieq5a6a5LmJ6ZWc5YOP5aSx6LSl"></span>
### Migration failure to custom image


1. Log in to the [Server Migration Center console](https://console.byteplus.com/ecs/migrationTask). 

2. In the left directory tree, select "Server Migration Center \> Migration Job".

3. Select the "Migrate to server" tab.

4. Click the "Logs" button in the Actions column on the right side of the target migration task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2117a5d5a8814d5902825d48c1e1141f.png) </span>

   Resource description:

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Temporary Vpc |Temporary VPC ID. |vpc\-rr28b0ltcv0x5xxxxxar |
   |Temporary Subnet |Temporary subnet ID. |subnet\-miz1h8r1egw5smxxxxxijz |
   |Temporary SecurityGroup |Temporary security group ID. |sg\-13felynf2xxxxxhm08y |
   |KeyPair |Temporary key pair ID. |kp\-ycsx7ibxxxxxv1mr |
   |Temporary Instance |Temporary instance ID. |i\-ycsx7icttxxxxxume |
   |Transition Data Volume |Temporary data volume ID. |vol\-99t3i6xxxxx6g781c |
   |Temporary Eip |Temporary EIP ID. |eip\-miz2fdza9lxxxxxmwr |
   

5. Manually release the corresponding resources based on the resource IDs displayed in the log information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Additionally, you can check the Agent logs located in the migration Agent directory on your source server.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Linux operating system: Execute the <code>cat smc.log</code> command.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Windows operating system: View the smc.txt file.   </div>
   

   * Release temporary instance

      You can release the temporary instance and the temporary system volume, data volume, and temporary EIP associated with it in a single operation.

      1. Log in to the [Instances console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance). 

      2. In the top menu bar, select the region where the target instance resides.

      3. In the top search box, select "Instances ID" from the dropdown, and enter the value of `Temporary Instance` in the log information to search for the target instance.

      4. Click the "... \> Delete" button in the Actions column on the right side of the target instance.

      5. In the pop\-up window, check the temporary data volume, temporary EIP, and "I am aware of the Instances and related resources that are about to be deleted and understand the associated risks."

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4aa90073c8cee503de782c73bacfc711.png) </span>

      6. Click "Delete" to complete the action.

   * Release temporary key pair

      1. Log in to the[ Key Pair console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/keyPair). 

      2. In the top menu bar, select the region where the target instance resides.

      3. In the search box at the top right, select "ID" from the dropdown, and enter the value of `KeyPair` in the log information to search for the target key pair.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7459f0e6669f022643f9074c3ea977a9.png) </span>

      4. Click the "Unbind instances" button in the Actions column to the right of the target key pair, and in the pop\-up window, check the instance corresponding to the `Instance` parameter.

      5. Click the "Confirm" button to complete disassociation.

      6. Click the "Delete" button in the Actions column to the right of the target key pair, and confirm the key pair information in the pop\-up window.

      7. Click the "Delete" button to complete deletion.

   * Release temporary security group

      1. Log in to [the Security Group console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/securityGroup). 

      2. In the top menu bar, select the region where the target instance resides.

      3. In the search box at the top right, select "ID" from the dropdown, and enter the value of `Temporary SecurityGroup` in the log information to search for the target security group.

      4. Click the "Associate ENI" button in the Actions column to the right of the target security group. On the "Associate ENI" tab, select the network interface associated with the instance corresponding to the `Instance` parameter.

      5. Click the "Disassociate" button in the Actions column to the right of the target network interface, confirm the network interface information in the pop\-up window, and click the "Disassociate" button to complete the disassociation.

      6. Switch back to the security group list page, click the "... \> Delete" button in the Actions column to the right of the target security group, and confirm the security group information in the pop\-up window.

      7. Click the "Delete" button to complete deletion.

   * Release temporary subnet

      1. Log in to [the Subnet console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/subnet). 

      2. In the top menu bar, select the region where the migration target instance resides.

      3. In the search box at the top right, select "ID" from the dropdown, and enter the value of `Temporary Subnet` in the log information to search for the target subnet.

      4. Click the "Delete" button in the Actions column to the right of the target subnet, and confirm the subnet information in the pop\-up window.

      5. Click the "Delete" button to complete deletion.

   * Release temporary VPC

      1. Log in to the [VPC console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/vpc). 

      2. In the top menu bar, select the region where the migration target instance resides.

      3. In the search box at the top right, select "ID" from the dropdown, and enter the value of `Temporary Vpc` in the log information to search for the target subnet.

      4. Click the "Delete" button in the Actions column to the right of the target VPC, and confirm the VPC information in the pop\-up window.

      5. Click the "Delete" button to complete deletion.

6. Afterwards, you can use SMC to migrate source server data to the BytePlus. For details, see [Getting started](https://docs.byteplus.com/en/docs/smc/Preparations).
