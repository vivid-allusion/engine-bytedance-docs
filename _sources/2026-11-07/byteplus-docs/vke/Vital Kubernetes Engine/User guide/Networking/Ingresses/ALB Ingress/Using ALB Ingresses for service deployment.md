---
title: "Using ALB Ingresses for service deployment"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-an-ALB-Ingress-to-deploy-an-application"
---

An Application Load Balancer (ALB) Ingress, built on the BytePlus ALB, offers more comprehensive Layer 7 load balancing capabilities. This topic introduces how to release services by using ALB Ingresses and related considerations.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* To prevent ALB exceptions, do not directly modify an ALB instance, its listeners, back\-end server groups, or forwarding rules managed by an ALB Ingress from the ALB console. Any such modifications are undertaken at your own risk.

* Do not modify any content prefixed with `k8s_` in the name of a listener or backend server group.

* Do not modify any content prefixed with `k8s_` in the description of a forwarding rule.

* Using the ALB console to modify resources and configurations specified or maintained by an ALB Ingress (for example, forwarding rules) may cause configurations to be overwritten.

* Using ALB incurs fees for the use of cloud infrastructure resources. For details, see [ALB billing](https://docs.byteplus.com/en/docs/clb/Billing-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LWFsYmluc3RhbmNl"></span>
### Step 1: Create an ALBInstance


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to create an ALBInstance.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.


```yaml
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb     # The name of the ALBInstance.
spec:
  instanceID: "alb-2dgns526uiv41fi5********" # The ID of the existing ALB instance.
  listeners:
  - protocol: "HTTP" # The protocol for the listener.
    port: 80 # The port used for HTTP listeners.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this example, the ALBInstance configuration is simple because the ALBInstance is created by using an existing ALB instance. For more configuration details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl">Creating ALB Ingresses by using kubectl</a>.</div>



5. After the ALBInstance resource is created, click **albinstance** on the **Resource Explorer** page to view details of the resource.


<span id=".5q2l6aqk5LqM77ya6YOo572y5bqU55So5ZKM5pyN5Yqh"></span>
### Step 2: Deploy an application and service


1. Create the YAML file of the workload. The code of the sample file `deployment-demo.yaml` is as follows:


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # Deployment name
  namespace: default # Namespace of the Deployment
spec: 
  replicas: 1 # Number of replicas for the Deployment
  selector: 
    matchLabels: 
      app: nginx
  template: 
    metadata: 
      labels: 
        app: nginx
    spec:
      containers:
      - name: nginx # Container name
        image: nginx:latest # The container image address and tag.
        ports:
        - containerPort: 80 # Exposed container port number
```



2. Run the following command to create the workload.


```bash
kubectl apply -f deployment-demo.yaml
```



3. A YAML file for creating the service. The code of the sample file `deployment-demo.yaml` is as follows:


```yaml
apiVersion: v1
kind: Service
metadata:
  name: service-demo # Service name
spec:
  selector:
    app: nginx # Bind the service to backend pods via a label selector.
  ports:
  - name: rule # Port mapping rule name
    protocol: TCP # Service protocol, can be TCP or UDP
    port: 80 # Service port
    nodePort: 30000 # NodePort, which can be an integer from 30000 to 32767.
    targetPort: 80 # Container port, a port number or port name through which a workload provides service, e.g., the default port number for Nginx is 80
  type: NodePort # Service type
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When the network model of the cluster is Flannel, you can select only a NodePort or LoadBalancer service.</div>


* <div data-tips="true" data-tips-type="warning">When the network model of the cluster is VPC\-CNI:</div>


   * <div data-tips="true" data-tips-type="warning">If the <strong>LB\-to\-pod direct access mode</strong> is enabled for the Ingress, you can select a NodePort, LoadBalancer, or ClusterIP service.</div>


   * <div data-tips="true" data-tips-type="warning">If the <strong>LB\-to\-pod direct access mode</strong> is not enabled for the Ingress, you can select only a NodePort or LoadBalancer service.</div>


4. Execute the following command to create a service.


```bash
kubectl apply -f service-demo.yaml
```


<span id=".5q2l6aqk5LiJ77yaLeWIm-W7ui1hbGItaW5ncmVzcw=="></span>
### Step 3: Create an ALB Ingress


1. Create a YAML file for the Ingress. The following `alb-ingress.yaml` file provides an example:

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: alb-ingress-demo # The name of the Ingress.
     namespace: default  # Namespace of the Ingress
   spec:
     ingressClassName: alb  # The name of the ALBInstance.
     rules:
       - host: example.com  # Domain names for external access
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-demo # The name of the service to forward requests to.
                 port: 
                   number: 80 # The service port number to forward to.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This example uses the simplest method to create an ALB Ingress. For more configuration details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl">Creating ALB Ingresses by using kubectl</a>.   </div>
   

2. Run the following command to create the ALB Ingress.

   ```bash
   kubectl apply -f alb-ingress.yaml
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

Access the service by using the domain name configured in the ALB Ingress.

```bash
curl http://example.com
```


The response similar to the following indicates that the back\-end service can be accessed through the ALB Ingress.

```html
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
