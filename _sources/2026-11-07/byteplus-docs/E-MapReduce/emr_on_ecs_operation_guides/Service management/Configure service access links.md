---
title: "Configure service access links"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_access_link"
---

This article describes how to access the Web UI of open\-source components in a Volcano Engine E\-MapReduce (EMR) cluster.

<span id="_1-前提条件"></span>
## **prerequisites**


1. The EMR cluster has been created. For details, see [Create clusters (3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_clusters_3180_and_earlier).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The node domain naming conventions may differ between EMR versions, so the "emr\-master\-1\-1" above can be adjusted by referring to EMR <a href="https://docs.byteplus.com/docs/E-MapReduce/ecs_domain_name_rules">Note on node domain name rules</a>.   </div>
   

2. (Optional) Bind a public IP address.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Perform different steps depending on the high availability type of the cluster.   </div>
   

   1. Highly available cluster.

      1. Click **Access link** to go to the **Highly available virtual IP** page.

      2. On the **Bind resource** \> **Public IP** page, bind the public IP address to the cluster's virtual IP.

   2. Non\-highly available cluster.

      1. Switch to the **Node management** page, click the ID link for the Master\-1\-1 node to go to the ECS **Instance page**.

      2. On the **Elastic public IP** page, bind the public IP address to this node.

3. In **Cluster details \> Access link \> Quick configure service port**, add the source address and corresponding port to the allowlist to continue accessing.


<span id="_2-设置安全组访问权限"></span>
## **Configure security group access permissions**

When accessing a component's Web UI for the first time via the access link, you must add access rules for the corresponding port in the security group to securely access it from your local browser.


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the left navigation bar, click **Resource management \> on ECS \> Cluster name \> Cluster details \>Access link** to go to the **Access link**interface.

3. In the upper right corner of the access link interface, click **Configure server port** to quickly configure port access rules.

4. In the CIDR source address input box, enter your local "IP address/subnet mask length" using one of the following three methods:

   1. Single IP address: for example, 192.168.10.10/32

   2. IP address range: for example, 192.168.52.0/24


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When adding security group access rules, follow the principle of least privilege by only opening the corresponding addresses and ports. If you only add the <a href="http://myip.ipip.net/">local address</a>, set the source address to <strong>local address/32</strong>. If the source address is set to <strong>0.0.0.0/0</strong>, this means all users can request the service port, which is extremely risky and is disabled by default.</div>



5. After entering the source address, select the port range you want to enable access for. In the Access rulesPreview area below, check that the settings are correct, then click the **Confirm** button to complete the configuration.


<span id="_3-访问开源组件的-web-ui"></span>
## **Access the Web UI of open\-source components**

After configuring security group access permissions, you can access the Web UI of open\-source components.


1. On the **Cluster details** page, you can access the Web UI of open\-source components in the following two ways:

   * In the **Access link**interface, click the access link for the corresponding service name to access the Web UI page of that component.

   * Click **Service list** to enter the list of all component services in the cluster. Click the corresponding service name to enter the service details page. Click the **Service Link** button in the upper right corner of the page to access the Web UI of the component.

2. When accessing the Web UI of the component, if a message appears indicating that the page is not a secure connection, this is because the network service in the cluster does not use a commercial certificate. Please allow access.

3. Enter the username and password for the corresponding component in the cluster:

   For regular users, enter the user information that has been added in user management. If no user has been added, you can click the **Add user** button to add a user. For details, see [User management](https://docs.byteplus.com/docs/E-MapReduce/ecs_user_management).
