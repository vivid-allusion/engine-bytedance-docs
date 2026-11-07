---
title: "Add-on release notes"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Plug-in_Release_Notes"
---

The O11yAgent collection add\-on serves as the collection add\-on of ECS. This topic mainly describes the release records of the add\-on.

<span id="Cjge4Yoe"></span>
## o11yagentd


|Version number |Release month |Version status |Description |Impact |
|---|---|---|---|---|
|1.2.5 |October 2025 |Maintained |The add\-on is released for the first time in the Chinese mainland on the BytePlus platform. |1. Downloading, decompressing, and installing the package can consume a certain amount of network bandwidth and read and write bandwidth of the disk. Therefore, it is recommended to upgrade the add\-on during off\-peak hours.<br><br>2. If you upgrade the o11yagent add\-on that is already installed, the add\-on will be restarted. |
|1.2.4 |September 2025 |Maintained |When you quickly install the script on ECS instances by using the command line, you can inject environment variables into the o11yagent add\-on by using the `--o11yagent.envs` parameter. ||
|1.2.3 |August 2025 |Maintained |Added a signature to the Windows artifact package to resolve the issue that the security policy identifies executable files as virus files. ||
|1.2.2 |July 2025 |Maintained |* Adapted for the cgroup mounting scenario. The cpu, cpuacct, and cpuset subsystems are mounted to the same directory.<br><br>* Adapted for metaserver hardening mode.<br><br>* Integrated the ECS add\-on installation logic with the Windows system installation script. ||
|1.2.1 |July 2025 |Maintained |* Supported automatic injection of the MY_MEM_LIMIT environment variable during the installation of o11yagent.<br><br>* Supported passing in custom environment variables during the installation of o11yagent. ||
|1.2.0 |May 2025 |Maintained |1. Supported the installation of the `latest` version of the o11yagent add\-on.<br><br>2. Metaserver addresses can be read through local files.<br><br>3. Detected the liveness of o11yagent. ||
|1.1.1 |April 2025 |Maintained |1. The standard output of the managed o11yagent process is redirected to the operational log file of o11yagentd.<br><br>2. The process management configuration files of upstart and sysvinit are optimized to ensure processes start after the network is ready. ||
|1.1.0 |April 2025 |Maintained |The add\-on is compatible with the Windows operating system. ||
|1.0.6 |April 2025 |Maintained |Fixed the issue that the resource quota configurations of o11yagent are lost during the version upgrade. ||
|1.0.5 |March 2025 |EOM |1. The script o11yagentd_ecs.sh of ECS Cloud\-Monitor\-Agent can be replaced with a few clicks.<br><br>2. The SDK version of metrics_core is upgraded to v0.0.43\-beta. ||
|1.0.4 |February 2025 |EOM |1. The installation script is updated:<br><br>   * You can specify a site by using the `--site` parameter.<br><br>   * Supported specifying the region of the o11yagent control plane by using the `--o11yagentd.control_plane_region` parameter.<br><br>   * The logic of clearing local residual files is added.<br><br>2. The `--o11yagentd.credential_region` parameter of the installation script is deprecated. ||
|1.0.3 |February 2025 |EOM |For the Tao physical machine installation scenario, the `--o11yagent.attrs a=b,c=d` parameter can be specified to inject custom environment variables into o11yagent. ||
|1.0.2 |February 2025 |EOM |1. The default resource quota of o11yagent is changed from 1C1G to 4C4G.<br><br>2. The writing addresses of self\-monitoring metrics are built into the installation script in regions where the service is available.<br><br>3. The issue where the installation user is incorrectly identified during ECS public command installation without standard `$USER` and `$HOME` environment variables is fixed. ||
|1.0.1 |January 2025 |EOM |1. The default cgroupv1 root path is optimized in the tiger user installation scenario on physical machines.<br><br>2. The storage database of self\-monitoring metrics is changed from o11yagentd_metrics_ops to o11yagent_metrics_ops. ||
|1.0.0 |January 2025 |EOM |The add\-on is released for the first time. ||


<span id="lQP9tzlS"></span>
## o11yagent_ecs

The o11yagent_ecs add\-on applies to ECS instances, excluding ECS instances of the **heterogeneous computing** type.


|Version number |Release month |Version status |Description |Impacts |
|---|---|---|---|---|
|3.28.2 |November 2025 |Maintained |* Supported second\-level monitoring, which can identify sudden performance fluctuations. This enables you to promptly detect exceptions and quickly locate root causes.<br><br>* Added file handle utilization to monitor instance exceptions that occur when the maximum number of file handles is reached.<br><br>* Added the mount directory to the disk monitoring dimensions to monitor the disk usage of mount directories.<br><br>* Fixed inaccurate CPU utilization collection on high\-spec Windows ECS instances (\> 64 cores).<br><br>* Fixed the issue of occasional missing disk utilization data. |During the upgrade process, downloading, decompressing, and installing the package can consume a certain amount of network bandwidth and read and write bandwidth of the disk. Therefore, it is recommended to upgrade the add\-on during off\-peak hours. |
|3.25.3 |March 2025 |Maintained |* The metrics of the system process are added.<br><br>* The monitoring metrics of vrdma, including Memory Region, Completion Queue, Queue Pair, and Protection Domain are added.<br><br>* Memory swap metrics are added. |During the upgrade process, downloading, decompressing, and installing the package can consume a certain amount of network bandwidth and read and write bandwidth of the disk. Therefore, it is recommended to upgrade the add\-on during off\-peak hours. |
|3.23.0 |January 2025 |Maintained |The add\-on is released for the first time. |None |


<span id="ElSgu2Ub"></span>
## o11yagent_hpc

The o11yagent_hpc add\-on applies to ECS instances of the **heterogeneous computing** type configured with NVIDIA GPUs.


|Version number |Release month |Version status |Description |Impacts |
|---|---|---|---|---|
|3.30.0 |March 2026 |Maintained |* Added the InfiniBand ENI monitoring capability based on the Verbs API. Supported core metrics such as bandwidth, latency, packet loss, and connection status of the InfiniBand ENI. This ensures network stability for high\-performance clusters.<br><br>* Periodically refreshes the basic information cache of monitored ENIs to ensure that the basic information on the monitoring dashboard is always up\-to\-date. This prevents misjudgments due to outdated information.<br><br>* Expanded the reporting scope of GPU completion timeout information to all GPUs of an instance.<br><br>* Added fault tolerance and handling logic for the msg add\-on in abnormal scenarios. This improves the stability of the msg add\-on.<br><br>* Added metadata security hardening to ensure the authenticity and integrity of metadata obtained by the Agent. This improves the accuracy of monitoring data.<br><br>* Fixed the error in local disk identification.<br><br>* Fixed the error in VMP data units. |During the upgrade process, downloading, decompressing, and installing the package can consume a certain amount of network bandwidth and read and write bandwidth of the disk. Therefore, it is recommended to upgrade the add\-on during off\-peak hours. |
|3.29.0 |December 2025 |Maintained |* Supported heterogeneous Windows instances.<br><br>* Fixed the issue of missing xid information in some operating systems to enhance compatibility. |During the upgrade process, downloading, decompressing, and installing the package can consume a certain amount of network bandwidth and read and write bandwidth of the disk. Therefore, it is recommended to upgrade the add\-on during off\-peak hours. |
|3.28.0 |November 2025 |Maintained |* Added the SRAM collection capability.<br><br>* Added the RDMA configuration collection capability.<br><br>* Added GPM and RDMA data collection capabilities at the millisecond level. |During the upgrade process, downloading, decompressing, and installing the package can consume a certain amount of network bandwidth and read and write bandwidth of the disk. Therefore, it is recommended to upgrade the add\-on during off\-peak hours. |
|3.25.0 |April 2025 |Maintained |1. The metrics of the system process are added.<br><br>2. The metrics of vrdma are added.<br><br>3. Add support for Broadcom network cards. |During the upgrade process, downloading, decompressing, and installing the package can consume a certain amount of network bandwidth and read and write bandwidth of the disk. Therefore, it is recommended to upgrade the add\-on during off\-peak hours. |
|3.23.0 |January 2025 |Maintained |The add\-on is released for the first time. |None |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the types of ECS instances, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance type and specification</a>.</div>
