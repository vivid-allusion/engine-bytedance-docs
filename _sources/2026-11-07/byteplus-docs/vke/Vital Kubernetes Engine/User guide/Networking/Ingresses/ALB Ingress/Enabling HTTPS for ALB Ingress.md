---
title: "Enabling HTTPS for ALB Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ALB_Ingress_configuring_the_HTTPS_protocol"
---

To ensure communication security in public network environments, services are typically exposed to the public internet via Ingresses using the HTTPS protocol for communication. This topic explains how to configure an ALB Ingress that uses HTTPS.

<span id=".6K-B5Lmm6YWN572u5qaC6L-w"></span>
## Certificate configuration overview

<span id=".6K-B5Lmm5YiG57G7"></span>
### Certificate categories

From the perspective of HTTPS certificate coverage, Application Load Balancer (ALB) supports two types of certificates: default certificates and extension certificates. When a client establishes an HTTPS connection with ALB, ALB presents the appropriate certificate to the client.


|Certificate category |Configuration method |
|---|---|
|Default certificate |* Each HTTPS listener requires exactly one default certificate.<br><br>* No domain name is required on Ingress/albinstance.<br><br>* Updating is supported.<br><br>* Deletion is not supported. |
|Extension certificate |* Extension certificates are optional for creating an HTTPS listener. A listener can have multiple extension certificates.<br><br>* Domain names are specified on Ingress/albinstance.<br><br>* Updating is supported.<br><br>* Deletion is supported. |


ALB selects the certificate to send to the client based on the mapping between the domain name, forwarding rules, and certificate. For details on the process, see [Certificate matching](https://docs.byteplus.com/en/docs/clb/Configuring-SNI-for-an-HTTPS-listener).

<span id=".6K-B5Lmm6YWN572u5pa55byP"></span>
### Certificate configuration methods

In an VKE cluster, an ALB Ingress involves two major Kubernetes resources.


* **ALBInstance**: A custom resource for configuring ALB instances and listeners.

* **Ingress**: A standard Kubernetes object used to configure forwarding rules and backend servers on an ALB instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a detailed introduction to Ingress and ALBInstance resources, see <a href="https://docs.byteplus.com/en/docs/vke/Ingress-overview">Ingress overview</a>.</div>


You can configure a certificate independently by using either an ALBInstance or an Ingress:


* To configure a certificate by using an Ingress, specify the Secret containing the certificate information (the ID of the certificate uploaded to BytePlus or certificate key) in `Ingress.spec`.

* To configure a certificate by using an ALBInstance, specify the ID of the certificate uploaded to BytePlus in `albinstance.spec`.


An ALB Ingress supports three certificate configuration methods. The differences between each method and their applicable scenarios are shown in the table below.


|Configuration method |Certificate source |Application scenario |Certificate update method |
|---|---|---|---|
|Use the Secret that contains the certificate ID |ALB certificates |A certificate has already been purchased or uploaded via the ALB console. |Update the certificate ID in the Secret. |
|Use an ALBInstance to specify a certificate |ALB certificates |A certificate has already been purchased or uploaded via the ALB console. |Update the certificate ID on the ALBInstance. |


<span id=".6YWN572u56S65L6L"></span>
## Configuration examples

<span id=".6buY6K6k6K-B5LmmLXZzLeaJqeWxleivgeS5pg=="></span>
### Default certificates vs extension certificates

Configure a default certificate or an extension certificate by using an Ingress. The following content provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress-demo # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-port: "443" # Listening port.
    ingress.vke.volcengine.com/loadbalancer-protocol: "https"  # Listener protocol. In this example, the value is https.
spec:
  ingressClassName: alb  # The name of the ALB instance.
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
  tls:
  - secretName: https-secret-demo # The default certificate. No domain name required.
  - secretName: https-secret-demo-extension
    hosts:
    - example.com # (Optional) Extension certificates. You need to specify domain names to be protected.
```


Configure a default certificate or an extension certificate by using an ALBInstance. The following content provides an example:

```YAML
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb # The name of the ALBInstance.
spec:
  instance:
    name: "demo-alb" # The name of the ALB instance.
    zoneMappings: # The list of subnets in multiple availability zones where ALB instances are located.
    - subnetId: "subnet-bp12mw1f8k3jg0****" # The subnet ID. The ALB instance has a private IP address within the subnet block in this availability zone.
    addressType: "public" # The load balancing type. Possible values: public for the public network type and private for the private network type.
    eipSpec:
      isp: "BGP" # ISP type for EIP of an Internet-accessible LoadBalancer instance. Value: BGP
      bandwidth: 10 # Bandwidth limit. When billingType is 2, the valid range is 1–500 Mbps. When billingType is 3, the valid range is 1–200 Mbps.
      billingType: 2 # Billing type. Value: 2 (Pay-as-you-go - by bandwidth limit) or 3 (Pay-as-you-go - by actual traffic)
    ipVersion: "ipv4" # The IP version. Value: ipv4
    deleteProtection: "on" # Deletion protection configuration of the ALB instance. The value on indicates that deletion protection is enabled. The value off indicates that deletion protection is disabled.
  listeners:
  - protocol: "HTTPS" # The protocol for the listener.
    port: 443 # The port used for HTTPS listeners.
    certificateSource: "alb" # Certificate source. Valid values: alb.
    certificateID: "cert-2wx20lm7uquww7oot********" # The default certificate, which will be used by all domains for HTTPS listeners.
    domainExtensions:  # Extension certificates, which apply to individual domain names.
    - domain: "example.com" # A separate server certificate can be specified for a domain for HTTPS listeners.
      certificateSource: "alb" # Certificate source. Valid values: alb.
      certificateID: "cert-2wx20lo6vuww07oot********" # A separate server certificate can be specified for a domain for HTTPS listeners.
```


<span id=".c2VjcmV0LeaMh-WumuivgeS5pi1pZA=="></span>
### Use the Secret that contains the certificate ID

You can provide the certificate ID in the Secret, and then associate the Secret with the Ingress that you want to create. The example is as follows:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: https-secret-demo
type: Opaque
data:
  cert_id: Y2V***== # The Base64-encoded certificate ID in the Secret.
  cert_source: YWxi # The Base64-encoded certificate source. Valid values: YWxi for alb.
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress-demo # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-port: "443" # Listening port.
    ingress.vke.volcengine.com/loadbalancer-protocol: "https"  # Listener protocol. In this example, the value is https.
spec:
  ingressClassName: alb  # The name of the ALB instance.
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
  tls:
  - secretName: https-secret-demo # Associate the Secret with the Ingress.
  - hosts:
    - example.com # (Optional) Specify the domain name to be encrypted.
    secretName: https-secret-demo # Configure an extension certificate for the specified domain name by using the Secret.
```


<span id=".dGxzLeexu-Weiy1zZWNyZXQ="></span>
### Use a Secret of type TLS that contains the certificate content

You can enter the certificate content in the Secret, and then associate the Secret when configuring Ingress. The example is as follows:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: https-secret-demo
type: kubernetes.io/tls
data:
  # The certificate key and crt
  tls.key: |
        LS0tLS1CRUdJTiBSU0EgUFJJVkFURS*** # The Base64-encoded tls.key
  tls.crt: |
        LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS*** # The Base64-encoded tls.crt
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress-demo # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-port: "443" # Listening port.
    ingress.vke.volcengine.com/loadbalancer-protocol: "https"  # Listener protocol. In this example, the value is https.
spec:
  ingressClassName: alb  # The name of the ALB instance.
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
  tls:
  - secretName: https-secret-demo # Associate the Secret with the Ingress.
  - hosts:
    - example.com # (Optional) Specify the domain name to be encrypted.
    secretName: https-secret-demo # Configure an extension certificate for the specified domain name by using the Secret.
```


<span id=".5ZyoLWFsYmluc3RhbmNlLeS4iuaMh-WumuivgeS5pi1pZA=="></span>
### Specify a certificate ID in the ALBInstance

You can purchase or upload a certificate in the ALB console, and then specify the certificate ID in an ALBInstance configuration. The example is as follows:

```yaml
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb # The name of the ALBInstance.
spec:
  instance:
    name: "demo-alb" # The name of the ALB instance.
    zoneMappings: # The list of subnets in multiple availability zones where ALB instances are located.
    - subnetId: "subnet-bp12mw1f8k3jg0****" # The subnet ID. The ALB instance has a private IP address within the subnet block in this availability zone.
    addressType: "public" # The load balancing type. Possible values: public for the public network type and private for the private network type.
    eipSpec:
      isp: "BGP" # ISP type for EIP of an Internet-accessible LoadBalancer instance. Value: BGP
      bandwidth: 10 # Bandwidth limit. When billingType is 2, the valid range is 1–500 Mbps. When billingType is 3, the valid range is 1–200 Mbps.
      billingType: 2 # Billing type. Value: 2 (Pay-as-you-go - by bandwidth limit) or 3 (Pay-as-you-go - by actual traffic)
    ipVersion: "ipv4" # The IP version. Value: ipv4
    deleteProtection: "on" # Deletion protection configuration of the ALB instance. The value on indicates that deletion protection is enabled. The value off indicates that deletion protection is disabled.
  listeners:
  - protocol: "HTTPS" # The protocol for the listener.
    port: 443 # The port used for HTTPS listeners.
    certificateSource: "alb" # Certificate source. Valid values: alb.
    certificateID: "cert-2wx20lm7uquww7oot********" # The default certificate, which will be used by all domains for HTTPS listeners.
    domainExtensions:  # Extension certificates, which apply to individual domain names.
    - domain: "example.com" # A separate server certificate can be specified for a domain for HTTPS listeners.
      certificateSource: "alb" # Certificate source. Valid values: alb.
      certificateID: "cert-2wx20lo6vuww07oot********" # A separate server certificate can be specified for a domain for HTTPS listeners.
```


<span id=".6K-B5Lmm55Sf5pWI6YC76L6R"></span>
## Certificate selection logic

Certificates for ALB instances are configured at the listener level. Both Ingresses and ALBInstances can specify certificates for a listener. Therefore, a single listener may be associated with one ALBInstance and multiple Ingresses simultaneously. Certificates configured on these associated resources may differ. When certificate conflicts occur across multiple resources, **VKE selects the certificate with the ‌longest validity period‌ to associate with the ALB instance**.

For example, suppose that the port 80 listener of an ALB instance has certificates: A (configured by Ingress\-A), B (configured by Ingress\-B), and C (configured by Ingress\-C). If certificate C has the longest expiration validity period, VKE will pick certificate C for the ALB instance.

<span id=".5L6L5aSW5oOF5Ya1"></span>
## Exceptions

To prevent traffic interruption caused by accidental certificate deletion, VKE clusters implement special handling in the following two scenarios:


1. The system records the hash value of the certificate configuration on Kubernetes resources. When the hash value remains unchanged, the system does not proactively modify the certificate.


In addition to adding a certificate to ALB by using alb\-ingress\-controller during configuration of ALB Ingress or ALBInstance, you can also directly modify the certificate associated with listeners in the ALB console. To prevent manually added or deleted certificates from being overwritten by alb\-ingress\-controller during ALB Ingress or ALBInstance reconciliation, alb\-ingress\-controller uses certificate hashes for protection – it ‌never alters ALB certificate configurations if hashes remain consistent‌. The following table lists main scenarios and provides examples.


|Scenario |Example |
|---|---|
|When the hash value does not change, alb\-ingress\-controller does not proactively modify the certificate. |* When certificate A is configured on an ALB Ingress, alb\-ingress\-controller associates certificate A with the ALB instance and records the certificate hash value as hash\-a.<br><br>* You change the certificate to certificate B in the ALB console.<br><br>* When the ALB Ingress triggers reconciliation, alb\-ingress\-controller detects that the recorded hash (hash\-a) remains unchanged, so it skips the certificate modification step. As a result, the ALB instance remains associated with certificate B. |
|When the hash value changes, the alb\-ingress\-controller changes the certificate. |* When certificate A is configured on an ALB Ingress, alb\-ingress\-controller associates certificate A with the ALB instance and records the certificate hash value as hash\-a.<br><br>* You change the certificate to certificate B in the ALB console. <br><br>* When certificate C is included in the ALB Ingress, the alb\-ingress\-controller detects during reconciliation that the current certificate hash value for the ALB Ingress  is hash\-c, which differs from the previously recorded hash\-a. The controller then changes the associated certificate to certificate C. |



2. Certificates are ‌not deleted while the domain still has active forwarding rules‌. For example:

   * When you create an ALB Ingress, an extension certificate for example.com is configured. The associated certificates on the ALB instance are the default certificate and the extension certificate for example.com.

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: alb-ingress-demo # The name of the Ingress.
     namespace: default  # Namespace of the Ingress
     annotations:
       ingress.vke.volcengine.com/loadbalancer-port: "443" # Listening port.
       ingress.vke.volcengine.com/loadbalancer-protocol: "https"  # Listener protocol. In this example, the value is https.
   spec:
     ingressClassName: alb  # The name of the ALB instance.
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
     - host: another.com
       http:
         paths:
         - pathType: Prefix
           path: /
           backend:
             service:
               name: service-demo
               port:
                 number: 80                   
     tls:
     - secretName: https-secret-demo # The default certificate. No domain name required.
     - secretName: https-secret-demo-extension
       hosts:
       - example.com # (Optional) Extension certificates. You need to specify domain names to be protected.
   ```
   

   * If the certificate is removed from the ALB Ingress while the forwarding rules for example.com still exist, alb\-ingress\-controller ‌skips deletion‌ of the extension certificate on the ALB Ingress or ALBInstance to prevent traffic disruption. The extension certificate for example.com is only removed ‌after‌ its forwarding rules are deleted.

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: alb-ingress-demo # The name of the Ingress.
     namespace: default  # Namespace of the Ingress
     annotations:
       ingress.vke.volcengine.com/loadbalancer-port: "443" # Listening port.
       ingress.vke.volcengine.com/loadbalancer-protocol: "https"  # Listener protocol. In this example, the value is https.
   spec:
     ingressClassName: alb  # The name of the ALB instance.
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
     - host: another.com
       http:
         paths:
         - pathType: Prefix
           path: /
           backend:
             service:
               name: service-demo
               port:
                 number: 80                   
     tls:
     - secretName: https-secret-demo # The default certificate. No domain name required.
   ```
   


<span id=".dmtlLeaOp-WItuWPsOWSjC15YW1sLeeUqOazleeahOWMuuWIqw=="></span>
## Differences between using the VKE console and YAML

You can edit resources such as ALB Ingress, ALBInstance, and Secret by using YAML or the VKE console. The main differences are as follows:


* When you configure a certificate for example.com through the VKE console, the certificate ID is ‌automatically synchronized‌ to the ALBInstance. Removing the certificate for example.com ‌simultaneously deletes‌ the certificate ID from the ALBInstance.

* When you configure a certificate for example.com by editing the ALB\-Ingress YAML, the certificate ID is ‌not automatically updated‌ on the ALBInstance. Removing the certificate ‌does not delete‌ the certificate ID from the ALBInstance.


<span id="faq"></span>
## FAQ

<span id=".5Li65LuA5LmI5ZyoLXZrZS3mjqfliLblj7Dnp7vpmaTkuobmianlsZXor4HkuablkI7vvIzmianlsZXor4Hkuabku43nhLbnu5HlrprlnKgtYWxiLeS4ig=="></span>
### Why does the extension certificate remain bound to the ALB instance after it was removed through the VKE console?

There may be two reasons:


1. Some active forwarding rules on the Ingress still reference the extension certificate. As a result, the alb\-ingress\-controller skips removal of the extension certificate.

   1. Solution: If you confirm that the certificate is no longer needed, manually delete the extension certificate in the ALB console.

2. The ALBInstance YAML was edited and still records the ID of the extension certificate.

   1. Solution: If you confirm that the certificate is no longer needed, remove the extension certificate from the ALBInstance YAML file.


<span id=".5Li65LuA5LmILXZrZS3mjqfliLblj7Dmj5DnpLror4HkuabkuI3nrKblkIjpooTmnJ8="></span>
### Why does the VKE console indicate that the certificate is not as expected?

There are two possible reasons:


1. You modified the certificate directly in the ALB console, causing inconsistency between the ‌actual certificate on ALB‌ and ‌the Kubernetes resource.

   1. Solution: We recommend that you configure certificates on the VKE side and bind the intended certificate to the ALB Ingress.

2. When multiple ALB Ingresses with conflicting certificate configurations share the same ALB instance, the alb\-ingress\-controller selects the certificate with the ‌longest validity period‌ for the ALB instance. ALB Ingresses whose certificates weren't selected will show this warning.

   1. Solution: Maintain ‌consistent certificate configurations‌ across all ALB Ingresses for the same ALB instance.


<span id=".5pyA5L2z5a6e6Le1"></span>
## Best practices


* Do not combine VKE console operations with direct YAML edits when you configure certificates for the same instance.

* When configuring certificate in the VKE console, follow the on\-screen instructions.

   * The default certificate remains consistent across multiple Ingress resources.

   * Each Ingress manages different additional domain names and certificates.

   * ingress\-A

      * Default certificate A

      * www.a.com \-\> certificate b

   * ingress\-B

      * Default certificate a

      * www.b.com \-\> certificate c

* When configuring certificates by using YAML

   * If you have the certificate ID, specify the certificate ID on the ALBInstance.
