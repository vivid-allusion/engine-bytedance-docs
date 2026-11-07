---
title: "veLinux overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/veLinux-image-overview"
---

<span id=".dmVMaW51eOamgui_sA=="></span>
## veLinux overview

veLinux is a self\-developed Linux operating system launched by the platform. It integrates the system\-level technical experience that the platform has accumulated over years when supporting massive services and 100M\-level concurrency.

veLinux is deeply customized and optimized for the platform public cloud environments. This aims to provide you with a stable, high\-performance, secure, and user\-friendly Linux operating system option, as well as a comprehensive full\-lifecycle management solution. You can use the public images of versions veLinux 1.0 and veLinux 2.0 free of charge, and receive long\-term support for the operating system from the platform at no cost.

<span id=".6YCC55So6K-05piO"></span>
## Applicable scenarios

veLinux supports a wide range of cloud workloads across scenarios, with specific optimizations to fit high\-concurrency, high\-I/O, and hybrid deployment scenarios.

<span id=".5LyY5Yq_"></span>
## Advantage


* **Service:**  The platform provides an enterprise\-level server Linux operating system with long\-term service support. Services include updates at least once every four months, 24/7 dedicated customer service, and official support available through tickets and other methods.

* **Security:**  The platform provides security guarantees that include rapid kernel issue fixes and general vulnerability fixes such as those for data security.

* **Stability:**  veLinux has been running stably on more than one million ECS instances that host internal ByteDance services, and its downtime rate is 50% lower than that of community Linux distributions.

* **Performance:**  Through in\-depth integration and optimization with the platform infrastructure, the system continuously improves its runtime performance. This enables common end\-to\-end (E2E) applications to outperform open\-source Linux by over 20%.

* **Ecology:**  veLinux is compatible with CentOS 7, Debian 10, and Debian 12 ecosystems. Most software that can run on CentOS 7, Debian 10, and Debian 12 can run on veLinux without or with minimal modification.

* **Feature:**  The veLinux kernel is customized based on the LTS versions of 5.4 and 5.15 from the kernel community. Effective bug fixes and feature enhancements are applied to modules such as memory management, networking, I/O, and file systems.


<span id=".5a6J5YWo"></span>
## Security


* In collaboration with the security team of the platform, veLinux uses standard vulnerability scanning and security testing tools for security scans.

* The security team assesses CVEs and patches in a timely manner and issues user security alerts and patch updates accordingly.

* The security team regularly updates the system to fix high\-risk and critical CVEs, and updates and releases public images.


<span id=".546v5aKD6K-05piO"></span>
## Environment

<span id=".55So5oi35oCB546v5aKD"></span>
### User\-space environment


* veLinux 1.0 user\-space packages are compatible with the latest Debian 10. That means Debian 10 packages can be directly used in veLinux 1.0.

* veLinux 1.0 CentOS\-compatible edition user\-space software packages remain compatible with the latest CentOS. That means CentOS 7 packages can be used directly in the veLinux 1.0 CentOS\-compatible edition image.

* veLinux 2.0 user\-space packages are compatible with the latest Debian 12. That means Debian 12 packages can be directly used in veLinux 2.0.

* veLinux 2.0 CentOS\-compatible edition user\-space software packages remain compatible with the latest CentOS Stream 9. That means CentOS Stream 9 packages can be used directly in the veLinux 2.0 CentOS\-compatible edition image.


<span id=".5YaF5qC4"></span>
### Kernel

The veLinux kernel is customized based on versions 5.4 and 5.15 of the long\-term support (LTS) kernel from the kernel community. It has bugs fixed and improved performance of kernel modules such as memory, network, I/O, and file systems. New features targeted at cloud applications are introduced. For details, refer to [Feature description of veLinux 1.0 system](https://docs.byteplus.com/en/docs/ecs/Introduction-to-veLinux-features) and [Feature description of veLinux 2.0 system](https://docs.byteplus.com/en/docs/ecs/Introduction-to-veLinux-2-features).

<span id=".55Sf5ZG95ZGo5pyf"></span>
## Lifecycle

The veLinux lifecycle refers to all stages from the initial release of the image for your use to the discontinuation of service. For more details, refer to the [Operating system maintenance cycle](https://docs.byteplus.com/en/docs/ecs/OS-discontinuing-plan).


|Phase |Description |
|---|---|
|Full support phase |During this phase, compatibility support for new instance types and new features are provided. Provided support includes fixes for image bugs and CVE security vulnerabilities. |
|Maintenance and support phase |During this phase, only existing instance types can access the support. Provided support includes fixes for key bugs and for major CVE security vulnerabilities. |
|Extended support phase |Only technical support for issue diagnosis is provided. |


<span id=".5Y-R5biD6K-05piO"></span>
## Release notes

For information about the veLinux images and detailed updates, refer to [Image release notes](https://docs.byteplus.com/en/docs/ecs/Public-image-overview#.dmVMaW51eOmVnOWDjw==).

<span id=".6I635Y-WdmVMaW51eOaTjeS9nOezu-e7nw=="></span>
## veLinux access

You can access and use veLinux operating system with the following methods:


* When you purchase an instance in the ECS console, select a public image and the corresponding version of veLinux.

* For a created ECS instance, you can replace its current operating system with the veLinux operating system.

* The Operating System Migration feature of SMC (Server Migration Center) enables you to seamlessly switch the operating system of an instance from CentOS 7.x or CentOS Stream 8 to veLinux (CentOS\-compatible version). You do not need to replace the operating system (that means no impacts on the system volume data). [Learn more](https://docs.byteplus.com/en/docs/smc/Operating-System-Migration-Task).


<span id=".5oqA5pyv5pSv5oyB"></span>
## Technical support

BytePlus platform provides the following technical support for veLinux:


* Long\-term support that includes security updates and issue fixes. For the veLinux version lifecycle, refer to the [EOL policies for veLinux](https://docs.byteplus.com/en/docs/ecs/OS-discontinuing-plan#.dmVMaW51eCBFT0zorqHliJI=). You can obtain free technical support through the following methods:

   * [GitHub](https://github.com/bytedance)

* The image is updated every four months. Each update covers new features, security updates, fixes for known issues, and other contents.​


<span id=".6LS555So6K-05piO"></span>
## Billing

veLinux images are free of charge. However, when you use a veLinux image to create an ECS instance, you need to pay for other resources, such as vCPUs, memory, storage, and Internet bandwidth. For billing details, refer to the [Billing by instance type](https://docs.byteplus.com/en/docs/ecs/Instance-type-billing).
