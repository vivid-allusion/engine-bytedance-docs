---
title: "Migrating from NGINX Ingresses to ALB Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Migrating_from_NGINX_Ingresses_to_ALB_Ingresses"
---

As the Ingress NGINX Controller has entered the retirement process, continuing to use NGINX Ingresses will gradually introduce risks to scalability, security, and stability. To ensure business security, we recommend promptly migrating from NGINX Ingresses to other Ingress alternatives. This topic describes how to safely migrate from NGINX Ingresses to ALB Ingresses.

<span id="W7tuQeI7"></span>
## Background

<span id="JtymaHAk"></span>
### Issues caused by the EOM of NGINX Ingresses

NGINX Ingress maintenance will be discontinued soon (see [[Product announcement] NGINX Ingress EOM](https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM) for details). Continued use of NGINX Ingresses will lead to the following problems:


* **Security risks**: No future security patches will be available. As a result, your applications are exposed to unfixed vulnerabilities.

* **Functional bottlenecks**: No new features will be developed. This makes it difficult to support business needs for complex scenarios such as advanced API governance (rate limiting, circuit breaking, and so on) and multi\-protocol support (gRPC and WebSocket).

* **Long\-term stability risks**: Lack of official technical support will make it challenging to resolve issues quickly, affecting business continuity.


<span id="XVnNSJ0k"></span>
### Feasibility of ALB Ingresses as an alternative

BytePlus Application Load Balancer (ALB) is a cloud\-based load balancing product used for Layer 7 business scenarios. In a VKE cluster, compared with the traditional Nginx Ingress, the ALB Ingress features the following core advantages:


* **Higher capacity and stronger protocol support**: A single instance can handle millions of QPS and natively supports multiple application\-layer protocols, such as HTTP, HTTPS, HTTP/2, WebSocket, and QUIC. Therefore, it adapts to complex business scenarios, such as e\-commerce, audio and video, and high\-traffic scenarios. It significantly outperforms the community\-based Nginx Ingress solution in throughput capacity and protocol coverage.

* **Fully managed service without manual O&M**: ALB is the official managed service of BytePlus. The version updates, feature upgrades, and infrastructure maintenance of ALB are managed by the platform in a central manner. You only need to use standard Kubernetes Ingress rules and annotations to manage traffic, without the need to perform O&M on gateway add\-ons. Compared with the traditional Nginx Ingress, which relies on community version iterations and requires you to maintain version upgrades and troubleshoot issues, the ALB Ingress greatly reduces the costs of long\-term O&M.

* **Native Kubernetes ecosystem integration**: In a VKE cluster, the ALB Ingress can function as a replacement for the Kubernetes native Nginx Ingress. The ALB Ingress can quickly associate services within the cluster with ALB instances, and you do not need to develop or deploy additional gateway add\-ons. The ALB Ingress can effectively improve the overall traffic stability and service availability of the cluster by leveraging the high\-performance forwarding capabilities and comprehensive advanced routing features of ALB.

* **Comprehensive observability capabilities**: ALB natively provides complete Layer 7 access logs, including core fields such as the client IP, request path, server response status, and latency. These logs can be integrated with TLS for user behavior analysis, refined O&M, and quick fault location. You do not need to deploy additional log collection add\-ons.


<span id="PZ49Xxjd"></span>
### **Automatically converted annotations**

When you use the automatic migration tool to migrate Nginx Ingresses in a cluster, the migration tool automatically converts the Nginx Ingress annotations listed in the following table to ALB Ingress annotations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Nginx Ingress annotations that are not listed in the following table will be retained during conversion and displayed in the conversion results. Check whether the settings of the ALB Ingress meet your expectations after the conversion is complete, and whether any Nginx Ingress annotations that are not converted exist. This prevents inconsistencies between the settings after the conversion and your business requirements.</div>


* <div data-tips="true" data-tips-type="warning">For a detailed description of ALB Ingress annotations, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-an-ALB-Ingress-using-annotations">Using annotations to configure ALB Ingresses</a>.</div>




|**Feature** |**Original Nginx Ingress annotation** |**ALB annotation after conversion** |
|---|---|---|
|Scheduler<br><br> |`nginx.ingress.kubernetes.io/load-balance`<br><br> |`ingress.vke.volcengine.com/loadbalancer-scheduler` |
|CORS |`nginx.ingress.kubernetes.io/enable-cors` |```Bash```<br>```ingress.vke.volcengine.com/loadbalancer-actions.{{service-name}}: \|  ```<br>```      [```<br>```            {```<br>```                "type": "Cors",```<br>```                ...```<br>```                 }```<br>```            }```<br>```      ]```<br> |
||`nginx.ingress.kubernetes.io/cors-allow-methods` ||
||`nginx.ingress.kubernetes.io/cors-allow-origin` ||
||`nginx.ingress.kubernetes.io/cors-max-age` ||
||`nginx.ingress.kubernetes.io/cors-allow-headers` ||
|Redirect |`nginx.ingress.kubernetes.io/ssl-redirectnginx.ingress.kubernetes.io/force-ssl`<br><br> |```Bash```<br>```ingress.vke.volcengine.com/loadbalancer-actions.{{service-name}}: \|  ```<br>```      [```<br>```            {```<br>```                "type": "Redirect",```<br>```                ...```<br>```                 }```<br>```            }```<br>```      ]```<br> |
|Rewrite |`nginx.ingress.kubernetes.io/rewrite-target` |```Bash```<br>```ingress.vke.volcengine.com/loadbalancer-actions.{{service-name}}: \|  ```<br>```      [```<br>```            {```<br>```                "type": "Rewrite",```<br>```                ...```<br>```                 }```<br>```            }```<br>```      ]```<br> |
|Protocol |`nginx.ingress.kubernetes.io/backend-protocol` |`ingress.vke.volcengine.com/loadbalancer-protocol` |


<span id="2cSvW8Ep"></span>
## Migration process

Assume that you have deployed a business application in a VKE cluster and configured an NGINX Ingress that contains domain and path forwarding policies. You also have configured DNS to resolve a custom domain name (example.com). The NGINX Ingress will forward client\-initiated requests targeting example.com to the Pod for the corresponding Service based on the forwarding policies.

To align with your business development needs and considerations for maintainability and security, you decide to migrate from the NGINX Ingress to an ALB Ingress. To maintain business stability, the migration is expected to be complete without changing service domain names or backend service settings. In this scenario, you can deploy an ALB Ingress within the VKE cluster, configuring it with forwarding policies identical to those of the NGINX Ingress, and then perform traffic migration by adjusting the weight settings in DNS resolution.

When all traffic is transferred to the ALB Ingress after the migration, delete the NGINX Ingress resolution record from the DNS and the NGINX Ingress resource from the cluster. The entire migration is seamless and transparent to clients.

<span id="jf6AebGW"></span>
## Migration steps

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">We recommend migrating traffic during off\-peak business hours.</div>


* <div data-tips="true" data-tips-type="warning">Before migrating traffic, first compare the forwarding policies and functionality of the NGINX Ingress and ALB Ingress, and conduct thorough testing to ensure strict functional consistency. This practice helps prevent undesired influences on your business from the migration. If the capabilities or annotations supported by ALB do not meet your business requirements, <a href="https://console.byteplus.com/workorder/create?step=1">submit a ticket</a> or contact our technical support.</div>


* <div data-tips="true" data-tips-type="warning">Using ALB will incur fees. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Billing-rules">Billing rules</a>.</div>



<span id="WJ6fhGQE"></span>
### Step 1: Configure conversion

VKE clusters allow you to configure conversion from Nginx Ingresses to ALB Ingresses via an automatic conversion tool. The tool does not directly create available ALB resources. Instead, it reads the Nginx Ingress settings in the clusters and returns ALBInstance and Ingress YAML files for manual confirmation. After verifying the settings are correct, you manually apply them.

Procedure:


1. [Use kubectl to connect to the clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create the YAML file for the automatic conversion tool. This file includes the Job required to execute the conversion task and the corresponding RBAC permissions. The code of the sample `nginxingress2albconfig.yaml` file is as follows:

   ```YAML
   apiVersion: batch/v1
   kind: Job
   metadata:
     name: nginxingress2albconfig
     namespace: default
   spec:
     template:
       spec:
         containers:
         - name: nginxingress2albconfig
           image: open-registry-cn-beijing.cr.volces.com/vke/nginxingress2albconfig:v0.0.1
           command: ["./nginxingress2albconfig", "print"]
         restartPolicy: Never
         serviceAccount: nginxingress2albconfig
         serviceAccountName: nginxingress2albconfig
     backoffLimit: 4
   ---
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: system:nginxingress2albconfig
   rules:
   - apiGroups:
     - networking.k8s.io
     resources:
     - ingresses
     - ingressclasses
     verbs:
     - get
     - list
     - watch
     - update
     - create
     - patch
   ---
   apiVersion: v1
   kind: ServiceAccount
   metadata:
     name: nginxingress2albconfig
     namespace: default
   ---
   kind: ClusterRoleBinding
   apiVersion: rbac.authorization.k8s.io/v1
   metadata:
     name: system:nginxingress2albconfig
   roleRef:
     apiGroup: rbac.authorization.k8s.io
     kind: ClusterRole
     name: system:nginxingress2albconfig
   subjects:
     - kind: ServiceAccount
       name: nginxingress2albconfig
       namespace: default
   ```
   

2. Run the following command to create the automatic conversion task.

   ```bash
   kubectl apply -f nginxingress2albconfig.yaml
   ```
   

   The expected output is as follows:

   ```Bash
   job.batch/nginxingress2albconfig created
   clusterrole.rbac.authorization.k8s.io/system:nginxingress2albconfig created
   serviceaccount/nginxingress2albconfig created
   clusterrolebinding.rbac.authorization.k8s.io/system:nginxingress2albconfig created
   ```
   

3. View the status of the pod executing the conversion task.

   ```Bash
   kubectl get pod -l job-name=nginxingress2albconfig
   ```
   

   The expected output is as follows. When `STATUS` of the Pod changes to `Completed`, it indicates that the configuration conversion task is complete.

   ```Bash
   NAME                           READY   STATUS      RESTARTS   AGE
   nginxingress2albconfig-6m***   0/1     Completed   0          11s
   ```
   

4. Run the following command to view the logs of the Pod for the configuration conversion task and obtain the final ALB configuration file. Replace `nginxingress2albconfig-6m***` with the actual Job name.

   ```Bash
   kubectl logs nginxingress2albconfig-6m***
   ```
   

   The expected result is as follows. The automatic conversion tool will return a detailed configuration overview, the ALBInstance settings, and the Ingress rules after conversion.

   ```Bash
   === ALBInstance configuration ===
   apiVersion: loadbalancer.vke.volcengine.com/v1beta1
   kind: ALBInstance
   metadata:
     name: from-nginx
   spec:
     instance:
       name: from-nginx
       edition: Standard
       zoneMappings:
         - subnetId: subnet-xxx # The cluster subnet ID. The ALB instance has a private IP address within the subnet block in this availability zone.
         - subnetId: subnet-yyy # The cluster subnet ID. The ALB instance has a private IP address within the subnet block in this availability zone.
     listeners:
       - port: 80
         protocol: HTTP
       - port: 443
         protocol: HTTPS
         certificateSource: cert_center # The listener certificate source.
         certificateID: cert-**** # The server certificate bound to the domain name.
   
   === Ingresses configuration ===
   
   --- Ingress 1 --->
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     annotations:
       ingress.vke.volcengine.com/loadbalancer-actions.service-demo: |-
         [
           {
             "corsConfig": {
               "allowHeaders": [
                 "CT"
               ],
               "allowMethods": [
                 "GET"
               ],
               "allowOrigin": [
                 "*"
               ],
               "maxAge": 7777
             },
             "type": "Cors"
           },
           {
             "rewriteConfig": {
               "path": "/${2}"
             },
             "type": "Rewrite"
           },
           {
             "redirectConfig": {
               "httpCode": "308",
               "port": 443,
               "protocol": "HTTPS"
             },
             "type": "Redirect"
           }
         ]
       ingress.vke.volcengine.com/loadbalancer-backend-protocol: tcp
       nginx.ingress.kubernetes.io/permanent-redirect: https://www.volcengine.com # Nginx Ingress annotations that do not support automatic conversion.
     creationTimestamp: null
     labels: {}
     name: alb-nginx-ingress
     namespace: default
   spec:
     ingressClassName: from-nginx
     rules:
       - host: example.com
         http:
           paths:
             - backend:
                 service:
                   name: service-demo
                   port:
                     name: use-annotation
               path: /
               pathType: Prefix
     tls: []
   ```
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Nginx Ingress annotations that do not support automatic conversion will be retained during conversion and displayed in the conversion results. For example, <code>nginx.ingress.kubernetes.io/permanent-redirect: https://www.volcengine.com</code> in this example. Check whether the settings of the ALB Ingress meet your expectations after the conversion is complete. This prevents inconsistencies between the settings after the conversion and your business requirements.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b41e7cc4e41a4ba3979069e87782a3a0.png" width="884px" />   </div>
   

&nbsp;

<span id="XRq3BO2i"></span>
### Step 2: Create an ALB Ingress

After confirming that the YAML file generated in the automatic conversion tool log is correct:


1. Copy the ALBInstance settings from the log and save them as the `alb-instance.yaml` file. Set the `subnetId`, `certificateID`, and other parameters to actual values.

   ```YAML
   apiVersion: loadbalancer.vke.volcengine.com/v1beta1
   kind: ALBInstance
   metadata:
     name: from-nginx
   spec:
     instance:
       name: from-nginx
       edition: Standard
       zoneMappings:
         - subnetId: subnet-iiv1ux50my*** # The cluster subnet ID. The ALB instance has a private IP address within the subnet block in this availability zone.
         - subnetId: subnet-iiv23muxjo*** # The cluster subnet ID. The ALB instance has a private IP address within the subnet block in this availability zone.
     listeners:
       - port: 80
         protocol: HTTP
       - port: 443
         protocol: HTTPS
         certificateSource: cert_center # The listener certificate source.
         certificateID: cert-bfe8f*** # The server certificate bound to the domain name.
   
   ```
   

2. Run the following command to apply the ALBInstance settings to the cluster.

   ```Bash
   kubectl apply -f alb-instance.yaml
   ```
   

3. Copy the Ingress settings from the log and save them as the `alb-ingress.yaml` file.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     annotations:
       ingress.vke.volcengine.com/loadbalancer-actions.service-demo: |-
         [
           {
             "corsConfig": {
               "allowHeaders": [
                 "CT"
               ],
               "allowMethods": [
                 "GET"
               ],
               "allowOrigin": [
                 "*"
               ],
               "maxAge": 7777
             },
             "type": "Cors"
           },
           {
             "rewriteConfig": {
               "path": "/${2}"
             },
             "type": "Rewrite"
           },
           {
             "redirectConfig": {
               "httpCode": "308",
               "port": 443,
               "protocol": "HTTPS"
             },
             "type": "Redirect"
           }
         ]
       ingress.vke.volcengine.com/loadbalancer-backend-protocol: tcp
     creationTimestamp: null
     labels: {}
     name: alb-nginx-ingress
     namespace: default
   spec:
     ingressClassName: from-nginx
     rules:
       - host: example.com
         http:
           paths:
             - backend:
                 service:
                   name: service-demo
                   port:
                     name: use-annotation
               path: /
               pathType: Prefix
     tls: []
   
   ```
   

4. Run the following command to apply the ALB Ingress settings to the cluster.

   ```Bash
   kubectl apply -f alb-ingress.yaml
   ```
   


<span id="c5C3UQ9X"></span>
### Step 3: Switch traffic

Assume that before the migration, you have added an A record that points the domain name to the public address of the NGINX Ingress. At this point, you can add the IP address of the ALB instance to the original DNS record and enable load balancing. Then, adjust the DNS resolution weight to gradually switch traffic originally to the NGINX Ingress to the ALB Ingress.

In this topic, the DNS service on BytePlus is used for demonstration.


1. Log in to the [DNS console](https://console.byteplus.com/TrafficRoute/dns).

2. In the left navigation bar, click **Domain management**.

3. In the domain name list, click the target domain name to go to the domain name details page.

4. Edit the DNS record for the target domain name. Enable **Load balancing**, and add the IP address of the ALB instance in the **Record value** section, and then configure the weight.

5. After you complete the configuration, check whether DNS resolution and services function as expected.

   * DNS query: Use the dig or nslookup command to query the domain name.

      ```Bash
      dig example.com +short
      ```
      

      The expected result is as follows: The returned IP address list includes both the Nginx Ingress address and the ALB Ingress address.

      ```Bash
      118.xxx.xxx.xxx
      14.xxx.xxx.xxx
      ```
      

   * Business verification: Check whether the business traffic is forwarded as expected, and whether error codes or exceptions exist. Verify that traffic has been forwarded to the ALB Ingress, with no exceptions.

      1. Log in to the [ALB console](https://console.byteplus.com/alb).

      2. In the left navigation bar, click **Instance**. Click the name of the target instance to go to the instance details page.

      3. Click the **Monitoring information** tab. Check whether exceptions occur in the traffic of the ALB instance.

6. Gradually adjust the DNS resolution weight until all traffic has been forwarded to the ALB Ingress.


<span id="TmkOgSHD"></span>
### Step 4: Delete redundant resources

After traffic is forwarded by the ALB Ingress as expected and all persistent connections of the NGINX Ingress are processed, you can monitor traffic forwarding for a certain period of time. If no anomalies are detected, you can then delete redundant resources.


1. Delete or disable the DNS record of the NGINX Ingress. After the DNS time to live (TTL) has elapsed, all new requests will be routed to the ALB instance.

2. Delete the NGINX Ingress resource from the cluster. Only perform this after confirming that no traffic is on the NGINX Ingress via continuous monitoring using the [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability) feature of VKE [cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<span id="Bx3DYSbx"></span>
## Other considerations

<span id="6RWk8wtS"></span>
### **Common events**


* `listener is not exist in alb`: Indicates that the listener (such as 80/HTTP and 443/HTTPS) requested by the Ingress has not been created on the associated ALB instance. Check the definitions of listeners in the ALBInstance.

* `none certificate found for host`: Indicates that TLS is enabled for a domain name in the Ingress, but ALB cannot find a certificate that matches the domain name. Check whether the configurations of the certificate source, such as the Secret and automatic discovery, are valid and whether the certificate is valid.


<span id="aAp6cZ2a"></span>
### Incompatible annotations and features

During migration, you may encounter Nginx\-specific annotations or features that are not supported by the ALB Ingress. In this case, you can [submit a ticket](https://console.byteplus.com/workorder/create?step=1) or contact technical support.

<span id="nhINv8mh"></span>
### Rollback process

If an exception is detected during or after migration to the ALB instance, you can roll back the traffic migration. Rollback is the reverse process of migration, with the same basic principle: Achieving lossless rollback by changing the IP address in the DNS record from the IP address for the ALB instance to the one associated with the NGINX Ingress.


1. Gradually reduce the weight of DNS records pointing to ALB to 0, or directly restore the original Nginx Ingress DNS records.

2. Continuously monitor business access success rate, error code, latency, and backend service health status.

3. After you confirm that the rollback is complete and the business is stable, troubleshoot ALB configuration issues.
