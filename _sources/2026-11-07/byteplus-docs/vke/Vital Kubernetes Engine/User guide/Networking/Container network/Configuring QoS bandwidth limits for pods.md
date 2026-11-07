---
title: "Configuring QoS bandwidth limits for pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_QoS_bandwidth_limits_for_pods"
---

VKE clusters allow you to use annotations to configure QoS bandwidth limits for a pod, which prevents a high\-traffic pod from slowing down the network transmission of the entire cluster. This topic describes how to configure QoS bandwidth limits for a pod.

<span id="HxC61fuU"></span>
## Background information

In most cases, users deploy various types of workloads in a cluster, including online and offline workloads. Online pods are sensitive to network responses and require low network latency. You can prevent high\-traffic pods (such as those involved in large\-scale data transmission or abnormal requests) from consuming excessive bandwidth, as this can cause network latency and timeouts for other pods. To ensure network priority for core pods (such as payment and transaction pods) and prevent non\-core pods from hogging bandwidth, you can use annotations to limit a single pod's bandwidth during deployment. This prevents network congestion. It also stops individual pods from slowing cross\-node network transmission for the entire cluster, ensuring fair network resource allocation.

In VKE clusters, you can configure bandwidth limits for pods by using standard Kubernetes pod annotations.


|**Annotation** |**Description** |
|---|---|
|kubernetes.io/egress\-bandwidth: 1M |The outbound bandwidth limit for the pod. For example, 1 Mbps. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">VKE clusters currently support outbound bandwidth limits for pods but do not support inbound bandwidth limits.</div>


<span id="EJZ0GjLg"></span>
## Limits


* This feature can be used only in clusters that use the VPC\-CNI network model.

* The vpc\-cni add\-on of v1.7.10 or later has been installed in the cluster. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).


<span id="ceKy1wNM"></span>
## Configuration examples


1. Create the YAML file of the workload. The code of the sample file `deployment-demo.yaml` is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-demo
     namespace: default
   spec: 
     replicas: 1
     selector: 
       matchLabels: 
         app: demo
     template: 
       metadata: 
         labels: 
           app: demo
         annotations:
           kubernetes.io/egress-bandwidth: 1M # Configure the outbound bandwidth limit for the pod. For example, 1M.
       spec:
         containers:
         - name: demo
           image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1
           ports:
           - containerPort: 80
           command: ["sleep", "3600"]  # Keep the pod running for 1 hour for testing.
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl apply -f deployment-demo.yaml
   ```
   

3. Log in to the pod console and run the following command to test the pod bandwidth by using iperf. `-c` indicates that the client mode is used, and `192.168.1.126` indicates the IP address of the iperf server. The sample values in this topic are for reference only.

   ```Bash
   iperf3 -c 192.168.1.126
   ```
   

   The following output is the expected result. The pod outbound bandwidth is limited to 1 Mbps, indicating that the pod QoS bandwidth limit feature has taken effect.

   ```Bash
   Connecting to host 192.168.1.126, port 5201
   [  5] local 192.168.1.131 port 57792 connected to 192.168.1.126 port 5201
   [ ID] Interval           Transfer     Bitrate         Retr  Cwnd
   [  5]   0.00-1.00   sec   226 KBytes  1.85 Mbits/sec    0   29.7 KBytes       
   [  5]   1.00-2.00   sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   [  5]   2.00-3.00   sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   [  5]   3.00-4.00   sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   [  5]   4.00-5.00   sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   [  5]   5.00-6.00   sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   [  5]   6.00-7.00   sec  63.6 KBytes   521 Kbits/sec    0   29.7 KBytes       
   [  5]   7.00-8.00   sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   [  5]   8.00-9.00   sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   [  5]   9.00-10.00  sec   127 KBytes  1.04 Mbits/sec    0   29.7 KBytes       
   - - - - - - - - - - - - - - - - - - - - - - - - -
   [ ID] Interval           Transfer     Bitrate         Retr
   [  5]   0.00-10.00  sec  1.28 MBytes  1.07 Mbits/sec    0             sender
   [  5]   0.00-10.03  sec  1.14 MBytes   956 Kbits/sec                  receiver
   
   iperf Done.
   ```
