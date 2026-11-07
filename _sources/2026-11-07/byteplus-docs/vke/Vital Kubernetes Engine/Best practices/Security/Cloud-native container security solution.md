---
title: "Cloud-native container security solution"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cloud-native-container-security-solution"
---

Cloud computing has penetrated various industries and scenarios. It serves as the foundational infrastructure for enterprises to implement digital transformation and supports diverse types of applications. Meanwhile, cloud\-native security risks associated with containers are continuously amplified, becoming the greatest challenge for enterprises migrating to the cloud.

<span id=".6IOM5pmv6K-05piO"></span>
## Background information

Container technology is the foundation of cloud\-native applications and serves as the standard infrastructure for software development and operations in the cloud\-native era. As cloud\-native adoption increases, security challenges for containers and cloud\-native ecosystems intensify.

<span id=".6ZWc5YOP6L2v5Lu25L6b5bqU6ZO-5a6J5YWo6aOO6Zmp"></span>
### Security risks from image supply chains

Developers typically get source images from internet\-based container registries, and then go through multiple stages in the local environment, including image building, image storage in registries, testing, and deployment to production environments. Each stage may introduce security risks to container images.

Common risks from image supply chains include:


* Security risks inherent to container images. For example, vulnerabilities, insecure configurations, and malicious code injections.

* Untrusted image sources. Many source images come from third\-party organizations or even individuals. These images may be outdated or may have embedded malware.

* Security risks in third\-party add\-ons, such as vulnerabilities in third\-party package dependencies (JAR files).


<span id=".5a655Zmo6L-Q6KGM5pe25a6J5YWo6aOO6Zmp"></span>
### Security risks from container runtimes

Attackers may use various intrusion methods to target running containers, including malware attacks, internal container intrusions, container escape, and high\-risk operations.

Among these, container escape is the most serious issue. It directly affects the underlying infrastructure hosting containers, as well as cluster\-wide security risks and instability. For example, hazardous configurations, mounts, program vulnerabilities, and kernel exploits may all lead to container escape.

<span id=".5a655Zmo5bmz5Y-w546v5aKD5a6J5YWo6aOO6Zmp"></span>
### Security risks in container platform environments

The underlying operating system, container engine, and orchestration system in a container platform environment may have security risks, such as vulnerabilities, improper configurations, and malicious files. Attackers can exploit these platform environment vulnerabilities to easily gain high\-level privileges, posing significant security risks.

Common platform environment risks include multiple security threats. Platform vulnerabilities lead to unauthorized privilege escalation and evasion attacks. Insecure configurations cause account management issues and system intrusions. Mixed container deployments expose high\-security containers to intrusion risks. Unlimited resource usage triggers denial\-of\-service attacks. Improper access policies result in unauthorized access.

<span id=".5a655Zmo572R57uc5bqU55So5a6J5YWo6aOO6Zmp"></span>
### Security risks in container networks

In container environments, complex invocation relationships between microservices lead to increased east\-west network traffic, weak network isolation between containers, lack of application\-layer protection, and insufficient traffic visibility due to rapid changes in encapsulated IP addresses. If a container is compromised, it can be used as a springboard to attack other accessible assets in the container network, which exposes all assets in the network to significant risks.

Traditional security tools, such as vulnerability scanning tools, EDR, security baseline scanners, firewalls, and security management platforms, cannot address the above container security risks. Traditional vulnerability scanners cannot cover container images. EDR is limited to the host level and cannot detect container\-level threats. Security baselines cannot cover container platform environment risks. Firewalls are designed for physical boundaries and cannot support east\-west traffic isolation, address changes, or application\-layer protection. Security management platforms are limited to Ops personnel and do not integrate DevOps processes.

Therefore, it is necessary to deeply study the requirements of container security scenarios. Perform a bottom\-up analysis of the security risks in container scenarios. Develop a container security protection platform to ensure the stable, continuous operation of enterprise workloads on container platforms.

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

The solution effectively implements full\-lifecycle security management for the image supply chain by shifting security efforts from the runtime layer to the CI build phase and integrating security capabilities with the DevOps platform. This seamlessly embeds security capabilities into all stages of cloud\-native application development: building, publishing to repositories, deploying to cluster nodes, and image launching. The lifecycle protection measures are shown in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fc5617707c291497ac1759c8433f0e1.png) </span>

&nbsp;

During the application creation stage, pay attention to source image security, third\-party development toolkit security, and build configuration security. Set effective blocking strategies to prevent risky creation behaviors.

After images are built and pushed to an image repository, it is recommended to perform regular image scanning for vulnerabilities, configuration issues, malicious files, and other risks to prevent images in the repository from being tampered with or replaced by malicious copies. For deploying images from the repository to the production environment, security checkpoints must be configured to prevent risky images from entering the production environment.

In the container runtime stage, effective intrusion prevention and detection capabilities are needed, and alerting or container isolation can be set to mitigate potential threats. Effective network micro\-segmentation strategies should be configured at the network layer, and WAF security capabilities are needed at the application layer. The underlying components of the container platform (including the container engine and Kubernetes orchestration engine) need security hardening.

In container security practices, real\-world scenarios have the following characteristics:


1. Multiple roles. Both development and operations teams use images for development, testing, and deployment. The operations team provides secure system images. The development team packages application code into base images to create container images. If issues arise with images, they must be routed to the responsible team for remediation.

2. Multiple repositories. User environments include multiple repository types, such as base image repositories, test repositories, and production repositories.

3. Secure interaction between development and production environments. Development and production environments belong to separate zones. Consistent access control policies must be applied to ensure security across both environments.


Best practices for ensuring container security from the business perspective are shown in the following figure.


1. The operations team provides base images (golden images) and conducts regular security scans on the repositories that host these base images.

2. When building container images, perform real\-time scans and block security threats found.

3. Fix image vulnerabilities with clear role assignments. The operations department handles base image vulnerabilities, while the development department handles container image vulnerabilities.

4. Upload the images to the test repository and perform another round of scanning.

5. Conduct business validation and runtime security detection in a test environment.

6. After validation in the test environment is complete, synchronize the images to the production repository.

7. Configure image operation policies and implement startup blocking.

8. After containers are running, enforce security policies including runtime protection, network micro\-segmentation, and container application protection capabilities (such as WAF).

9. Perform baseline security testing on container environment configurations.


With the above best practices, container security capabilities effectively align with actual business scenarios, providing tailored cloud\-native security and effectively controlling potential security risks at every stage of DevOps.

<span id=".5qC45b-D6IO95Yqb5bGV56S6"></span>
## Core capabilities

<span id=".6ZWc5YOP5ryP5rSe6aOO6Zmp5YWo5rWB56iL6L-Q6JCl566h5o6n"></span>
### End\-to\-end management and control of image vulnerability risks

The end\-to\-end workflow of managing image vulnerabilities consists of several phases: vulnerability detection, vulnerability analysis, vulnerability remediation, and vulnerability blocking.


* Vulnerability detection scans source images, third\-party development add\-ons, and images in repositories for vulnerabilities.

* Vulnerability analysis involves intelligent analysis and scoring of vulnerability risks, providing remediation priorities.

* The vulnerability remediation phase implements automatic identification of the responsible department for remediation. This enables timely remediation and handling.

* Vulnerability blocking effectively prevents non\-compliant images from entering the production environment.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The vulnerability analysis and vulnerability remediation phases are crucial for enhancing the effectiveness and efficiency of image vulnerability remediation efforts.</div>


<span id=".5ryP5rSe5YiG5p6Q"></span>
#### Vulnerability analysis

Intelligent analysis and scoring of vulnerability risks should be performed based on the characteristics of the business environment. The scoring considers both the risk factors of the CVE itself and the environmental risk factors, analyzing the likelihood of vulnerabilities being exploited from a practical perspective.


* The risk factors of the CVE itself include at least vulnerability severity, permission requirements, time of occurrence, attack methods, availability of fixes, and attack complexity.

* Environmental risk factors include at least privileged containers, root permissions, listening ports, threat attacks, and abnormal behaviors. By integrating these factors, a comprehensive risk score is generated to deliver remediation priority recommendations tailored to the actual operational scenario.


Additionally, more dimensions are introduced to identify and display the vulnerability status and impact scope, providing deeper actionable insights for security operations. Innovative methodologies are used to categorize vulnerability statuses into distinct tiers, such as Undisclosed PoC, Disclosed PoC, Exp (exploit), and Weaponized. Among these, Exp and Weaponized statuses require special attention because they indicate mature attack methods that are already beginning to circulate in underground cybercrime ecosystems. The scope of vulnerability impact is visualized by mapping vulnerabilities to associated assets, such as containers, images, software packages, and hosts.

By leveraging technical capabilities like vulnerability risk scoring, status tagging, and associated asset mapping, security teams can rapidly and accurately prioritize remediation efforts and provide clear direction for vulnerability remediation workflows.

<span id=".5ryP5rSe5L-u5aSN"></span>
#### Vulnerability remediation

Vulnerability remediation follows internal workflows of BytePlus. The security team first pre\-labels system images. In the case of processing large\-scale vulnerability scan data, a proprietary image risk stratification technique is applied to rapidly differentiate between vulnerabilities originating from system images and from upper\-layer application packages. This helps quickly allocate remediation responsibility between the operations team and the development team for efficient handling.

<span id=".5pm66IO95YyW5aiB6IOB5qOA5rWL5YWo5qCI6KaG55uW"></span>
### Intelligent threat detection with full\-stack coverage

Threat detection leverages behavioral baseline engines, sensitive behavior engines, and CEP (Complex Event Processing) correlation analysis to accurately identify threats from container security events. It comprehensively covers all types of known and unknown threats.


* Built on an event\-driven mechanism, it collects multi\-dimensional data from inside containers, including network traffic, file operations, process activities, and system calls. This enables real\-time, in\-depth, and comprehensive visibility into container behavior, forming a solid foundation for security detection and analysis.

* It incorporates hundreds of sensitive behavior detection rules refined by security experts through years of research and actual practice. Rules are continuously updated to align with the latest threat intelligence.

* Behavior baselines for images are automatically generated using intelligent data analytics. This analytics leverages the microservices architecture of modern enterprise applications and continuously monitors and analyzes potential behavior risks in containers

* Based on continuous monitoring of behavior risks, data correlation analysis and AI\-driven methods are used to rapidly and accurately detect intrusion threats, which cover more than ten threat scenarios, such as reverse shell, privilege escalation, mining, persistent backdoors, and remote control.

* For compromised containers, multiple flexible response measures, such as alerting and isolation, are provided, along with detailed event forensics and visualization methods. In addition, alerts can be sent to third\-party systems, such as threat intelligence (TI) platforms and security information and event management (SIEM) platforms. All these capabilities help security teams investigate and act quickly.


<span id=".56uL5L2T5YyW5LqR5Y6f55Sf572R57uc6Ziy5oqk6IO95Yqb"></span>
### Comprehensive cloud\-native network protection capabilities

The container security solution supports industry\-leading WAF protection capabilities for container applications and provides threat protection services that integrate alerting and attack interception. It defends against typical web application attacks such as web shells, SQL injection, and remote control.

This security solution offers Kubernetes ecosystem\-based network micro\-segmentation to block abnormal network connections and enhance the security of east\-west traffic. It adopts a unique near\-source design, with network control efficiently compatible with various cloud\-native network solutions such as Calico, Flannel, and VPC\-CNI.

<span id=".5LqR5Y6f55Sf5YyW6YOo572y6L-Q6KGM"></span>
### Cloud\-native deployment and operation

All container security protection components, including the console and agents, run as non\-privileged parallel containers. They allow autonomous setting of resource consumption limits and have minimal intrusion on the container platform. Among these, protection probes are deployed as Kubernetes DaemonSets and support one\-click deployment across multiple nodes.

The entire deployment is lightweight, supports high availability and elastic resource scaling, and features excellent self\-healing capabilities, automatic fault recovery within seconds, and strong fault tolerance.

Fine\-grained access control is supported for container engine interfaces. User clients can manage container platform resources at the fine\-grained command\-line level via container engine interfaces. This enables effective and secure isolation of container resources, ensuring stable operation of the container platform.
