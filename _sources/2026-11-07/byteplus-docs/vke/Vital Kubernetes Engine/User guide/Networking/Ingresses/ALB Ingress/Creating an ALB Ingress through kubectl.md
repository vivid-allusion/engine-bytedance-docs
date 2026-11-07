---
title: "Creating an ALB Ingress through kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl"
---

An Application Load Balancer (ALB) Ingress, built on the BytePlus ALB, offers more comprehensive Layer 7 load balancing capabilities. This topic describes how to create an ALBInstance using a YAML file and configure an Ingress for the ALBInstance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

ALBInstances are CustomResourceDefinition (CRD) resources managed by the ALB Ingress Controller, which uses them to configure and monitor ALB instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An ALBInstance represents a single ALB instance managed by the controller and can be associated with multiple Ingress resources.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* To prevent Ingress exceptions, do not directly modify an ALB instance, its listeners, back\-end server groups, or forwarding rules managed by an ALB Ingress from the ALB console. Any such modifications are undertaken at your own risk.

* Do not modify any content prefixed with `k8s_` in the name of a listener or backend server group.

* Do not modify any content prefixed with `k8s_` in the description of a forwarding rule.

* Using the ALB console to modify resources and configurations specified or maintained by an ALB Ingress (for example, forwarding rules) may cause configurations to be overwritten.

* When the content of the `listeners` field in an ALBInstance changes, the system automatically adjusts and updates the listener and certificate.

* If multiple ALBInstances specify different certificates for the same domain name and a certificate already exists for that domain name, the system will decide whether to overwrite the existing certificate according to the status of the certificate specified by the respective ALBInstance:

   * If the certificate specified by the ALBInstance does not exist, the existing certificate will not be overwritten.

   * If the certificate specified by the ALBInstance has expired, the existing certificate will not be overwritten.

   * If the certificate specified by the ALBInstance exists and has not expired, the existing certificate will not be overwritten.

* Using ALB incurs fees for the use of cloud infrastructure resources. For details, see [ALB billing](https://docs.byteplus.com/en/docs/clb/Billing-rules).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster have been created. For details, see[ Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The cluster has been connected. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* (Optional) If you want to create an ALB Ingress that uses HTTPS, a certificate has been created. For details, see [Configuring ALB Ingresses over HTTPS](https://docs.byteplus.com/en/docs/vke/ALB_Ingress_configuring_the_HTTPS_protocol).


<span id=".5Yib5bu6LWFsYmluc3RhbmNl"></span>
## Creating ALBInstances

<span id=".5a-55o6l5bey5pyJLWFsYi3lrp7kvos="></span>
### Associating with existing ALB instances

Create an ALBInstance and associate it with an existing ALB instance by using a YAML file. The following file is an example:

```yaml
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb # The name of the ALBInstance.
spec:
  instanceID: "alb-2dgns526uiv41fi5***" # The ID of an existing ALB instance.
  listeners:
  - protocol: "HTTP" # The protocol for the listener.
    port: 80 # The port used for HTTP listeners.
  - protocol: "HTTPS" # The protocol for the listener.
    port: 443 # The port used for HTTPS listeners.
    certificateSource: "alb" # Listener certificate source. Valid values: alb
    certificateID: "cert-2wx20lm7uquww7oot***" # The server certificate used by all domains for HTTPS listeners.
    domainExtensions:
    - domain: "example.com" # A separate server certificate can be specified for a domain for HTTPS listeners.
      certificateSource: "alb" # Listener certificate source. Valid values: alb
      certificateID: "cert-2wx20lo6vuww07oot***" # A separate server certificate can be specified for a domain for HTTPS listeners.
    enableHTTP2: false
    enableQUIC: false
```


The parameters under `spec` are listed below.


|Parameter |Type |Required |Description |Sample value |Changeable |
|---|---|---|---|---|---|
|instanceID |String |Yes |The ID of an existing ALB instance. |alb\-2dgns526uiv41fi5\*\*\* |No |
|listeners.protocol |String |No |The listener protocol. Valid values:<br><br><br>* **HTTP** (Default value)<br><br>* **HTTPS** |HTTP |Yes |
|listeners.port |Integer |No |Listener port. Valid values:<br><br><br>* Value range: 1–65535<br><br>* Default value: 80 ( HTTP)  and 443 (HTTPS) |80 |Yes |
|listeners.certificateSource |String |No |The source of the default certificate for the listener. Valid values:<br><br><br>* **alb**: The certificate is managed by ALB. |alb |Yes |
|listeners.certificateID |String |No |The ID of the default certificate for the listener. |cert\-2wx20lm7uquww7\*\*\* |Yes |
|listeners.domainExtensions.domain |String |No |The associated extension domain. A wildcard domain can be specified. |example.com |Yes |
|listeners.domainExtensions.certificateSource |String |No |The source of the certificate for the extension domain.  Valid values:<br><br><br>* **alb**: The certificate is managed by ALB. |alb |Yes |
|listeners.domainExtensions.certificateID |String |No |The ID of the certificate of the extension domain for the HTTPS listener. |cert\-2wx20lo6vuww07\*\*\* |Yes |
|listeners.enableHTTP2 |Boolean |No |Whether to enable HTTP/2. This parameter is only valid for HTTPS listeners. Valid values:<br><br><br>* **true**: Enable HTTP/2.<br><br>* **false**: (Default value) Disable HTTP/2. |false |Yes |
|listeners.enableQUIC |Boolean |No |Whether to enable QUIC. This parameter is only valid for HTTPS listeners. Valid values:<br><br><br>* **true**: Enable QUIC.<br><br>* **false**: (Default value) Disable QUIC.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is a beta feature from ALB. To use it, contact your account manager to get a trial.</div><br> |false |Yes |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you create a listener that uses the HTTPS protocol, create an HTTPS certificate first. For details, see <a href="https://docs.byteplus.com/en/docs/vke/ALB_Ingress_configuring_the_HTTPS_protocol">Configuring ALB Ingresses over HTTPS</a>.</div>


<span id=".5paw5bu6LWFsYi3lrp7kvos="></span>
### Creating ALB instances

Create an ALBInstance and an ALB instance by using a YAML file.

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
    - subnetId: "subnet-bp12mw1f8k3jg1****" 
    addressType: "public" # The load balancing type. Possible values: public for the public network type and private for the private network type.
    eipSpec:
      isp: "BGP" # Line type for EIP of an Internet-accessible LoadBalancer instance. Value: BGP
      bandwidth: 10 # Bandwidth limit. When billingType is 2, the valid range is 1–500 Mbps. When billingType is 3, the valid range is 1–200 Mbps.
      billingType: 2 # Billing type. Value: 2 (Pay-as-you-go - by bandwidth limit) or 3 (Pay-as-you-go - by actual traffic)
      bandwidthPackageID: "bwp-2d63yyj3ki4u858oz***" # The ID of the shared bandwidth package.
    ipVersion: "ipv4" # The IP version. Value: ipv4
    deleteProtection: "on" # Deletion protection configuration of the ALB instance. The value on indicates that deletion protection is enabled. The value off indicates that deletion protection is disabled.
  blockCascadeDeletion: true # Whether to delete the ALBInstance when the ALB Ingress is deleted.
  listeners:
  - protocol: "HTTP" # The protocol for the listener.
    port: 80 # The port used for HTTP listeners.
  - protocol: "HTTPS" # The protocol for the listener.
    port: 443 # The port used for HTTPS listeners.
    certificateSource: "alb" # Listener certificate source. Valid values: alb 
    certificateID: "cert-2wx20lm7uquww7oot********" # The server certificate used by all domains for HTTPS listeners.
    domainExtensions:
    - domain: "test.com" # A separate server certificate can be specified for a domain for HTTPS listeners.
      certificateSource: "alb" # Listener certificate source. Valid values: alb 
      certificateID: "cert-2wx20lo6vuww07oot********" # A separate server certificate can be specified for a domain for HTTPS listeners.
    enableHTTP2: false
    enableQUIC: false
```


The parameters under `spec` are listed below.


|Parameter |Type |Required |Description |Sample value |Changeable |
|---|---|---|---|---|---|
|instance.name |String |Yes |The name of the ALB instance. |alb |No |
|instance.zoneMappings.N.subnetId |String |Yes |The ID of the subnet. The ALB instance will have a private IP address within the specified subnet.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can configure multiple subnets.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The subnets cannot be located in the same availability zone (AZ).</div><br> |subnet\-bp12mw1f8k3jg0\*\*\* |No |
|instance.addressType |String |No |The network type of the ALB instance. Valid values:<br><br><br>* **public** (default value):  Public network<br><br>* **private**: Private network |public |No |
|instance.eipSpec.isp |String |No |The line type for the publicly\-accessible Elastic IP Address (EIP) assigned to the ALB instance. The available types include BGP, SingleLine_BGP, Static_BGP, Fusion_BGP, ChinaMobile, ChinaTelecom, ChinaUnicom, ChinaMobile_Value, ChinaUnicom_Value, and ChinaTelecom_Value. For details, see [EIP documentation](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Except for <strong>BGP</strong>, all the line types are beta features of EIP products. To apply for use of these features, please contact your account manager.</div><br> |BGP |No |
|instance.eipSpec.bandwidth |Integer |No |The peak bandwidth of the EIP of the ALB instance.<br><br><br>* When `instance.eipSpec.billingType` is set to 2, the valid range is 1 Mbps to 500 Mbps.<br><br>* When `instance.eipSpec.billingType` is set to 3, the valid range is 1 Mbps to 200 Mbps.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have applied for an increase in the bandwidth limit, the maximum peak bandwidth also increases. For details, see <a href="https://docs.byteplus.com/en/docs/eip/Limits">EIP limits</a>.</div><br> |10 |No |
|instance.eipSpec.billingType |Integer |No |The billing method of the EIP for the ALB instance. Valid values:<br><br><br>* **2**: (default) The billing method is "Pay\-as\-you\-go \- Billing by bandwidth cap."<br><br>* **3**: The billing method is "Pay\-as\-you\-go \- by actual traffic." |2 |No |
|instance.eipSpec.bandwidthPackageID |String |No |ID of the shared bandwidth package. |\- |Yes |
|instance.ipVersion |String |No |The IP version. The value is ipv4. |IPv4 |No |
|instance.deleteProtection |String |No |Whether to enable deletion protection for the ALB instance. Valid values:<br><br><br>* **on**<br><br>* **off** |on |Yes |
|blockCascadeDeletion |Boolean |No |Whether to delete the corresponding ALBInstance when you delete an ALB Ingress. Valid values:<br><br><br>* **true**: When the ALB Ingress is deleted, the corresponding ALBInstance is not deleted.<br><br>* **false**: When the last ALB Ingress associated with an ALBInstance is deleted, the corresponding ALBInstance is also deleted.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not specify this parameter, the actual behaviour defaults to that of the <code>false</code> value, which deletes the ALBInstance when its last ALB Ingress is deleted.</div><br> |true |Yes |
|listeners.protocol |String |No |The listener protocol. Valid values:<br><br><br>* **HTTP** (default)<br><br>* **HTTPS** |HTTP |Yes |
|listeners.port |Integer |No |Listener port. Valid values:<br><br><br>* Value range: 1–65535<br><br>* Default value: 80 ( HTTP)  and 443 (HTTPS) |80 |Yes |
|listeners.certificateSource |String |No |The source of the default certificate for the listener. Valid values:<br><br><br>* **alb**: The certificate is managed by ALB. |alb |Yes |
|listeners.certificateID |String |No |The ID of the default certificate for the listener. |cert\-2wx20lm7uquww7\*\*\* |Yes |
|listeners.domainExtensions.domain |String |No |The associated extension domain. A wildcard domain can be specified. |example.com |Yes |
|listeners.domainExtensions.certificateSource |String |No |The source of the certificate for the extension domain.  Valid values:<br><br><br>* **alb**: The certificate is managed by ALB. |alb |Yes |
|listeners.domainExtensions.certificateID |String |No |The ID of the certificate of the extension domain for the HTTPS listener. |cert\-2wx20lo6vuww07\*\*\* |Yes |
|listeners.enableHTTP2 |Boolean |No |Whether to enable HTTP/2. This parameter is only valid for HTTPS listeners. Valid values:<br><br><br>* **true**: Enable HTTP/2.<br><br>* **false**: (Default value) Disable HTTP/2. |false |Yes |
|listeners.enableQUIC |Boolean |No |Whether to enable QUIC. This parameter is only valid for HTTPS listeners. Valid values:<br><br><br>* **true**: Enable QUIC.<br><br>* **false**: (Default value) Disable QUIC.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is a beta feature from ALB. To use it, contact your account manager to get a trial.</div><br> |false |Yes |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you create a listener that uses the HTTPS protocol, create an HTTPS certificate first. For details, see <a href="https://docs.byteplus.com/en/docs/vke/ALB_Ingress_configuring_the_HTTPS_protocol">Configuring ALB Ingresses over HTTPS</a>.</div>


<span id="z5r4L1er"></span>
### Configuring access log delivery

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you configure access log delivery for an ALB instance, consider the following items:</div>



* <div data-tips="true" data-tips-type="default">The alb\-ingress\-controller add\-on has been installed and upgraded to version v0.31.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


* <div data-tips="true" data-tips-type="default">A log project and a log topic have been created. For details, see <a href="https://docs.byteplus.com/en/docs/tls/Managing_projects">Log projects</a> and <a href="https://docs.byteplus.com/en/docs/tls/Managing_topics">Log topics</a>.</div>


* <div data-tips="true" data-tips-type="default">You can configure access log delivery for an existing ALB instance in the <a href="https://console.byteplus.com/alb">ALB console </a>.</div>



When you create an ALB instance by using an ALBInstance, you can configure access log delivery for the ALB instance by using the `tlsAccessLogConfig` field in `spec.instance`. After you enable access log delivery, access logs of the instance will be delivered to TLS. When the `tlsAccessLogConfig` field is not configured, VKE does not modify the configuration on the ALB side. This section uses an ALB instance in the private network for demonstration:

```yaml
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb # The name of the ALBInstance.
spec:
  instance:
    name: "demo-alb" # The name of the ALB instance.
    zoneMappings: # The list of subnets in multiple availability zones where ALB instances are located.
    - subnetId: "subnet-22joc5bb2gnpc7r2***" # The subnet ID. The ALB instance has a private IP address within the subnet block in this availability zone.
    addressType: "private" # The load balancing type. Possible values: public for the public network type and private for the private network type.
    tlsAccessLogConfig: # Log delivery configuration for the ALB instance.
      tlsAccessLogEnabled: "on" # Log delivery switch. Values: on and off.
      tlsProjectID: "1155d3bb-4a85-4208***" # Log project ID.
      tlsTopicID: "7b0aa3b3-5d46-47e0-9a37***" # Log topic ID.
  blockCascadeDeletion: true # Whether to delete the ALBInstance when the ALB Ingress is deleted.
  listeners:
  - protocol: "HTTP" # The protocol for the listener.
    port: 80 # The port used for HTTP listeners.
```


The following table describes fields in `tlsAccessLogConfig` of the `spec.instance`.


|Parameter |Type |Required |Description |Sample value |Changeable |
|---|---|---|---|---|---|
|tlsAccessLogEnabled |String |Yes |Whether to enable access log delivery for the ALB instance. Valid values:<br><br><br>* **on**: Enable access log delivery.<br><br>* **off**: Disable access log delivery. |on |Yes |
|tlsTopicID |String |No |The ID of the log project.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>tlsAccessLogEnabled</code> is <code>on</code>, this field must be configured.</div><br> |76fa2b9b\-73e4\-4d8b\-9528\-a4b000\*\*\* |Yes |
|tlsProjectID |String |No |The ID of the log topic.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>tlsAccessLogEnabled</code> is <code>on</code>, this field must be configured.</div><br> |7bcd0f1b\-be4a\-4e47\-b103\-51a3f\*\*\* |Yes |


<span id="MDbmVlWs"></span>
### Configuring ACLs for listeners

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you configure ACLs for listeners of ALB instances, consider the following items:</div>



* <div data-tips="true" data-tips-type="default">The alb\-ingress\-controller add\-on has been installed and upgraded to version v0.31.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


* <div data-tips="true" data-tips-type="default">Access control policy groups have already been configured. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Access-control">Access control</a>.</div>



When you use an ALBInstance to associate with an existing ALB instance or create a new ALB instance, you can configure an ACL for the listener by using the `aclConfig` field in `spec.listeners`. When the `aclConfig` field is not configured, VKE does not modify the configuration on the ALB side. This section demonstrates how to associate with an existing ALB instance. The following is an example:

```yaml
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb # The name of the ALBInstance.
spec:
  instanceID: "alb-2dgns526uiv41fi5***" # The ID of the existing ALB instance.
  listeners:
  - protocol: "HTTP" # The protocol for the listener.
    port: 80 # The port used for HTTP listeners.
    aclConfig: # The ACL for the listener.
      aclEnabled: "on" # ACL feature switch. Values: on and off.
      aclType: "white" # The ACL control mode. Values: white and black.
      aclIDs: # The ID of the policy group.
        - "acl-2tgv80851uku81***"
        - "acl-2tgv80660qiv41***"
...
```


The following table describes subfields in the `aclConfig` field of the `spec.listeners`.


|Parameter |Type |Required |Description |Sample value |Changeable |
|---|---|---|---|---|---|
|aclEnabled |String |Yes |Whether to enable access control for the listener. Valid values:<br><br><br>* **on**: Enable access control.<br><br>* **off**: Disable access control. |on |Yes |
|aclType |String |No |The access control mode. Valid values:<br><br><br>* **white**: Allowlist\-based access control. This mode allows access only from IP addresses within the selected policy group.<br><br>* **black**: Blocklist\-based access control. This mode denies access from IP addresses within the selected policy group.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>aclStatus</code> is <code>on</code>, this field must be configured.</div><br> |white |Yes |
|aclIDs |Array of String |No |The ID of the access policy group.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>aclStatus</code> is <code>on</code>, this field must be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A maximum of 5 policy groups can be configured. Each policy group can include up to 300 IP address entries. Each IP address entry can be an IP address or a CIDR address block. For more information about policy groups, see <a href="https://docs.byteplus.com/en/docs/clb/Access-control">Access control</a>.</div><br> |acl\-1 |Yes |


<span id="meJPdW5U"></span>
### Specifying a custom configuration for listeners

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you specify a custom listener configuration for an ALB instance, make sure that:</div>



* <div data-tips="true" data-tips-type="default">The alb\-ingress\-controller add\-on has been installed and upgraded to version v0.31.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


* <div data-tips="true" data-tips-type="default">A custom configuration has been created. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Custom-configurations">Custom configurations</a>.</div>



When you use an ALBInstance to associate with an existing ALB instance or create a new ALB instance, you can use the `customizedConfig` field in the `spec.listeners` configuration to specify a custom configuration for the ALB listener. When the `customizedConfig` field is not configured, VKE does not modify the configuration on the ALB side. A custom configuration allows you to create and manage standard NGINX configuration policies. For details, see [custom configurations](https://docs.byteplus.com/en/docs/clb/Custom-configurations). This section demonstrates how to associate with an existing ALB instance. The following is an example:

```yaml
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: ALBInstance
metadata:
  name: alb # The name of the ALBInstance.
spec:
  instanceID: "alb-2dgns526uiv41fi5***" # The ID of the existing ALB instance.
  listeners:
  - protocol: "HTTP" # The protocol for the listener.
    port: 80 # The port used for HTTP listeners.
    customizedConfig:
      customizedConfigEnabled: "on" # Custom configuration switch. Values: on and off
      customizedCfgID: "ccfg-2dbdimgq77sao3r***" # The ID of the custom configuration.
...
```


The following table describes subfields in the `customizedConfig` field of the `spec.listeners`.


|Parameter |Type |Required |Description |Sample value |Changeable |
|---|---|---|---|---|---|
|customizedConfigEnabled |String |Yes |Whether a custom configuration is specified. Valid values:<br><br><br>* **on**: A custom configuration is specified.<br><br>* **off**: No custom configuration is specified. |on |Yes |
|customizedCfgID |String |No |The ID of the custom configuration.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>customizedConfigEnabled</code> is <code>on</code>, this field must be configured.</div><br> |ccfg\-2dbdimgq77sao3r\*\*\* |Yes |


<span id=".5p-l55yLLWFsYmluc3RhbmNlLeWQjeensOWSjOeKtuaAgQ=="></span>
## Viewing the name and status of an ALBInstance

After you create an ALBInstance in the cluster, you can check the status of the ALBInstance by using the following steps.


1. Log in to the [VKE console ](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Workload \> Resource Explorer**.

5. On the **Resource Explorer** page, under the **CRD** category, click **albinstance**.

6. On the **albinstance** details page, view the resource name of the created ALBInstance.

7. In the **Actions** column, click **Edit Yaml** to view the details of the ALBInstance resource. The `status` field shows the status of the ALBInstance resource.

   The following table describes the meanings of different parameters in the `status` field.

   
   |Parameter |Type |Meaning |
   |---|---|---|
   |phase |String |The status of the ALBInstance resource:<br><br><br>* **Pending**: The associated ALBInstance has not yet been provisioned.<br><br>* **Running**: All configurations of the ALBInstance have been updated to the server side.<br><br>* **Configuring**: The ALBInstance is being configured.<br><br>* **Deleting**: The ALBInstance is being deleted. |
   |instanceID |String |The ID of the associated ALB instance. |
   |ingress |\*v1.LoadBalancerIngress |The IP address, listener port, and protocol of the ALB instance. |
   


<span id=".5Yib5bu6LWFsYi1pbmdyZXNz"></span>
## Creating ALB Ingresses

<span id=".5Z-65LqO5Z-f5ZCN6L2s5Y-R"></span>
### Forwarding based on domain names

An ALB Ingress supports forwarding requests from different domain names to different backends. The following `alb-ingress.yaml` file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: first.example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo-a # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
    - host: second.example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Valid values: Exact and Prefix.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo-b # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


<span id=".5Z-65LqO6Lev5b6E6L2s5Y-R"></span>
### Forwarding based on paths

An ALB Ingress supports forwarding access requests that come from the same domain but have different paths to different backends. The following `alb-ingress.yaml` file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # The domain name that is externally accessible.
      http:
        paths:
        - path: /foo # The path that matches the request.
          pathType: Prefix # The path matching rule. Default value: Prefix.
          backend:
            service:
              name: service-demo-a # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
        - path: /bar # The path that matches the request.
          pathType: Prefix # The path matching rule. Default value: Prefix.
          backend:
            service:
              name: service-demo-b # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


<span id=".6YWN572u5pyq5oyH5a6aLWhvc3Qt6KeE5YiZ"></span>
### Configuration without a specified host rule

An ALB Ingress supports a configuration without a specified host. The following `alb-ingress.yaml` file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: first.example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo-a # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
    - host: second.example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo-b # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
    - http:
       paths:
       - pathType: Prefix
         path: /
         backend:
           service:
             name: service-demo
             port:
               number: 80
```


<span id=".6YWN572u6buY6K6k6L2s5Y-R6KeE5YiZ55qE5ZCO56uv5pyN5Yqh5Zmo"></span>
### Configuring backend servers for the default forwarding rule

The following `alb-ingress.yaml` file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - http:
       paths:
       - pathType: Prefix
         path: /
         backend:
           service:
             name: service-demo
             port:
               number: 80
```


<span id=".5Yy56YWN5q2j5YiZ6KGo6L6-5byP6Lev5b6E"></span>
### Regular expression\-based path matching

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is in the beta stage for both VKE and ALB. To use it, <a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>submit a trial application</strong></a>.</div>


ALB Ingresses supports regular expression\-based paths and non\-regular expression paths, as shown in the following table.


|Path matching method |Description |
|---|---|
|Not a regular expression |* The value must start with a forward slash (`/`).<br><br>* The value can contain only letters, digits, and special characters `-`, `_`, `/`, `.`, `%`, `?`, `#`, `&=`. The value cannot contain `//`. |
|Regular expression |* The value must start with `/~` and can contain only one occurrence of `/~`.<br><br>* Supported characters include letters, digits and special characters `.`, `-`, `_`, `/`, `＝`,`?`, `~`, `^`, `*`,`$`, `:`, `()`, `[]`,`+`, `\|`.<br><br>* A leading `/~` indicates case\-sensitive regular expression matching, and a leading `/~*` indicates case\-insensitive regular expression matching. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use <code>/~</code> or <code>/~*</code> to configure a regular expression pattern in the path setting, when VKE passes the pattern to the ALB instance, it removes <code>/</code>. For example, when you specify the <code>/~/test/[a-z]*</code> pattern, the actual path pattern than ALB uses is <code>~/test/[a-z]*</code>. In this case, paths such as <code>/test/test</code> will match the regular expression pattern.</div>


The following `alb-ingress.yaml` file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress
  namespace: default 
spec:
  ingressClassName: alb
  rules:
    - host: example.com
      http:
        paths:
        - path: /~/test/[a-z]* # Use a regular expression for path matching.
          pathType: Prefix
          backend:
            service:
              name: service-demo
              port: 
                number: 80
```
