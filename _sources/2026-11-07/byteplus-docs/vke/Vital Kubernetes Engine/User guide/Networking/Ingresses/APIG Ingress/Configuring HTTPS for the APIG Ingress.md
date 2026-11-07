---
title: "Configuring HTTPS for the APIG Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_HTTPS_for_the_APIG_Ingress"
---

To ensure communication security in public networks, HTTPS is typically used for communication when services are exposed to public networks through Ingresses. This topic describes how to configure HTTPS for an APIG Ingress.

<span id="h2xhbQlr"></span>
## Prerequisites


* A cluster has been connected. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* The apig\-controller add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* You have already purchased a Secure Sockets Layer (SSL) certificate and key in BytePlus SSL Certificate Service or created an SSL certificate and key by using OpenSSL.


<span id="l7PpAJxM"></span>
## Procedure

<span id="7lIhkbTQ"></span>
### Step 1: Configure a Secret


1. The SSL certificate and key have been obtained. This topic takes `tls.key` and `tls.crt` as an example.

2. Run the following command to create a Secret named ingress\-secret of type `kubernetes.io/tls`.

   ```Bash
   kubectl create secret tls ingress-secret --key tls.key --cert tls.crt
   ```
   


<span id="07bNxPYw"></span>
### Step 2: Deploy an application and service


1. Create the YAML file of a workload. The code of the sample file `deployment-demo.yaml` is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-demo # The Deployment name.
     namespace: default # The namespace where the Deployment resides.
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
         - name: nginx # The container name.
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # The container image address and tag.
           ports:
           - containerPort: 80 # Exposed container port number
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl apply -f deployment-demo.yaml
   ```
   

3. Create a YAML file for the Service. The following code is the content of a sample YAML file named `service-demo.yaml`.

   ```YAML
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
       port: 80 # The service port.
       nodePort: 30000 # NodePort, which can be an integer from 30000 to 32767.
       targetPort: 80 # Container port, a port number or port name through which a workload provides service, e.g., the default port number for Nginx is 80
     type: NodePort # Service type.
   ```
   

4. Execute the following command to create a service.

   ```Bash
   kubectl apply -f service-demo.yaml
   ```
   


<span id="eFlUVfk8"></span>
### Step 3: Configure the APIG Ingress


<Tabs>
<Tab zoneid="Or9xLvT7jH" title="Creating through the console">
<TabTitle>Creating through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar, click **Services and Ingresses \> Ingress**, and click **Create Ingress**.

   * Select Automatically create or Use existing for the **Gateway specifications** parameter. This topic uses an existing APIG instance as an example.

   * Select **HTTPS** for the **Protocol** parameter and select the configured Secret for the **Certificate** parameter.

   * In the **Forwarding rules** section, specify the domain name, path, and back\-end service related to forwarding.

4. Click **Confirm**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more configuration methods and descriptions of APIG Ingresses, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console">Creating APIG Ingresses in the console</a>.</div>



</Tab>
<Tab zoneid="lcbhdgK91f" title="Creating through kubectl">
<TabTitle>Creating through kubectl</TabTitle>

1. Create an APIGInstance. You can connect to an existing APIG instance or create an APIG instance. For details, see [Creating APIG Ingresses by using kubectl](https://docs.byteplus.com/en/docs/vke/Create_an_APIG_Ingress_using_kubectl).

2. Create a YAML file for an APIG Ingress. The following is an example named `apig-ingress.yaml`.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: apig-ingress # The name of the Ingress.
     namespace: default  # Namespace of the Ingress
     annotations:
       ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
   spec:
     ingressClassName: apig # Specify an Ingress controller.
     rules:
     - host: example.com # The domain name in the forwarding rule.
       http:
         paths:
         - backend:
             service:
               name: service-demo # The name of the service where requests are forwarded.
               port:
                 number: 80 # The port that the service opens to receive forwarded requests.
           path: / # The access path.
           pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
     tls:
     - hosts:
       - example.com # (Optional) Specify the domain name to be encrypted. If you do not specify this parameter, it indicates that all domain names will be encrypted.
       secretName: ingress-secret # Specify the Secret name.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to ensure the DNS resolution relationship between the custom domain name and the IP address that corresponds to the APIG Ingress in your network environment.   </div>
   

3. Execute the following command to create an APIG Ingress.

   ```Bash
   kubectl apply -f nginx-ingress.yaml
   ```
   


</Tab>
</Tabs>


<span id="HkAtC2Pq"></span>
## Validating results

<span id="GJTyTjGS"></span>
### Viewing configuration


1. Run the following command to view the APIG Ingress configurations.

   ```Bash
   kubectl get ingress
   ```
   

   If the response is similar to the following one, the APIG Ingress has been created. The address `180.xxx.xxx.xxx` is the IP address of the APIG Ingress access endpoint.

   ```Bash
   NAME            CLASS   HOSTS           ADDRESS           PORTS   AGE
   apig-ingress    apig    example.com     180.xxx.xxx.xxx   443     74s
   ```
   


<span id="TIX3b90q"></span>
### Testing the connections to services

Run the following command to access the service by using the domain name.

```Bash
curl -H "Host: example.com" https://180.xxx.xxx.xxx --insecure
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When you use a self\-signed certificate, you can use the <code>-k</code> or <code>--insecure</code> parameter to ignore certificate verification.</div>


* <div data-tips="true" data-tips-type="warning">If you need to use a TLS certificate in production, we recommend that you use a trusted one. Using self\-signed certificates and ignoring certificate verification may expose you to man\-in\-the\-middle attacks.</div>



If the response is similar to the following one, the back\-end service is accessible through the domain name.

```HTML
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


<span id="yA1OAqUx"></span>
## Operation and maintenance configuration

<span id="DL0c6qfW"></span>
### Using OpenSSL to create a self\-signed certificate


1. Download OpenSSL from the [OpenSSL website](https://www.openssl.org/) to your local environment and install it.

2. Execute the following command to generate a 4096\-bit RSA private key.

   ```Bash
   openssl genrsa -out tls.key 4096
   ```
   

   The expected result is as follows:

   ```Bash
   Generating RSA private key, 4096 bit long modulus
   ........+++++
   ...+++++
   e is 65537 (0x10001)
   ```
   

3. Execute the following command to use the RSA private key to create a certificate.

   ```Bash
   openssl req -new -key tls.key -out tls.csr
   ```
   

   The expected response is that you need to provide information such as the country, region, organization name, domain, and email address.

   ```Bash
   You are about to be asked to enter information that will be incorporated
   into your certificate request.
   What you are about to enter is what is called a Distinguished Name or a DN.
   There are quite a few fields but you can leave some blank
   For some fields there will be a default value,
   If you enter '.', the field will be left blank.
   -----
   Country Name (2 letter code) []:CN # A two-letter country code, for example, CN.
   State or Province Name (full name) []:Shanghai # Region name, for example, Shanghai.
   Locality Name (eg, city) []:Shanghai # City name, for example, Shanghai.
   Organization Name (eg, company) []:vke # Organization name.
   Organizational Unit Name (eg, section) []:vke # Organizational unit name.
   Common Name (eg, fully qualified host name) []:example.com # Domain name of the certificate.
   Email Address []:user@example.com # Email address.
   
   Please enter the following 'extra' attributes
   to be sent with your certificate request
   A challenge password []:mypassword # Password (optional).
   ```
   

4. Execute the following command to use the private key to sign the certificate and set the validity period to 365 days.

   ```Bash
   openssl x509 -req -in tls.csr -out tls.crt -signkey tls.key -days 365
   ```
   

5. At this point, the private key `tls.key` and certificate `tls.crt` required for HTTPS encryption have been created.


&nbsp;

<span id="J0kLKlmH"></span>
### Replacing an HTTPS certificate

You need to perform the following steps to replace the HTTPS certificate for the APIG Ingress.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. In the left navigation bar, click **Configurations** \> **Secret**. On the Secret page, click Create Secret to create a Secret and upload a new certificate and key.

4. In the left navigation bar, click **Services and Ingresses \> Ingress**. In the Ingress list, find the Ingress for which you need to update the HTTPS certificate and click **Update** in the **Actions** column.

4. In the **Listener configuration** section, select the new Secret.

6. Click **Confirm**. The certificate update is complete. After the update is complete, click the **Event** tab on the Ingress details page to view the successful reconciliation events for the Ingress.

7. Log in to the [APIG console](https://console.byteplus.com/veapig) to view certificate information.

   1. In the left navigation bar, click **Instance management**. In the instance list, find the target APIG instance, and click its name to view its details.

   2. In the left navigation bar, click **Service list (Domain name)** . Click the name of the target service to go to the service overview page.

   3. Click the **Domain name management** tab. You can view the certificate information that corresponds to the domain name in the **Custom domain name** section.
