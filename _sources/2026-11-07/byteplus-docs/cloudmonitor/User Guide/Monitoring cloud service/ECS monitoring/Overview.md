---
title: "Overview"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1"
---

Cloud Monitor provides multiple monitoring methods for Elastic Compute Service (ECS) instances. The methods include basic monitoring, operating system monitoring, GPU monitoring, Remote Direct Memory Access (RDMA) monitoring, and process monitoring.

<span id=".5Z-656GA55uR5o6n"></span>
## Basic monitoring

Basic monitoring is a physical server\-oriented monitoring capability provided by Cloud Monitor, which monitors the basic metrics (such as CPU, disk, and network) of physical servers that correspond to ECS instances.

<span id=".5pON5L2c57O757uf55uR5o6n"></span>
## Operating system monitoring

By default, Cloud Monitor provides a monitoring add\-on (cloud\-monitor\-agent) to monitor the internal status of ECS instances, which obtains more in\-depth and accurate information about the running status of the instances.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Cloud Monitor provides a next\-generation monitoring add\-on O11yAgent. You can install this add\-on by using the console or command line, or enable the automatic installation of the O11yAgent add\-on for newly purchased ECS instances. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console">Installing the O11yAgent collection add\-on by using the GUI</a> and <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually">Manually installing the O11yAgent collection add\-on</a>.</div>


<span id="mfZjwMMM"></span>
### Use public images

When you purchase and create an ECS instance by using a public image, the system installs the cloud\-monitor\-agent add\-on by default.


* For CentOS systems, only ECS instances with image tags of Centos7 or later are installed with the cloud\-monitor\-agent add\-on by default.

* The existing public images may not be installed with the cloud\-monitor\-agent add\-on. Therefore, if you are not sure whether ECS instances are installed with the cloud\-monitor\-agent add\-on, you can run the following command on the instances to check:



|System |Command |Verifying results |
|---|---|---|
|Linux |```Bash```<br>```systemctl status cloud-monitor-agent```<br> |If information such as the status of the `cloud-monitor-agent` add\-on is returned, it indicates that the instance is installed with the cloud\-monitor\-agent add\-on. Example:<br><br><span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/%E2%80%9Djvk_hymup/ljhwZthlaukjlkulzlp/cloudmonitor_doc/linux-agent.png) </span> |
|Windows |```PowerShell```<br>```sc query "cloud-monitor-agent"```<br> |If information such as the status of the `cloud-monitor-agent` add\-on is returned, it indicates that the instance is installed with the cloud\-monitor\-agent add\-on. Example:<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/%E2%80%9Djvk_hymup/ljhwZthlaukjlkulzlp/cloudmonitor_doc/win-agent.png) </span> |


<span id=".55u45YWz5paH5qGj"></span>
### Use custom images

In addition to the public images provided by the platform, you can also install the cloud\-monitor\-agent add\-on on the target instance of a custom image. You need to pay attention to the following matters:


* **Operating system compatibility**: Due to the variety of operating systems and versions, the cloud\-monitor\-agent add\-on is only compatible with specific operating systems and versions. The cloud\-monitor\-agent add\-on supports the same operating systems and versions as public images. For more details, refer to [Public Image Overview](https://docs.byteplus.com/en/docs/ecs/Public-image-overview).

* **Add\-on installation methods**: For methods of installing the cloud\-monitor\-agent add\-on in custom images, refer to [Installing an add-on](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Full compatibility between the cloud\-monitor\-agent add\-on and custom images cannot be guaranteed. It is recommended to use the public images provided by the platform.   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related document


* For specific operations on viewing basic monitoring metrics, refer to [Basic monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Basic-monitoring).

* If your instance is installed with the cloud\-monitor\-agent add\-on, you can view operating system monitoring information in the Cloud Monitor console. For details, see [Operating system monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-operating-system-monitoring-data).

* If your instance is not installed with the cloud\-monitor\-agent add\-on, you need to install the add\-on to monitor the operating system.

   1. [Installing the add-on](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console)

   2. [Operating system monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-operating-system-monitoring-data)

* For ECS monitoring metrics, refer to [Supported cloud services](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).
