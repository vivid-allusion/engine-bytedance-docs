---
title: "How to solve the error \"checkVirtioInstall fail\" or \"Check initramfs failed\" reported by migration tool Agent?"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/checkVirtioInstall-failed-or-Check-initramfs-failed"
---

<span id=".5pWF6Zqc546w6LGh"></span>
## Issue description

Migration fails, and the migration log file smc.log records one of the following ERROR messages: "checkVirtioInstall fail" or "Check initramfs failed".

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

The SMC migration tool Agent has detected that the Virtio driver on your source server is not installed or not properly configured, and therefore fails to run as expected.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

<span id=".5q2l6aqk5LiA77ya56Gu6K6k5YaF5qC45piv5ZCm5pSv5oyBVmlydGlv6amx5Yqo"></span>
### I: Confirm whether the kernel supports the Virtio driver


1. Execute the following command to check whether the current virtual machine operating system supports the Virtio driver.

   ```Plain Text
   grep -i virtio /boot/config-$(uname -r)
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a160beea6fd59bf8d476d9a20ab3de8e.png) </span>

   Output description:

   From the output, check the values of the `CONFIG_VIRTIO_BLK` and `CONFIG_VIRTIO_NET` parameters, and then proceed with the appropriate follow\-up actions based on their values.

   
   |Results |Description |
   |---|---|
   |Parameter value: `m` |The operating system kernel supports the Virtio driver.<br><br>Perform the operation in [II](https://docs.byteplus.com/en/docs/smc/checkVirtioInstall-failed-or-Check-initramfs-failed#.5q2l6aqk5LqM77ya56Gu6K6k5Li05pe25paH5Lu257O757uf5piv5ZCm5YyF5ZCrVmlydGlv6amx5Yqo) to check whether the Virtio driver is included in the initramfs or initrd file system. |
   |Parameter value: `y` |The operating system kernel already includes the Virtio driver. You can proceed with migrating to the BytePlus platform. |
   |These two parameters are not available. |This indicates that the kernel of the corresponding operating system does not support the Virtio driver. As a result, direct migration to the BytePlus platform is currently not supported. You need to write code to install the Virtio driver yourself. |
   


<span id=".5q2l6aqk5LqM77ya56Gu6K6k5Li05pe25paH5Lu257O757uf5piv5ZCm5YyF5ZCrVmlydGlv6amx5Yqo"></span>
### II: Check whether the temporary file system includes the Virtio driver

Based on the operating system of the virtual machine, execute the corresponding command below.


* CentOS 6/CentOS 7/CentOS 8/RedHat 6/RedHat 7 operating systems.

   ```Plain Text
   lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
   ```
   

* RedHat 5/CentOS 5 operating systems.

   ```Plain Text
   mkdir -p /tmp/initrd && cd /tmp/initrd
   zcat /boot/initrd-$(uname -r).img | cpio -idmv
   find . -name "virtio*"
   ```
   

* Debian/Ubuntu operating systems.

   ```Plain Text
   lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57fe1034197e37f7669d5fdb9df7abac.png) </span>

   Output description:

   * If the output is as shown above, this indicates that the initramfs temporary file system already contains the virtio_blk driver and the virtio.ko, virtio_pci.ko, and virtio_ring.ko dependencies. You can proceed with migrating to the BytePlus platform. For operation details, see [Importing migration sources](https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources).

   * If the output is empty, the temporary file system does not contain the Virtio driver. Proceed to [III](https://docs.byteplus.com/en/docs/smc/checkVirtioInstall-failed-or-Check-initramfs-failed#.5q2l6aqk5LiJ77ya5L-u5aSN5Li05pe25paH5Lu257O757uf) to repair the temporary file system.


<span id=".5q2l6aqk5LiJ77ya5L-u5aSN5Li05pe25paH5Lu257O757uf"></span>
### III: Repair the temporary file system


<Tabs>
<Tab zoneid="EyZS6Cwpn5" title="CentOS 6/AlmaLinux 8/Fedora 33 and later versions">
<TabTitle>CentOS 6/AlmaLinux 8/Fedora 33 and later versions</TabTitle>

For CentOS 6/AlmaLinux 8/Fedora 33 and later versions, with kernel versions higher than 2.6.24, follow the steps below to complete the repair.


1. Execute the following command to open the dracut.conf file.


```Plain Text
vim /etc/dracut.conf
```



2. Press `i` to enter edit mode and add the following content.


```Plain Text
add_drivers+="virtio_blk virtio_scsi virtio_net virtio_pci virtio_ring virtio"
```



3. After you modify the file, press `Esc`, enter `:wq`, and then press Enter to save the modification and exit the file.

4. Execute the following command to regenerate initrd.


```Plain Text
dracut -f
```





</Tab>
<Tab zoneid="u76hNiGvJa" title="Debian/Ubuntu">
<TabTitle>Debian/Ubuntu</TabTitle>

For Debian/Ubuntu operating systems, follow the steps below to complete the repair.


1. Execute the following command to open the modules file.


```Plain Text
vim /etc/initramfs-tools/modules
```



2. Press `i` to enter edit mode and add the following content.


```Plain Text
virtio_blk
virtio_scsi
virtio_net
virtio_pci
virtio_ring
virtio
```



3. After you modify the file, press `Esc`, enter `:wq`, and then press Enter to save the modification and exit the file.

4. Execute the following command to regenerate initramfs.


```Plain Text
update-initramfs -u
```


<span id=".5q2l6aqk5Zub77ya6aqM6K-B5L-u5aSN57uT5p6c"></span>
### 


</Tab>
</Tabs>


<span id="iQN7iqDm"></span>
### IV: Verify the repair results

After you repair the temporary file system, you can execute the command in [II](https://docs.byteplus.com/en/docs/smc/checkVirtioInstall-failed-or-Check-initramfs-failed#.5q2l6aqk5LqM77ya56Gu6K6k5Li05pe25paH5Lu257O757uf5piv5ZCm5YyF5ZCrVmlydGlv6amx5Yqo) again to verify that the Virtio driver is contained in the initramfs or initrd temporary file system.
