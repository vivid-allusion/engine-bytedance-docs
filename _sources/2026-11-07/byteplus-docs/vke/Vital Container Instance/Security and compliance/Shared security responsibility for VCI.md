---
title: "Shared security responsibility for VCI"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Shared_security_responsibility_for_VCI"
---

This topic introduces the shared security responsibility model for VCI.

Compared with traditional on\-premises data centers, cloud computing separates service operators from customers, offering greater flexibility and control while effectively reducing operational burdens on customers. Therefore, cloud computing security cannot be fully borne by a single party. Cloud security requires joint efforts from BytePlus and you.

<span id="dpfbsKfl"></span>
## Security responsibility division

<span id="EOANvK6b"></span>
### **BytePlus security responsibilities**

BytePlus VCI maintains the security and reliability of the Serverless platform. Its core responsibilities include:


* Ensuring platform infrastructure security

* Providing secure data storage and processing services

* Protecting customer data confidentiality


BytePlus ensures compliance of its infrastructure, management, and security practices. This protects your applications from attacks and safeguards your data's privacy and integrity.

&nbsp;

<span id="pEHMVvfQ"></span>
### **Your ** security **responsibilities**

You, as a customer of BytePlus, are responsible for the security of your Serverless applications throughout the entire lifecycle. This involves a wide range of factors, such as application and data security, access control, code development audits, authentication and authorization rule configuration, and permission assignment only to authorized individuals or teams. The core responsibilities are as follows:


* Responsibility for self\-introduced security risks: You are fully responsible for application failures and security issues caused by operations such as deploying Pods with security vulnerabilities or configuring over\-privileged authorization policies.

* Responsibility for risks from actively applied container privileges: BytePlus disables privileged features such as Capabilities by default, as they may affect container stability and security. If you enable these privileges by actively applying for them, you are responsible for stability issues and container security risks (such as lateral attacks on other Pods within the cluster) caused by improper privilege configurations.


<span id="kK10UuEI"></span>
### **Security responsibility for** jointly managed resources

One\-party management models like full hosting cannot be applied to some BytePlus resources (such as pod security groups) due to customer requirements for autonomous management and refined control. Therefore, the following principles for defining mutual security responsibilities are established:


* The party introducing risks shall bear responsibility. You are solely responsible for failures and losses caused by autonomous operations, such as creating pods with security vulnerabilities or using malicious images. BytePlus ensures that VCI pods are free of security risks and do not affect the normal operation of your applications.

* Both parties adhere to the principle of least privilege. You are responsible for security attacks and their consequences caused by situations such as overly broad public network access scope. BytePlus ensures that pod security groups within the VCI scope follow least privilege configuration, will not expand access scope beyond authorized limits, and will prevent container escape.


Cloud security requires clear responsibility boundaries between you and BytePlus, as well as close cooperation between both parties: BytePlus is responsible for cloud infrastructure security and compliance assurance, while you are responsible for the security of your own applications and data. For areas with overlapping responsibilities, BytePlus will take the initiative to prevent and control risks, eliminate risk blind spots, and provide more secure Serverless services.

<span id="rv2muV7m"></span>
## Understanding the shared responsibility model

Before designing and deploying enterprise application systems, understand the security responsibility boundaries between you and BytePlus. For VCI, BytePlus manages the infrastructure and also ensures the security of pod runtime environments and related runtime components. The figure below shows the responsibility boundaries between BytePlus and customers (you) in scenarios of using VCI in a Serverless architecture.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_21c18e1aff74a25ca100f176c616ce7b.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb85ce8ca223f7e31f37d1b5ee8d1f8c.png) </span>

<span id="zDWvYF0A"></span>
### BytePlus **responsibilities**

On the control plane, BytePlus implements security hardening for VCI control plane components based on industry\-wide security standards such as the Kubernetes security baseline. It also builds and provides standardized security system support for typical scenarios of full\-lifecycle security protection for enterprise cloud\-native applications. Specific responsibilities are as follows:


|**Security category** |**Details** |
|---|---|
|Infrastructure security |* Ensure continuous updates of Kubernetes engine versions and timely patching of CVE vulnerabilities.<br><br>* Maintain stability of basic security capabilities, such as Kubernetes control isolation, network isolation (for example, VPC configuration and tunnels between VPCs), and storage isolation. |
|Security of elastic computing resource pools |Adopt lightweight virtual machine isolation technology for container operating systems to implement secure isolation of underlying resources. |
|Security of cluster management and management components |Ensure security for core management capabilities, including cluster authentication and certificate management, in\-cluster Secret management, compliance control of externally exposed ports, VPC isolation, and security group configuration validation. |
|Security of unmanaged add\-ons and application marketplace Charts |Provide standardized core configurations to mitigate basic security issues at the baseline configuration level, ensuring the initial security baseline of unmanaged add\-ons and marketplace Charts. |


<span id="dwE4cs8b"></span>
### **Your responsibilities**

On the data plane, your security operation and maintenance (O&M) team is responsible for the security protection of business applications deployed on the cloud, as well as the secure configuration and dynamic update of cloud resources. You need to fulfill security responsibilities for data plane processes. Specific responsibilities are as follows:


|**Security category** |**Detail** |
|---|---|
|Application security |* Ensure the security of the application artifact supply chain and application runtime.<br><br>* Configure account and role authorization in accordance with the principle of least privilege.<br><br>* Promptly detect and mitigate potential security risks using application\-level prevention and control tools provided by the Cloud Security Center.<br><br>* Strictly restrict container privilege configurations. Avoid actively requesting privileged features unless necessary. |
|O&M security |Ensure security compliance of network configuration, storage configuration, and business observability configuration for your cloud applications, eliminating security vulnerabilities throughout the entire O&M process. |
|Security of business components |Impose strict restrictions on the operational logic of business components, such as Operators and Webhooks, and prevent abnormal component behaviors that affect the secure operation of other applications. |
|Security of unmanaged add\-ons and application marketplace Charts |* Install security patches or version updates recommended in BytePlus announcements in a timely manner.<br><br>* Configure parameters and permissions in strict accordance with security principles to avoid security risks caused by improper configurations or excessive permission assignment. |


<span id="4BTM5ueP"></span>
## Related documentation

[Shared security responsibility for VKE](https://docs.byteplus.com/en/docs/vke/Shared_security_responsibility_for_VKE)
