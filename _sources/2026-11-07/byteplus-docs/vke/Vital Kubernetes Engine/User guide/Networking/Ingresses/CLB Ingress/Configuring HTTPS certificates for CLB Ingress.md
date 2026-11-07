---
title: "Configuring HTTPS certificates for CLB Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-HTTPS-for-a-CLB-Ingress"
---

To ensure communication security in public networks, HTTPS is typically used for communication when services are exposed to public networks through Ingresses. This topic describes how to configure CLB Ingress with the HTTPS protocol.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before you begin, thoroughly read <a href="https://docs.byteplus.com/en/docs/vke/Precautions_for_using_CLB_Ingress">CLB Ingress considerations</a>.</div>


<span id=".6K-B5Lmm566h55CG"></span>
## Certificate management

VKE CLB Ingress supports the following certificate management methods, with key differences shown in the table below.


|Item |CLB certificate |[Recommended] Certificates from Certificate Center  |
|---|---|---|
|Certificate storage method |CLB storage. |Storage at Certificate Center. |
|Certificate discovery method |Discover by certificate ID. |Discover by certificate ID. |
|Certificate replacement method |Manual update. |* Manual update.<br><br>* Update via Certificate Center, supporting batch updates and deployment. |


<span id="s9bHtly2"></span>
## Prerequisites


* A workload and service have been created. For more details, see [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments) and [Creating services](https://docs.byteplus.com/en/docs/vke/Services).

* You have logged in to the [CLB console](https://console.byteplus.com/clb) or [Certificate Center](https://console.byteplus.com/certificate-center) and purchased or uploaded a certificate.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To use certificates from Certificate Center, log in to the BytePlus console with your account, click <a href="https://console.byteplus.com/iam/service/attach_role/?ServiceName=clb">Service authorization</a>, and on the page that appears, click <strong>Authorize now</strong> to complete cross\-service authorization.   </div>
   

* (Optional) To configure the certificate via YAML, install kubectl in your local environment and connect it to the target cluster. For details, see [ Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="SNRMvm7u"></span>
## Procedure


<Tabs>
<Tab zoneid="T9SZEUPWZv" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the cluster list page, click the target cluster name to enter the cluster configuration management page.

3. In the left navigation pane, select **Services and Ingresses \> Ingress**, and click **Create Ingress** to create a CLB Ingress.

   * Under **Ingress type**, select **CLB**.

   * Under listener configuration, select the **HTTPS** protocol, and in the certificate selection box, click Create Secret to configure the certificate.

4. Configure the Secret name, certificate source, and select the corresponding certificate. Click **Confirm** to complete the Secret configuration.

5. Return to the "Create Ingress" page, select the new Secret, and complete the other settings in the page. For more parameter descriptions, see [Creating CLB Ingress via console](https://docs.byteplus.com/en/docs/vke/Creating-a-CLB-Ingress-in-the-console).

6. Click **Confirm**.


</Tab>
<Tab zoneid="lC5gWtQVOV" title="Use kubectl">
<TabTitle>Use kubectl</TabTitle>

1. Create a Secret YAML file that specifies the certificate source and certificate ID. The sample file `secret-demo.yaml` has the following code:

   ```YAML
   apiVersion: v1
   kind: Secret
   metadata:
     name: https-secret-demo
   type: Opaque
   data:
     cert_id: Y2V***== # Base64-encoded certificate ID
     cert_source: Y2VydF9jZW50ZXI= # The Base64-encoded certificate source. Values: Y2xi (clb) and Y2VydF9jZW50ZXI= (cert_center, i.e., the certificate center).
   ```
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use the <code>echo -n "$(cert)" | base64</code> command to Base64\-encode the certificate ID and source. Replace <code>$(cert)</code> with your actual value. For example, if <code>$(cert)</code> is <code>cert_center</code>, the encoding command is <code>echo -n "cert_center" | base64</code>. The encoded value is <code>Y2VydF9jZW50ZXI=</code>.   </div>
   

2. Run the following command to create the Secret.

   ```Bash
   kubectl apply -f secret-demo.yaml
   ```
   

3. Create a YAML file for an Ingress. The sample file `clb-ingress.yaml` has the following code:

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     annotations:
       ingress.vke.volcengine.com/loadbalancer-name: "clb-demo" # Configure the CLB name
       ingress.vke.volcengine.com/loadbalancer-spec: "small_1" # Configure the specification of the CLB instance to be created. small_1：200Mbps、small_2：500Mbps、medium_1：1000Mbps、meidum_2：2000Mbps、large_1：5000Mbps、large_2：10000Mbps
       ingress.vke.volcengine.com/loadbalancer-subnet-id: "subnet-rrhvmyikek1sv0x58***" # Configure the subnet for the CLB instance.
       ingress.vke.volcengine.com/loadbalancer-address-type: "public" # Configure the CLB type. Value: public (public network) or private (private network)
       ingress.vke.volcengine.com/loadbalancer-bandwidth:  "10" # Configure the EIP bandwidth peak for the public CLB instance. Value range: 1 to 500 Mbps.
       ingress.vke.volcengine.com/loadbalancer-scheduler: "wrr" # Specify the scheduling algorithm. Valid values include wrr, wlc, and sh.
       ingress.vke.volcengine.com/loadbalancer-protocol: "https" # Specify the listener protocol for the CLB instance. Value: http or https
       ingress.vke.volcengine.com/loadbalancer-port: "443" # Specify the listening port for the CLB. Value range: 1 to 65535. The default port is 80 for HTTP and 443 for HTTPS.
     name: clb-ingress
     namespace: default
   spec:
     ingressClassName: clb
     rules:
     - host: example.com # The domain name that is externally accessible.
       http:
         paths:
         - backend:
             service:
               name: service-demo
               port:
                 number: 80
           path: / # The path that matches the request.
           pathType: Prefix # Path type. Available values include Exact (exact match) and Prefix (prefix match).
     tls:
     - secretName: https-secret-demo # Default certificate
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">CLB Ingress currently only supports configuring default certificates. Configuring extension certificates for specified domain names is not supported yet.   </div>
   

4. Execute the following command to create an Ingress.

   ```Bash
   kubectl apply -f clb-ingress.yaml
   ```
   





</Tab>
</Tabs>


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

<span id=".5p-l55yL6YWN572u"></span>
### Viewing settings

Run the following command to view the Ingress configuration.

```Bash
kubectl get ingress
```


If the response is similar to the following one, the Ingress has been created successfully, and the service is accessible.

```Bash
NAME          CLASS   HOSTS           ADDRESS          PORTS    AGE
clb-ingress   clb     example.com     180.xxx.xxx.xxx   80,443  74s
```


<span id=".6K6_6Zeu5pyN5Yqh"></span>
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


<span id="gof9eFDj"></span>
## Other configurations

<span id=".5aaC5L2V5L2_55SoLW9wZW5zc2wt5Yib5bu66Ieq562-5ZCN6K-B5Lmm"></span>
### Using OpenSSL to create a self\-signed certificate

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Self\-signed certificates are typically used for testing, integration debugging, or temporary HTTPS configuration validation. Using them directly in production environments is not recommended. For production environments, we recommend using certificates from Certificate Center or TLS certificates issued by a trusted CA to avoid browser trust issues or MITM attacks.</div>



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
