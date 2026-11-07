---
title: "Turn off mmap read-ahead"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Turn-off-mmap-read-ahead"
---

In the mmap random read scenario, if your real network bandwidth is much larger than the effective business bandwidth, pre\-reading may be triggered. You can refer to this article to turn off mmap pre\-reading in the client.

<span id="2419d65d"></span>
## Background Information

In the mmap random read scenario, if your random read block size is 4KB, read\-ahead will not be triggered, and the real business network bandwidth and effective bandwidth remain consistent; if the random read block size is greater than 4KB, read\-ahead will be triggered, for example, 8KB read The operation triggers 4MB data pre\-reading, causing the actual network bandwidth to be much larger than the effective service bandwidth. It is therefore recommended that you turn off mmap read\-ahead in the client management cluster.

<span id="e5084bad"></span>
## **Procedure**


1. Log in to the PFS management node. For specific steps, see Logging in to the cloud server.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you create a mount point, ECS will automatically create three PFS management nodes. You can log in to the PFS console to view the corresponding management node IP and login password.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The PFS management node name format is <code>client-vepfs-{file system ID}-{mount point ID}-{number}</code>.   </div>
   

2. Execute the following command to view the read\-ahead parameters.

   ```Plain
   mmlsconfig|grep prefetch
   ```
   

   The return information is as follows.

   ```Plain
   prefetchAggressivenessWrite 0
   prefetchAggressivenessRead 2
   ```
   

3. Execute the following command to modify the parameters.

   ```Plain
   mmchconfig prefetchAggressivenessRead=0 -i
   ```
   

   The return information is as follows, indicating that the modification was successful.

   ```Plain
   mmchconfig: Command successfully completed
   ```
   

4. Execute the following command to modify the parameters.

   ```Plain
   mmchconfig prefetchAggressiveness=0 -i
   ```
   

   The return information is as follows, indicating that the modification was successful.

   ```Plain
   mmchconfig: Command successfully completed
   ```
