---
title: "How do I resolve the \"conntrack full\" error?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-resolve-the-conntrack-full-error"
---

<span id="2GJ7oQUb"></span>
## Cause

The `conntrack full` error in kernel logs (queryable via the "dmesg" command) indicates the Linux connection tracking (Conntrack) table has reached the limit defined by `conntrack_max`. You need to increase the Conntrack entry limit.

<span id="KGNlMZ9k"></span>
## Solution


1. Log in to the target node where the error occurred. For detailed instructions, see [ECS Terminal](https://docs.volcengine.com/docs/6460/100953?lang=zh#ecs-terminal).

2. Run the following commands to check the entry count and resource usage of each protocol in the Conntrack.

   ```Bash
   # View table details. You can filter output with the grep pipeline to check status, or run "cat /proc/net/nf_conntrack" as an alternative.
   conntrack -L
   
   # View the entry count.
   cat /proc/sys/net/netfilter/nf_conntrack_count
   
   # View the current maximum allowed number of entries in the table.
   cat /proc/sys/net/netfilter/nf_conntrack_max
   ```
   

   * If there are a large number of TCP entries, identify the corresponding applications and their network protocols. For applications using short\-lived connections, we recommend refactoring them to use persistent connections.

   * If there are a large number of DNS entries, we recommend using NodeLocal DNSCache in your VKE cluster to improve DNS performance and reduce Conntrack usage. For detailed instructions, see [Using NodeLocal DNSCache as a DNS caching agent](https://docs.volcengine.com/docs/6460/1158255).

   * If the actual Conntrack usage is reasonable, or you do not want to modify the workloads, you can adjust the Conntrack entry limit by configuring the `maxPerCore` parameter for kube\-proxy. To do so, follow the steps below:

      1. Log in to the [VKE console](https://console.byteplus.com/vke). 

      2. In the left navigation bar, click **Cluster**.

      3. In the cluster list, click the name of the target cluster.

      4. In the left navigation pane of the cluster management page, click **Configurations** \> **ConfigMap**.

      5. On the **ConfigMap** page, find the **kube\-proxy** ConfigMap and click its name to enter the **ConfigMaps details page**.

      6. In the upper\-right corner of the **ConfigMaps details page**, click `...` \> **Edit Yaml**.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_50eb9d6276181744f602145d94771864.png) </span>

      7. Add the `maxPerCore` parameter to the YAML file and save the change.

         ```YAML
         apiVersion: v1
         data:
           config.conf: |-
             apiVersion: kubeproxy.config.k8s.io/v1alpha1
             bindAddress: 0.0.0.0
             bindAddressHardFail: false
             clientConnection:
               acceptContentTypes: ""
               burst: 10
               contentType: application/vnd.kubernetes.protobuf
               kubeconfig: /var/lib/kube-proxy/kubeconfig.conf
               qps: 5
             clusterCIDR: 172.30.112.0/21
             configSyncPeriod: 15m0s
             conntrack:
               maxPerCore: 32768 # The default value is 32768. You can adjust it as needed.
               min: 131072
               tcpCloseWaitTimeout: 1h0m0s
               tcpEstablishedTimeout: 24h0m0s
             detectLocalMode: ""
             enableProfiling: false
             healthzBindAddress: 0.0.0.0:10256
             hostnameOverride: ""
             ......
         ```
