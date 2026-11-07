---
title: "Instance diagnosis"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Diagnose_instance_health_status"
---

You can use instance diagnosis to check whether an instance is in normal status, troubleshoot, or identify performance metrics that fall short of expectations. Issues that you can diagnose with this feature include instance performance issues, instance login failures, operational behavior audit, security risk detection, and instance device detection.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Check if the instance to be diagnosed has the cloud assistant Agent installed. If not, [install the cloud assistant Agent first](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client). Otherwise, the following issues may occur:


|Issue type/scenario |Impact |
|---|---|
|Instance performance issues |If the cloud assistant is not installed, this may cause some diagnosis items not to be detected. |
|Instance login failure ||
|Operational behavior audit ||
|Security risk detection ||
|Network problem diagnosis ||
|Comprehensive instance diagnosis ||
|Instance device detection |If the cloud assistant is not installed, you can not diagnose the instance device. |


<span id=".5pON5L2c57O757uf"></span>
### Operating systems

If the issue scenario you select requires testing of the internal configurations of the operating system, make sure that the operating system of your instance meets the following version requirement:


|Operating system type |Operating system version |
|---|---|
|CentOS |* CentOS Stream 9 64 bit<br><br>* CentOS Stream 8 64 bit<br><br>* CentOS 7.1 ~ 7.9 64 bit<br><br>* CentOS 6.9 64 bit |
|Ubuntu |* Ubuntu 16.04 64 bit<br><br>* Ubuntu 18.04 64 bit<br><br>* Ubuntu 20.04 64 bit<br><br>* Ubuntu 22.04 64 bit |
|Debian |* Debian 12 64 bit<br><br>* Debian 11 64 bit<br><br>* Debian 10 64 bit<br><br>* Debian 9 64 bit |
|veLinux |* veLinux 1.0 64 bit<br><br>* veLinux 1.0 Quick Boot 64 bit<br><br>* veLinux 1.0 MLPS(Dengbao) 64 bit<br><br>* veLinux 1.0 CentOS Compatible with 5.10 kernel 64 bit<br><br>* veLinux 1.0 CentOS Compatible 64 bit<br><br>* veLinux 1.0 with 5.10 kernel 64 bit |
|Windows Server |* Windows Server 2022<br><br>* Windows Server 2019<br><br>* Windows Server 2016<br><br>* Windows Server 2012 R2 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you diagnose an instance that runs on an operating system not officially supported, you can not have guaranteed effect of your diagnosis.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Issue type/scenario |Times of diagnosis |Diagnosis interval |Number of instances for one diagnosis |
|---|---|---|---|
|Instance performance issues |A maximum of 100 diagnoses is available for one account per day. |The interval between two consecutive diagnoses must exceed 5 minutes. Otherwise, the report from the last diagnosis is returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the target instance is in the <strong>diagnosis analysis</strong>, wait for the diagnosis to complete before you select the instance for a new diagnosis.</div><br> |1 |
|Instance login failure ||||
|Operational behavior audit ||||
|Security risk detection ||||
|Network problem diagnosis ||||
|Comprehensive instance diagnosis ||||
|Instance device detection |Unlimited |There is no limit on the diagnosis interval, but when the target instance is already in **diagnosis analysis**, please wait for the diagnosis to finish before selecting the instance for a new diagnosis. |* GPU device health check: no more than 100<br><br>* High\-performance computing cluster connectivity check: no more than 2000 |


<span id=".5pON5L2c6K-05piO"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Instance Diagnosis", or "Instances & Images \> Instances".

3. In the top navigation bar, select the project and region of the target instance. 

4. Click "Instance Diagnosis". Or, click the target instance name, select the "Diagnosis" tab, and click the "Create instance diagnosis" button. Then, configure the corresponding information based on the instance issue to be diagnosed.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Current issue |Select the issue that you encounter when using the instance. Value:<br><br><br>* **Instance performance issues**: The usage of the CPU, memory, hard disk, and other components of the instance is high.<br><br>* **Instance login failure**: Scenarios where you can not access a running instance remotely or fail to start an instance.<br><br>* **Operational behavior audit**: Audit operations, such as instance fee changes, unexpected changes of the instance status and of the security group configuration for the instance.<br><br>* **Network problem diagnosis**: Detect network performance issues (such as packet loss and rate limit) that affect business stability, availability, and other issues.<br><br>* **Security risk detection**: Detect security risk of the instance.<br><br>* **Instance device detection**: Check the instance GPU, the connectivity of HPC cluster and other devices for exceptions. This feature is mainly used to locate GPU exceptions or performance metrics that fall short of your expectations.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This diagnosis process may affect the businesses that run on the instance and stop your businesses. Before you start the diagnosis, confirm the business status and select an appropriate time. For example, you can diagnose the instance during business idle periods.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before the diagnosis, related packages and dependencies are automatically installed on the instance. If the instance is based on a custom image, you may fail to install required packages and dependencies and thereby fail to detect some diagnostic items.   </div><br>   <br><br>   * **GPU device health check**: Instance\-level diagnosis available for all [GPU Accelerated](https://docs.byteplus.com/en/docs/gpu/GPU-Accelerated-gni3cl) instances. Diagnosis items include devices within one GPU instance (such as driver configuration, GPU card, and network interface configuration), NCCL Test, intra\-machine bandwidth, and other items.<br><br>   * **High\-performance computing cluster connectivity check**: Cluster\-level detection diagnosis available for all [HPC-optimized](https://docs.byteplus.com/en/docs/gpu/High-Performance-Computing-Optimized-hpcpni3h) instances. Diagnosis items include the connectivity of RDMA network interfaces and switches within the cluster and whether the selected instances are within the same HPC cluster.<br><br>* **Comprehensive instance diagnosis:**  Comprehensive detection across all dimensions except for "Instance device detection". Applicable scenarios cover daily O&M when the issue is unclear or when a regular comprehensive check of an instance is required. This feature can be used to detect instances in dimensions such as operating system, network, and disk status, helping you identify potential issues more easily. |Instance performance issues |
   |Investigation date |Specify the start and end dates for the diagnosis.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the current issue is "Instance device detection", you can not specify the investigation date. And the investigation date defaults to the time when you submitted an instance diagnosis request.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the current issue is "Network problem diagnosis", you do not need to specify the investigation date.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can diagnose instances based on the operation logs of the latest 7 days, and the selected range can not exceed 12 hours for all issues other than "Instance device detection" issues. Suppose the current date is March 12, 2024, so you may select a period that falls between March 6, 2024 and the current date and does not exceed 12 hours. Example:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">2024\-03\-06 00:00 \- 2024\-03\-06 12:00</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">2024\-03\-07 00:00 \- 2024\-03\-07 08:00</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">2024\-03\-09 23:00 \- 2024\-03\-10 09:00</div><br> |2024\-03\-06 00:00 \- 2024\-03\-06 12:00 |
   |Instance selected |Select the target instance to be diagnosed.<br><br><br>* **Diagnosis of one instance**: Select one target instance for diagnosis. All current issues support this feature.<br><br>* **Batch diagnosis**: Multiple target instances can be selected for diagnosis at once. Currently, only "Instance device detection" issues support this feature.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the target instance is <strong>undergoing diagnosis analysis</strong>, wait for the diagnosis to complete before you reselect the instance for another diagnosis.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the current issue is "Network problem diagnosis", you do not need to select the instance.</div><br> |\- |
   |Network connectivity diagnosis<br><br> |Specify the source and destination of the business network to diagnose whether the network is connected.<br><br><br>* source: Select the type of source end and the corresponding instance. The type of source end defaults to and currently only supports ECS instances.<br><br>* destination: Select the type of destination end and the corresponding instance. The type of destination end defaults to and currently only supports ECS instances.<br><br>* agreement: Default value is ICMP and does not allow changes.<br><br>* destination port: Default value is 0 and does not allow changes.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You need to complete the settings only when the current issue is "Network problem diagnosis".</div><br> |\- |
   

5. After you complete the configuration, click the "Start diagnosis" button to begin the diagnosis.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The detection time varies depending on the diagnostic item. Please be patient, as it will take no more than 30 minutes.   </div>
   

6. Once the diagnosis is complete, you can view the results.

   * **Recommended repairs**

      If there are exceptions which you are suggested to fix, you can follow the repair suggestion or the [diagnosis item repair suggestions](https://docs.byteplus.com/en/docs/ecs/Diagnosis_summary). Then click the "Re\-diagnosis" button to perform the diagnosis again and confirm whether the exceptions have been resolved.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When the diagnosis item is "Detecting ICMP connectivity of instances under the same VPC", the "Re\-diagnosis" button is grayed out. This means that you can not diagnose the selected instance again.      </div>
      

   * **Diagnosis download**

      Diagnosis includes detailed data from this diagnosis result, such as the actual and expected values of GDR performance and other performance metrics.

      Click the "Diagnosis download" button to download the analysis report of this diagnosis in a txt file format to your local device. The file name is "dr\-$auto\-generated file number$\-detail".

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Currently, you can only download the diagnosis analysis reports for "GPU device health check" in instance device detection, and only reports generated during the last 7 days can be downloaded.      </div>
      

   * **Feedback for diagnosis result**

      You can provide feedback on the diagnosis results to facilitate the platform to provide evaluation, calibration, or technical support for your issues.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can provide feedback repeatedly, and the latest feedback result will prevail.      </div>
      

      * Problem has been solved: If the problem is resolved, click "Problem has been solved". At this point, your feedback has been received. Thank you for your comment.

      * Problem has not been solved: If the problem is not resolved, click "Problem not solved" and [submit a ticket](https://console.byteplus.com/workorder/create) to seek technical support.
