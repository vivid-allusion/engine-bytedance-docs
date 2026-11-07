---
title: "Troubleshooting and solution for high CPU usage or load of ECS instance with Windows system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Investigation_and_Solution_for_High_CPU_Usage_or_Load_Issues_in_ECS_Instances_with_Windows_Systems"
---

This topic describes how to use the Microsoft tool Resource Monitor to troubleshoot the issue of high CPU usage or load (CPU usage ≥ 85%) during the usage of a Windows instance.


> * For Windows Server 2008 and later systems, the built\-in Resource Monitor is typically used to monitor CPU performance.

> * This topic may contain information about third\-party products, which is provided for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.


<span id="AOoKuORX"></span>
## Procedure

<span id="V3vZ616e"></span>
### Step 1: Locate the issue


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1?LibVersion=markdown备份版本#.55m75b2V5pa55byP).

2. In the lower left corner of the desktop, click the Start menu and select "Run".

3. In the "Run" dialog box, enter perfmon \-res, and click the "OK" button.

4. On the Resource Monitor page, check if any processes have excessively high CPU usage.

5. For processes with high CPU resource usage, record their corresponding Process IDs (PIDs) and names to locate the specific program paths in the next step.

6. Identify whether high\-CPU processes are abnormal and locate the specific paths of the programs.

   1. In Task Manager, click the "Details" tab.

   2. Click PID to sort processes, then locate the abnormal processes identified in the previous step. Right\-click the process name, open the file location, and check for the process abnormality, such as:

      * The ECS instance is infected with viruses or Trojans.

      * Third\-party antivirus software is running on the ECS instance.

      * Abnormal applications, faulty drivers, high I/O usage, or applications with heavy interrupt processing on the ECS instance.


<span id="Fma380it"></span>
### Step 2: Analyze and handle

Determine whether the processes causing high CPU usage are normal, and follow the corresponding steps below for handling.


|**Process** |**Operation** |
|---|---|
|Normal processes |Generally, frequent business access or Windows built\-in services (such as update services) may consume high network traffic and CPU resources.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For Windows Server 2012 R2 instances, we recommend that you configure at least 2 GiB of memory.</div><br> |
|Abnormal processes |Excessively high CPU usage may also result from malicious viruses or Trojan intrusions. You need to manually detect and solve the process exception. Example:<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Some third\-party malicious programs may disguise themselves as svchost.exe or TCPSVCS.EXE of the operating system, causing high CPU usage. If you cannot determine whether a process is a virus or a Trojan, search for the process name online to confirm.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We recommend <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot?LibVersion=markdown备份版本">creating a snapshot</a> first to back up instance data before you scan and remove the viruses. This improves your fault tolerance and ensures data security.</div><br><br><br>* Use commercial antivirus software, or use the free security tool "Microsoft Safety Scanner" to scan and remove viruses in safe mode.<br><br>* Run Windows Update to install the latest Microsoft security patches.<br><br>* Use MSconfig to disable all non\-Microsoft built\-in services and drivers, then check if the issue recurs. |


<div style="text-align: right">
</div>
