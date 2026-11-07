---
title: "How do I determine if a node-local-dns add-on is used?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-confirm-that-the-node-local-dns-add-on-is-used"
---

<span id=".6IOM5pmv5LuL57uN"></span>
## Background

The node\-local\-dns functions as a NodeLocal DNSCache add\-on for clusters. This add\-on runs in a DaemonSet on each node in the cluster, working as a DNS cache proxy on nodes to improve the performance and stability of DNS service discovery in the cluster.

DNS cache configuration is injected into pods as soon as the node\-local\-dns add\-on is deployed in the cluster. In this case, the pods have two DNS configurations for round\-robin DNS resolution.


1. **NodeLocal DNSCache configuration**: The Pod first accesses the DNS cache configuration (169.254.20.10) of the current node. If the configuration is inaccessible, the Pod then accesses the CoreDNS configuration of the cluster.

2. **CoreDNS configuration**: The global DNS configuration of the cluster.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_057f78865efe9f05fc37922465a52ea5.png) </span>


<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

After you deploy the node\-local\-dns add\-on, check whether the Pods use the local cache of the nodes.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

You can log in to the Pods in the cluster and use the `dig` command to view the DNS resolution result. When the DNS server is shown as `169.254.20.10`, it indicates that the current Pod is using the node\-local\-dns cache of the node where it is located.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a3be73fc212fcdc7ef3ddf76b54d7a62.png) </span>
