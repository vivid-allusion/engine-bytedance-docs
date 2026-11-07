---
title: "Transfer external mirror to Container Registry"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Migrate_external_images_to_mirror_repository"
---

This article describes how to transfer a user's historical mirror to BytePlus for easy use in the Machine Learning Platform.

Main process of transfer:


1. Pull the mirror from the user\-specified external Container Registry to the local machine.

2. Push the local mirror to the user's BytePlus Mirror repository CR, at which point the mirror can be used in the Machine Learning Platform.

3. [Optional] Register the above mirror as a custom mirror in the [Container Registry] of the Machine Learning Platform.


<span id="相关概念"></span>
# Related concepts


* Machine Learning Platform Container Registry （see [Feature Overview](https://docs.byteplus.com/docs/mlp/54009)）

* BytePlus Mirror repository CR （see [Common concepts](https://docs.byteplus.com/docs/mlp/76491)）

* [rights management](https://docs.byteplus.com/docs/mlp/54011)


<span id="使用前提"></span>
# Premise of use


* **Main account** has been in the [BytePlus mirror (CR) console page ](https://console.byteplus.com/cr/region:cr+ap-southeast-1/instances?tab=enterprise)Activate the service and set the password for the repository, see [Container Registry - Set Access Password ](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

* If the mirror transfer is a **sub account** , the sub account needs to have a `CRFullAccess`, `MLPlatformMemberAccess`(or `MLPlatformAdminAccess`) permission policy. For details on how to modify permissions, see [rights management](https://docs.byteplus.com/docs/mlp/54011), and then go to the BytePlus Container Registry (CR) console page to set the warehouse password.

* Has \> = 1 mirror to be transferred, and can obtain the address of the mirror.

   * If the external mirror is stored in an external private repository, the repository's username and login key are also required for authentication.


<span id="操作步骤"></span>
# Procedure


1. If the external mirror is stored in a private repository, first log in to the remote private repository through `docker login`in the Terminal of the local machine.

2. Pull the mirror in the external Container Registry to the local machine as a `docker pull < mirror address >`.

3. Refer to the [push and pull mirror ](https://docs.byteplus.com/en/docs/cr/push-and-pull-images)to complete the login of CR and the push of mirror. After the push is successful, the mirror can be found in the [OCI product warehouse] of CR, and the address of the mirror can be obtained in the details page of the mirror.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12c03ddaea694e4fa8772d30832a0f1f~tplv-goo7wpa0wc-image.image) </span>


4. In the Machine Learning Platform, it is supported to select mirrors in BytePlus CR (not registered on the Machine Learning Platform) to Create Dev boxes, custom training, and other workloads.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5788773d1c8d4c0b87f1c164e17bead0~tplv-goo7wpa0wc-image.image) </span>
