---
title: "Troubleshooting and solutions for high memory usage in ECS instances running on Windows systems"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_Solution_for_High_Memory_Usage_in_ECS_Instances_with_Windows_System"
---

This topic describes how to use the Resource Monitor officially provided by Microsoft to troubleshoot the issue of high memory usage in a Windows instance.

In the example provided in this topic, Windows Server 2012 R2 is used. Take note that procedures may vary across different operating systems. For more information, see the instructions for your actual operating system.

> This topic may contain information about third\-party products, which is provided for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

For Windows systems, Resource Monitor can be used to monitor memory and view memory usage.


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Enter the Resource Monitor.

   1. In the lower\-left corner of the desktop, click the "Start" icon.

   2. Select the "Task Manager" card.

   3. On the Task Manager page, select the "Performance" tab, and click the "Open Resource Monitor" button.

3. View memory usage.

   On the Resource Monitor page, click the "Memory" tab. In the "Commit (KB)" column, check each process's memory size to find processes using excessive resources.



&nbsp;

4. End the process that consumes excessive resources.

   1. For the process that consumes excessive resources (memory), we recommend that you right\-click it and select "End Process".

   2. After you confirm the information about the process to be finished, click the "End Process" button to complete the operation.
