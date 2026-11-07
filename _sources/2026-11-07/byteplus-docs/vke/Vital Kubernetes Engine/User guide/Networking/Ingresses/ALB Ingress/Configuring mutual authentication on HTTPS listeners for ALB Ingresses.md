---
title: "Configuring mutual authentication on HTTPS listeners for ALB Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configure_HTTPS_mutual_authentication_for_ALB_Ingress"
---

An Application Load Balancer (ALB) Ingress supports mutual authentication, which ensures server and client security in HTTPS scenarios. This topic describes the scenarios and configuration methods of mutual authentication for ALB instances over HTTPS.

<span id="p5yBmhHd"></span>
## Background information

In Internet communication security, the HTTPS protocol implements data encryption and identity authentication through the SSL/TLS layer. Common core authentication modes include one\-way authentication and mutual (two\-way) authentication. The following table describes the two modes.


|Authentication method |Explanation |Authentication process |
|---|---|---|
|One\-way authentication |* It is a fundamental, client\-initiated security authentication method.<br><br>* The core logic is that only the client verifies the identity of the server and that the server does not verify the identity of the client.<br><br>* The purpose is to ensure that the client accesses the legitimate server (not phishing or fraudulent sites) through the digital certificate mechanism. |1. The client initiates an HTTPS connection request to the server, explicitly specifying supported SSL/TLS versions and encryption algorithms.<br><br>2. Upon receiving the request, the server sends its SSL certificate to the client (containing critical server data including the public key, domain information, certificate validity period, and the digital signature of the CA).<br><br>3. The client performs multi\-layer validation on the received certificate. It first checks certificate expiration status, then verifies certificate signature legitimacy using locally stored trusted CA root certificates, and confirms that the domain name in the certificate matches the domain of the server. If all validations pass, the client uses the public key in the certificate to negotiate a symmetric encryption key for subsequent data transmission with the server, establishing a secure connection. |
|Mutual authentication |* It is a high\-security authentication method where both client and server mutually verify each other.<br><br>* It extends the one\-way authentication model by adding "server verification of client identity," forming a bidirectional trust mechanism: "client verifies server + server verifies client."<br><br>* It is designed for scenarios that require elevated security assurance. |1. The first three steps are the same as one\-way authentication: the client initiates a request, the server sends a certificate, and the client successfully verifies the server certificate.<br><br>2. Upon successful client verification, the server sends the client a ‌certificate request‌ to demand its SSL certificate.<br><br>3. The client sends its ‌client certificate‌ containing identity information (such as the user ID, device serial number) to the server.<br><br>4. The server verifies the client certificate using the same logic: It checks the validity period of the client certificate, validates cryptographic signature (requires trusting the client certificate's issuing CA), and performs business\-rule validation (for example, confirms whether the certificate holder is an authorized enterprise employee or belongs to permitted device groups). If the client certificate verification passes, the server negotiates symmetric session keys to establish a mutually authenticated secure connection. If verification fails at any stage, the connection attempt immediately terminates. |


<span id="my4ZdBmT"></span>
## Prerequisites


* The clusters have been created. For details, see[ Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The cluster has been connected. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* The alb\-ingress\-controller add\-on has been installed and upgraded to v0.32.0 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* You have purchased or obtained the server certificate and CA certificate, and uploaded them to the ALB console. 


<span id="2yi4GcLo"></span>
## Procedure

<span id="5iDIwhSI"></span>
### Step 1: Generate a certificate

<span id="Z9IFiGVw"></span>
#### Generate a self\-signed CA certificate


1. Download OpenSSL from the [OpenSSL website](https://www.openssl.org/) to your local environment and install it.

2. Execute the following command to generate a 4096\-bit private key of the CA.


```Bash
openssl genrsa -out ca.key 4096
```



3. Run the following command to generate the root CA certificate using the private key of the CA.


```Bash
openssl req -new -x509 -key ca.key -out ca.crt
```


The expected response is that you need to provide information such as the country, region, organization name, domain, and email address.

```bash
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



4. Complete the creation of the root CA certificate, including the private key `ca.key` and the certificate`ca.crt`.


<span id="5rD2HnJo"></span>
#### Generate a server certificate


1. Run the following command to generate a 2048\-bit private key for the server.


```bash
openssl genrsa -out server.key 2048
```



2. Run the following command to use the private key of the server to generate a certificate request.


```bash
openssl req -new -key server.key -out server.csr
```


The expected response is that you need to provide information such as the country, region, organization name, domain, and email address.

```bash
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



3. Run the following command to use the CA certificate to issue a server certificate, with the validity period set to 365 days.


```bash
openssl x509 -req -in server.csr -out server.crt -CA ca.crt -CAkey ca.key -CAcreateserial -days 365
```



4. Finish creating the server certificate, including the private key `server.key` and certificate `server.crt`.


<span id="kfqDusp6"></span>
#### Generate a client certificate


1. Run the following command to generate a 2048\-bit private key for the client.


```bash
openssl genrsa -out client.key 2048
```



2. Run the following command to generate a client certificate request using the private key of the client.


```bash
openssl req -new -key client.key -out client.csr
```


The expected response is that you need to provide information such as the country, region, organization name, domain, and email address.

```bash
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



4. Run the following command to issue a client certificate using the CA certificate, with the validity period set to 365 days.


```bash
openssl x509 -req -in client.csr -out client.crt -CA ca.crt -CAkey ca.key -CAcreateserial -days 365
```



5. Complete the creation of the client certificate, including the private key `client.key` and the certificate `client.crt`.


<span id="cSGFRNgz"></span>
### Step 2: Upload certificates

In the [ALB console](https://console.byteplus.com/alb), upload the certificates and keys. For details, see [Managing certificates](https://docs.byteplus.com/en/docs/clb/Manage-certificates). After the certificates have been added, record the IDs of the certificates. The certificate IDs will be used in configuration later.

<span id="mEAHqykw"></span>
### Step 3: Configure the ALBInstance

When you use an ALBInstance to associate with an existing ALB instance or create a new ALB instance, you can configure HTTPS mutual authentication by using fields `caEnabled` and `caCertificates` in `spec.listeners`. This section demonstrates how to associate with an existing ALB instance. The following is an example:

```YAML
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb # The name of the ALBInstance.
spec:
  instanceID: "alb-2dgns526uiv41fi5***" # The ID of the existing ALB instance.
  listeners:
  - protocol: "HTTP" # The protocol for the listener.
    port: 80 # The port used for HTTP listeners.
  - protocol: "HTTPS" # The protocol for the listener.
    port: 443 # The port used for HTTPS listeners.
    certificateSource: "alb" # Listener certificate source. Valid values: alb. 
    certificateID: "cert-2wx20lm7uquww7oot***" # The server certificate used by all domains for HTTPS listeners.
    caEnabled: true # Whether to enable mutual authentication for HTTPS listeners. Valid values: true and false.
    caCertificates:
    - caCertificateID: "cert-xobjnz7dx0jk54o***" # The ID of the private root CA certificate.
      caCertificateSource: "alb" # The source of the certificate for mutual authentication. Valid values: alb. 
```


The following table describes subfields in the `caEnabled` and `caCertificates` fields of the `spec.listeners`.


|Parameter |Type |Required |Description |Sample value |Editable |
|---|---|---|---|---|---|
|caEnabled |Boolean |None |The mutual authentication switch for HTTPS listeners. Valid values:<br><br><br>* **true**: Enable mutual authentication.<br><br>* **false**: Disable mutual authentication.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this field is not configured, the mutual authentication configuration of the ALB listener will not be modified.</div><br> |true |Yes |
|caCertificateID |String |None |The ID of the certificate for mutual authentication.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>caEnabled</code> is <code>true</code>, this field must be configured.</div><br> |cert\-2wx20lm7uquww7oot\*\*\*\*\*\*\*\* |Yes |
|caCertificateSource |String |None |The source of the certificate for mutual authentication. Valid values:<br><br><br>* **alb** (default): Certificates uploaded to ALB.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When <code>caEnabled</code> is <code>true</code>, this field must be configured.</div><br> |alb |Yes |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The <code>caCertificates</code> field can contain only a certificate source and certificate ID.</div>


<span id="TPbWtCX8"></span>
### Step 4: Configure an ALB Ingress

Create an Ingress and choose an HTTPS listener. The following code provides an example:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress-demo # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-port: "443" # Listening port.
    ingress.vke.volcengine.com/loadbalancer-protocol: "https"  # Listener protocol. In this example, the value is https.
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


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This example uses the simplest method to create an ALB Ingress. For more configuration details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl">Creating ALB Ingresses by using kubectl</a>.</div>


<span id="Hv1wvPh5"></span>
## Validating results

<span id="Se6an9nl"></span>
### Viewing configuration


1. Run the following command to view the Ingress configuration.


```Bash
kubectl get ingress
```


If the response is similar to the following one, the ALB Ingress has been created.

```Bash
NAME               CLASS   HOSTS           ADDRESS          PORTS    AGE
alb-ingress-demo   alb     example.com     180.xxx.xxx.xxx   80,443  74s
```



1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left navigation bar, select **Instance**.  On the page that appears, click the name of the target ALB instance to go to the instance details page.

3. Click the **Listener information** tab. Click the name of the listener whose port is 443 to view the listener details. You can see that mutual authentication has been enabled for the listener.


<span id="RhVmFJPT"></span>
### Testing the connections to services

<div data-tips="true" data-tips-type="tip">Description</div>


<div data-tips="true" data-tips-type="tip">Before verification, make sure that you have deployed backend applications and services in the cluster. This example uses the nginx image and the path <code>/</code>. For deployment steps, see <a href="https://docs.byteplus.com/en/docs/vke/Using-an-ALB-Ingress-to-deploy-an-application">Using ALB Ingresses for service deployment</a>.</div>



1. Run the following command to access the service by using the domain name.


```bash
curl -H "Host: example.com" https://180.xxx.xxx.xxx --insecure
```


The expected response is that the service is inaccessible because the request contains no client certificate for mutual authentication.

```HTML
<html>
<head><title>400 No required SSL certificate was sent</title></head>
<body bgcolor="white">
<center><h1>400 Bad Request</h1></center>
<center>No required SSL certificate was sent</center>
</body>
</html>
```



2. Run the following command to access the service with the client certificate and key.


```Bash
curl -H "Host: example.com" https://180.xxx.xxx.xxx --insecure --cert client.crt --key client.key
```


The expected response is that the service is accessible because the request contains a valid client certificate for mutual authentication.

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


<span id="f78wHuDl"></span>
###
