---
title: "How do I resolve disk anomalies caused by io_uring on instances that use the veLinux 5.15 kernel?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/velinux-5-15-disk-error-troubleshoot"
---

## Issue description

When ECS instances that use a veLinux 5.15.x kernel image run io_uring workloads, two types of anomalies may occur under high I/O load.

* **Disk I/O becomes unresponsive for an extended period**

   ```Plain Text
   2025-12-08 06:51:03 +951710  INFO: task node_exporter:2301919 blocked for more than 1063649 seconds.
   2025-12-08 06:51:03 +952029        Tainted: G S         OE     5.15.152.bsk.13-amd64 #5.15.152.bsk.13
   2025-12-08 06:51:03 +952299  "echo 0 > /proc/sys/kernel/hung_task_timeout_secs" disables this message.
   2025-12-08 06:51:03 +952565  task:node_exporter   state:D stack:    0 pid:2301919 ppid:  9209 flags:0x00000000
   2025-12-08 06:51:03 +952567  Call Trace:
   2025-12-08 06:51:03 +952567   <TASK>
   2025-12-08 06:51:03 +952568   __schedule+0x9f9/0x10e0
   2025-12-08 06:51:03 +952571   schedule+0x51/0xd0
   2025-12-08 06:51:03 +952573   schedule_preempt_disabled+0xa/0x10
   2025-12-08 06:51:03 +952575   __mutex_lock.isra.11+0x329/0x440
   2025-12-08 06:51:03 +952576   queue_attr_show+0x2b/0x60
   2025-12-08 06:51:03 +952579   sysfs_kf_seq_show+0x98/0x100
   2025-12-08 06:51:03 +952581   seq_read_iter+0x186/0x3c0
   2025-12-08 06:51:03 +952583   new_sync_read+0x112/0x190
   2025-12-08 06:51:03 +952585   vfs_read+0xee/0x190
   2025-12-08 06:51:03 +952587   ksys_read+0x59/0xd0
   2025-12-08 06:51:03 +952589   do_syscall_64+0x34/0xb0
   2025-12-08 06:51:03 +952592   entry_SYSCALL_64_after_hwframe+0x61/0xcb
   2025-12-08 06:51:03 +952593  RIP: 0033:0x4ac9db
   2025-12-08 06:51:03 +952595  RSP: 002b:000000c015aa8ee0 EFLAGS: 00000206 ORIG_RAX: 0000000000000000
   2025-12-08 06:51:03 +952596  RAX: ffffffffffffffda RBX: 000000c00005b000 RCX: 00000000004ac9db
   2025-12-08 06:51:03 +952597  RDX: 0000000000001001 RSI: 000000c015366000 RDI: 000000000000005c
   2025-12-08 06:51:03 +952597  RBP: 000000c015aa8f30 R08: 0000000000000001 R09: 000000c016165e00
   2025-12-08 06:51:03 +952598  R10: 00007fd64d083c70 R11: 0000000000000206 R12: 000000c015366000
   2025-12-08 06:51:03 +952599  R13: 0000000000000000 R14: 000000c00607cb60 R15: 0000000000000009
   2025-12-08 06:51:03 +952600   </TASK>
   2025-12-08 06:51:03 +952735  INFO: task node_exporter:2301919 is blocked on a mutex likely owned by task sh:2540448.
   2025-12-08 06:51:03 +953062  task:sh              state:D stack:    0 pid:2540448 ppid:  9995 flags:0x00000000
   2025-12-08 06:51:03 +953064  Call Trace:
   2025-12-08 06:51:03 +953065   <TASK>
   2025-12-08 06:51:03 +953066   __schedule+0x9f9/0x10e0
   2025-12-08 06:51:03 +953069   ? call_rcu+0xd8/0x580
   2025-12-08 06:51:03 +953071   schedule+0x51/0xd0
   2025-12-08 06:51:03 +953074   blk_mq_freeze_queue_wait+0x62/0x90
   2025-12-08 06:51:03 +953076   ? finish_wait+0x80/0x80
   2025-12-08 06:51:03 +953078   blk_mq_update_nr_requests+0x4b/0x150
   2025-12-08 06:51:03 +953080   queue_requests_store+0x69/0xa0
   2025-12-08 06:51:03 +953083   queue_attr_store+0x3c/0x60
   2025-12-08 06:51:03 +953085   kernfs_fop_write_iter+0x12d/0x1c0
   2025-12-08 06:51:03 +953088   new_sync_write+0x119/0x1a0
   2025-12-08 06:51:03 +953090   vfs_write+0x181/0x260
   ```

* **Workload data validation fails**

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c28104fc833acb21619484aa3f7bfa3a.png)

## Causes

The io_uring implementation in the 5.15 kernel has defects. Under high I/O load, these defects may trigger disk anomalies through the following two paths:

* When a batch of direct I/O requests that includes both reads and writes is submitted, the block device layer may incorrectly initialize the read/write flags of the requests. This causes read and write requests to be processed incorrectly and may affect data integrity. For example, submitting 8 DIRECT I/O requests at once with io_uring, where read and write requests are included together, may trigger this issue.

* During io_uring request processing, the reference count of the block device queue may not be released correctly. When operations that require freezing the queue are performed afterward, such as adjusting disk queue parameters, switching the I/O scheduler, resetting the device, or hot\-plugging, the queue may fail to complete the freeze for an extended period, which appears as I/O being stuck on a single disk.

## Solutions

With a kernel hot patch, you can fix the issue without restarting the instance or the workloads running on it, preventing subsequent requests from triggering the issue.

> **warning**

> Currently, you can fix this issue with a hot patch only on instances running kernel version `5.15.152-7.1.ve2`. The hot patch only prevents subsequent requests from triggering this issue again. It cannot recover data that has already been corrupted.

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to check the kernel version of the operating system.

   ```Bash
   sudo uname -r
   ```

   When the following output is displayed, the kernel version is `5.15.152-7.1.ve2`.

   ```Bash
   5.15.152-7.1.ve2.x86_64
   ```

3. Install the hot patch by running the corresponding command according to the operating system and kernel version.

   ```Bash
   sudo yum makecache
   sudo yum install -y livepatch-5.15.152-7.1.ve2-io-uring-data-corruption-1.0-1.x86_64
   ```

4. Execute the following command to check whether the hot patch is successfully installed.

   ```Bash
   rpm -qa | grep -F 'livepatch-5.15.152-7.1.ve2-io-uring-data-corruption-1.0-1.x86_64'
   ```

   When the following output is displayed, the hot patch is successfully installed.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d18ad3d5d6f9ed1f96672ba3bb2c8c8.png)

5. Execute the following command to verify that the hot patch module has been loaded successfully.

   ```Bash
   sudo lsmod | grep -i livepatch
   ```

   When the following output is displayed, the hot patch is loaded successfully and is in effect.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de4fbc38c5dbf091ff6c27a23d12898f.png)
