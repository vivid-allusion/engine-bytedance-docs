---
title: "Configuring the IP mode of the LoadBalancer Service"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_the_IP_mode_of_the_LoadBalancer_Service"
---

VKE allows you to configure the IP mode of the LoadBalancer Service by using annotations. In this way, traffic can be directly forwarded within clusters, or all traffic can be forwarded to CLB instances. This topic describes the principles and configuration methods of different IP modes.

<span id="2ubGhX9u"></span>
## Background information

In a VKE cluster, for the Service of the `LoadBalancer` type, the IP mode determines the traffic forwarding path within the cluster (especially in scenarios when internal pods access the Service). The main difference between IP modes is whether the traffic passes through an external CLB instance. The following table describes the details of different modes.


|IP mode |VIP (local routing mode) |Proxy |
|---|---|---|
|Core principle |By default, kube\-proxy in the cluster writes the IP address of the CLB instance associated with the Service into the node forwarding rules. When an internal pod in the cluster accesses the IP address of the Service, kube\-proxy directly intercepts the traffic and forwards traffic within the cluster. In this case, traffic does not pass through the CLB instance. |The kube\-proxy in the cluster does not write the IP address of the CLB instance into node rules. Instead, it uses the ClusterIP of the Service as the entry point for traffic. All traffic from pods to the Service is first sent to the CLB instance, which then forwards the traffic to back\-end pods based on its load balancing policy. |
|Advantages |* Provides shorter traffic paths, which reduce network latency and CLB instance performance overhead.<br><br>* Prevents bandwidth waste caused by internal traffic processing by the CLB instance.<br><br>* Prevents network loops Prevents network loops that would occur when the destination IP address of a packet forwarded by the CLB instance is the IP of the CLB instance itself. packet forwarded by a CLB instance is the source IP address. |* All advanced CLB features are supported, such as TLS offloading, traffic monitoring, protocol transformation, and source IP passthrough (Proxy\-Protocol/TOA).<br><br>* Unifies internal and external network traffic paths, which facilitates log auditing and traffic management. |
|Limitations |In this mode, traffic does not pass through the CLB instance. Therefore, advanced CLB features are unavailable, such as TLS termination, protocol proxying, and Proxy\-Protocol passthrough. |* Provides longer traffic paths, which increase network latency for CLB forwarding.<br><br>* Consumes bandwidth and concurrency quota of the CLB instance, which increases costs. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details, see the <a href="https://kubernetes.io/docs/concepts/services-networking/service/#load-balancer-ip-mode">community documentation</a>.</div>


<span id="B0NlhE1S"></span>
## Prerequisites


* A cluster has been created and meets the following requirements: For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * The cluster Kubernetes version is v1.30 or later. If the cluster version is outdated, upgrade it first. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

   * The cluster uses the VPC\-CNI network model, with IPvlan as the pod network interface and eBPF as the Service forwarding mode. For the method of querying cluster information, see [Cluster basic information](https://docs.byteplus.com/en/docs/vke/Cluster-basics).

* A workload has been created. For more information, see [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments).

* The cloud\-controller\-manager add\-on has been installed and upgraded to v1.43.0 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).


<span id="eCJvWDAV"></span>
## Usage limits

When the IP mode is set to Proxy, the client pod and server pod cannot run on the same node. When the IP mode is set to Proxy, the client pod and the server pod cannot run on the same node. This is because when a request from a client pod is forwarded by the CLB instance to a server pod on the same node, the CLB instance may retain the source IP of the client. Since the source IP of the client exists on that same node, the response packet is sent directly back to the client without passing through the CLB, which results in abnormal traffic and request failures.

<span id="Py9gPauO"></span>
## Procedure


1. Create a YAML file for the Service and specify the IP mode by using an annotation. Here is an example file named `service-demo.yaml` :

   ```YAML
   apiVersion: v1
   kind: Service
   metadata:
     name: service-demo # Service name
     annotations:
       service.beta.kubernetes.io/volcengine-loadbalancer-ip-mode: "Proxy" # Specify the IP mode of the LoadBalancer Service. Valid values: VIP and Proxy.
   spec:
     selector:
       app: nginx
     ports:
     - name: rule
       protocol: TCP
       port: 80
       targetPort: 80
     type: LoadBalancer
   ```
   

   The following table describes the annotations.

   
   |Key |Type |Required |Description |Changeable |
   |---|---|---|---|---|
   |service.beta.kubernetes.io/volcengine\-loadbalancer\-ip\-mode |String |No |The IP mode of the LoadBalancer Service. Valid values:<br><br><br>* **VIP**: (Default) In this mode, kube\-proxy directly redirects traffic destined for the IP address and port of the CLB instance to back\-end pods.<br><br>* **Proxy**: In this mode, kube\-proxy does not redirect traffic. All traffic passes through the CLB instance and is then forwarded to back\-end pods.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <strong>VIP</strong> mode is used by default when an annotation is not configured.</div><br> |No |
   

2. Run the following command to create a Service.

   ```Bash
   kubectl apply -f service-demo.yaml
   ```
   


<span id="5HW6L2d0"></span>
## Validate results

<span id="SJecWzX7"></span>
### Confirming configurations

After the configuration is complete, you can view the details of the Service to check whether the configurations have taken effect through the `status` field. The `status.ipMode` field indicates the IP mode of the Service.

<span id="g0i5qTe1"></span>
### Checking traffic

After the configuration is complete, you can view the CLB monitoring dashboard to check the traffic forwarding status.


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the left navigation bar, click **Instances**. In the instance list on the right side, find the CLB instance created by VKE (typically named `k8s-f040f***`).

3. Click the instance name to go to the instance details page. Click the **Monitoring** tab to view the monitoring information of the instance.

4. Log in to a container in the cluster and then access the CLB address and port number. Note: This container cannot be on the same node as any back\-end pod of the Service.

   1. Run the following command to log in to the container.

   ```Bash
   kubectl exec -it nginx-7c*** -- /bin/sh
   ```
   

   2. Run the following command to access the address and port number of the CLB instance.

   ```Bash
   curl 14.***.***.***:80
   ```
   

   The expected result is as follows: The back\-end service can be accessed as expected through the IP address and port number of the CLB instance.

   ```Bash
   <!DOCTYPE html>
   <html>
   <head>
   <title>Welcome to nginx!</title>
   <style>
   html { color-scheme: light dark; }
   body { width: 35em; margin: 0 auto;
   font-family: Tahoma, Verdana, Arial, sans-serif; }
   </style>
   </head>
   <body>
   <h1>Welcome to nginx!</h1>
   <p>If you see this page, the nginx web server is successfully installed and
   working. Further configuration is required.</p>
   
   <p>For online documentation and support please refer to
   <a href="http://nginx.org/">nginx.org</a>.<br/>
   Commercial support is available at
   <a href="http://nginx.com/">nginx.com</a>.</p>
   
   <p><em>Thank you for using nginx.</em></p>
   </body>
   </html>
   ```
   

5. Wait for a period of time and then view the monitoring data of the CLB instance.

   * If the IP mode is VIP, no data about new connections is displayed in the CLB instance monitoring information. This indicates that the traffic does not pass through the CLB instance.

   * If the IP mode is Proxy, data about new connections is displayed in the CLB instance monitoring information. This indicates that the traffic passes through the CLB instance and is forwarded by the CLB instance as expected.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
