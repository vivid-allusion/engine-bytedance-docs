---
title: "Expiration instructions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Expiration_instructions"
---

For E\-MapReduce (EMR) clusters, if a subscription instance expires and is not renewed, your resources will enter a retention period and resource usage will be restricted. After the resource retention period has expired, your resources will be forcibly reclaimed. Once reclaimed, resources cannot be restored. Please [Renewal policy](https://docs.byteplus.com/docs/E-MapReduce/109016) within the specified time (before resources are forcibly reclaimed) to avoid losing access to the relevant resources. You can view the expiration time of subscription instances on the **Cluster Overview** page for the specific cluster.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ccbb5e6d04e4760912f5e08549c2ade~tplv-goo7wpa0wc-image.image) </span>


* Expiration time: 23:59:59 on the expiration date.

* Shutdown time: 12 hours after the expiration time. For example, if the expiration time is December 31, the cluster will be shut down at 12:00:00 on January 1.

   * During the retention period, the resources have been shut down. The following operations are restricted:

      * Create clusters

      * Cluster scaling

      * Cluster scale\-in

      * Disk expansion

      * Node reconfiguration

      * Cluster release

      * All service operations

* Resource release time: 15 days after expiration. If the cluster expires on December 31, the cluster's resources will be released at midnight at the end of January 15 (that is, at 00:00:00 on January 16). The resources will be forcibly released and cannot be restored.

   * After the cluster is released, all instances in the cluster will be released, including subscription and pay\-as\-you\-go instances.


<span id="8681db22"></span>
## **Expiration reminders**


* Expiration reminders are sent once per day on the 7th, 3rd, and 1st days before expiration, as well as on the expiration date. Depending on account settings, expiration notifications can be received via internal message, email, or SMS.

* Notification that the service has already been shut down due to expiration, sent once at 13:00 on the day after expiration. According to account user settings, notifications about expiration and shutdown can be received via internal message, email, or SMS.
