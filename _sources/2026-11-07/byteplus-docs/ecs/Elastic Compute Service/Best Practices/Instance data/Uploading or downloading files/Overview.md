---
title: "Overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview"
---

The methods for transferring files between local computers and ECS instances vary depending on the operating systems. You can refer to this topic and select a suitable file transfer method based on your actual needs, either to upload files from your local computer to an ECS instance or download files from an ECS instance to your local computer.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you need to upload a file to multiple ECS instances at the same time, you can use the operation orchestration feature for batch upload in the ECS console. <a href="https://docs.byteplus.com/en/docs/ecs/Download_files_to_multiple_instances">Learn more</a>.</div>



|Operating system of the local computer |Linux instances |Windows instances |
|---|---|---|
|Windows |[Transferring files from local Windows system to Linux instance (WinSCP)](https://docs.byteplus.com/en/docs/ecs/Using-WinSCP-to-upload-files-from-a-local-Windows-to-a-Linux-instance) |[Transferring files from local Windows system to Windows instance (MSTSC)](https://docs.byteplus.com/en/docs/ecs/Using-MSTSC-to-upload-files-from-a-local-Windows-to-a-Windows-instance) |
||[Transferring files from local Windows system to ECS instance (FTP)](https://docs.byteplus.com/en/docs/ecs/Using-FTP-to-upload-files-to-a-Windows-instance) |[Transferring files from local Windows system to ECS instance (FTP)](https://docs.byteplus.com/en/docs/ecs/Using-FTP-to-upload-files-to-a-Windows-instance) |
|Linux |[Transferring files from local Linux system to Linux instance (SCP)](https://docs.byteplus.com/en/docs/ecs/Using-SCP-to-upload-files-from-a-local-Linux-or-MacOS-to-a-Linux-instance) |[Transferring files from local Linux system to Windows instance (RDP)](https://docs.byteplus.com/en/docs/ecs/Using-RDP-to-upload-files-from-a-local-Linux-to-a-Windows-instance) |
||[Transferring files from local Linux system to ECS instance (FTP)](https://docs.byteplus.com/en/docs/ecs/Using-FTP-to-upload-files-to-a-Linux-instance) |[Transferring files from local Windows system to ECS instance (FTP)](https://docs.byteplus.com/en/docs/ecs/Using-FTP-to-upload-files-to-a-Windows-instance) |
|macOS |[Transferring files from local macOS system to Linux instance (SCP)](https://docs.byteplus.com/en/docs/ecs/Using-SCP-to-upload-files-from-a-local-Linux-or-MacOS-to-a-Linux-instance) |[Transferring files from local macOS system to Windows instance (MRD)](https://docs.byteplus.com/en/docs/ecs/Using-MRD-to-upload-file-from-a-local-MacOS-to-a-Windows-instance) |
|Unix\-like |[Transferring files between Unix/Linux-like systems (SCP/Rsync/Netcat)](https://docs.byteplus.com/en/docs/ecs/Transferring_files_between_UNIX_Linux) |\-\- |
