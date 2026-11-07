---
title: "Disassociating key pairs from instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Unbinding-key-pairs-from-instances"
---

If you want to change the key pair associated with an instance or switch its login credential from a key pair to a password, follow the steps in this topic to disassociate the key pair from the instance in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

You can disassociate a key pair from an instance only when the instance is installed with the reset\-authentication plug\-in.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Method for querying whether an instance has the reset\-authentication plug\-in installed:</div>



1. <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance">Log in to a Linux instance</a>.</div>


2. <div data-tips="true" data-tips-type="tip">Execute the <code>systemctl status reset-authentication</code> command.</div>


   <div data-tips="true" data-tips-type="tip">If <code>reset-authentication.service could not be found.</code> is returned, the reset\-authentication plug\-in is not installed.   </div>
   

3. <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in">Install the reset\-authentication plug\-in</a> before you perform the steps in this topic.</div>



<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* Currently, you can disassociate a key pair from an instance only when the instance is in the **Running ** or **Stopped ** status.

* After a key pair is disassociated from an instance, the key pair is no longer valid. If password\-based login is enabled for the instance, you can still log in to the instance by using the password after the key pair is disassociated from the instance. Otherwise, you need to re\-associate a key pair with the instance or reset the password before you can log in to the instance. Proceed with caution.

* Each time you disassociate a key pair from an instance, you need to restart the instance for the disassociation to take effect. If you disassociate key pair A from an instance without restarting the instance, associate and disassociate key pair B, and then restart the instance, the disassociation of key pair B does not take effect. The instance remains associated with key pair A.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="UsScjBDb1o" title="Disassociate on the Key Pair page">
<TabTitle>Disassociate on the Key Pair page</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the key pair is located. 

3. Click "Unbind instances" in the "Actions" column of the target key pair.

4. On the "Unbind instances" page, select the instances to be disassociated from the list on the left. After selection, the instances automatically appear in the selected instances list on the right.

5. Select "Restart selected instances now" to make the operation take effect.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the restart process, instances whose status is <strong>Running</strong> are restarted by default, and instances whose status is <strong>Stopped</strong> are started.   </div>
   

6. Click "Save" to complete the operation.


</Tab>
<Tab zoneid="TaUfKBwg7V" title="Disassociate on the Instances page">
<TabTitle>Disassociate on the Instances page</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the instance is located.

3. In the left\-side navigation pane, select "Instances & Images \> Instances" to go to the Instances page.

4. Click "... \> Instance property \> Unbind key pair" in the "Actions" column of the target instance.

5. On the "Unbind key pair" page, confirm the details of the instance to be disassociated.

6. Select "Agree to restart Instances now" to make the operation take effect.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the restart process, instances whose status is <strong>Running</strong> are restarted by default, and instances whose status is <strong>Stopped</strong> are started.   </div>
   

7. Click "OK" to complete the operation.


</Tab>
</Tabs>


<span id=".57uT5p6c6aqM6K-B"></span>
## Results verification

After you disassociate a key pair from an instance, you can view the instances associated with the key pair on the "Bound Instances" tab of the key pair details page, or check whether the key pair is displayed in the "Key pair" field on the "Overview" tab of the instance details page.

<span id=".55u45YWz5paH5qGj"></span>
## Related document

[DetachKeyPair](https://docs.byteplus.com/en/docs/ecs/DetachKeyPair)
