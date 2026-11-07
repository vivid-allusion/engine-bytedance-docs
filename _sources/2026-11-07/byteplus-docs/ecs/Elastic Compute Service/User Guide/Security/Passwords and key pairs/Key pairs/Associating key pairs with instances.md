---
title: "Associating key pairs with instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances"
---

You can associate a key pair when you create an instance. Alternatively, you can follow the steps in this topic to associate a key pair with an existing instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You already have a key pair. If no key pair is available, [create a key pair](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs).

* You can associate a key pair with an instance that is installed with the reset\-authentication plug\-in.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Method for querying whether an instance has the reset\-authentication plug\-in installed:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance">Log in to a Linux instance</a>.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Execute the <code>systemctl status reset-authentication</code> command.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <code>reset-authentication.service could not be found.</code> is returned, the reset\-authentication plug\-in is not installed.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in">Install the reset\-authentication plug\-in</a> before you perform the steps in this topic.   </div>
   


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* If you have already associated a key pair with an instance in the console, the newly associated key pair overwrites the existing key pair. However, this does not affect any key pairs that you have manually added within the instance.

* After you associate a key pair with an instance, you need to restart the instance for the key pair to take effect. If your instance is configured for password login, the password login method is automatically disabled after you associate a key pair with the instance and restart the instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="V25tkiimTx" title="Associate on the key pair list page">
<TabTitle>Associate on the key pair list page</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the key pair is located. 

3. Click the "Bind instances" button in the "Actions" column of the target key pair.

4. On the "Bind instances" page, select the instances in the list on the left that you want to associate with the key pair. After you select the instances, the instances automatically appear in the selected instances list on the right.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If there are instances that cannot be selected, those instances have already been associated with the current key pair and no further action is required.   </div>
   

5. Select "Restart selected instances now" to make the operation take effect.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the restart process, instances whose status is <strong>Running</strong> are restarted by default, and instances whose status is <strong>Stopped</strong> are started.   </div>
   

6. Click "Bind" to complete the operation.


</Tab>
<Tab zoneid="az3pIJzt74" title="Associate on the Instances page">
<TabTitle>Associate on the Instances page</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the instance is located.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. On the Instances page, use one of the following methods to go to the page for associating a key pair with instances.

   * Associate a key pair with a single instance: Click "... \> Instance property \> Bind key pair" in the "Actions" column of the target instance.

   * Associate a key pair with multiple instances at the same time: Select one or more instances that you want to associate with a key pair, and click "··· \> Bind key pair" at the bottom of the list.

5. On the "Associated key pair in bulk" page, select the key pair to associate from the drop\-down list.

6. Select "Agree to restart Instances now" to make the operation take effect. You can also [manually restart the instances](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) after the instances are associated with the key pair.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the restart process, instances whose status is <strong>Running</strong> are restarted by default, and instances whose status is <strong>Stopped</strong> are started.   </div>
   

7. Click the "bind" button to complete the operation.

8. After you submit the association request, you can click "Go to instance maintenance attribute" to go to the orchestration page and view the task details. This step is applicable only when you associate a key pair with multiple instances at the same time. When the task status is **Success**, the key pair is associated with the instances. For information about task\-related parameters, see [Viewing task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The first time you use the Orchestration service, you need to create the CustomRoleForOOS role to complete the authorization. <a href="https://docs.byteplus.com/en/docs/ecs/Preparation">Learn more</a>.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d6c8b6d70acce4ba4f10d0d16414ab5.png) </span>


</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


* [View instances associated with a key pair](https://docs.byteplus.com/en/docs/ecs/Viewing-key-pairs-bound-to-instances).

* After you associate a key pair with an instance, you can use the key pair to [log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

* If you want to log in to an instance by using a password after you associate a key pair with the instance, [reset the login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords). After the reset, you can log in to the instance by using either the key pair or the password.

* If multiple users want to access the same instance, you can manually [add multiple key pairs](https://docs.byteplus.com/en/docs/ecs/Adding-or-replacing-key-pairs-for-instances) within the instance.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[AttachKeyPair](https://docs.byteplus.com/en/docs/ecs/AttachKeyPair)
