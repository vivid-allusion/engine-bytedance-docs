---
title: "Cause analysis and solutions for DeepEP errors in Ubuntu 24.04 + Nvidia drive 570 + doca 2.9.1 environment"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Analysis_of_the_Error_Causes_and_Solutions_for_DeepEP"
---

<span id="c1ht4VOo"></span>
## Issue description​

After nvshmem 3.2.5 was downloaded and installed in Ubuntu 24.04 + Nvidia drive 570 + doca 2.9.1 environment, DeepEP was installed. When the sample program `test_low_latency.py` officially provided by DeepEP was running, the following error occurred.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3b77bc7bdb8e133e86f6e973164546de.png) </span>

<span id="YBjLXTXK"></span>
## Cause

During OFED installation, the `ib_uverbs.ko` file should have been compiled and generated. However, during the installation process, because a critical patch has not been applied, `ib_uverbs.ko` failed to mount nvidia\-peermem to the system path `/sys/kernel/mm`. This prevented the upper\-layer nvshmem library from detecting nvidia\-peermem.

<span id="rdfdKzxx"></span>
## Solution


1. Execute the following command to enter the nvshmem source code directory.

   ```Bash
   cd /path/to/nvshmem_src
   ```
   

2. Modify the logic for verifying `nvidia-peermem.ko`.

   1. Execute the following command to open the `transport_ib_common.cpp` file.

      ```Bash
      vim /path/to/nvshmem/src/modules/transport/common/transport_ib_common.cpp
      ```
      

   2. Change the return value of the `nvshmemt_ib_common_nv_peer_mem_available()` to `NVSHMEMX_SUCCESS`.

      * Before change:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1fe2edbd7240652721211a0bcb9942c1.png) </span>

      * After change:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1e38d3f7738beead8b299f3a8e112c4.png) </span>

3. Store the following patch file in the directory where the DeepEP source code is installed. [How to upload files to an ECS instance](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07a88847117e8301c9c2f3b43e20cb2d.patch" name="latest_commit.patch">latest_commit.patch</Attachment>
   

4. Execute the following command to apply the patch file to the relevant code in the current directory where the DeepEP source code is installed.

   ```Bash
   git apply latest_commit.patch
   ```
   

5. Follow DeepEP official installation tutorial to reinstall nvshmem and DeepEP.
