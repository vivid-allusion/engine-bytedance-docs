---
title: "Mounting FAQ"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Mounting-FAQ"
---

This topic introduces common issues you may encounter when mounting or unmounting file systems.

<span id="7182c173"></span>
### Device is busy when uninstalling FileNAS?


* Problem description: When uninstalling FileNAS, it shows that the device is busy and cannot be uninstalled.

* Solution: You can terminate the process that is occupying the disk first, and then uninstall the FileNAS again.

   The specific steps are as follows:

   1. Execute the command `lsof {Directory address}` to view the processes that occupy the directory. This topic takes the example of mounting to the local directory `/nasdir`.

      ```Plain
      lsof /nasdir/
      ```
      

      The return information is as follows.

      ```Plain
      COMMAND    PID USER   FD   TYPE DEVICE SIZE/OFF    NODE NAME
      bash     36462 root  cwd    DIR  259,2     4096 4849665 /nasdir
      ```
      

   2. After confirming that this process does not affect the business, execute the command `kill -9 $PID`to terminate the process.

      ```Plain
      kill -9 36462
      ```
      


<span id="921adbf9"></span>
### Stuck when uninstalling a deleted FileNAS, with no response or information returned?


* Problem description: When uninstalling a deleted FileNAS, executing the umount command does not return any information, making it impossible to unmount.

* Solution: You can execute the`umount -f` command to forcefully unmount the FileNAS.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If there is an error, you can try executing it more than 5 times in a row.   </div>
