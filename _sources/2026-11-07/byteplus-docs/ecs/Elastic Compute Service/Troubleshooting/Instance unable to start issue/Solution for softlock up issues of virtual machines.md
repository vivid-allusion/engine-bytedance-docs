---
title: "Solution for softlock up issues of virtual machines"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_Softlock_up_Issue_in_Virtual_Machines"
---

This topic describes how to troubleshoot soft lockup issues on Linux instances that occur when the system kernel occupies CPU resources for a long time. Soft lockup and related issues, such as high system load, kernel infinite loops, deadlocks, or kernel scheduling exceptions, can cause failed system logins, unresponsiveness, application freezes, and errors similar to `BUG: soft lockup - CPU#0 stuck for 61s`.

<span id=".5qOA5p-l57O757uf6LSf6L29"></span>
## Check system load

You can use tools like Atop to check system load. If the load is too high, adjust the system configuration or add hardware resources to mitigate it. For more information, see [Troubleshooting and solution for high CPU usage or load of ECS instance with Linux system](https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_solution_for_high_CPU_usage_or_CPU_load_issues_on_the__instance) and [Troubleshooting and solution for high disk BPS/IOPS load of ECS instance with Linux system](https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_solution_for_high_BPS_or_IOPS_load_issues_on_ECS_instance_disks_of_Linux_systems).

<span id=".5qOA5p-l5YaF5qC45piv5ZCm5a2Y5Zyo5q275b6q546v5oiW5q276ZSB44CB5YaF5qC46LCD5bqm5byC5bi4"></span>
## Check for infinite loops, deadlocks, or scheduling exceptions in the kernel

You can use kernel debugging tools (such as Kgdb) to inspect the kernel code, identify potential infinite loops, deadlocks, and kernel scheduling issues. After you locate the problems, resolve them by modifying the code or applying patches.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Kernel debugging tools are third\-party tools. After you select a tool, refer to its manual to check for infinite loops, deadlocks, or scheduling exceptions in the kernel, and then troubleshoot your issue accordingly.</div>
