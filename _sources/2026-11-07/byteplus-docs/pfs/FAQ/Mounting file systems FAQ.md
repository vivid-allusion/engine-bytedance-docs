---
title: "Mounting file systems FAQ"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Mounting-file-systems-FAQ"
---

This topic introduces common issues you may encounter when mounting a file system for your reference.

<span id=".5aaC5L2V5qOA5p-l566h55CG6IqC54K55piv5ZCm5a2Y5Zyo5oyC6L296ISa5pys77yf"></span>
### How to check if the management node has a mounted script?

You can refer to the following steps to check if the mounting script exists.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">If your management node does not have a mounted script, please submit a ticket to contact technical support.</div>



1. Execute the following command to check if the vepfs command is present in the `/usr/local/bin/` directory.

   ```Plain
   ls /usr/local/bin/   
   ```
   

   The return information is as follows. If there is `vepfs` in the return information, it means that the command `vepfs` exists in that directory.

   ```Plain
   cloud-id  cloud-init  cloud-init-per  jsondiff  jsonpatch  jsonpointer  jsonschema  normalizer  reset-authentication  vepfs   
   ```
   

2. Execute the following command to check if the files `region_id`, `vepfs.sh`, and `vepfs_update.sh` exist in the `/opt/vepfs/`directory.

   ```Plain
   ls /opt/vepfs/   
   ```
   

   The return information is as follows. If the return information contains a file name, it means that the mounted file already exists in the directory.

   ```Plain
   region_id  vepfs.sh  vepfs_update.sh   
   ```
   


<span id=".5oyC6L295paH5Lu257O757uf5aSx6LSl77yM5o-Q56S6LW5vZGUtYWxyZWFkeS1iZWxvbmdzLXRvLXRoZS1ncGZzLWNsdXN0ZXLvvIzmgI7kuYjlip7vvJ8="></span>
### Failed to mount file system, prompting `Node * already belongs to the GPFS cluster`?


* Problem description

   After resetting the ECS instance, remounting the PFS file system fails with an error message stating that the node already belongs to the GPFS cluster.

* Solution

   After determining the nodes that need to be remounted, you can log in to any client management node and execute the following command to remove the node from the cluster, and then remount the file system.

   ```Plain
   vepfs delforce {IP address of the reinstalled node}   
   ```
   


<span id=".5oyC6L295paH5Lu257O757uf5aSx6LSl77yM5o-Q56S6LXh4eC1uby1zdWNoLWZpbGUtb3ItZGlyZWN0b3J577yM5oCO5LmI5Yqe77yf"></span>
### Mounting file system failed, indicating `xxx: No such file or directory`?


* Problem description

   Failed to mount file system, indicating that the file or path does not exist.

* Solution

   It could be caused by the unavailability of the `/home` path. You can execute the following command to check if the corresponding path file is available.

   ```Plain
   ls -l /home   
   ```
   


<span id=".5L-u5pS5566h55CG6IqC54K55L-h5oGv5ZCO77yM5paH5Lu257O757uf5oyC6L295aSx6LSl5oCO5LmI5Yqe"></span>
### After modifying the management node information, the file system failed to mount?


* Problem description

   Modify the management node information, such as changing the node name, which results in the failure of file system mounting.

* Solution

   It may be caused by inconsistent hostName of the management node. You can refer to the following steps to view the management node information.

   1. Execute the following command to view the information of the management node.

      ```JSON
      mmlscluster
      ```
      

      The return information is as follows.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b19883e3a50462b860fe4a569f2d521~tplv-goo7wpa0wc-image.image) </span>

   2. Execute the following command to view the management node information in the hosts file.

      ```JSON
      cat /etc/hosts
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the management node information in the hosts file is consistent with the node information queried in step 1, the file system can be mounted.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If they are not consistent, you need to modify the node information in the hosts file to match the node information obtained in step 1 before you can continue to mount the file system.      </div>
      


<span id=".5ZCv5YqoLWRvY2tlci3miZPlvIAtaXB0YWJsZXMt5ZCO77yM5paH5Lu257O757uf5oyC6L295aSx6LSl5oCO5LmI5Yqe77yf"></span>
### After starting Docker and opening iptables, the file system fails to mount?


* Problem description

   After starting Docker and enabling iptables, the file system failed to mount.

* Solution

   It may be caused by the failure to connect to port 1191 after opening iptables. You can refer to the following steps to check if the port is open.

   Execute the following command to view the allowed port information.

   ```Plain
   iptables -L | grep -A 10 IN_public_allow
      
   ```
   

   The return information is as follows.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a952588b17d9b94f7d992a40c87176a8.png) </span>

   * If the returned information contains the message 1191, it means that the port is open and can be mounted normally.

   * If the returned information does not contain the 1191 information, please execute the following command to open the corresponding port.

      ```Plain
       iptables -A IN_public_allow -p tcp --dport 1191 -j
      ```
      


<span id=".5Y2H57qnLWdjYy3niYjmnKzlkI7vvIzmjILovb0tdmVwZnMt5pe25ZyoLW1tYnVpbGRncGwt6Zi25q615oql6ZSZ5oCO5LmI5Yqe77yf"></span>
### After upgrading the GCC version, an error occurs during the PFS mounting process in the mmbuildgpl stage.


* Problem description

   After upgrading the GCC version, an error occurred during the mmbuildgpl phase when mounting PFS. The error message is as follows.

   ```Plain
   cc kdump.o kdump-kern.o kdump-kern-dwarfs.o -o kdump -no-pie     -lpthread
      
   /bin/ld: kdump-kern.o: in function `GetOffset':
      
   kdump-kern.c:(.text+0x15): undefined reference to `__x86_return_thunk'
      
   /bin/ld: kdump-kern.o: in function `KernInit':
      
   kdump-kern.c:(.text+0x1f7): undefined reference to `__x86_return_thunk'
      
   /bin/ld: kdump-kern.o: in function `GenericGet':
      
   kdump-kern.c:(.text+0x37a): undefined reference to `__x86_return_thunk'
      
   /bin/ld: kdump-kern.c:(.text+0x38e): undefined reference to `__x86_return_thunk'
      
   /bin/ld: kdump-kern.o: in function `tiNext':
      
   kdump-kern.c:(.text+0x429): undefined reference to `__x86_return_thunk'
      
   /bin/ld: kdump-kern.o:kdump-kern.c:(.text+0x468): more undefined references to `__x86_return_thunk' follow
      
   collect2: error: ld returned 1 exit status
      
   ```
   

* Solution

   You can refer to the following instructions to modify the `/opt/vepfs/vepfs.sh` script.

   Add the following code before the `"ssh root@$1 "cd /usr/lpp/mmfs/bin && ./mmbuildgpl"` code.

   ```Plain
   ssh root@$1 "sed -i '/$(KBHOSTPROGS) := lxtrace/i\CFLAGS_kdump-kern.o += -mfunction-return=keep' /usr/lpp/mmfs/src/gpl-linux/Kbuild"
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After successful mounting, you need to restore the mounting script and delete the added code, otherwise it may cause other file system mounting failures.   </div>
