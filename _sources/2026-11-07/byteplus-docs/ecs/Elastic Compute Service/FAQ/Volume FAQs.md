---
title: "Volume FAQs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Volume-faqs"
---

* General questions

   * [What is a volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#what-is-a-volume)

   * [What common operations can I perform on a volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#what-common-operations-can-i-perform-on-a-volume)

   * [What volume specifications are offered?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#what-volume-specifications-are-offered)

   * [How is a volume billed?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#how-is-a-volume-billed)

   * [How can I reduce volume capacity?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#how-can-i-reduce-volume-capacity)

   * [How can I release a subscription volume in advance?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#how-can-i-release-a-subscription-volume-in-advance)

* Questions on mounting or unmounting volumes

   * [Can I mount one volume on multiple Elastic Compute Service (ECS) instances?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#can-i-mount-one-volume-on-multiple-elastic-compute-service-ecs-instances)

   * [How many volumes can be mounted on one instance?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#how-many-volumes-can-be-mounted-on-one-instance)

   * [Can I mount a volume on an instance if they are in different Availability Zones?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#can-i-mount-a-volume-on-an-instance-if-they-are-in-different-availability-zones)

   * [Can I unmount a system volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#can-i-unmount-a-system-volume)

   * [Why is the space not displayed in the system after I create and mount a volume using the console?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#why-is-the-space-not-displayed-in-the-system-after-i-create-and-mount-a-volume-using-the-console)

   * [Why is the volume deletion feature in the console unable to delete my volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#why-is-the-volume-deletion-feature-in-the-console-unable-to-delete-my-volume)

   * [Can I merge the capacity of a data volume and a system volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#can-i-merge-the-capacity-of-a-data-volume-and-a-system-volume)

   * [Why is my data volume not recognized through the fdisk or lsblk command after I restart the instance?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#why-is-my-data-volume-not-recognized-through-the-fdisk-or-lsblk-command-after-i-restart-the-instance)

* Questions on separately bought volumes

   * [Why is the volume that I separately created released with my instance?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#why-is-the-volume-that-i-separately-created-released-with-my-instance)

   * [Can I mount a pay-as-you-go data volume that is separately bought on a subscription ECS instance?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#can-i-mount-a-pay-as-you-go-data-volume-that-is-separately-bought-on-a-subscription-ecs-instance)

   * [Can I unmount a data volume from a subscription ECS instance?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#can-i-unmount-a-data-volume-from-a-subscription-ecs-instance)

   * [Can I separately buy a subscription volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#can-i-separately-buy-a-subscription-volume)

* Questions on expanding system volumes

   * [How can I expand a system volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#how-can-i-expand-a-system-volume)

   * [Do subscription and pay-as-you-go ECS instances support system volume expansion?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#do-subscription-and-pay-as-you-go-ecs-instances-support-system-volume-expansion)

   * [What is the capacity range of a system volume? What is the upper limit to which I can expand my system volume? How can I expand a system volume?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#what-is-the-capacity-range-of-a-system-volume-what-is-the-upper-limit-to-which-i-can-expand-my-system-volume-how-can-i-expand-a-system-volume)

   * [Why does automatic volume expansion not take effect?](https://docs.byteplus.com/en/docs/ecs/Volume-faqs#why-does-automatic-volume-expansion-not-take-effect)


<span id="general-questions"></span>
## General questions

<span id="what-is-a-volume"></span>
### What is a volume?

A volume is also known as an Elastic Block Storage (EBS) device. It is offered by BytePlus, and features scalability, high availability, high reliability, and high performance. It can be used as a scalable hard drive for Elastic Compute Service (ECS) and Volcengine Container Instance.

<span id="what-common-operations-can-i-perform-on-a-volume"></span>
### What common operations can I perform on a volume?

For information on common operations on volumes, refer to [Overview of volume operations](https://docs.byteplus.com/en/docs/ecs/Overview-of-volume-operations).

<span id="what-volume-specifications-are-offered"></span>
### What volume specifications are offered?

ESSD_FlexPL and ESSD_PL0 are supported. For more information, refer to [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).

<span id="how-is-a-volume-billed"></span>
### How is a volume billed?

This service supports the pay\-as\-you\-go billing method and the subscription billing method. For information on billing details, refer to [Billing details about volumes](https://docs.byteplus.com/en/docs/ecs/Volume-billing).

<span id="how-can-i-reduce-volume-capacity"></span>
### How can I reduce volume capacity?

BytePlus does not allow you to reduce volume capacity. If you want to reduce volume capacity, we recommend that you create and mount a volume, replicate the data of the old volume to the new volume, and unmount and delete the old volume.

<span id="how-can-i-release-a-subscription-volume-in-advance"></span>
### How can I release a subscription volume in advance?

Before you release the volume, unsubscribe from it. For more information, refer to [Description of unsubscribing](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription).

&nbsp;

<span id="questions-on-mounting-or-unmounting-volumes"></span>
## Questions on mounting or unmounting volumes

<span id="can-i-mount-one-volume-on-multiple-elastic-compute-service-ecs-instances"></span>
### Can I mount one volume on multiple Elastic Compute Service (ECS) instances?

No. You can mount a volume on each ECS instance if they are deployed in the same Availability Zone.

<span id="how-many-volumes-can-be-mounted-on-one-instance"></span>
### How many volumes can be mounted on one instance?

The number of volumes that can be mounted on one instance varies based on the instance type. For more information, refer to [Limits on volumes](https://docs.byteplus.com/en/docs/ecs/Limits#volumes).

<span id="can-i-mount-a-volume-on-an-instance-if-they-are-in-different-availability-zones"></span>
### Can I mount a volume on an instance if they are in different Availability Zones?

No. Volumes cannot be mounted on an instance if they are in different Regions or Availability Zones.

<span id="can-i-unmount-a-system-volume"></span>
### Can I unmount a system volume?

BytePlus does not allow you to unmount a system volume.

<span id="why-is-the-space-not-displayed-in-the-system-after-i-create-and-mount-a-volume-using-the-console"></span>
### Why is the space not displayed in the system after I create and mount a volume using the console?

After you mount a volume just created, initialize the volume. For example, you can format and partition the volume and create a file system. For information on the detailed procedure, refer to [Partitioning and formatting volumes](https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview).

<span id="why-is-the-volume-deletion-feature-in-the-console-unable-to-delete-my-volume"></span>
### Why is the volume deletion feature in the console unable to delete my volume?

You can manually delete a pay\-as\-you\-go volume rather than a subscription volume. Before you manually delete a volume, make sure it is a data volume and the status is **Available**. This status indicates the volume is not mounted on an ECS instance.

<span id="can-i-merge-the-capacity-of-a-data-volume-and-a-system-volume"></span>
### Can I merge the capacity of a data volume and a system volume?

No. You can expand the capacity of a data volume or a system volume to increase storage. For more information, refer to [Expanding volumes](https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume).

<span id="why-is-my-data-volume-not-recognized-through-the-fdisk-or-lsblk-command-after-i-restart-the-instance"></span>
### Why is my data volume not recognized through the fdisk or lsblk command after I restart the instance?

Because a data volume partition cannot be automatically mounted after you restart your instance.For information on how to enable the auto mount feature, refer to [Allowing disk partitions to be automatically mounted during restarts](https://docs.byteplus.com/en/docs/ecs/Allowing-disk-partitions-to-be-automatically-mounted-during-restarts).

<span id="questions-on-separately-bought-volumes"></span>
## Questions on separately bought volumes

<span id="why-is-the-volume-that-i-separately-created-released-with-my-instance"></span>
### Why is the volume that I separately created released with my instance?

When you mount the volume, you may select to enable the feature specifying that the volume is released with the instance. You can disable this feature in the console. For information on the detailed procedure, refer to [Modify a volume property](https://docs.byteplus.com/en/docs/ecs/Modify-volume-attribute).

<span id="can-i-mount-a-pay-as-you-go-data-volume-that-is-separately-bought-on-a-subscription-ecs-instance"></span>
### Can I mount a pay\-as\-you\-go data volume that is separately bought on a subscription ECS instance?

Yes.

<span id="can-i-unmount-a-data-volume-from-a-subscription-ecs-instance"></span>
### Can I unmount a data volume from a subscription ECS instance?

A data volume cannot be directly unmounted from a subscription ECS instance. This type of data volume uses the subscription billing method. They have identical expiration time and are released simultaneously.

<span id="can-i-separately-buy-a-subscription-volume"></span>
### Can I separately buy a subscription volume?

No. You can buy a subscription volume when you buy a subscription ECS instance. A subscription ECS instance and its subscription volume have the same lifecycle. You cannot mount, unmount, and delete this type of volume.

<span id="questions-on-expanding-system-volumes"></span>
## Questions on expanding system volumes

<span id="how-can-i-expand-a-system-volume"></span>
### How can I expand a system volume?

For information on the detailed procedure, refer to [Extend a volume](https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume).

<span id="do-subscription-and-pay-as-you-go-ecs-instances-support-system-volume-expansion"></span>
### Do subscription and pay\-as\-you\-go ECS instances support system volume expansion?

Yes.

<span id="what-is-the-capacity-range-of-a-system-volume-what-is-the-upper-limit-to-which-i-can-expand-my-system-volume-how-can-i-expand-a-system-volume"></span>
### What is the capacity range of a system volume? What is the upper limit to which I can expand my system volume? How can I expand a system volume?

Supported capacity range after system volume expansion: current capacity to 500 GiB. For more information, refer to [Extend a volume](https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume).

<span id="why-does-automatic-volume-expansion-not-take-effect"></span>
### Why does automatic volume expansion not take effect?

If you use CentOS 6.9 as your operating system, restart your system after you create a volume for the first time and expansion is automatically performed. Otherwise, the expansion fails.
