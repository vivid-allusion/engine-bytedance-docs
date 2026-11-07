---
title: "File Storage PFS"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/File_Storage_PFS"
---

BytePlus PFS is a high\-throughput, low\-latency, scalable and parallel file system. Users can achieve high\-performance data reading and writing by mounting PFS into Dev boxes and custom tasks. At the same time, the Machine Learning Platform supports users to configure mount permissions based on PFS Fileset to achieve finer permission control.

<span id="相关概念"></span>
# Related concepts


* [Change the PFS instance of a prepaid resource group](https://docs.byteplus.com/docs/mlp/Change_the_PFS_instance_of_a_prepaid_resource_group)


<span id="使用前提"></span>
# Premise of use


1. The current user has `MLPlatformAdminAccess`IAM policies .

   1. If you configure mount permissions as user groups in IAM, you need to configure an additional policy for `IAMReadOnlyAccess`to get a list of user groups.

2. The instance creation has been completed in the File storage PFS console.


<span id="使用步骤"></span>
# Procedure

<span id="绑定第一个-vepfs-实例"></span>
## Bind the first PFS instance


1. Log in to the Machine Learning Platform and click [global configuration] in the left navigation bar to enter the corresponding page.

2. Click [Add Authorization] in [File storage PFS] to enter the instance selection page, select a PFS instance that needs to be used, and wait for the binding to complete after submitting the form.

   1. Binding a PFS instance for the first time helps the user create a PFS mount service on the platform.

   2. If there is no PFS instance currently available, go to PFS Control and create it.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5859fcec60a454eb6d356131bb979a2~tplv-goo7wpa0wc-image.image) </span>

3. After the instance binding is completed, click [Add mount permission] to enter the corresponding page and need to configure the following parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5be4f9bc61484f00a7fc79c78a5c1bf8~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/baa3c4ae342f48e697f761edba3af4ea~tplv-goo7wpa0wc-image.image) </span>



|**Parameter** |**Parameter Description** |
|---|---|
|PFS instance |Select a bound PFS instance in which to fine\-grain mount permission isolation. **Required** . |
|authorization directory |Directory that needs to configure mount permissions, support for root directory, Fileset directory and subdirectories under Fileset **Required** .<br><br><br>* Root directory ( `/`): The root directory of the PFS file system, which can access all directories under the instance after mounting, equivalent to the highest privilege.<br><br>* Fileset directory: The directory corresponding to a Fileset in the PFS. After mounting, only this directory and its subdirectories can be accessed. Fileset needs to be created in advance.<br><br>* Secondary subdirectory: After selecting the root directory or a Fileset directory, users are also supported to manually fill in a subdirectory path under this directory for more fine grained permission control. |
|scope of authorization |To which users the above directory is authorized, it is supported to be open to all users in the main account or only within the specified scope. **Required** .<br><br><br>* All members in the main account: All sub accounts in the main account can mount this directory.<br><br>* Members within the specified range:<br><br>   * Specify queue: Only members of the specified queue can mount the directory.<br><br>   * Specify user group: Only members of the specified user group can mount this directory, and the configuration of the user group needs to be completed in [Identity and Access Management] in advance. The `IAMReadOnlyAccess`policy is required for this configuration, otherwise the list of user groups cannot be obtained.<br><br>   * Specify sub account: Only the specified sub account can mount this directory, and the creation of the sub account needs to be completed in [Identity and Access Management] in advance.<br><br><br>Read and write permissions. Required.<br><br><br>* Read and write permissions: that is, authorized members have the read and write permissions of the authorized directory. Users can also mount with read\-only privileges during load mount.<br><br>* Read\-only permissions: that is, authorized members have read\-only permissions to the authorized directory. |



4. After completing the submission of the above form, a configuration record of mount permissions will be generated, and subsequent users can mount the PFS shared file system at the granularity of the directory when creating Dev boxes and custom tasks.

5. If necessary, the user can then dynamically modify the authorization scope through the [Edit] entry or delete the record through the [Delete] entry. After deletion, the mount permission will be reclaimed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/969ad682cf4241d9aef2545f33057789~tplv-goo7wpa0wc-image.image) </span>


6. Go to the resource group to bind the PFS instance. Please see [[New Function]Create ResourceGroup](https://docs.byteplus.com/docs/mlp/39873) for binding PFS.


<span id="绑定第二个-vepfs-实例"></span>
## Bind the second PFS instance


1. Log in to the Machine Learning Platform and click [global configuration] in the left navigation bar to enter the corresponding page.

2. Click the bound PFS mount service in [File storage PFS], click the [Bind instance] operation to enter the instance selection page, select a PFS instance to be used, and wait for the binding to complete after submitting the form.

   1. **The VPC managed by the selected PFS instance needs to be consistent with the VPC of the PFS mount service** .

   2. If you need to select PFS instances of different VPCs, you need to use the PFS multi\-mount service capability, please contact the platform to activate.

3. After the instance is bound, you can complete the authorization of the permission through [Add mount permission].

4. Go to the Resource Group module to bind a PFS instance for a resource group. Please see [[New Function]Create ResourceGroup](https://docs.byteplus.com/docs/mlp/39873) for binding PFS.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26ef854fe18744608018572ded70bea3~tplv-goo7wpa0wc-image.image) </span>


<span id="注意事项"></span>
# Precautions


1. If you have two PFS instances mounted on the Machine Learning Platform, please note the following:

   1. When mounting a PFS via the CLI (command line) and SDK, you need to specify a PFS instance ID, otherwise you cannot commit the load task of mounting a PFS instance.

   2. Using PFS to store TensorBoard logs similarly requires specifying the instance ID.

2. If there is only one PFS instance, commit through the CLI (command line) and SDK without specifying the PFS instance ID (instances that use global configuration binding by default when empty).
