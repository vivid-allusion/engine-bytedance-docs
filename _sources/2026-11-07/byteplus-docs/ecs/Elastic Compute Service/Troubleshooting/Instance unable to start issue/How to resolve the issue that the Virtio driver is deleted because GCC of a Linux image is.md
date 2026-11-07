---
title: "How to resolve the issue that the Virtio driver is deleted because GCC of a Linux image is uninstalled?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/resolve-Virtio-driver-deleted"
---

## Issue description

When GCC is uninstalled, the Virtio driver in an image is also uninstalled, causing a startup failure of the Bare Metal instance.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6957d8ecf007441a92a779a257bf883f.jpg)

## Causes

Due to the risks of in\-place upgrading/uninstalling core components of the system, such as GCC and glibc, we recommend using devtoolset for lossless upgrading of GCC and glibc, as well as the maintenance of multiple environments.

## Solutions

1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. Execute the following command to comment out `exclude=centos-release`.

   ```Plain Text
   sed -i "s/^exclude=centos-release/#exclude=centos-release/g" /etc/yum.conf
   ```

3. Execute the following command to install the SCL repository.

   ```Plain Text
   yum install -y centos-release-scl
   ```

4. Execute the following command to install GCC 11.2 via devtoolset:

   > Install the GCC version based on your needs.

   ```Plain Text
   yum install -y devtoolset-11-gcc\* 
   ```

5. Execute the following command to specify the GCC version to use.

   > **tip**

   * > This command temporarily activates and enables GCC 11.2. After you exit the current Shell environment or restart the system, the original GCC version is restored.

   * > To use GCC of a higher version permanently, execute the `echo "source /opt/rh/devtoolset-11/enable" >> /etc/profile && source /etc/profile` command to configure GCC 11.2 in the environment variables.

   ```Plain Text
   source /opt/rh/devtoolset-11/enable
   ```

6. Execute the following command to verify whether the activation succeeds.

   ```Plain Text
   gcc -v
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03ca877c097cb39f412e1f3f4a316351.png)
