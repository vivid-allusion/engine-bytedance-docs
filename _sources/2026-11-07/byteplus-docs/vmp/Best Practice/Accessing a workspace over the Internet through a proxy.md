---
title: "Accessing a workspace over the Internet through a proxy"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Using-proxy-to-connect-workspace-form-internet"
---

The workspace of Vital Managed Service for Prometheus (VMP) can be accessed over the Internet through a proxy. This topic describes how to create a proxy in a Vital Kubernetes Engine (VKE) cluster to access a workspace over the Internet.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

A VMP workspace offers a standard remote write URL and a standard query URL that can be accessed over internal networks. This allows you to collect service metrics and business metrics in the internal networks of the public cloud and deploy Grafana in a VKE cluster to create and view metric dashboards. For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

In some scenarios, you may need to access the data of a VMP workspace over the Internet. For example, in multi\-cloud scenarios, you need to aggregate data from multiple public clouds to Grafana for centralized viewing. In this case, you can configure a proxy in a VKE cluster to access the VMP workspace over the Internet.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created, and basic authentication has been enabled. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* A VKE cluster is created. For more details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The ingress\-nginx agent or a self\-built NGINX Ingress is installed in the cluster, and the corresponding Classic Load Balancer (CLB) instance is configured.

   * If you use the ingress\-nginx agent, you need to configure the corresponding CLB instance based on your business requirements when you install the agent. For example, set the **Load Balancing type** parameter to **Public network**, and set the Billing method parameter to **Pay\-as\-you\-go \- by bandwidth limit** or **Pay\-as\-you\-go \- by actual traffic** based on your business requirements. For more details, refer to the [ingress-nginx](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=) section of the Installing an add\-on topic.

   * For the configuration method of a self\-built NGINX Ingress in the cluster, refer to [Deploying multiple Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5L-d5a-G5a2X5YW4"></span>
### Step 1: Configure the Secret

To ensure communication security over the Internet, use HTTPS for communication between Grafana and VMP. Therefore, it is necessary to use a Secret to configure the SSL certificate and key used by HTTPS.


1. Obtain the SSL certificate and key. This topic takes `tls.key` and `tls.crt` as an example.

2. Use kubectl to connect to the target cluster and run the following command to create a Secret named grafana\-key of type `kubernetes.io/tls`:


```bash
kubectl create secret tls grafana-key --key tls.key --cert tls.crt
```


<span id=".5q2l6aqk5LqM77ya6YWN572u5pyN5Yqh5ZKM6Lev55Sx6KeE5YiZ"></span>
### Step 2: Configure a service and an Ingress


1. In the left navigation bar, click **Services and Ingresses** \> **Service**. Click **Create with Yaml** to create a service. You can access the VMP workspace by using a service of type `ExternalName`.


```yaml
apiVersion: v1
kind: Service
metadata:
  name: vmp-service
spec:
  externalName: query.prometheus-cn-beijing.ivolces.com # The domain name of the VMP workspace. Domain names of workspaces vary based on different regions.
  ports:
  - name: vmp
    port: 80
    protocol: TCP
    targetPort: 80
  sessionAffinity: None
  type: ExternalName
```



2. Click **Workload \> Resource Explorer** in the left navigation pane. Click **Create with Yaml** to create an Ingress. Specify the mapping relationship between the external domain name and the service.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml**field.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: vmp-ingress
spec:
  ingressClassName: nginx # The class name of the Ingress controller in the cluster. This field is used to select the Ingress instance.
  rules:
  - host: vmp-test.com # The custom domain name of the VMP workspace that can be accessed over the Internet.
    http:
      paths:
      - backend:
          service:
            name: vmp-service # The service name, which must be consistent with the service configuration.
            port:
              number: 80
        path: /
        pathType: Prefix
  tls:
  - hosts:
    - vmp-test.com # Specify the domain name to be encrypted.
    secretName: grafana-key # Specify the name of the Secret used by the Ingress.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to ensure the DNS resolution relationship between the custom domain name and the public IP address of the CLB instance for the Ingress in the public network environment.</div>


<span id=".5q2l6aqk5LiJ77ya5o6l5YWl5bel5L2c5Yy65pWw5o2u5rqQ"></span>
### Step 3: Integrate a workspace data source


1. Log in to Grafana in the public network.

2. Click **Connections \> Data sources** in the left navigation pane.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ded4dc33c39042fd34638b8d64e70621.png) </span>

3. Click **Add data source** to create a new data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e19addc9f3c41abf7ff61ed439c82eb0.png) </span>

4. On the Add data source page, click **Prometheus**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11943066b25290a5cced71f4e85d2006.png) </span>

5. In the HTTP section, paste the modified query URL of the workspace in the **Prometheus server URL** field.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to modify the original query URL of the workspace as follows:</div>



1. <div data-tips="true" data-tips-type="tip">Change the protocol to <code>https</code>.</div>


2. <div data-tips="true" data-tips-type="tip">Replace the domain name with the public domain name configured in the Ingress.</div>


3. <div data-tips="true" data-tips-type="tip">The values of other parameters remain unchanged.</div>



<div data-tips="true" data-tips-type="tip">For example, change the query URL to <code>https://vmp-test.com/workspaces/1c3***</code>.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c417fa43b481e687122dddf5be2dab09.png) </span>

6. Switch on **Basic auth** in the Auth section and configure the username and password used for workspace authentication in the **Basic Auth Details** section.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If your certificate is a self\-signed or other untrusted certificate, you also need to switch on <strong>Skip TLS Verify</strong>. Otherwise, Grafana will report a certificate verification error.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c26980757b58403ae677b02aec849af0.png) </span>

7. Click **Save & test** at the bottom of the page. When the message **Successfully queried the Prometheus API** is displayed, it indicates the data source is configured and the workspace is integrated with Grafana.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_694c3ab091976f68ac406eed6fc9b3b3.png) </span>

<span id=".5q2l6aqk5Zub77ya5Yib5bu65bm25p-l55yL5aSn55uY"></span>
### Step 4: Create and view a dashboard


1. Click **Dashboards** in the left navigation pane.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ba027d15557998dc6686a481ba09694.png) </span>

2. Click **New** to create or import an observability dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_67318dc44dbf40409adf4771ae1e1148.png) </span>

3. You can view valid monitoring information by using the dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c8f86a41e94525245c8ba91106d60e5.png) </span>


<span id=".55uR5o6n5ZKM6L-Q57u0"></span>
## Monitoring and O&M

The proxy is used to read and write data in the VMP workspace over the Internet. The read or write performance is closely related to the performance of the Ingress instance in the VKE cluster. It is recommended that you use the observability feature of the VKE cluster to monitor and perform O&M on the Ingress instance. You can refer to the following topics:


* [ingress-nginx monitoring](https://docs.byteplus.com/en/docs/vke/Ingress-observability)

* [Nginx Ingress best practices](https://docs.byteplus.com/en/docs/vke/Nginx-Ingress-best-practices)

* [Monitoring custom Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Best-practices-for-monitoring-custom-Nginx-Ingress-controllers)


<span id=".5Y-C6ICD5L-h5oGv"></span>
## References

<span id=".5aaC5L2V5L2_55SoIE9wZW5TU0wg5Yib5bu66Ieq562-5ZCN6K-B5Lmm"></span>
### Create a self\-signed certificate by using OpenSSL


1. In the local environment, visit the [OpenSSL official website](https://www.openssl.org/) and download and install OpenSSL.

2. Run the following command to generate a 2048\-bit RSA private key:


```bash
openssl genrsa -out tls.key 2048
```


The following section shows the expected response result.

```bash
Generating RSA private key, 2048 bit long modulus
........+++++
...+++++
e is 65537 (0x10001)
```



3. Run the following command to use the RSA private key to generate a certificate:


```bash
openssl req -new -key tls.key -out tls.csr
```


The following section displays the expected response. You need to enter information about the certificate, such as the country, region, organization name, domain name, and email address.

```bash
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:CN # The country code, such as CN.
State or Province Name (full name) []:Shanghai # The region name, such as Shanghai.
Locality Name (eg, city) []:Shanghai # The city name, such as Shanghai.
Organization Name (eg, company) []:vke # The organization name.
Organizational Unit Name (eg, section) []:vke # The unit name in the organization.
Common Name (eg, fully qualified host name) []:vmp-test.com # The domain name that corresponds to the certificate. Enter vmp-test.com for this example.
Email Address []:user@example.com # The email address.

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:mypassword # The password, which can be left empty.
```



4. Run the following command to sign the certificate with the private key and set the validity period of the signature to 365 days:


```bash
openssl x509 -req -in tls.csr -out tls.crt -signkey tls.key -days 365
```



5. The private key (tls.key) and certificate (tls.crt) required for HTTPS encryption are created.
