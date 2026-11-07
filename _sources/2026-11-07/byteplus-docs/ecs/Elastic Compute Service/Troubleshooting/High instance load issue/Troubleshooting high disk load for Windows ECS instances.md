---
title: "Troubleshooting high disk load for Windows ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_Solution_for_High-Disk_Load_Issues_on_Windows_System_ECS_Instances"
---

This topic describes how to troubleshoot the issue of a high disk load (usage) in a Windows instance.

> This topic may contain information about third\-party products. Related information is for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5o6S5p-l5bm25a6a5L2N6Zeu6aKY"></span>
### Step 1: Troubleshoot and locate the problem


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. View disk I/O metrics by monitoring.

   1. On the Instances page, click the name of the target instance.

   2. Click the "Monitoring" tab and the "Basic monitoring" tab in sequence, and view monitoring metrics such as disk read/write speed, IOPS, and latency. This helps you check for abnormal fluctuations or sustained high load.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Disk I/O performance is affected by factors such as hardware performance, system configuration, and application operations. Compare historical data to identify abnormal current load.      </div>
      

3. Check disk usage.

   1. Use disk management tools ("This PC" or "Disk Management") to view disk usage.

   2. Check the used and available space for each partition, and whether a large amount of data occupies disk space.

   3. In folders that occupy a large space, search comprehensively for unnecessary or temporary files.

      To handle folders that occupy a large space, follow the guide in [Step 2: Analyze and fix issues](https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_Solution_for_High-Disk_Load_Issues_on_Windows_System_ECS_Instances#.5q2l6aqk5LqM77ya5YiG5p6Q5aSE55CG6Zeu6aKY).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Pay closer attention to the usage of system volume and application data volumes.      </div>
      

4. Analyze processes and applications.

   1. In the search box at the lower left corner of the desktop, enter "Task Manager", and press the Enter key to open Task Manager.

   2. View disk usage: In the "Performance" tab of Task Manager, view the disk read/write speed and queue length.

   3. Click the "Processes" or "Details" tab, find the process that uses the most disk resources based on the sort in the "volumes" column.

   4. For an application occupying a large amount of resources, view its log and configuration file to analyze whether unreasonable disk access exists.

      To handle unreasonable disk access, follow the guide in [Step 2: Analyze and fix issues](https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_Solution_for_High-Disk_Load_Issues_on_Windows_System_ECS_Instances#.5q2l6aqk5LqM77ya5YiG5p6Q5aSE55CG6Zeu6aKY).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Do not arbitrarily end the process of unfamiliar applications. Otherwise, the system or applications may become unstable.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For a suspicious application, we recommend considering uninstalling it or updating it to the latest version.      </div>
      

5. Check system logs.

   1. Press `Win+R` key to open the "Run" dialog box, enter `eventvwr.msc`, and press the "Enter" key to open the Event Viewer.

   2. Expand the "System" and "Application" logs under "Windows Logs", and search for error or warning messages related to disk performance.

      If an exception occurs, follow the guide in [Step 2: Analyze and fix issues](https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_Solution_for_High-Disk_Load_Issues_on_Windows_System_ECS_Instances#.5q2l6aqk5LqM77ya5YiG5p6Q5aSE55CG6Zeu6aKY) for the solution.


<span id=".5q2l6aqk5LqM77ya5YiG5p6Q5aSE55CG6Zeu6aKY"></span>
### Step 2: Analyze and fix issues


|Solution |Procedures/descriptions |Usage notes |
|---|---|---|
|Optimize disk access |* Optimize applications: For an application frequently accessing a disk, consider optimizing its data access pattern to reduce unnecessary disk read and write operations.<br><br>* Use faster storage media: If conditions allow, replace the existing system volume or data volume with an SSD to improve read/write speed.<br><br>* Optimize databases and file systems: For database and file system\-intensive applications, consider optimizing database query statements, indexes, and table structures, as well as the storage layout and access strategies of file systems. |* Optimizing disk access requires custom operations for specific applications.<br><br>* We recommend [creating a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) first before any optimization to back up instance data. This improves your fault tolerance and ensures data security. |
|Clean up disk space |* Delete unused files and logs: Regularly clean up files you no longer need, including system temporary files, Recycle Bin items, and application logs.<br><br>* Uninstall unused applications: For applications that are no longer in use, you can uninstall them and delete their associated files via "Programs and Features" in Control Panel. |When you uninstall or delete unnecessary applications, files, or logs, proceed with caution. Confirm the operation is secure and necessary to avoid accidental uninstallation or deletion. |
|Adjust system configurations |* Optimize virtual memory configurations: In the "Advanced" tab of "System Properties", adjust the size and location of the virtual memory to optimize system performance.<br><br>* Disable unnecessary Windows services: Use the "Services" management tool to disable unnecessary Windows services. This reduces system access requirements for the disk. |* Adjust virtual memory configuration appropriately based on system memory size and application requirements.<br><br>* Before you disable a Windows service, make sure this does not impact the current operation of the system and applications. |
|Upgrade or expand capacity |1. Evaluate whether to upgrade hardware based on the current disk load and system requirements.<br><br>2. Based on the evaluation, select an appropriate hard disk type (such as SSD) for upgrade and capacity expansion. |* Upgrading hardware affects data stored on local volumes. Please back up data in advance to prevent data loss, such as [creating snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) and copying important data to external storage devices like hard disks or USB drives.<br><br>* Upgrading hardware may require downtime. Please plan the downtime and the scope of business impact. |
