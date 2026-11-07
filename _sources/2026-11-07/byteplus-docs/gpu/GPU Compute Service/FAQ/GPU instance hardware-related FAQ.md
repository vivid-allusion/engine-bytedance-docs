---
title: "GPU instance hardware-related FAQ"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU-instance-hardware-FAQs"
---

&nbsp;

<span id="7KNWjNzE"></span>
## How to identify and handle hardware\-related failures?

Compared with general ECS instances, GPU instances have more peripherals,such as GPUs, RDMA pass\-through network interfaces, and local volumes. Therefore, in addition to common issues that may occur with general ECS instances, there may also be sub\-healthy states or failures involving the GPUs, pass\-through network interfaces, and PCIe links. For common failures and recommended solutions for GPU instances, see [Figure 1](https://docs.byteplus.com/en/docs/95/20699#Z2EdGTRZ).

<span id="Z2EdGTRZ"></span>
### Figure 1 Common failures and recommended solutions

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_208f7a43009468c6be21972dbbd4dc4a.png) </span>

<span id="xtqYJ3Zp"></span>
### Figure 2 Troubleshooting process

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_221c885a95ff001a8ab78b2a0b5b43f0.png) </span>

The process for handling GPU sub\-healthy states or failures is shown in Figure 2. The following section focuses on the process for handling sub\-healthy states.

> For other failures other than sub\-healthy states, you can directly submit a failure ticket in the [Ticket System](https://console.byteplus.com/workorder/create/) , or wait for the system to automatically detect the abnormal situation and automatically submit a failure ticket for handling.


1. When a "monitoring exception event notification" or "instance business interruption exception" occurs, you need to analyze whether it is a sub\-healthy state (refer to [Figure 1](https://docs.byteplus.com/en/docs/95/20699#Z2EdGTRZ)).

   * If yes, please [restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) or [reset the GPU](https://docs.byteplus.com/en/docs/gpu/Resetting-GPUs). For details, refer to the "Handle sub\-healthy state" part in [Figure 1](https://docs.byteplus.com/en/docs/95/20699#Z2EdGTRZ).

   * If not, it is a failure. Please contact OnCall or submit a ticket for handling.

2. Check whether the sub\-healthy state has been resolved.

   * If not resolved, contact Oncall or submit a ticket for handling.

   * If recovered, the process is complete.


<span id="K9u0MyWe"></span>
## List of common issues


|Failure types (see [Figure 1](https://docs.byteplus.com/en/docs/95/20699#Z2EdGTRZ)) |Related documents |
|---|---|
|GPU disconnection failures |[How to check whether the GPU card is disconnected?](https://docs.byteplus.com/en/docs/6419/1115088#%E5%A6%82%E4%BD%95%E6%9F%A5%E7%9C%8Bgpu%E6%98%AF%E5%90%A6%E6%8E%89%E5%8D%A1%EF%BC%9F) |
|Link failures |[How to check whether the bandwidth/link is normal?](https://docs.byteplus.com/en/docs/6419/1115088#%E5%A6%82%E4%BD%95%E6%9F%A5%E7%9C%8B%E5%B8%A6%E5%AE%BD-%E9%93%BE%E8%B7%AF%E6%98%AF%E5%90%A6%E6%AD%A3%E5%B8%B8%EF%BC%9F) |
|\- |[How to view XID information?](https://docs.byteplus.com/en/docs/6419/1115088#%E5%A6%82%E4%BD%95%E6%9F%A5%E7%9C%8Bxid%E4%BF%A1%E6%81%AF%EF%BC%9F) |
|\- |[How to collect NVIDIA logs?](https://docs.byteplus.com/en/docs/6419/1115088#%E5%A6%82%E4%BD%95%E6%94%B6%E9%9B%86nvidia%E6%97%A5%E5%BF%97%EF%BC%9F) |


<span id="iECV9fAU"></span>
### How to check whether the GPU card is disconnected?


* **Method 1**

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   2. Execute the following command. If the output ends with (rev ff), it indicates a GPU recognition exception.

      `lspci | grep -i nvidia`

      ```Plain Text
          # lspci | grep -i nvidia
          31:00.0 3D controller: NVIDIA Corporation Device 2236 (rev a1)
          65:00.0 3D controller: NVIDIA Corporation Device 2236 (rev a1)
          98:00.0 3D controller: NVIDIA Corporation Device 2236 (rev a1)
          e3:00.0 3D controller: NVIDIA Corporation Device 2236 (rev ff)
      ```
      

   3. Execute the following command to check the number of GPU cards. As shown below, the query is for a 4\-card configuration, with 1 card missing.

      `nvidia-smi`

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ccb4c2e7ec2fcda74451974c188f4bd1.jpg) </span>

* **Method 2**

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   2. Execute the following command to view system logs.

      `cat /var/log/kern.log | grep -i xid`

      The following output indicates that a GPU card is missing.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35c3b444c3266366ff5deeb8c969594d.jpg) </span>


<span id="IJQBgtwd"></span>
### How to check whether the bandwidth/link is normal?


* **Method 1: lspci bandwidth check**

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   2. Execute the following commands.

      `lspci -vvd 10de: | grep -i "Lnkcap:\|Lnksta:"`

      The output is as follows. Lnkcap is the rated bandwidth, and Lnksta is the current bandwidth. If the two values are consistent, it indicates that the bandwidth/link is normal.

      ```Plain Text
      # lspci -vvd 10de: | grep -i Lnkcap:
                      LnkCap: Port #0, Speed 8GT/s, Width x16, ASPM not supported
                      LnkCap: Port #4, Speed 8GT/s, Width x16, ASPM not supported
                      LnkCap: Port #16, Speed 8GT/s, Width x16, ASPM not supported
                      LnkCap: Port #20, Speed 8GT/s, Width x16, ASPM not supported
      # lspci -vvd 10de: | grep -i Lnksta:
                      LnkSta: Speed 2.5GT/s (downgraded), Width x16 (ok)
                      LnkSta: Speed 2.5GT/s (downgraded), Width x16 (ok)
                      LnkSta: Speed 2.5GT/s (downgraded), Width x16 (ok)
                      LnkSta: Speed 2.5GT/s (downgraded), Width x16 (ok)
      ```
      

* **Method 2: Nvidia\-smi check**

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   2. Execute the following commands.

      `nvidia-smi -q | grep -i -A 2 'Link width'`

      The output is as follows. The values of Max and Current are consistent, indicating that no bandwidth or link exception has occurred.

      ```Plain Text
      # nvidia-smi -q | grep -i -A 2 'Link width'
                  Link Width
                      Max                       : 16x
                      Current                   : 16x
      --
                  Link Width
                      Max                       : 16x
                      Current                   : 16x
      --
                  Link Width
                      Max                       : 16x
                      Current                   : 16x
      --
                  Link Width
                      Max                       : 16x
                      Current                   : 16x
      ```
      


<span id="yE7QM4sW"></span>
### How to view XID information?


1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following commands.

   ```Bash
   cat /var/log/messages | grep "Xid (PCI"
   cat /var/log/kern.log | grep "Xid (PCI"
   ```
   

   The output is displayed as shown below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93fc78005749205da81bdbbb51f0a76f.jpg) </span>

   If XID error information is detected on the GPU node, follow the recommended solution for the corresponding XID error code. For details, refer to [Common XID solutions](https://docs.byteplus.com/en/docs/6419/1928467#Rtznt7dq).


<span id="TFQCVrTh"></span>
### How to collect NVIDIA logs?

<span id="2CFrAqpE"></span>
#### Virtual machine scenario


1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following commands.

   ```JSON
   sudo nvidia-bug-report.sh
   ```
   

   The collected files are shown in the following figure.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dd54345e90d81deab99f7e9e48d5a435.jpg) </span>

   The **`nvidia-bug-report.sh`** script automatically collects system kernel logs, NVIDIA driver logs, and other debugging information, and generates a compressed file named `nvidia-bug-report.log.gz`.

   > This file can be attached when you submit a ticket.   
   

   In most scenarios, the **`nvidia-bug-report.sh`** script is quickly executed.

   * If it is slow, reserve up to 1\-hour waiting time.

   * If the command hangs, you can collect alternative logs in safe mode by adding additional parameters to avoid the risk of hanging.

      ```Bash
      nvidia-bug-report.sh --safe-mode --extra-system-data
      ```
      


<span id="1jmqHfbb"></span>
#### **VKE scenario**


1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to obtain the log download link.

   ```Bash
   curl -s https://diagnose-beijing.tos-cn-beijing.ivolces.com/cmds/diagnose.sh | bash
   ```
   

   The result is as follows.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6dc1c8d374712b7635f352d8df9043a2.png) </span>

3. Execute the wget command generated above to obtain the log file.
