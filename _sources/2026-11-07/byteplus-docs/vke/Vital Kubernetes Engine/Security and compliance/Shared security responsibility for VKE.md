---
title: "Shared security responsibility for VKE"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Shared_security_responsibility_for_VKE"
---

This topic describes the shared security and compliance responsibility model for the architecture of managed VKE clusters.

Compared with traditional on\-premises data centers, cloud computing separates service operators from customers, offering greater flexibility and control while effectively reducing operational burdens on customers. Therefore, cloud computing security cannot be fully borne by a single party. Cloud security requires joint efforts from BytePlus and you.

<span id="O7Mb2Azy"></span>
## Security responsibility division

<span id="49L30JnH"></span>
### BytePlus responsibilities

On the control plane side, BytePlus leverages comprehensive platform security capabilities to ensure the security of control plane infrastructure, including cloud service resources such as computing, storage, and networking. Meanwhile, based on universal BytePlus security baseline standards (such as operating system security hardening), BytePlus implements standard\-aligned security hardening for VKE cluster control plane component configurations and images. For security vulnerabilities at the node operating system or Kubernetes component level, BytePlus is responsible for promptly issuing relevant announcements and providing corresponding vulnerability patches or version update capabilities.

<span id="1LPAH1Wj"></span>
### Your responsibilities

Your security and operations team is responsible for the security protection of business applications deployed on the cloud, as well as the security configuration and update of cloud resources. Specific responsibilities are as follows:


* Based on BytePlus announcements and the provided patch or version upgrade methods, promptly repair vulnerabilities and update versions of operating systems, cluster system add\-ons, and cluster runtimes. Based on BytePlus announcements and the provided patch or version upgrade methods, promptly repair vulnerabilities and update versions of operating systems, cluster system add\-ons, and cluster runtimes.

* Configure parameters related to VKE clusters, node pools, and networks in accordance with the security principles to prevent attackers from exploiting improper parameter or permission configurations.

* Perform application authorization, account or role authorization, and credential management in accordance with the principle of least privilege.

* Implement and deploy security policies based on usage requirements, and ensure the security of application parameter settings.

* Ensure the supply chain security of artifacts such as container images required for application deployment.

* Ensure the security of application data and applications.

* Delete IAM users or roles associated with resigned employees or untrusted personnel, and revoke the corresponding KubeConfig credentials. For specific operations, see [Managing cluster access credentials](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster#.566h55CG6ZuG576k6K6_6Zeu5Yet6K-B).


<span id="uyMaIhZt"></span>
## Understanding the shared responsibility model

Before designing and deploying enterprise application systems, understand the security responsibility boundaries between you and BytePlus.

The shared cluster security responsibility model for VKE cluster management architecture is shown in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51c129aa8ba6948d18aebb2d29bfe62d.png) </span>

<span id="J6p7cpk0"></span>
## Related documentation

[Shared security responsibility for VCI](https://docs.byteplus.com/en/docs/vke/Shared_security_responsibility_for_VCI)
