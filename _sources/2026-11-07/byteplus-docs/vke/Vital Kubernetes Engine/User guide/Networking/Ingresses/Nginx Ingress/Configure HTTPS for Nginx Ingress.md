---
title: "Configure HTTPS for Nginx Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-HTTPS-for-an-Nginx-Ingress"
---

To ensure secure communication in a public network environment, when services are exposed to the public network using Ingress, they typically use the HTTPS protocol for communication. This article describes how to configure HTTPS for Nginx Ingress.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster has been connected. For more details, refer to [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* The ingress\-nginx add\-on has already been installed in the cluster. For more details, refer to the [ingress-nginx add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=).

* You have already purchased or used SSL certificates and keys in SSL Certificate Service or created them using OpenSSL.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5L-d5a-G5a2X5YW4"></span>
### Step 1: Configure Secret


1. The SSL certificate and key have been obtained; this document uses `tls.key` and `tls.crt` as examples.

2. Run the following command to create a Secret named ingress\-secret with the type `kubernetes.io/tls`.


```bash
kubectl create secret tls ingress-secret --key tls.key --cert tls.crt
```


<span id=".5q2l6aqk5LqM77ya6YOo572y5bqU55So5ZKM5pyN5Yqh"></span>
### Step 2: Deploy applications and services


1. Create the YAML file of the workload. The code of the sample file `deployment-demo.yaml` is as follows:


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # Deployment name
  namespace: default # The namespace where the Deployment is located
spec: 
  replicas: 1 # Number of Deployment replicas
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
        image: nginx:latest # Address of the container image and tag
        ports:
        - containerPort: 80 # Exposed ports of the container
```



2. Run the following command to create the workload.


```bash
kubectl apply -f deployment-demo.yaml
```



3. Create a YAML file for the Service. Here is an example file named `service-demo.yaml` :


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
    protocol: TCP # Service protocols supported: TCP or UDP
    port: 80 # service port
    nodePort: 30000 # NodePort, which can be an integer from 30000 to 32767.
    targetPort: 80 # Container port, which refers to the port number or port name through which a workload provides external services, for example, the default port for Nginx is 80.
  type: NodePort # type of Service
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When the cluster's network model is Flannel, only Services of the NodePort and LoadBalancer types can be selected and associated.</div>


* <div data-tips="true" data-tips-type="warning">When the network model of the cluster is VPC\-CNI:</div>


   * <div data-tips="true" data-tips-type="warning">If Ingress has enabled <strong>LB\-to\-pod direct access mode</strong>, it supports associating with and selecting Service of type NodePort, LoadBalancer, or ClusterIP.</div>


   * <div data-tips="true" data-tips-type="warning">If Ingress does not enable <strong>LB\-to\-pod direct access mode</strong>, it only supports associating with and selecting NodePort or LoadBalancer type services.</div>


4. Execute the following command to create a service.


```bash
kubectl apply -f service-demo.yaml
```


<span id=".5q2l6aqk5LiJ77ya6YWN572uLW5naW54LWluZ3Jlc3M="></span>
### Step 3: Configure Nginx Ingress


1. Create an Ingress YAML file. The code for the example file `nginx-ingress.yaml` is as follows:


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress # The name of the Ingress
spec:
  ingressClassName: nginx # Specify the Ingress Controller
  rules:
  - host: example.com # Domain name for forwarding rules
    http:
      paths:
      - backend:
          service:
            name: service-demo # Name of the target Service to which the request is forwarded
            port:
              number: 80 # The open port number of the target service to which the request is forwarded
        path: / # Access paths
        pathType: Prefix # Path type: Exact (exact match) / Prefix (prefix match)
  tls:
  - hosts:
    - example.com # (Optional) Specify the domain names to be encrypted. Not configured means all domain names will be encrypted.
    secretName: ingress-secret # Specify the name of the Secret used by ingress
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In a public network environment, you need to independently ensure the DNS resolution mapping between your custom domain and the EIP of the ingress LoadBalancer.</div>


* <div data-tips="true" data-tips-type="tip">When the <strong>HTTPS</strong> protocol is selected, the system will open both port 80 and port 443 by default. To ensure data security, it is recommended to configure port 80 redirection, that is, redirect HTTP to HTTPS. For details, refer to <a href="https://docs.byteplus.com/en/docs/vke/Configuring-redirect-rules-for-an-Nginx-Ingress">Nginx Ingress redirect rule configuration</a>.</div>


2. Run the following command to create an Ingress.


```bash
kubectl apply -f nginx-ingress.yaml
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

<span id=".5p-l55yL6YWN572u"></span>
### Viewing configuration


1. Run the following command to view the ingress configuration.


```bash
kubectl get ingress
```


The expected response result is as follows, indicating that the Ingress was created successfully. Here, `180.xxx.xxx.xxx` is the public or private IP address of the CLB associated with Nginx Ingress.

```bash
NAME            CLASS   HOSTS           ADDRESS           PORTS   AGE
nginx-ingress   nginx   example.com     180.xxx.xxx.xxx   80,443  74s
```


<span id=".6K6_6Zeu5pyN5Yqh"></span>
### Testing the connections to services

Use the following commands to access the Service via domain name.

```bash
curl -H "Host: example.com" https://180.xxx.xxx.xxx --insecure
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When you use a self\-signed certificate, you can use the <code>-k</code> or <code>--insecure</code> parameter to ignore certificate validation.</div>


* <div data-tips="true" data-tips-type="warning">When using TLS certificates in a production environment, it is recommended that you use official trusted certificates. Using a self\-signed certificate and ignoring certificate verification may expose you to man\-in\-the\-middle attacks.</div>



The expected output is as follows, indicating that the backend service can be accessed via the domain name.

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


<span id=".6L-Q57u06YWN572u"></span>
## Operation and maintenance configuration

<span id=".5aaC5L2V5pu05o2iLWh0dHBzLeivgeS5pg=="></span>
### How to replace an HTTPS certificate

When you need to replace the HTTPS certificate for Nginx Ingress, you must follow the procedure below:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the cluster list page, click the target cluster name to enter the cluster management page.

3. In the left navigation bar, select **Services and Ingresses \> Ingress**. In Ingress, select the Ingress rule for which you need to update the HTTPS certificate. In the **Actions ** column, click **Update**.

4. In the **Listener configuration ** section, click **Create Secret ** to create a secret.

5. Create and upload new certificates and keys, and click **Confirm** to update the Ingress.

6. Click the Ingress name, and on the Ingress details page, click the **Event** tab to view the successful reconciliation events for the Ingress.
