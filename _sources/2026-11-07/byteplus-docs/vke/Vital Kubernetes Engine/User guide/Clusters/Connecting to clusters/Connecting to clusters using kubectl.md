---
title: "Connecting to clusters using kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster"
---

After you create a cluster, you can connect to it to access and manage cluster resources. VKE allows your local computer to access a Kubernetes cluster through kubectl.

<span id="q2sE983j"></span>
## Background

kubectl is the native command\-line tool provided by Kubernetes. It is used to interact with clusters. You can use kubectl to efficiently perform routine cluster O&M tasks in the terminal, such as resource management, application deployment, status checking, and debugging.

Based on your network environment plan, you can choose one of the following two methods to connect to clusters using kubectl:


* Private network access: The client communicates with the API server of clusters via a private IP address. Data traffic is entirely routed within VPCs and is not routed to the Internet. This provides high security and network stability.

* Public network access: The API server of clusters exposes entry points for public traffic. This allows clients to connect to the clusters via the Internet. After connecting to clusters, you also need to perform custom security configuration based on the security measures provided by VKE to ensure secure Internet communication. For details, see [Configuring security groups](https://docs.byteplus.com/en/docs/vke/Security-group-settings).


<span id="6hsunYiH"></span>
## Procedure


1. Download and install the latest version of the kubectl tool from the official Kubernetes website to your on\-premises computer.

   For specific installation guidance, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

2. Log in to the [VKE console](https://console.byteplus.com/vke).  In the top navigation bar, select the region where your business is located.

3. In the left navigation bar, click **Cluster**. Find the target cluster and click its name.

4. On the **Overview** page, click the **Connection** tab to obtain the cluster access credentials.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more operations on cluster access credentials, see the Manage cluster access credentials section in this topic.   </div>
   

   
   <Tabs>
   <Tab zoneid="vPosxtJgxc" title="Private access">
   <TabTitle>Private access</TabTitle>
   
   On the **Private network** tab, click **Generate KubeConfig** to obtain cluster private access credentials. After you use the credentials to connect to the cluster, resources in the same VPC can access the cluster.
   
   
   </Tab>
   <Tab zoneid="E0q6STD5xj" title="Internet">
   <TabTitle>Internet</TabTitle>
   
   1. In the **Cluster API Server configuration** section of the **Overview** tab, check whether **Public access to API Server** is switched on.
   
      Enable Public access to API Server if it is disabled.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you switch on Public access to API Server, VKE automatically creates an elastic IP address (EIP) of the BGP (Multipath) type and associates it with a Cloud Load Balancer (CLB) instance. You will be charged for using EIP. For details, see <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">EIP billing overview</a>.   </div>
      
   
   2. On the **Connection** tab, click the **Public network** tab to obtain cluster public access credentials.
   
   
   </Tab>
   </Tabs>
   

5. Copy the cluster access credentials to the local `$HOME/.kube/config` file generated after you install kubectl.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you do not have the <code>$HOME/.kube/config</code> file, create a file and copy the access credentials into it.   </div>
   

6. Run the following command in kubectl to check the status of namespaces in the cluster and verify that the connection is successful.

   ```Bash
   kubectl get namespace
   ```
   

   If output similar to the following is returned, kubectl has connected to the cluster successfully.

   ```Bash
   NAME              STATUS   AGE
   default           Active   17h
   kube-node-lease   Active   17h
   kube-public       Active   17h
   kube-system       Active   17h
   ```
   


<span id="P1CI9Cnk"></span>
## Subsequent operations


* After obtaining cluster access credentials, review the security group settings provided by VKE to help secure cluster access. For details, see [Configuring security groups](https://docs.byteplus.com/en/docs/vke/Security-group-settings).

* For subsequent management operations related to access credentials, see [Managing access credentials](https://docs.volcengine.com/docs/6460/2301425).
