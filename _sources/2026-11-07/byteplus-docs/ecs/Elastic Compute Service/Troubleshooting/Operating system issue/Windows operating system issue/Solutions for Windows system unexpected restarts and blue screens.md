---
title: "Solutions for Windows system unexpected restarts and blue screens"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_for_Handle_Windows_System_Exception_Restart_and_Blue_Screen"
---

This topic describes how to prevent and resolve Blue Screen of Death (BSOD) or unexpected system restart issues on Windows systems.


> * A system blue screen or unexpected restart may prevent the preservation of relevant information for troubleshooting.

> * This topic may contain information about third\-party products, which is provided for reference only. The BytePlus platform makes no representations or warranties of any kind, express or implied, regarding the performance, reliability, or availability of any third\-party product, or any consequences arising from its use.

> * The copyright of the official Microsoft links cited in this topic belongs to Microsoft. The BytePlus platform assumes no responsibility for the scope of operating systems applicable to this topic, or issues that may arise from Microsoft Windows product iterations or delayed document updates.


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

When the system is configured to collect memory dump files (crash dumps), it automatically generates a blue screen dump file and saves it to the specified directory (default: `C:\Windows\memory.dmp`). This prevents data loss when the system crashes and displays a blue screen.

<span id=".5pON5L2c6K-05piO"></span>
## Usage note

If you want to modify the configuration or data of an instance (including but not limited to ECS or RDS instances), we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) in advance to back up the instance data. This helps improve fault tolerance and ensure data security.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

The common causes of operating system blue screens are as follows:


* Corruption of system files or the registry caused by incorrect operations or viruses.

* Abnormal memory access due to incompatibility between device drivers and the operating system.

* Bugs in the operating system itself.

* Faulty drivers of third\-party antivirus software.


<span id=".57u05oqk5bu66K6u"></span>
## Maintenance suggestions

To prevent system blue screens and potential data loss, we recommend that you follow the operations below, referring to the common causes, official Microsoft advice, and daily troubleshooting experience.


* Run regular antivirus scans in the Cloud Security Center and update your antivirus software version periodically to prevent blue screens caused by viruses or incompatibility between antivirus software drivers and the operating system.

* Run Windows Update regularly to ensure that the latest Microsoft security updates are installed.

* Do not store important data on the system volume. Instead, store it on a data volume.

* [Create regular snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) of the system volume and data volume to back up instance data for future data recovery.

* Back up the registry file before modifying the system registry to avoid accidental changes to system files.


<span id=".5pON5L2c6K-05piO"></span>
## Usage note

When the operating system encounters a blue screen, it displays the corresponding Bug Check Code Reference, as well as the modules and related causes that may have triggered the blue screen. You can perform operations based on the prompted information. For more information, refer to the [Bug Check Code Reference](https://msdn.microsoft.com/en-us/library/windows/hardware/ff560129(v=vs.85).aspx) listed on Microsoft official website  for assistance.
