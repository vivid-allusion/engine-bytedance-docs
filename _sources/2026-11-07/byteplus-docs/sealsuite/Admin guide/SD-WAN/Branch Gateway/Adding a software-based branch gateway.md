---
title: "Adding a software-based branch gateway"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-a-branch-gateway-software-version-"
---

Through the configuration of branch gateways, you can enable on\-premises networks to be connected with SealSuite’s public cloud via nearby access points named POP nodes. This helps you integrate the networks of branch offices, the headquarter, the Internet data center and cloud servers into a larger corporate network and optimize network interconnectivity later on. The branch gateway is divided into software\-based and hardware\-based. This article mainly introduces how to add a software\-based branch gateway.

<span id="aacf4509"></span>
# Prerequisite

SealSuite's branch gateway components must be deployed to on\-premises server or virtual machines in each branch office to support the use of software\-based branch gateways. Thus, you need to ensure each of your enterprise's branch offices has one or more servers that run Linux, or other operating systems such as the stable version of CentOS, Debian, and Ubuntu. These servers that host SealSuite's branch gateway components function as branch gateway servers.

<span id="94b4b1ef"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. In the upper right corner of the **Branch Gateway** page, select **Add Branch** \> **Software**.

4. On the **Add Branch Gateway** page, complete the following configuration.

   1. On the **Basic configuration** page, fill in the configuration items and click **Next Step**.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Branch Name** |Enter a custom name for the branch gateway in Chinese and English. |
      |**Branch Gateway Type** |Identify the enterprise organization corresponding to the branch gateway. Optional:<br><br><br>* **Office Branch**: Indicates a gateway associated with a branch of the enterprise.<br><br>* **Headquarter**: Indicates the gateway associated with the enterprise headquarters.<br><br>* **Data Center**: Indicates the gateway associated with the Internet Data Center (IDC) machine room.<br><br>* **Public Cloud**: Indicates a gateway associated with a public cloud service provider.<br><br>* **Other**: This is a general option used to identify other types of corporate institutions or network locations. |
      |**Source Network Address Translation (SNAT)**  |SNAT is used to hide internal network addresses and resolve private network address conflicts.<br><br><br>* \*\*Enabled: \*\*When the branch network segment of the current branch gateway conflicts with other branch network segments, you need to select **Enabled**. When SNAT is enabled, SealSuite automatically generates branch network segments for branch gateways to communicate with the SealSuite public cloud.<br><br>* **Disabled:**  When SNAT is disabled, you need to manually set the branch segment for the branch gateway. After setup, SealSuite automatically sends the branch network segment corresponding to the branch gateway to each access point or the POP node (POP node), enabling network communication between the branch gateway and the SealSuite public cloud. |
      |**DNS Proxy** |DNS proxy is a network service used to proxy client DNS query requests:<br><br><br>* **Enable**: After enabling, if the intranet PC points the DNS server address to the LAN port of the branch gateway, the branch gateway will use the primary and backup DNS servers configured here for DNS proxy resolution.<br><br>* **Disable**: The DNS proxy function will be disabled, and the intranet PC cannot point the DNS server address to the LAN of the branch gateway. |
      |**High Availability** |Enabling high availability increases system redundancy and reliability. If one node fails or interrupts, another node can take over the work to ensure the continuity and availability of the branches:<br><br><br>* **Enable**: After enabling high availability, this branch will automatically generate two branch nodes, and floating IPs can be used between the two CPE nodes to achieve high availability. Currently, only AWS is supported.<br><br>* **Disable**: Disabling high availability means that the system does not automatically generate additional branch nodes and does not support floating IP for high availability. In this case, if a node fails, it may cause the branch to be interrupted or unavailable. |
      

   2. On the **Deploy** page, complete the installation of SealSuite's branch gateway component on your Linux server by using the provided steps and commands on the webpage. After you complete the installation process, click **Next Step**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to enable high availability, then during the deployment and installation process, you need to complete the deployment and installation steps for two nodes separately.      </div>
      

   3. On the **Connectivity Test** page, complete a connectivity test by using the provided prompts on the webpage. After ensuring the Internet connections between SealSuite's public cloud and the server that hosts SealSuite's branch gateway component function properly, click **Finish**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to enable high availability, then when conducting connectivity testing, you need to ensure that both nodes pass the connectivity test in order to complete the addition of the branch gateway.      </div>
      

<span id="c5e8b346"></span>
# Related information


* After you deploy branch gateways for your enterprise's offices in different locations and ensure these branch gateways are operational, the networks of branch offices are automatically connected to nearby POP nodes, facilitating the setup of an integrated corporate network. After that, you can choose to enable the **Remote Working** capability under the networking module, allowing users to access the corporate network through the SealSuite client or Web browsers. For more information, please refer to [Enabling remote working on the cloud](https://docs.byteplus.com/docs/sealsuite/docs-enabling-telecommuting-on-the-cloud).

* In the regular server operation and maintenance processes, it is suggested to manage software\-based branch gateways through the Admin Console by using the procedures provided in the following topics:

   * [Configuring branch gateway routing.](https://docs.byteplus.com/docs/sealsuite/docs-configuring-branch-gateway-routing)

   * [Viewing basic information and performance statistics of a branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-e51gqmg9ny).

   * [Editing or deleting a branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-editing-or-deleting-a-branch-gateway).
