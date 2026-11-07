---
title: "Creating APIG Ingresses by using kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Create_an_APIG_Ingress_using_kubectl"
---

Built based on BytePlus [API Gateway (APIG)](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), APIG Ingress functions as a managed cloud\-native gateway that achieves Ingress traffic management featuring high availability and scalability. This topic mainly describes how to create an APIGInstance by using a YAML file and how to configure the APIG Ingress.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Do not modify the configurations of the APIG instance that is maintained by the APIG Ingress in the APIG console without authorization. Otherwise, Ingress services in the cluster may become abnormal, and you will be responsible for the consequences.

* If you modify resources or configurations specified or maintained by the APIG Ingress in the APIG console, the configurations may be overwritten.

* Using APIG products will incur resource fees.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The APIG service has been activated. If the service is not activated, log in to [APIG console](https://console.byteplus.com/veapig) and activate the service based on the on\-screen prompts.

* The apig\-controller add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A KubeConfig for private networks has been generated in the cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* (Optional) If you need to connect to an existing APIG instance, ensure that an instance in the **Running** status exists on the APIG console. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* To use the monitoring feature, make the following preparations:

   * The Vital Managed Service for Prometheus (VMP) service has been activated.

   * In the region where APIG is deployed, a [VMP workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces) has been created.

* To use the log feature, make the following preparations:

   * The Torch Log Service (TLS) service has been activated.

   * A log project and a log topic have been created. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).


<span id=".5Yib5bu6LWFwaWdpbnN0YW5jZQ=="></span>
## Creating APIGInstances

<span id=".5a-55o6l5bey5pyJLWFwaWct5a6e5L6L"></span>
### Connecting to existing APIG instances

Use the following YAML file to create an APIGInstance and connect to an existing APIG instance.

```YAML
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: APIGInstance
metadata:
  name: apig-instance-demo # APIGInstance resource name
spec:
  id: gcq12c2tfm0mpjrej4*** # The ID of the existing APIG instance.
  ingress:
    enable: true # Specify whether to enable APIG Ingress synchronization. Valid values: true and false.
    enableAllIngressClasses: false # Specify whether to synchronize all IngressClasses. Valid values: true and false.
    enableIngressWithoutIngressClass: false # Specify whether to synchronize Ingresses that are not associated with IngressClasses. Valid values: true and false.
    ingressClasses: # Specify the IngressClasses for which Ingress synchronization takes effect.
      - apig
    enableAllNamespaces: false # Specify whether to synchronize Ingresses in all namespaces. Valid values: true and false.
    watchNamespaces: # Specify the namespaces for which Ingress synchronization takes effect.
      - doc-demo
      - default
```


The parameters under `spec` are listed below.


|Parameter |Type |Required |Description |Sample value |Changeable |
|---|---|---|---|---|---|
|id |String |Yes |Specify an existing APIG instance ID. |gcq12c2tfm0mpjrej4\*\*\* |No |
|ingress.enable |Boolean |No |Specify whether to enable Ingress synchronization. After you enable the feature, only Ingresses within the synchronization scope will be synchronized to APIG. Valid values:<br><br><br>* **true**: Enables the Ingress synchronization feature. This value is used by default.<br><br>* **false**: Disables the Ingress synchronization feature. |true |No |
|ingress.enableAllIngressClasses |Boolean |No |Specify whether to synchronize all IngressClasses. Valid values:<br><br><br>* **true**: Synchronizes all IngressClasses.<br><br>* **false**: Only synchronizes the specified IngressClasses. This value is used by default. |true |No |
|ingress.enableIngressWithoutIngressClass |Boolean |No |Specify whether to synchronize Ingresses that are not associated with IngressClasses. Valid values:<br><br><br>* **true**: Synchronizes Ingresses that are not associated with IngressClasses.<br><br>* **false**: Does not synchronize Ingresses that are not associated with IngressClasses. This value is used by default. |true |No |
|ingress.ingressClasses |String |No |Specify the IngressClasses for which Ingress synchronization takes effect. You can enter multiple values or multiple IngressClasses. If this field is left empty, synchronization does not take effect.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>enableAllIngressClasses</code> is set to <code>false</code>, you need to specify this parameter to specify the IngressClass to which the Ingress to be synchronized belongs. Otherwise, synchronization does not take effect.</div><br> |apig |No |
|ingress.enableAllNamespaces |Boolean |No |Specify whether to synchronize all namespaces. Valid values:<br><br><br>* **true**: Synchronizes all namespaces.<br><br>* **false**: Only synchronizes the specified namespaces. This value is used by default. |true |No |
|ingress.watchNamespaces |String |No |Specify the namespaces for which Ingress synchronization takes effect. You can enter multiple namespaces. If this field is left empty, synchronization does not take effect.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>enableAllNamespaces</code> is set to <code>false</code>, you need to specify this parameter to specify the namespaces for which Ingress synchronization takes effect. Otherwise, synchronization does not take effect.</div><br> |default |No |


<span id=".5paw5bu6LWFwaWct5a6e5L6L"></span>
### Creating APIG instances

Use the following YAML file to create an APIGInstance and create an APIG instance.

```YAML
apiVersion: loadbalancer.vke.volcengine.com/v1beta1
kind: APIGInstance
metadata:
  name: apig-instance-demo # The name of the APIGInstance resource.
spec:
  name: apig-demo # The name of the APIG instance.
  common:
    resource:
      replicas: 2 # The number of APIG nodes.
      instanceSpecCode: 1c2g # The specification of the APIG instance. Valid values: 1c2g, 2c4g, 4c8g, and 8c16g.
      clbSpecCode: medium_1 # The CLB specification used by APIG. Valid values: small_1, small_2, medium_1, medium_2, large_1, and large_2.
      publicNetworkBillingType: traffic # The billing type of the elastic IP address (EIP). Valid values: traffic and bandwidth.
      publicNetworkBandwidth: 100 # The maximum bandwidth value of the EIP. This field is required if publicNetworkBillingType is set to bandwidth. Valid values: 1 to 500.
    network:
      subnetIds: # The Virtual Private Cloud (VPC) subnet of the APIG instance. If this field is left empty, the subnet where the cluster is located will be used.
        - subnet-22j0hss***
        - subnet-31x0qss***
  ingress:
    enable: true # Specify whether to enable APIG Ingress synchronization. Valid values: true and false.
    enableAllIngressClasses: false # Specify whether to synchronize all IngressClasses. Valid values: true and false.
    enableIngressWithoutIngressClass: false # Specify whether to synchronize Ingresses that are not associated with IngressClasses. Valid values: true and false.
    ingressClasses: # Specify the IngressClasses for which Ingress synchronization takes effect.
      - apig
    enableAllNamespaces: false # Specify whether to synchronize Ingresses in all namespaces. Valid values: true and false.
    watchNamespaces: # Specify the namespaces for which Ingress synchronization takes effect.
      - doc-demo
      - default
  monitor: 
    enable: true # Specify whether to enable APIG monitoring. Valid values: true and false.
    workspaceId: e963bbaa-*** # Specify the ID of the VMP workspace.
  log:
    enable: true # Specify whether to enable APIG instance logging. Valid values: true and false.
    projectId: f0abf4c1-*** # The TLS project ID.
    topicId: a95db607-*** # The TLS topic ID.
```


The parameters under `spec` are listed below.


|Parameter |Type |Required |Description |Sample value |Is modification supported |
|---|---|---|---|---|---|
|name |String |Yes |Specify the APIG instance name. |apig\-demo |No |
|common.resource.replicas |Integer |No |Specify the number of APIG instances. Default value: 2.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To ensure high availability of APIG instances, select at least two instances.</div><br> |2 |No |
|common.resource.instanceSpecCode |String |No |Configure the specification of the APIG instance. Valid values:<br><br><br>* 1c2g<br><br>* 2c4g<br><br>* 4c8g. This value is used by default.<br><br>* 8c16g |2c4g |No |
|common.resource.clbSpecCode |String |No |Specify the CLB specification used by the APIG instance. Valid values: small_1, small_2, medium_1, medium_2, large_1, and large_2. For details, see [Product types and specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). |medium_1 |No |
|common.resource.publicNetworkBillingType |String |No |Specify the billing type of the EIPs for the CLB instances used by the APIG instances. Valid values:<br><br><br>* **traffic**: pay\-as\-you\-go. This value is used by default.<br><br>* **bandwidth**: pay\-by\-bandwidth |traffic |No |
|common.resource.publicNetworkBandwidth |Integer |This field is required when `publicNetworkBillingType` is set to `bandwidth`. |Specify the maximum bandwidth value of the EIPs for the CLB instances used by the APIG instances. Valid values: 1 to 500. Unit: Mbit/s. |10 |No |
|common.network.subnetIds |No |No |The VPC subnet of the APIG instance. If this field is left empty, the subnet where the cluster is located will be used.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can configure multiple subnets.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The subnets cannot be located in the same availability zone (AZ).</div><br> |subnet\-31x0qss\*\*\* |No |
|ingress.enable |Boolean |No |Specify whether to enable Ingress synchronization. After you enable the feature, only Ingresses within the synchronization scope will be synchronized to APIG. Valid values:<br><br><br>* **true**: Enables the Ingress synchronization feature. This value is used by default.<br><br>* **false**: Disables the Ingress synchronization feature. |true |No |
|ingress.enableAllIngressClasses |Boolean |No |Specify whether to synchronize all IngressClasses. Valid values:<br><br><br>* **true**: synchronizes all IngressClasses.<br><br>* **false**: only synchronizes the specified IngressClasses. This value is used by default. |true |No |
|ingress.enableIngressWithoutIngressClass |Boolean |No |Specify whether to synchronize Ingresses that are not associated with IngressClasses. Valid values:<br><br><br>* **true**: Synchronizes Ingresses that are not associated with IngressClasses.<br><br>* **false**: Does not synchronize Ingresses that are not associated with IngressClasses. This value is used by default. |true |No |
|ingress.ingressClasses |String |No |Specify the IngressClasses for which Ingress synchronization takes effect. You can enter multiple namespaces. If this field is left empty, synchronization does not take effect.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>enableAllIngressClasses</code> is set to <code>false</code>, you need to specify this parameter to specify the IngressClass to which the Ingress to be synchronized belongs. Otherwise, synchronization does not take effect.</div><br> |apig |No |
|ingress.enableAllNamespaces |Boolean |No |Specify whether to synchronize all namespaces. Valid values:<br><br><br>* **true**: Synchronizes all namespaces.<br><br>* **false**: Only synchronizes the specified namespaces. This value is used by default. |true |No |
|ingress.watchNamespaces |String |No |Specify the namespaces for which Ingress synchronization takes effect. You can enter multiple namespaces. If this field is left empty, synchronization does not take effect.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>enableAllNamespaces</code> is set to <code>false</code>, you need to specify this parameter to specify the namespaces for which Ingress synchronization takes effect. Otherwise, synchronization does not take effect.</div><br> |default |No |
|monitor.enable |Boolean |No |Specify whether to enable APIG monitoring. Valid values:<br><br><br>* **true**: Enables the APIG monitoring feature.<br><br>* **false**: Disables the APIG monitoring feature. This value is used by default. |true |No |
|monitor.workspaceId |String |This field is required when `monitor.enable` is set to `true`. |Specify the ID of the VMP workspace used for APIG monitoring. For more information, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces). |e963bbaa\*\*\* |No |
|log.enable |Boolean |No |Specify whether to enable the APIG logging feature. Valid values:<br><br><br>* **true**: Enables the APIG logging feature.<br><br>* **false**: Disables the APIG logging feature. This value is used by default. |true |No |
|log.projectId |String |This field is required when `log.enable` is set to `true`. |Specify the ID of the project used by APIG logs. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects). |f0abf4\*\*\* |No |
|log.topicId |String |No |Specify the ID of the topic used by APIG logs. If this field is left empty, the default topic will be used. For details, see [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics). |a95db\*\*\* |No |


<span id=".5p-l55yLLWFwaWdpbnN0YW5jZS3lkI3np7DlkoznirbmgIE="></span>
## Viewing APIGInstance names and status

After you create an APIGInstance in the cluster, you can use the following method to view the status of the APIGInstance.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Workload \> Resource Explorer**.

5. If you select **CRD** from the Category list on the **Resource Explorer** page, click **apiginstance**.

6. On the **apiginstance** details page, view the name of the created APIGInstance resource.

7. Click **Edit Yaml** in the **Actions** column to view the details of the APIGInstance resource. The `status` field displays the ID and status of the APIG instance.

   The following table describes the meanings of different parameters in the `status` field.

   
   |Parameter |Type |Meaning |
   |---|---|---|
   |id |String |The ID of the associated APIG instance. |
   |phase |String |The state of the APIG instance. Valid values:<br><br><br>* **Pending**: Indicates that the associated APIG instance has not been orchestrated.<br><br>* **Running**: Indicates that all configurations of the APIG instance have been updated.<br><br>* **Configuring**: Indicates that the APIG instance is being orchestrated.<br><br>* **Deleting**: Indicates that the APIG instance is being deleted. |
   


<span id=".5Yib5bu6LWFwaWctaW5ncmVzcw=="></span>
## Creating APIG Ingresses

<span id=".5Z-65LqO5Z-f5ZCN6L2s5Y-R"></span>
### Domain name\-based forwarding

APIG Ingress can forward requests targeting different domain names to the expected backends. Sample `apig-ingress.yaml` code:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
spec:
  ingressClassName: apig
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
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo-b # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


<span id=".5Z-65LqO6Lev5b6E6L2s5Y-R"></span>
### Path\-based forwarding

APIG Ingress can forward requests targeting different paths under the same domain name to the expected backends. Sample `apig-ingress.yaml` code:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
      http:
        paths:
        - path: /foo # The path that matches the request.
          pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          backend:
            service:
              name: service-demo-a # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
        - path: /bar # The matching path for the request.
          pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          backend:
            service:
              name: service-demo-b # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


<span id=".6YWN572u6buY6K6k6L2s5Y-R6KeE5YiZ55qE5ZCO56uv5pyN5Yqh5Zmo"></span>
### Configuring backend servers for the default forwarding rule

Sample `apig-ingress.yaml` code:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
spec:
  ingressClassName: apig
  rules:
    - http:
       paths:
       - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
         path: / # The matching path for the request.
         backend:
           service:
             name: service-demo # The name of the service to forward requests to.
             port:
               number: 80 # The service port number to forward to.
```
