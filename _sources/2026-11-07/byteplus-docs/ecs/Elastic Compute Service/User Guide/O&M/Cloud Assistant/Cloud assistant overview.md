---
title: "Cloud assistant overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant"
---

The cloud assistant is a native tool for automatic O&M, which is developed by BytePlus. With the cloud assistant, you can execute O&M commands on one or multiple objects. You do not need to input passwords, log in, or use a jump server.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

For ECS instances that are installed with the cloud assistant Agent and are in a **Running** state, you can perform batch O&M operations in the Cloud Assistant console. For example, install the Cloud Monitor plugin and modify instance passwords. You can also use the operation orchestration feature to combine and execute multiple cloud product actions and operations steps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">There are some differences between cloud assistant command execution and direct in\-instance command execution. For details, refer to  <a href="https://docs.byteplus.com/en/docs/ecs/Differences-between-cloud-assistant-execution-and-in-instance-execution">Description of differences between cloud assistant command executions and in\-instance command executions</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Currently, you can only install and use the cloud assistant Agent on instances running the following operating system versions.


|Image |Operating system type |Operating system version |
|---|---|---|
|Linux |veLinux |* veLinux 2.0 64 bit<br><br>* veLinux 2.0 for TDX 64 bit<br><br>* veLinux 2.0 CentOS Compatible for TDX 64 bit<br><br>* veLinux 2.0 CentOS Compatible 64 bit |
|||* veLinux 1.0 64 bit<br><br>* veLinux 1.0 CentOS Compatible with 5.10 kernel 64 bit<br><br>* veLinux 1.0 CentOS Compatible 64 bit<br><br>* veLinux 1.0 with 5.10 kernel 64 bit |
||Red Hat Enterprise Linux |* Red Hat 9.3 64 bit<br><br>* Red Hat 9.2 64 bit<br><br>* Red Hat 9.1 64 bit<br><br>* Red Hat 9.0 64 bit<br><br>* Red Hat 8.10 64 bit<br><br>* Red Hat 8.9 64 bit<br><br>* Red Hat 8.8 64 bit<br><br>* Red Hat 8.7 64 bit<br><br>* Red Hat 8.6 64 bit<br><br>* Red Hat 8.5 64 bit<br><br>* Red Hat 8.4 64 bit<br><br>* Red Hat 8.3 64 bit<br><br>* Red Hat 8.2 64 bit |
||CentOS |* CentOS Stream 9 64 bit<br><br>* CentOS Stream 8 64 bit<br><br>* CentOS 7.9 BIOS 64 bit<br><br>* CentOS 7.9 64 bit<br><br>* CentOS 7.8 64 bit<br><br>* CentOS 7.7 64 bit<br><br>* CentOS 7.6 64 bit<br><br>* CentOS 7.5 64 bit<br><br>* CentOS 7.4 64 bit<br><br>* CentOS 7.3 64 bit<br><br>* CentOS 7.2 64 bit<br><br>* CentOS 7.1 64 bit<br><br>* CentOS 6.9 64 bit |
||Ubuntu |* Ubuntu 24.04 64 bit<br><br>* Ubuntu 22.04 64 bit<br><br>* Ubuntu 22.04 BIOS 64 bit<br><br>* Ubuntu 20.04 64 bit<br><br>* Ubuntu 20.04 BIOS 64 bit<br><br>* Ubuntu 18.04 64 bit<br><br>* Ubuntu 16.04 64 bit |
||Debian |* Debian 12 64 bit<br><br>* Debian 11 64 bit<br><br>* Debian 10 64 bit<br><br>* Debian 10 BIOS 64 bit<br><br>* Debian 9 64 bit |
||OpenSUSE |OpenSUSE 15.4 64 bit |
||Fedora |Fedora 37 64 bit |
||Rocky Linux |* Rocky Linux 9.4 64 bit<br><br>* Rocky Linux 9.2 64 bit<br><br>* Rocky Linux 9.1 64 bit<br><br>* Rocky Linux 9.0 64 bit<br><br>* Rocky Linux 8.10 64 bit<br><br>* Rocky Linux 8.9 64 bit<br><br>* Rocky Linux 8.8 64 bit<br><br>* Rocky Linux 8.7 64 bit<br><br>* Rocky Linux 8.6 64 bit<br><br>* Rocky Linux 8.5 64 bit |
||AlmaLinux |* AlmaLinux 9.4 64 bit<br><br>* AlmaLinux 9.3 64 bit<br><br>* AlmaLinux 9.2 64 bit<br><br>* AlmaLinux 9.1 64 bit<br><br>* AlmaLinux 8.10 64 bit<br><br>* AlmaLinux 8.9 64 bit<br><br>* AlmaLinux 8.8 64 bit<br><br>* AlmaLinux 8.7 64 bit |
|Windows<br><br><div style="text-align: center"><br></div><br> |Windows Server 2022 |* Windows Server 2022 Datacenter Edition 64 bit Chinese<br><br>* Windows Server 2022 Datacenter Edition 64 bit English |
||Windows Server 2019 |* Windows Server 2019 Datacenter Edition 64 bit Chinese<br><br>* Windows Server 2019 Datacenter Edition 64 bit English |
||Windows Server 2016 |* Windows Server 2016 Datacenter Edition 64 bit Chinese<br><br>* Windows Server 2016 Datacenter Edition 64 bit English |
||Windows Server 2012 R2 |* Windows Server 2012 R2 Datacenter Edition 64 bit Chinese<br><br>* Windows Server 2012 R2 Datacenter Edition 64 bit English |


<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Concept |Description |
|---|---|
|Command |A command or script that can be executed on an object, typically for a specific atomic O&M action. For example, "Install software" and "Change password". |
|Execute task |Execute a command on the specified object​. |
|Object |The object selected for command execution in an O&M task (such as an ECS instance). The command then runs on each object. |
|Status |When a task runs, it transitions between different states. |
|Custom parameter |When defining a command, you can define variables with undetermined values as parameters. When creating the task, you need to enter the values of these parameters manually. For example, when running a password change script, you are required to enter the new password manually. |


<span id=".5L2_55So5rWB56iL"></span>
## Procedure


1. Install the cloud assistant Agent: You can install the cloud assistant Agent for objects by selecting the installation option during instance creation, or by using the [cloud assistant Agent installation](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) feature.

2. [Manage commands](https://docs.byteplus.com/en/docs/ecs/Managing-public-command): Before creating O&M tasks, you can check whether preset public commands meet your O&M requirements first. If those public commands fall short of what you expect, you can create custom commands yourself.

3. [Create a job](https://docs.byteplus.com/en/docs/ecs/Creating-a-job): Create and run an O&M task. The cloud assistant then executes O&M commands on the objects specified in the task.​

4. [View the job execution result](https://docs.byteplus.com/en/docs/ecs/View-job-execution-results): After the job starts, you can view the job execution progress and result.
