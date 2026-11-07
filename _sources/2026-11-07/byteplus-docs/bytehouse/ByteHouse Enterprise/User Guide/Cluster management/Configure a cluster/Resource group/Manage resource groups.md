---
title: "Manage resource groups"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-resource-groups"
---

Users can manage the created resource groups on the ByteHouse Console, performing actions such as edit and delete.

<span id="45811c3e"></span>
## Prerequisites


* Cluster Administrator or System Administrator permissions are required during the operation.


<span id="4d73a0d7"></span>
## Resource group management


1. Access **ByteHouse Console \> Manage clusters \> Cluster List \> Cluster details**, and then click on the "Load & Resource Groups" tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a29edddc43b413c944933e3fa265315~tplv-goo7wpa0wc-image.image) </span>

2. In the "Resource Group Management" section, we can see all the created resource groups, as well as their respective statuses. If the previous actions on the resource group have not activated, the system will issue a reminder to perform a "Cluster Restart".


<span id="b574c1a9"></span>
## Modify resource group


1. Click the "Edit" button on the far right side of the resource group that needs modification.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dab7907cd4984292bb5fb281ccabcbc9~tplv-goo7wpa0wc-image.image) </span>

2. The system will display an "Edit Resource Group" popup window. We can adjust all configuration items according to the requirements, and the configuration requirements are consistent with **creating a new resource group**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/262aa60be1694fe584fb0306827b61ca~tplv-goo7wpa0wc-image.image) </span>

3. Select "Restart Later" or "Restart Immediately" for the cluster, then click "Confirm" to complete the modification of the resource group. The modifications to this resource group will not activate before the cluster restarts.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If you choose "Restart Immediately", please confirm beforehand whether there is data currently being processed to avoid data loss or impacting business continuity.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you choose to "Restart Later" for the cluster, the resource group edit actions will not take effect, and the system will prompt a "Cluster Restart" is needed.</div>


<div data-tips="true" data-tips-type="tip">You may click on <strong>Cluster Details</strong> in the “<strong>Restart Cluster</strong>” button to restart the cluster and activate the changes in resource group settings.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c114d3ea1094d9882666a8035108e9a~tplv-goo7wpa0wc-image.image" width="2798px" /></div>


<span id="54e3f7f3"></span>
## Delete resource group


1. Click the "Delete" button on the far right side of the resource group that needs to be deleted.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22f225e15fc04b789d32a006574dc7c0~tplv-goo7wpa0wc-image.image) </span>

2. The system will display a confirmation popup window. If confirmation is needed, please click "Confirm".

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">After deleting a resource group, a cluster restart is necessary for it to take effect.   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Before manually restarting, please make sure no data is being processed to avoid data loss or impact on business continuity.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c861e0051f4a4e1c952008a18e122e2d~tplv-goo7wpa0wc-image.image) </span>
