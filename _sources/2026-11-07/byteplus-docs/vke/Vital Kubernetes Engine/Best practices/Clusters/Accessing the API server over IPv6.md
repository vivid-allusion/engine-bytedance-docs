---
title: "Accessing the API server over IPv6"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Accessing-an-API-server-over-IPv6"
---

VKE continuously enhances IPv6 capabilities, which allow you to access the API server over public or private IPv6 networks. This topic describes how to access the API server over IPv6.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features">Beta \- apply for trial</a>]: The IPv6\-related features of VKE are currently in beta. If you want to use these features, submit an application.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

With the development of the Internet, IPv4 addresses have gradually become exhausted. As the next\-generation Internet protocol, IPv6 offers a larger address space and enhanced security. The transition to a dual\-stack network is the best option to meet user demand for IPv6.

VKE fully supports IPv6 dual\-stack capabilities, which enable you to create IPv4/IPv6 dual\-stack clusters, access the API server by using public or private IPv6 networks, and access servers by using public IPv6 networks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An IPv4/IPv6 dual\-stack cluster has been created. For details, see [Creating IPv4/IPv6 clusters with VKE](https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE).

* You have downloaded and installed the latest version of kubectl from the official Kubernetes website on your local computer. For detailed installation instructions, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

To access the API server by using the public IPv6 network, take note of the following items:


* Currently, you cannot assign public bandwidth to IPv6 addresses through VKE. If needed, you can perform this operation in the CLB console.

* Do not delete the EIP, load balancer, or other resources associated with the API server. If you delete these resources, the API server will become inaccessible, and the deleted resources cannot be restored.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77yI5Y-v6YCJ77yJ77ya5byA6YCa5YWs572RLWlwdjYt5bim5a69"></span>
### Step 1 (optional): Enable IPv6 Internet bandwidth

To access the API server by using the public IPv6 network, perform the following steps to enable public IPv6 bandwidth. To access the API server by using the private IPv6 network, skip these steps.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster** to go to the cluster list page.

3. Click the name of the target dual\-stack cluster to go to the cluster management page. Click the **Overview** tab.

4. Click **CLB Console** in the IPv6 description of the **Public access to API Server** section. This redirects you to the management page of the IPv6 CLB instance associated with the cluster.

5. Disable **Modification Protection** for the CLB instance, and click  **...**   **\> Public \> Enable public IPv6 bandwidth** in the upper\-right corner. Configure the information about public bandwidth, such as the billing method, line type, and bandwidth limit, based on the on\-screen prompts.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If no IPv6 gateway is created in the VPC used to create the cluster, create an IPv6 gateway based on <a href="https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance">Creating IPv6 Gateway instances</a>.</div>


* <div data-tips="true" data-tips-type="tip">For more details about IPv6 Internet bandwidth, see <a href="https://docs.byteplus.com/en/docs/clb/Activating-or-Deleting-IPv6-Internet-bandwidth">Managing IPv6 Internet bandwidth</a>.</div>


6. Enable **Modification Protection** for the CLB instance again.


<span id=".5q2l6aqk5LqM77ya6I635Y-WLWlwdjYt57G75Z6L55qELWt1YmVjb25maWc="></span>
### Step 2: Obtain the IPv6\-based kubeconfig file

Unlike an IPv4 API server, an IPv6 API server uses the same IP address for both public and private access. Whether the IPv6 API server can be accessed over the public network depends on whether public bandwidth has been bound to its IPv6 address.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster** to go to the cluster list page.

3. Click the name of the target dual\-stack cluster to go to the cluster management page.

4. Click the **Connection** tab on the cluster management page to obtain the kubeconfig file configured for IPv6\-based access.


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

Copy your obtained IPv6 kubeconfig content to the `$HOME/.kube/config` file (default kubectl configuration path) on your computer. Then run the `kubectl get namespace` command in your kubectl client.

If the namespace information in the cluster is returned as expected, it indicates that the API server can be accessed over IPv6. The sample response is as follows:

```Bash
NAME              STATUS   AGE
default           Active   17h
kube-node-lease   Active   17h
kube-public       Active   17h
kube-system       Active   17h
```
