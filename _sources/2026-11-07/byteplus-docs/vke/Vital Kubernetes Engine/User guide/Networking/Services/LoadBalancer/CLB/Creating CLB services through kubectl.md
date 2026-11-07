---
title: "Creating CLB services through kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-using-kubectl"
---

VKE supports creating LoadBalancer Services. This topic describes how to create a LoadBalancer Service through a YAML file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring a LoadBalancer Service, be sure to carefully read <a href="https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_usage_precautions">Considerations for using LoadBalancer services</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created. For more details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The kubectl tool is installed on your computer. For details, please see [Installation and settings of kubectl](https://kubernetes.io/docs/tasks/tools/).

* The target cluster has been connected by using kubectl. For details, please see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* Deployments have been created. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment), [Creating StatefulSets](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet), and [Creating DaemonSets](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only Deployment, StatefulSet, and DaemonSet are supported.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Create a YAML file for the Service. Here is an example file named `service-demo.yaml` :

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: service-demo
   spec:
     selector:
       app: nginx
     ipFamilyPolicy: PreferDualStack
     ipFamilies: 
     - IPv6
     - IPv4
     ports:
     - name: rule 
       protocol: TCP 
       port: 80
       targetPort: 80
     type: LoadBalancer
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The system will create a CLB instance correspondingly based on the default settings when using the YAML file above to create a LoadBalancer service in an IPv4 cluster. If a custom CLB is required, we recommend using annotations to create it. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations">Using annotations to configure LoadBalancer services</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Dual\-stack clusters do not support CLB instances of PUBLIC type. Therefore, when creating a LoadBalancer Service in a dual\-stack cluster with a YAML file, add the annotation <code>service.beta.kubernetes.io/volcengine-loadbalancer-address-type: "PRIVATE"</code> to specify the CLB type as PRIVATE.   </div>
   

2. Execute the following command to create a service.

   ```bash
   kubectl apply -f service-demo.yaml
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results


1. Execute the following command to view the service created.


```bash
kubectl get svc -n default
```


The expected output is as follows. EXTERNAL\-IP indicates the public IP address of the CLB to which the Service is attached.

```bash
NAME           TYPE           CLUSTER-IP       EXTERNAL-IP       PORT(S)         AGE
service-demo   LoadBalancer   10.xxx.xxx.xxx   180.xxx.xxx.xxx   80:30891/TCP    44s
```



2. Run the following command to view the details of the created Service.


```bash
kubectl describe svc service-demo -n default
```


The information below is what will be printed on the screen. The Annotation on the screen displays the information about the CLB, including CLB instance ID, subnet ID, and EIP billing model. You can search for the CLB instance by its ID on the [LoadBalancer](https://console.byteplus.com/clb)  console page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about LoadBalancer service annotations, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations">Using annotations to configure LoadBalancer services</a>.</div>


```bash
Name:                     service-demo
Namespace:                default
Labels:                   service.beta.kubernetes.io/volcengine-loadbalancer-id=clb-3qe5tw***
Annotations:              service.beta.kubernetes.io/system-volcengine-loadbalancer-create-response-id: clb-3qe5twv8***
                          service.beta.kubernetes.io/volcengine-loadbalancer-address-type: PUBLIC
                          service.beta.kubernetes.io/volcengine-loadbalancer-bandwidth: 1
                          service.beta.kubernetes.io/volcengine-loadbalancer-eip-billing-type: 3
                          service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: off
                          service.beta.kubernetes.io/volcengine-loadbalancer-isp-type: BGP
                          service.beta.kubernetes.io/volcengine-loadbalancer-name: k8s-7f328f46***
                          service.beta.kubernetes.io/volcengine-loadbalancer-pass-through: false
                          service.beta.kubernetes.io/volcengine-loadbalancer-scheduler: wrr
                          service.beta.kubernetes.io/volcengine-loadbalancer-spec: small_1
                          service.beta.kubernetes.io/volcengine-loadbalancer-subnet-id: subnet-3qe2d3p***
Selector:                 app=nginx
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.xxx.xxx.xxx
IPs:                      10.xxx.xxx.xxx
LoadBalancer Ingress:     180.xxx.xxx.xxx
Port:                     rule  80/TCP
TargetPort:               80/TCP
NodePort:                 rule  30429/TCP
Endpoints:                192.168.112.4:80,192.168.128.9:80,192.168.48.3:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:
  Type     Reason                    Age                From                Message
  ----     ------                    ----               ----                -------
  Normal   EnsuringLoadBalancer      71s (x4 over 83s)  service-controller  Ensuring load balancer
  Normal   EnsuredLoadBalancer       70s (x2 over 71s)  service-controller  Ensured load balancer
```
