---
title: "Creating CLB Ingresses through kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-CLB-Ingress-using-kubectl"
---

By configuring specific annotations in the Ingress YAML files, you can achieve more comprehensive Layer 7 LoadBalancer capabilities and more diverse service routing rules.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Read <a href="https://docs.byteplus.com/en/docs/vke/Precautions_for_using_CLB_Ingress">CLB Ingress considerations</a> carefully before getting started.</div>


* <div data-tips="true" data-tips-type="warning">ALB Ingresses offer richer features and greater reliability. To ensure the security and stability of your business, we recommend ALB Ingresses for business deployments in clusters. For details, see <a href="https://docs.byteplus.com/en/docs/vke/ALB-Ingress">ALB Ingress</a>.</div>


* <div data-tips="true" data-tips-type="warning">The annotations in YAML files are case\-sensitive.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The clusters have been created. For details, see[ Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The kubectl tool is installed on your computer. For details, please see [Installation and settings of kubectl](https://kubernetes.io/docs/tasks/tools/).

* The target cluster has been connected through kubectl. For details, please see [Connect to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/vke/NodePort).


<span id=".5Yib5bu6LWNsYi1pbmdyZXNz"></span>
## Creating CLB Ingresses

<span id=".5a-55o6l5bey5pyJLWNsYi3lrp7kvos="></span>
### Binding to existing CLB instances 

The LoadBalancer (CLB) instances mentioned below refer to those manually created on the console. For detailed instructions, see [Creating LoadBalancer instances](https://docs.byteplus.com/en/docs/clb/CLB-instances-01).

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Do not bind to CLB instances already used by API servers (either API servers of the current cluster or from another cluster). Otherwise, cluster failures may occur.</div>


```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-id: "clb-rrxpqzg37eo0v0x58******"
  name: clb-ingress
  namespace: default
spec:
  ingressClassName: clb
  rules:
  - host: example.com
    http:
      paths:
      - backend:
          service:
            name: service-demo-a
            port:
              number: 80
        path: /foo
        pathType: Prefix
      - backend:
          service:
            name: service-demo
            port:
              number: 80
        path: /bar
        pathType: Prefix
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-id |String |Yes |Specify an existing CLB instance ID. |No |No |


<span id=".5paw5bu6LWNsYi3lrp7kvos="></span>
### Creating CLB instances

Use the following YAML configuration to create an Ingress and create a new CLB instance.

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-name: "clb-demo"
    ingress.vke.volcengine.com/loadbalancer-spec: "small_1"
    ingress.vke.volcengine.com/loadbalancer-subnet-id: "subnet-rrhvmyikek1sv0x58***"
    ingress.vke.volcengine.com/loadbalancer-address-type: "public" 
    ingress.vke.volcengine.com/loadbalancer-isp-type: "BGP"
    ingress.vke.volcengine.com/loadbalancer-bandwidth:  "10" 
    ingress.vke.volcengine.com/loadbalancer-eip-BandwidthPackageId: "bwp-2d63yyj3ki4u858oz***"
  name: clb-ingress
  namespace: default
spec:
  ingressClassName: clb
  rules:
  - host: example.com 
    http:
      paths:
      - backend:
          service:
            name: service-demo-a
            port:
              number: 80
        path: /foo
        pathType: Prefix
      - backend:
          service:
            name: service-demo-b
            port:
              number: 80
        path: /bar
        pathType: Prefix
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-name |String |No |The name of the newly created LoadBalancer instance. If not specified, the system will generate one automatically. |No |No |
|ingress.vke.volcengine.com/loadbalancer\-spec |String |Yes |Specification of the LoadBalancer instance. Available values: small_1, small_2, medium_1, medium_2, large_1, and large_2. For details, see [Product types and specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). |No |No |
|ingress.vke.volcengine.com/loadbalancer\-subnet\-id |String |Yes |Specify the subnet to which the created LoadBalancer instance belongs. |No |No |
|ingress.vke.volcengine.com/loadbalancer\-address\-type |String |No |Specify the type of LoadBalancer instance. Available values:<br><br><br>* **public**: A LoadBalancer instance accessible from the Internet.<br><br>* **private**: A LoadBalancer instance accessible only within private networks. |public |No |
|ingress.vke.volcengine.com/loadbalancer\-isp\-type |String |No |ISP type for EIP of an Internet\-accessible LoadBalancer instance. The available types include BGP, SingleLine_BGP, Static_BGP, Fusion_BGP, ChinaMobile, ChinaTelecom, ChinaUnicom, ChinaMobile_Value, ChinaUnicom_Value, and ChinaTelecom_Value. For details, see [EIP product documentation](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Except for <strong>BGP</strong>, all the ISP types are beta features of EIP products. To apply for these features, contact your account manager.</div><br> |BGP |No |
|ingress.vke.volcengine.com/loadbalancer\-bandwidth |Integer |No |The maximum bandwidth of the EIP of an Internet\-accessible LoadBalancer instance.<br><br><br>* Value: 1–500<br><br>* Unit: Mbps |10 |No |
|ingress.vke.volcengine.com/loadbalancer\-ip\-version |String |No |The IP version of the LoadBalancer instance. Value: ipv4. |IPv4 |No |
|ingress.vke.volcengine.com/loadbalancer\-scheduler |String |No |Scheduling algorithms used by LoadBalancer. Available values:<br><br><br>* **wrr**: Backend servers with higher weight values are polled more frequently (with higher probability).<br><br>* **wlc**: Forward requests to the backend server that has the lowest ratio of **current connections to weight**.<br><br>* **sh**: A hash\-based algorithm that forwards requests from the same IP to a single backend server. |wrr |No |
|ingress.vke.volcengine.com/loadbalancer\-protocol |String |No |The listening protocol of the LoadBalancer instance. Available values:<br><br><br>* **http**: The listening protocol for the LoadBalancer instance is HTTP.<br><br>* **https**: The listening protocol of the LoadBalancer instance is HTTPS. |http |No |
|ingress.vke.volcengine.com/loadbalancer\-port |Integer |No |The listening port of LoadBalancer ranges from 1 to 65535. |* HTTPS protocol: 443<br><br>* HTTP protocol: 80 |No |
|ingress.vke.volcengine.com/loadbalancer\-eip\-BandwidthPackageId |String |No |Specify the shared bandwidth package for the EIP.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A shared bandwidth package is a reusable cloud resource for bandwidth sharing. It aggregates multiple public IPs and IPv6 public bandwidths from the same region into a shared bandwidth pool, reducing public bandwidth costs through bandwidth sharing. For details, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package">What is a shared bandwidth package</a>.</div><br> |No |Yes |


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Execute the following command to view the newly created Ingress.


```bash
kubectl get ingress
```


The information below is expected to be printed on the screen.

```bash
NAME            CLASS   HOSTS         ADDRESS           PORTS   AGE
clb-ingress     clb     example.com   180.xxx.xxx.xxx   80      40s
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>ADDRESS</code> is the Elastic IP Address (EIP) of the CLB for this Ingress. You can use this IP to find the corresponding CLB instance on the <a href="https://console.byteplus.com/clb">LoadBalancer</a> console.</div>



2. Execute the following command to view the detailed information of the specified Ingress.


```bash
kubectl describe ingress clb-ingress
```


The information below is expected to be printed on the screen. The annotations below show the information about the CLB, including CLB ID, listener, and health check. For details, see [Using annotations to configure CLB Ingresses](https://docs.byteplus.com/en/docs/vke/Configuring-a-CLB-Ingress-using-annotations).

```basn
Name:             clb-ingress
Labels:           <none>
Namespace:        default
Address:          180.xxx.xxx.xxx
Default backend:  default-http-backend:80
Rules:
  Host         Path  Backends
  ----         ----  --------
  example.com  
               /   service:80 (192.168.112.4:80,192.168.128.9:80,192.168.48.3:80)
Annotations:   ingress.vke.volcengine.com/loadbalancer-healthcheck-enabled: true
               ingress.vke.volcengine.com/loadbalancer-healthcheck-httpcode: http_2xx,http_3xx
               ingress.vke.volcengine.com/loadbalancer-healthcheck-interval: 3
               ingress.vke.volcengine.com/loadbalancer-healthcheck-method: GET
               ingress.vke.volcengine.com/loadbalancer-healthcheck-path: /
               ingress.vke.volcengine.com/loadbalancer-healthcheck-timeout: 3
               ingress.vke.volcengine.com/loadbalancer-healthy-threshold: 3
               ingress.vke.volcengine.com/loadbalancer-id: clb-5g8puqwem0ao73i******
               ingress.vke.volcengine.com/loadbalancer-port: 80
               ingress.vke.volcengine.com/loadbalancer-protocol: http
               ingress.vke.volcengine.com/loadbalancer-scheduler: wrr
               ingress.vke.volcengine.com/loadbalancer-unhealthy-threshold: 3
Events:
  Type     Reason              Age                From     Message
  ----     ------              ----               ----     -------
  Normal   ReconcilingIngress  33s (x3 over 55s)  ingress  Reconciling Ingress
  Normal   ReconciledIngress   31s (x2 over 33s)  ingress  Reconciled Ingress
```
