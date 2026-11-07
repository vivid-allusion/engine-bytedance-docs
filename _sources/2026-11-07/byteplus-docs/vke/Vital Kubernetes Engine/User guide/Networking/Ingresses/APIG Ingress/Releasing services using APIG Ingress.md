---
title: "Releasing services using APIG Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Use_APIG_Ingress_for_service_release"
---

APIG Ingress is a managed cloud\-native gateway built on [API Gateway (APIG)](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), providing traffic management with high availability and scalability. This topic introduces how to release services using APIG Ingress and related considerations.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Do not change the APIG instances associated with the APIG Ingress you created. Otherwise, APIG services may malfunction, and you will be fully responsible for any consequences of your actions.

* If you modify resources or configurations specified or maintained by the APIG Ingress in the APIG console, the configurations may be overwritten.

* Using APIG products will incur resource fees.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The APIG service has been activated. If the service is not activated, log in to the [APIG console](https://console.byteplus.com/veapig) and activate the service based on the on\-screen prompts.

* The apig\-controller add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A KubeConfig for private networks has been generated in the cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* (Optional) If you need to connect to an existing APIG instance, ensure that an instance in the **Running** status exists on the APIG console. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LWFwaWdpbnN0YW5jZQ=="></span>
### Step 1: Create an APIGInstance


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to create Ingress. Configure the mapping between external domain names and services.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.


```yaml
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: APIGInstance
metadata:
  name: apig-instance-demo # APIGInstance resource name
spec:
  id: gcqplplr8a*** # An existing APIG instance ID
  ingress:
    enable: true # Enable APIG Ingress synchronization
    enableAllIngressClasses: false
    enableIngressWithoutIngressClass: false
    ingressClasses: # The IngressClasses for which Ingress synchronization takes effect
      - apig
    enableAllNamespaces: true # Synchronize all Ingresses in all namespaces
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The preceding example contains the simplest configurations, where an existing APIG instance is used to bind to an APIGInstance. For more configurations, see <a href="https://docs.byteplus.com/en/docs/vke/Create_an_APIG_Ingress_using_kubectl">Creating APIG Ingress using kubectl</a>.</div>



5. After APIGInstance is created, in the left navigation bar, select **Workload \> Resource Explorer ** and click the APIGInstance name **apig\-instance\-demo** to view the detailed information about it.


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
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # The address and version of the application image. Replace it with your own image address and version.
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



4. Execute the following command to create a service.


```bash
kubectl apply -f service-demo.yaml
```


<span id=".5q2l6aqk5LiJ77yaLeWIm-W7ui1hcGlnLWluZ3Jlc3M="></span>
### Step 3: Create an APIG Ingress


1. The following is an example YAML file named `apig-ingress.yaml` for creating an APIG Ingress.

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: apig-ingress # Ingress name
     namespace: default  # Namespace of the Ingress
     annotations: 
       ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # Specify the APIGInstance resource name
   spec:
     ingressClassName: apig
     rules:
       - host: example.com  # Domain names for external access
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-demo # Service name to forward to
                 port: 
                   number: 80 # Service port number to forward to
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This is an example with the simplest configurations. For more configurations, see <a href="https://docs.byteplus.com/en/docs/vke/Create_an_APIG_Ingress_using_kubectl">Creating APIG Ingress using kubectl</a>.   </div>
   

2. Execute the following command to create an APIG Ingress.

   ```bash
   kubectl apply -f apig-ingress.yaml
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

<span id=".5p-l55yLLWFwaWctaW5ncmVzcy3nirbmgIE="></span>
### Viewing APIG Ingress status


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster for which you need to configure an Ingress.

4. In the left navigation bar, select **Service and Ingresses \> Ingress**, and then view the status of APIG Ingresses on the page.

5. Click the APIG Ingress name to go to the details page. Select the **Event** tab to view the synchronization events of APIG Ingresses.


<span id=".6K6_6Zeu5bqU55So"></span>
### Accessing applications

Access the service using the domain name configured in the APIG Ingress.

```bash
curl http://example.com
```


The following output indicates that the backend service can be accessed through the APIG Ingress.

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
