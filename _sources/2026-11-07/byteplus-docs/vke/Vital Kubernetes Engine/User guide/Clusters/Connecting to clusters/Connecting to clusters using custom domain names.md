---
title: "Connecting to clusters using custom domain names"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Connecting_to_clusters_using_custom_domain_names"
---

This topic describes how to add a Subject Alternative Name (SAN) to the kube\-apiserver certificate of a VKE cluster to connect to the cluster by using a custom domain name.

<span id="l3I4U55U"></span>
## Application scenarios

SAN is an extension of the X.509 certificate. It allows multiple values, such as IP addresses and domain names, to be associated with the same certificate. During the TLS handshake, the client validates the legitimacy of the server certificate, including checking whether the SAN field of the certificate matches the address accessed by the client.

In VKE, when the client cannot directly use the default address of the kube\-apiserver (private network IP or EIP) because of network limitations, you can add a custom SAN to the kube\-apiserver certificate of a cluster. This adds the proxy IP or domain name accessible to the client to the certificate. In this way, even when accessing through an intermediate address, clients such as kubectl can still complete server certificate verification and establish a secure mutual TLS connection.

Typical application scenarios include:


* **DNAT proxy access**: Clients access kube\-apiserver through a Destination Network Address Translation (DNAT) device, and the actual accessed IP is different from the kube\-apiserver IP.

* **Cross\-cloud or on\-premises data center connection**: Clients located in other cloud providers or on\-premises data centers (IDC) need to connect to a VKE cluster via a specific domain name or fixed IP.

* **Unified domain access**: Configure a unified domain for kube\-apiserver across multiple clusters and manage access entries via DNS resolution. This prevents frequent client configuration changes due to IP changes.


<span id="hNQkrUpL"></span>
## Prerequisites

Before performing an operation, make sure that the following conditions are met:


* **Custom domain name**: You have prepared a custom domain to be used and configured DNS resolution to point the domain to an IP address that is accessible to the client and can route to kube\-apiserver (such as the proxy IP or load balancer IP). You need to perform this step by yourself.

* **Network reachability**: The client must be able to access the custom IP or domain to be added as a SAN over the network, and the IP or domain must ultimately route to the kube\-apiserver of the cluster.

* **Operation permissions**: Make sure that you have the necessary permissions to modify VKE cluster configurations. For detailed operations, see [Granting RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions).


<span id="98aXaU3i"></span>
## Procedure

<span id="0a08vUZY"></span>
### Step 1: Add a custom SAN


<Tabs>
<Tab zoneid="HNtCb7Mrh9" title="Use the console">
<TabTitle>Use the console</TabTitle>

You can add a custom SAN for a new or existing cluster in the VKE console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying custom SANs will trigger a brief restart of the kube\-apiserver add\-on to load the new certificate. This typically lasts a few minutes. To prevent your business from being affected, we recommend performing this operation during off\-peak hours. During the kube\-apiserver restart, cluster management operations may be briefly interrupted.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to go to its management page.

3. On the **Overview** tab of the **Overview** page for the cluster, find the **SAN domain name** parameter, and click the edit icon next to the parameter.

4. In the pop\-up dialog, enter or paste the custom IP addresses, domain names, or URIs that meet the requirements. Separate multiple entries with Chinese or English commas, line breaks, or spaces.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Up to six SANs are supported.   </div>
   

5. Click **Confirm** to save the changes.


</Tab>
<Tab zoneid="e1U5geHyZ0" title="Use the API">
<TabTitle>Use the API</TabTitle>

You can also configure a custom SAN by specifying the `CustomSans` field when you call the [CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster) API to create a cluster or the [UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) API to update a cluster.


</Tab>
</Tabs>


<span id="iRMwaHJl"></span>
### Step 2: Use the SAN to connect to the cluster

After the custom SAN is added and the kube\-apiserver is restarted, you can use kubectl to connect to the cluster by using the custom domain name.


1. Connect to the target cluster using kubectl. For details, see [Connecting to clusters using kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Copy the **private network** access credentials of the cluster and save them as a local `kubeconfig` file.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For the method of obtaining the private network access credentials of a cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Managing_access_credentials">Managing access credentials</a>.   </div>
   

   ```Bash
   echo 'Paste_your_copied_private_network_kubeconfig_here' > ~/cluster-private.kubeconfig
   export KUBECONFIG=~/cluster-private.kubeconfig
   ```
   

3. Run the following command to replace the `server` address in the private network access credentials with your custom domain name.

   ```Bash
   sed -i 's#${old-server-address}#https://${your-custom-domain}:6443#g' ~/cluster-private.kubeconfig
   ## Replace ${old-server-address} with the original value of the server parameter of the cluster private network access credentials.
   ## Replace ${your-custom-domain} with your custom domain name.
   ## The complete example is as follows:
   ## sed -i 's#https://192.168.214.185:6443#https://xxx.example.com:6443#g' ~/cluster-private.kubeconfig
   ```
   

4. Run the following command to check whether you can connect to the cluster after the replacement.

   ```Bash
   kubectl cluster-info
   ```
   

   The expected output is as follows. If it includes the custom SAN address you configured, the configuration is successful.

   ```Plain Text
   Kubernetes control plane is running at https://${your-custom-domain}:6443
   CoreDNS is running at https://${your-custom-domain}:6443/api/v1/namespaces/kube-system/services/coredns:dns/proxy
   ...
   ```
   


<span id="qVRFKoJw"></span>
## Subsequent operations

To ensure secure cluster access, learn about the security group settings provided by VKE. For details, see [Configuring security groups](https://docs.byteplus.com/en/docs/vke/Security-group-settings).
