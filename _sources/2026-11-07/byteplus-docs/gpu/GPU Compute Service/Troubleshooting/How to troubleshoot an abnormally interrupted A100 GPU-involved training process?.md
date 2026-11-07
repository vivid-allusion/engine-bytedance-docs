---
title: "How to troubleshoot an abnormally interrupted A100 GPU-involved training process?"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/How-should-I-troubleshoot-exceptional-interruptions-to-training-with-A100"
---

1. Check the system `syslog` or `dmesg` to check if any "xid" error appeared around the time of the failure. "xid" error messages contain `NVRM: Xid`. In the following example, the "xid" error code is 63:

   ```Plain Text
   [Mon Jan  9 13:49:48 2023] NVRM: Xid (PCI:0000:6b:01): 63, pid=4881, Row Remapper: New row marked for remapping, reset gpu to activate.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the "xid" error code is 13, 31, 43, 45, or 68, the GPU can usually perform the repair itself.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If other "xid" error codes appear, submit a ticket for solutions. This topic describes how to manually repair an "xid" error with the value of 63.   </div>
   

2. When "xid" error code 63 appears, and the "reset gpu" is displayed, execute the following command to check the status of the faulty GPU.

   ```Plain Text
   nvidia-smi -q | grep -Ei "ECC Errors|Correctable|Volatile|Aggregate|Remap|^GPU|Bit ECC|Retired Pages"
   ```
   

   For example, as shown below, GPU 6 has an unrecoverable error during `remapped rows`:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_599a0da29c251d86f61a412171d14ec5.png) </span>

3. Execute the following command to check the running status of **nvidia\-fabricmanager**. If the output is `Active: active (running)`, this indicates normal operation.

   `systemctl status nvidia-fabricmanager`

4. Execute the **nvidia\-smi \-r** command to repair.
