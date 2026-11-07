---
title: "Renew/match/unsubscribe for a resource group"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Renew-match-unsubscribe_for_a_resource_group"
---

In the process of using a resource group, you may encounter situations such as the need to renew the resource when it expires, the need to adjust the resource, and the need to unsubscribe when the resource group is no longer needed. This article will explain the relevant operation steps for users one by one.

<span id="相关概念"></span>
# related concepts


* IAM


<span id="资源组的状态"></span>
# Status of the resource group

The state of the resource group represents the different stages of the resource group, and users can perform different operations on the resource group in different states.


|Status |Note |
|---|---|
|Running |* Represents that the resource group has been **created** or **renewed** and is currently in the normal availability stage. This state supports **creating queues** , **editing** , **matching** , **renewing** and **unsubscribing** . |
|Recycled |* This status indicates that **the user\-triggered unsubscribe has been completed** or **the resource group has not been renewed within 15 days after expiration** , the resource group's resources have been released, at this time the resource group only supports **deletion** .<br><br>   After the resource group is recycled, the queues in the resource group are deleted. |
|Expired |* This state indicates that the purchase time of the resource group has expired, **the queue under the resource group will turn to the closed state, and the tasks in the queue that are still running will stop immediately and cannot submit new tasks to the queue** .<br><br>* This state supports **editing** , **renewal** and **deletion** . After **renewal** , the resource group and its queue will be restored to the available state, and the interrupted tasks need to be resubmitted.<br><br>* **If the user does not renew the resource group within 15 days (the monthly subscription is 15 days, and the daily subscription is 2 days), the resource group will be recycled and the queue under the resource group will be deleted** . |


<span id="更配"></span>
# more match

<span id="使用前提"></span>
## premise of use


1. The resource group status is `running`.

2. The user is a **resource group administrator** .


<span id="操作步骤"></span>
## Procedure


1. **The resource group administrator** logs into the Machine Learning Platform and clicks [Resource Group Management] \- [Resource Groups] in the left navigation bar to enter the list page. Click on the resource group that needs to change the resource configuration to go to the details page.



|more matching scene |instance specification |Cloud disk |
|---|---|---|
|Increase/decrease the number of purchased instance specifications |1. Click the [Instance Specifications] Tab on the resource group details page to find the specification that needs to be changed.<br><br>2. Click `volume expansion and contraction`<br><br>   1. If you need to increase the number of this specification, click or enter the value after increasing the specification.<br><br>   2. If you need to reduce the number of this specification, enter the value that the specification needs to retain.<br><br>> Before scaling, please confirm whether the unallocated quantity meets the target quantity to be scaled, otherwise, please change the number of machines in the queue to reach the target value.<br><br><br>3. After modifying the target value, click `OK`to enter the bill confirmation page and complete the bill payment.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ee7f7b74b344b2f8d7d0e6befcb6457~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba973768eff14583b5b614e4185731af~tplv-goo7wpa0wc-image.image) </span> |1. Click the [Instance Specifications] Tab on the resource group details page to find the specification that needs to be changed.<br><br>2. Click `volume expansion and contraction`<br><br>   1. If you need to increase the number of this specification, click or enter the value after increasing the specification.<br><br>   2. If you need to reduce the number of this specification, enter the value that the specification needs to retain.<br><br>> Before scaling, please confirm whether the unallocated quantity meets the target quantity to be scaled, otherwise, please change the number of machines in the queue to reach the target value.<br><br><br>3. After modifying the target value, click `OK`to enter the bill confirmation page and complete the bill payment.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c0d56a15f8540cd9c44bf1b7a1203fa~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6657379cfeb44af580102b615339da2f~tplv-goo7wpa0wc-image.image) </span> |
|Add instance specification |1. Click the [Instance Specifications] Tab on the resource group details page to find the specification that needs to be changed.<br><br>2. Click `New Specifications`to enter the New Specifications operation page.<br><br>3. Select the specifications and number of instances to add.<br><br>4. After clicking `Confirm Add`, you will enter the bill confirmation page and complete the bill payment.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d15689d918644f280754dfe499ac172~tplv-goo7wpa0wc-image.image) </span> |1. Click the [Instance Specifications] Tab on the resource group details page to find the specification that needs to be changed.<br><br>2. Click `New Specifications`to enter the New Specifications operation page.<br><br>3. Select the specifications and number of instances to add.<br><br>4. After clicking `Confirm Add`, you will enter the bill confirmation page and complete the bill payment.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cba7e78413a4786b461afb44c72d0ec~tplv-goo7wpa0wc-image.image) </span> |
|Purchased specs are replaced with other instance specs (the number of specs not yet assigned to the queue) |1. Click the [Instance Specifications] Tab on the resource group details page to find the specification that needs to be changed.<br><br>2. Click `Change Specifications`to enter the Change Specifications operation page<br><br>> Before changing the specification, please confirm whether the unallocated quantity meets the target quantity that needs to be scaled down, otherwise, please change the number of machines in the queue to reach the target value.<br><br><br>3. Please select the calculation specification that needs to be changed, and modify the quantity. The amount must not exceed the unallocated amount of the current specification.<br><br>4. After clicking `Confirm Changes`, you will enter the bill confirmation page and complete the bill payment.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02ee7b51f8b240f1b84f326c0bb1ebf5~tplv-goo7wpa0wc-image.image) </span> |Not supported |


<span id="续费"></span>
# Renewal fee

<span id="使用前提"></span>
## premise of use


1. The resource group status is `running`or `expired`.

2. The user is a **resource group administrator** .


<span id="操作步骤"></span>
## Procedure


1. **The resource group administrator** logs into the Machine Learning Platform and clicks [Resource Group Management] \- [Resource Groups] in the left navigation bar to enter the list page. Click [Renewal] in the operation area of the resource group to be renewed to enter the relevant page.

2. After adjusting the **renewal duration** , click [Go to Pay]. After the payment is completed, you can continue to use the renewed resource group. At this time, the status of the resource group will be restored to `running`.


<span id="退订"></span>
# unsubscribe

<span id="使用前提"></span>
## premise of use


1. The resource group status is `running`.

2. The user is a **resource group administrator** .


<span id="操作步骤"></span>
## Procedure


1. **The resource group administrator** logs into the Machine Learning Platform console and clicks Resource Group Management \- Resource Groups in the left navigation bar to go to the list page. Click [Unsubscribe] in the operation area of the resource group to be unsubscribed, and enter the relevant page after secondary confirmation.

2. After confirming that the information is correct, click [Confirm Unsubscribe]. After the unsubscribe is successful, the status of the resource group will become `recycled`, and the resource group is no longer available.
