---
title: "Enabling Kernel-mode Dump in Windows operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enable_kernel-mode_dump_in_the_Windows_operating_system"
---

While the Kdump service is not available on Windows operating systems, you can still collect key information for fault analysis when Windows crashes by using the Kernel\-mode Dump feature.

<span id="NWb8ZkWl"></span>
## What is Kernel\-mode Dump?

Kernel\-mode Dump is a specific type of memory dump. It is a technique that captures computer memory content, enabling the exact state of in\-memory data at a specific moment to be saved to a file. When a Windows instance encounters issues like blue screens, freezes, or crashes, dump files can be used to trace in\-memory information at the time of the system crash and identify the root cause of the failure. [Learn more](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/kernel-mode-dump-files).

<span id="3PpzW7ML"></span>
## Procedure

This section describes how to enable the Kernel\-mode Dump feature. In the example provided in this section, an instance running the Windows Server 2019 64 bit operating system is used.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Click the "Windows" button, and select "Control Panel".

3. Click the "System and Security" button.

4. Click the "System" button.

5. In the directory tree on the left, select "Advanced system settings".

6. Specify virtual memory and enable the Kernel\-mode Dump feature.

   1. Specify virtual memory.

      1. Select the "Advanced" tab, and click the "Settings" button in the "Performance" section.

      2. Select the "Advanced" tab, and click the "Change" button in the "Virtual memory" section.

      3. Clear "Automatically manage paging file size for all drives", select "Custom size", and then configure "Initial size (MB)" and "Maximum size (MB)" based on your needs.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">We recommend that you configure the size of the virtual memory (that is, the system paging file Pagefile.sys) according to the following rules.         </div>
         

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Initial size (MB): At least 1.5 times the physical memory, but no more than 3 times the physical memory.         </div>
         

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Maximum size (MB): At least twice the physical memory, but no more than 4 times the physical memory.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Make sure that the corresponding disk has enough free space to store the paging file and the subsequently generated dump files.         </div>
         

      4. After you configure the parameters, click the "Set" button to save the configuration, and then click the "OK" button to complete the operation.

   2. Enable the Kernel\-mode Dump feature.

      1. Select the "Advanced" tab, and click the "Settings" button in the "Startup and Recovery" section.

      2. In the "System failure" section, configure the parameters described in the following table.

         
         |Parameter​ |Description |
         |---|---|
         |Automatically restart |Specify whether to automatically restart the instance when a Windows system error occurs. |
         |Write debugging information |Select the type of information that you expect Windows to record in the memory dump file when Windows stops unexpectedly. Value:<br><br><br>* **none**: This dump type records no information in the memory dump file.<br><br>* **Small memory dump**: This dump type records the minimum amount of useful information that may help identify the cause of the unexpected stop of the computer. [Learn more](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/small-memory-dump).<br><br>* **Kernel memory dump**: This dump type records all memory content used by the kernel at the time of a crash. This dump type meets most debugging requirements. [Learn more](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/kernel-memory-dump).<br><br>* **Complete memory dump**: This dump type records all physical memory content used by Windows, including user\-mode data. Take note that the dump file size may be large. [Learn more](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/complete-memory-dump).<br><br>* **Automatic memory dump**: This dump type records the same content as a kernel memory dump, but differs in how it sets the system paging file (Pagefile.sys) size. This is the default dump type. [Learn more](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/automatic-memory-dump).<br><br>* **Active memory dump**: This dump type records information in a way similar to a complete memory dump, but it filters out pages that may be irrelevant to host fault diagnosis. [Learn more](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/active-memory-dump).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If there are no special requirements, we recommend you select <strong>Kernel memory dump.</strong> The information recorded by this method can meet the needs in most operation and maintenance (O&M) scenarios, enabling effective troubleshooting, while the dump file does not occupy excessive disk space.</div><br> |
         |Dump file |Specify the directory and name of the dump file. |
         |Overwrite any existing file |Select whether to overwrite an existing dump file of the same type in the same location on the disk when the system crashes. |
         |Disable automatic deletion of memory dumps when disk space is low |Specify whether to delete existing memory dump files when the system detects that the disk space is insufficient during system runtime. |
         

      3. After you configure the parameters, click the "OK" button.

      4. Click the "Apply" button, and then click the "OK" button to complete the configuration.

7. [Restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to make the configuration take effect.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend that you regularly check the generated memory dump files to ensure that they effectively record recent system crash events. Additionally, clean up old files based on your needs to free up disk space.   </div>
