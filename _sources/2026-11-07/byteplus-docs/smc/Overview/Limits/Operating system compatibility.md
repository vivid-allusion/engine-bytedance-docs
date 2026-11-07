---
title: "Operating system compatibility"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Actions_System_Compatibility_Notes"
---

This topic lists information such as the supported operating system versions and system architectures of source servers that can be migrated to the platform.

<span id=".5pyN5Yqh5Zmo6L-B56e7"></span>
## Server migration

Currently, only source servers running the following operating systems are supported for server migration. You can migrate the source server data to ECS instances or ECS instance images of the platform. [Learn more](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task).

<span id=".5pSv5oyB6L-B56e755qE5pON5L2c57O757uf"></span>
### Supported operating systems

For source servers running operating systems in this category, SMC not only supports data migration but also helps install supplementary tools such as the Cloud Monitor plug\-in, Cloud Security Center plug\-in, and reset\-authentication plug\-in. This ensures that the migrated servers can run properly on the platform.


|Operating system |Version |System architecture |
|---|---|---|
|CentOS |CentOS Stream 8/9 |x86 |
||CentOS 6/7/8 ||
|Ubuntu |16/18/20/22/24 ||
|Debian |9/10/11 ||
|Rocky Linux |8/9 ||
|Windows |Windows Server 2008 and later versions ||
|SUSE Linux Enterprise Server |15.x ||
|OpenSUSE |15.x ||
|AlmaLinux |8.x/9.x/10.x ||
|Oracle Linux |6.x/7.x/8.x/9.x ||


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the source server runs the official Linux operating system provided by UCloud, verify whether its system kernel is a UCloud\-customized version. If the kernel is customized by UCloud, you need to replace it with the official kernel of the corresponding operating system (for example, for CentOS, you can switch to the official CentOS kernel). Otherwise, incompatibility between this kernel and the target platform may prevent the migrated Linux instance from being started or stopped normally in the ECS console.</div>


<span id=".5LuF5o-Q5L6b6L-B56e75pyN5Yqh55qE5pON5L2c57O757uf"></span>
### Operating systems with migration\-only support

For source servers running operating systems in this category, SMC can be used to migrate data to the platform, but cannot guarantee that all platform\-provided services are available for use.


|Operating system |Version |System architecture |
|---|---|---|
|Alibaba Cloud Linux |2/3 |x86 |
|TencentOS Server |2.4/2.4 (TK4)/3.1 ||
|Amazon Linux |2/2023 ||
|openEuler |20.03/22.03 ||
|Huawei Cloud EulerOS |2.0 ||


<span id=".5pON5L2c57O757uf6L-B56e7"></span>
## Operating system migration

Currently, only source servers running the operating systems listed below support operating system migration. You can migrate the operating system of the source server to veLinux CentOS compatible edition without reinstalling the operating system. [Learn more](https://docs.byteplus.com/en/docs/smc/Operating-System-Migration-Task).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">veLinux is a self\-developed Linux operating system launched by the platform. It integrates the system\-level technical experience that the platform has accumulated over years when supporting massive services and 100M\-level concurrency. It is not only suitable for workloads across various cloud scenarios but also provides you with long\-term technical support services, as well as security and stability guarantees. <a href="https://docs.byteplus.com/en/docs/ecs/veLinux-image-overview">Learn more</a>.</div>



|<div style="text-align: center"><br><strong>Source server operating system</strong></div><br> ||<div style="text-align: center"><br>Target operating system</div><br> ||
|---|---|---|---|
|<div style="text-align: center"><br><strong>Operating system</strong></div><br> |<div style="text-align: center"><br><strong>System architecture</strong></div><br> |<div style="text-align: center"><br><strong>veLinux 1.0 CentOS Compatible</strong></div><br> |<div style="text-align: center"><br><strong>veLinux 2.0 CentOS Compatible</strong></div><br> |
|<div style="text-align: center"><br>CentOS Stream 8</div><br> |<div style="text-align: center"><br>x86</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |
|<div style="text-align: center"><br>CentOS 7</div><br> ||<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |
