---
title: "Unsubscribe policy"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Unsubscribe_policy"
---

If you no longer need the cluster after purchasing a Subscription cluster, you may choose to unsubscribe from the E\-MapReduce (EMR) cluster. After unsubscribing, data will be irrecoverable, so please proceed with caution.

After unsubscribing from a cluster, the amount paid for the order will be refunded to your account balance according to the type of unsubscription requested and the corresponding rules. Only the portion of the order paid in cash will be refunded; any amount covered by vouchers is excluded. Vouchers that have already been used cannot be refunded.

<span id="773ab3ce"></span>
## **Prerequisites**

Ensure that the cluster is a subscription cluster and is in the running, abnormal, or shut down state.

<span id="aaa45acc"></span>
## **Procedure**


1. Log in to EMR Console.

2. Select the region and project in the top menu bar as appropriate.

3. In the left navigation bar, click **Resource \> on ECS** to enter the cluster list page.

4. Click the **More \> Unsubscribe** button under the Action column on the right side of the cluster that needs to be released.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed79f10e871b47cab781ff6d36119c31~tplv-goo7wpa0wc-image.image) </span>


5. In the pop\-up dialog box, check **I know the operational risks**, then click **Confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Unsubscribing from the cluster will forcibly terminate all jobs running on the cluster and release all associated resources. Once resources are released, they cannot be restored. Please proceed with caution.   </div>
   

6. You can also go to the details page of the Subscription cluster you want to unsubscribe from, click **Cluster Actions \> Unsubscribe** in the upper right corner, check **I know the operational risks**, and click **Confirm**.

7. On the order cancellation confirmation page, confirm the cancellation information. If the information is correct, click **Confirm .** 


<span id="75cc05b2"></span>
## **The unsubscription process**

After unsubscribing from the cluster, the following actions will be triggered:


1. Forcibly terminate all jobs on the cluster.

2. Terminate and release cluster\-related resources, including all ECS instances, cloud disks, and public IP addresses.
