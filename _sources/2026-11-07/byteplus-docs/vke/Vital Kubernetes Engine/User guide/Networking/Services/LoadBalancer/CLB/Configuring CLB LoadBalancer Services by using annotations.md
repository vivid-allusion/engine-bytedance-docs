---
title: "Configuring CLB LoadBalancer Services by using annotations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations"
---

With annotations, Services can provide richer Layer\-4 load balancing (CLB) capabilities. This topic describes how to configure load balancing services using annotations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Annotations are case\-sensitive.</div>


* <div data-tips="true" data-tips-type="warning">Before configuring a LoadBalancer Service, be sure to carefully read <a href="https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_usage_precautions">Considerations for using LoadBalancer Services</a>.</div>



<span id=".5Yib5bu65pyN5Yqh"></span>
## Creating a service

<span id="nfPHwdQx"></span>
### Using an existing CLB instance

The following YAML file is an example of creating a service based on an existing LoadBalancer instance.

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-id |String |Yes |The ID of the existing LoadBalancer instance. |None |No |


<span id="ptOYn7Gt"></span>
### Using a new CLB instance

The following YAML file is an example of creating a service and a LoadBalancer instance at the same time.

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-name: "clb-demo" # Optional. Name of the newly created LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-subnet-id: "subnet-mizw4xqzpssg5smt1b******" # Required. Subnet ID of the LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-address-type: "PUBLIC" # Optional. The network type of the LoadBalancer instance. If not set, the default network type is PUBLIC
    service.beta.kubernetes.io/volcengine-loadbalancer-isp-type: "BGP" # Optional. The line type of the LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-billing-type: "2" # Optional. Billing model for LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-eip-billing-type: "3" # Optional.  Billing model for Elastic IP Address (EIP)
    service.beta.kubernetes.io/volcengine-loadbalancer-bandwidth: "25" # Optional. For a LoadBalancer instance exposed on the Internet, the maximum bandwidth for the Elastic IP Address (EIP) is required.
    service.beta.kubernetes.io/volcengine-loadbalancer-spec: "small_1" # Optional. Specification of the LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-sync-fields: "spec" # Required when updating the CLB instance specification. If this field is set to spec, the CLB instance specification will be updated according to the loadbalancer-spec field.
    service.beta.kubernetes.io/volcengine-loadbalancer-master-zone-id: "cn-beijing-a" # Optional. Primary availability zone ID of the LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-slave-zone-id: "cn-beijing-b" # Optional. Backup availability zone ID of the LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-modification-protection-status: "ConsoleProtection" # Optional. The modification protection status of the LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-eip-BandwidthPackageId: "bwp-2d63yyj3ki4u858oz***" # Optional. ID of shared bandwidth package 
    service.beta.kubernetes.io/volcengine-loadbalancer-eni-address-number: "2" # Optional. Number of private IPv4 addresses that the LoadBalancer instance can have
    service.beta.kubernetes.io/volcengine-loadbalancer-eni-address: "192.168.0.1" # Optional. The private IPv4 address of the LoadBalancer instance. It should be one of the IPs within the selected subnet and has not been occupied. 
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  ipFamilyPolicy: PreferDualStack  # Preferred protocol stack. SingleStack indicates single stack. PreferDualStack indicates dual stacks.
  ipFamilies: # The communication protocols actually used. The single stack supports IPv4. The dual stacks support IPv4&IPv6 and IPv6&IPv4.
  - IPv6
  - IPv4
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 8
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-name |String |No |Name of the LoadBalancer instance. If not specified, a name will be generated automatically. |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-subnet\-id |String |Yes |ID of the subnet in which the LoadBalancer instance is running. |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-address\-type |String |No |Network type of the LoadBalancer instance. Valid values:<br><br><br>* **PUBLIC**: LoadBalancer instance accessible on the Internet.<br><br>* **PRIVATE**: LoadBalancer instance accessible in private networks. |PUBLIC |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-isp\-type |String |No |The line type of the LoadBalancer instance. It includes BGP, SingleLine_BGP, Static_BGP, Fusion_BGP, ChinaMobile, ChinaTelecom, ChinaUnicom, ChinaMobile_Value, ChinaUnicom_Value, and ChinaTelecom_Value. For details, see [EIP documentation](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Except for <strong>BGP</strong>, all the line types are beta features of EIP products. To apply for these features, contact your account manager.</div><br> |BGP |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-billing\-type |String |No |The billing type of the LoadBalancer instance. Valid values:<br><br><br>* **2**: pay\-as\-you\-go \- specification\-based billing. Select an instance specification and pay according to your actual usage time.<br><br>* **3**: Pay\-as\-you\-go \- usage\-based billing. You do not need to specify instance specifications. You pay based on the actual resources consumed by the instance.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Pay\-as\-you\-go \- usage\-based billing</strong> is a beta feature of the LoadBalancer product. To apply for this billing model, contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">There is no need for <code>loadbalancer-spec</code> configuration if <strong>Pay\-as\-you\-go \- usage\-based billing</strong> is selected.</div><br> |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-eip\-billing\-type |String |No |EIP (Elastic IP Address) billing model. Available models:<br><br><br>* **2**: Pay\-as\-you\-go \- by bandwidth limit. This billing method requires a maximum bandwidth limit and incurs fees based on the usage duration, regardless of the actual traffic.<br><br>* **3**: Pay\-as\-you\-go \- by actual traffic. This billing method requires a maximum bandwidth limit and incurs fees based on the actual outbound traffic over the Internet, regardless of the usage duration. |3 |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-bandwidth |String |No |Maximum bandwidth for Internet access of the LoadBalancer instance, measured in Mbps, available values:<br><br><br>* If `eip-billing-type` is set to 2, the bandwidth range is 1 to 500.<br><br>* If `eip-billing-type` is set to 3, the bandwidth range is 1 to 200. |1 |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-spec |String |No |Instance specification of the LoadBalancer. Available types:<br><br><br>* **small_1**: small I<br><br>* **small_2**: small II<br><br>* **medium_1**: medium I<br><br>* **medium_2**: medium II<br><br>* **large_1**: large I<br><br>* **large_2**: large II<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For details about specifications and types of LoadBalancer instances, see <a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-02">Product types and specifications</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When <code>loadbalancer-billing-type</code> is set to <code>3</code>, LoadBalancer instances use the <strong>Pay\-as\-you\-go \- usage\-based billing</strong> type and this parameter is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This annotation needs to be used together with another one named <code>loadbalancer-sync-fields</code> with its value set to <code>spec</code>.</div><br> |small_1 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-sync\-fields |String |Required when updating the specification of a CLB instance |Whether to update the CLB instance according to the changes of the `loadbalancer-spec` field when updating the YAML file. Valid values:<br><br><br>* **spec**: Updates the CLB instance according to the changes of the `loadbalancer-spec` field. |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-master\-zone\-id |String |No |Primary availability zone ID of the LoadBalancer instance.<br><br><br>* The ID cannot be the same as that of the `slave-zone-id` parameter.<br><br>* If this parameter is missing or left empty, the availability zone where the subnet is allocated will be assigned as the master availability zone by default.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the availability zones supported by LoadBalancer in each region and their IDs, see <a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-08">Regions and Availability Zones</a>.</div><br> |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-slave\-zone\-id |String |No |Secondary availability zone ID of the LoadBalancer instance.<br><br><br>* The ID cannot be the same as that of the `master-zone-id` parameter.<br><br>* This parameter needs to be used together with `master-zone-id`. Otherwise, errors will occur.<br><br>* If you remove this parameter or leave it empty, the following logic will be applied:<br><br>   * For a specified region with a single availability zone, a single\-zone CLB instance will be created.<br><br>   * For a specified region with multiple availability zones, a CLB instance is created by default using randomly selected zones from the region. |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-modification\-protection\-status |String |No |Options for modification protection:<br><br><br>* **NonProtection**: It disables modification protection to allow instances to be altered or removed via the console page.<br><br>* **ConsoleProtection**: It enables modification protection to prevent instances from being altered or removed via the console page.<br><br>* Missing this parameter or leaving it empty (default) indicates modification protection is enabled.  |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-eip\-BandwidthPackageId |String |No |Shared bandwidth package ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Effective only if <code>service.beta.kubernetes.io/volcengine-loadbalancer-address-type=PUBLIC</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After it takes effect, the billing mode (usage\-based billing or subscription\-based billing with tied bandwidth) previously used will be replaced.</div><br> |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-eni\-address\-number |String |No |Configure the number of private network IPv4 addresses for the LoadBalancer instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">It is only applicable to private CLB instances.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">It cannot be used simultaneously with the <code>volcengine-loadbalancer-eni-address</code> parameter.</div><br> |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-eni\-address |String |No |Configure the private network IPv4 address for the LoadBalancer instance, which needs to be within the selected IPv4 subnet and not in use<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It cannot be used simultaneously with the <code>volcengine-loadbalancer-eni-address-number</code> parameter.</div><br> |None |No |


<span id="oAufBbc8"></span>
### Using a new CLB instance and binding to a VCI workload

The following YAML file is an example of creating a service and binding it to a workload deployed with VCI (abbreviation for Vital Container Instance).

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-name: "clb-demo" # Optional. Name of the newly created LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-subnet-id: "subnet-mizw4xqzpssg5smt1b******" # Required. Subnet ID of the LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-pass-through: "true" # Required. Enable LB-to-pod direct access mode for the LoadBalancer. It needs to be enabled when associating VCI workloads.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-name |String |No |Name of the LoadBalancer instance. If not specified, a name will be generated automatically. |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-subnet\-id |String |Yes |ID of the subnet in which the LoadBalancer instance is running. |None |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-pass\-through |String |Yes |Whether to enable LB\-to\-pod direct access mode for LoadBalancer. Valid values:<br><br><br>* **true**: Enable this feature. Associated pods serve as the backend of the LoadBalancer.<br><br>* **false**: Disable this feature. Associated nodes serve as the backend of the LoadBalancer. |false |Yes |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">It can only be enabled (by setting the annotation to <code>true</code>) for clusters using the VPC\-CNI network model. Modify this annotation with caution, as it will cause an interruption of network traffic.</div>


* <div data-tips="true" data-tips-type="warning">If the LoadBalancer Service is associated with workloads deployed on VCI, you must enable LB\-to\-pod direct access mode. Otherwise, the service will be unavailable.</div>



<span id=".55uR5ZCs5Zmo6YWN572u"></span>
## Listener configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A listener can be created based on an existing CLB instance or a new CLB instance. The following examples will use an existing CLB instance.</div>


<span id=".5Yib5bu6LXVkcC3ljY_orq7nm5HlkKzlmag="></span>
### Creating a UDP listener

To specify the protocol for the listener, you can use` spec.ports` in the YAML file instead of the annotation `service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port`. For example, with the `protocol` under `spec.ports` set to UDP, the system will create a UDP listener accordingly. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: UDP  # Port communication protocol. In this example, the value is UDP, indicating the creation of a UDP listener.
    targetPort: 80
  type: LoadBalancer
```


<span id=".5Yib5bu6LXRjcC3ljY_orq7nm5HlkKzlmag="></span>
### Creating a TCP listener

To specify the protocol for the listener, you can use `spec.ports` in the YAML file instead of the annotation `service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port`. For example, with the `protocol` under `spec.ports` set to UDP, the system will create a UDP listener accordingly. The example is as follows:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test 
    port: 80
    protocol: TCP  # Port communication protocol. In this example, the value is TCP, indicating the creation of a TCP listener.
    targetPort: 80
  type: LoadBalancer
```


<span id=".5Yib5bu6LWh0dHAt5Y2P6K6u55uR5ZCs5Zmo"></span>
### Creating an HTTP listener

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure an HTTP listener, upgrade the cloud\-controller\-manager component to v1.42.3 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading the component</a>.</div>


* <div data-tips="true" data-tips-type="warning">To configure a timeout for an HTTP listener:</div>


   * <div data-tips="true" data-tips-type="warning">Upgrade the cloud\-controller\-manager component to v1.50.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading the component</a>.</div>


   * <div data-tips="true" data-tips-type="warning">If a Service includes both HTTP and TCP ports, only the timeout configurations for the HTTP listener are updated.</div>


   * <div data-tips="true" data-tips-type="warning">When you delete annotations related to listener timeout, the listener retains the configuration that was used before the annotations were deleted. For example, if the default value of an annotation is 20, and you change the value to 60 and then delete the annotation, the system keeps the value 60.</div>



Annotations for LoadBalancer services can be used to create HTTP listeners running on CLB instances. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # Required. ID of an existing LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port: "HTTP:80" # Required. Configuration of Layer 7 protocol listener, including protocol (HTTP, HTTPS) and port number
    service.beta.kubernetes.io/volcengine-loadbalancer-keepalive-timeout: "75" # Optional. The idle timeout period of client connections. Specify an integer from 0 to 900. Default value: 75. Unit: seconds. A value of 0 indicates that persistent client connections are disabled.
    service.beta.kubernetes.io/volcengine-loadbalancer-client-header-timeout: "60" # Optional. The timeout period for client request headers. Specify an integer from 30 to 120. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-client-body-timeout: "30" # Optional. The timeout period for client request bodies. Specify an integer from 30 to 120. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-send-timeout: "60" # Optional. The timeout period for forwarding responses to clients. Specify an integer from 1 to 1300. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-proxy-read-timeout: "60" # Optional. The timeout period for backend responses. Specify an integer from 30 to 3600. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-proxy-send-timeout: "60" # Optional. The timeout period for backend responses. Specify an integer from 30 to 3600. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-proxy-connect-timeout: "4" # Optional. The timeout period for establishing backend connections. Specify an integer from 4 to 120. Default value: 4. Unit: seconds.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-protocol\-port |String |Yes |The Layer 7 protocol and port number for the listener. You can specify multiple values separated by commas (`,`), for example, `https:443,http:80`.<br><br><div data-tips="true" data-tips-type="danger">Warning</div><br><br><br><div data-tips="true" data-tips-type="danger">This annotation can be altered or deleted at any time. The system will remove the old listener and rebuild a new one according to the changes when the annotation is updated. Modify this annotation with caution, as it will cause an interruption of network traffic.</div><br> |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-keepalive\-timeout |String |No |The timeout period for persistent connections between clients and CLB. If no access requests are sent within the timeout period, CLB terminates the current connection and establishes a new connection when the next request arrives.<br><br><br>* The value is an integer. Valid values: 0 to 900.<br><br>* Unit: seconds.<br><br>* A value of 0 indicates that persistent connections are disabled. |75 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-client\-header\-timeout |String |No |The timeout period for reading client request headers. A client sends a request to CLB. If the client does not transmit the complete header within the timeout period, CLB returns the 408 error code, indicating a request timeout.<br><br><br>* The value is an integer. Valid values: 30 to 120.<br><br>* Unit: seconds. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-client\-body\-timeout |String |No |The timeout period for reading client request bodies. A client sends a request to CLB. If the client does not send any request body within the timeout period, CLB returns the 408 error code to indicate a request timeout.<br><br><br>* The value is an integer. Valid values: 30 to 120.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-send\-timeout |String |No |The timeout period for CLB to send responses to clients. CLB sends a response to a client. If the client does not receive any content within the timeout period, the connection is closed.<br><br><br>* The value is an integer. Valid values: 1 to 3600.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-proxy\-read\-timeout |String |No |The timeout period for CLB to read responses from backend servers. CLB sends a request to a backend server. If the backend server that receives the request does not respond within the timeout period, the connection is closed.<br><br><br>* The value is an integer. Valid values: 30 to 3600.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-proxy\-send\-timeout |String |No |The timeout period for CLB to transmit requests to backend servers. CLB sends a request to a backend server. If the backend server does not receive any content within the timeout period, the connection is closed.<br><br><br>* The value is an integer. Valid values: 30 to 3600.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-proxy\-connect\-timeout |String |No |The timeout period for establishing connections between CLB and backend servers. If CLB does not establish a connection to a backend server within the timeout period, the connection establishment operation is terminated.<br><br><br>* The value is an integer. Valid values: 4 to 120.<br><br>* Unit: seconds.<br><br>* We recommend setting this value to be greater than the health check timeout period. |4 |Yes |


<span id=".5Yib5bu6LWh0dHBzLeWNj-iuruebkeWQrOWZqA=="></span>
### Creating an HTTPS listener

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure an HTTPS listener, upgrade the cloud\-controller\-manager component to v1.42.3 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading the component</a>.</div>


* <div data-tips="true" data-tips-type="warning">To configure a timeout for an HTTP listener:</div>


   * <div data-tips="true" data-tips-type="warning">Upgrade the cloud\-controller\-manager component to v1.50.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading the component</a>.</div>


   * <div data-tips="true" data-tips-type="warning">If a Service includes both HTTPS and TCP ports, only the timeout configurations for the HTTPS listener are updated.</div>


   * <div data-tips="true" data-tips-type="warning">When you delete annotations related to listener timeout, the listener retains the configuration that was used before the annotations were deleted. For example, if the default value of an annotation is 20, and you change the value to 60 and then delete the annotation, the system keeps the value 60.</div>


* <div data-tips="true" data-tips-type="warning">Before creating an HTTPS listener, first log in to your BytePlus account, click <a href="https://console.byteplus.com/iam/service/attach_role/?ServiceName=clb">Service authorization</a>, then click <strong>Authorize Now</strong> on the page to complete cross\-service authorization.</div>


* <div data-tips="true" data-tips-type="warning">The CA and server certificate need to be uploaded first to the CLB console or Certificate Center before getting started. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Certificate-management">Certificate management</a>, <a href="https://docs.byteplus.com/en/docs/6638/118034">Creating SSL certificate</a>, and <a href="https://docs.byteplus.com/en/docs/6638/118039">Uploading SSL certificate</a>.</div>


* <div data-tips="true" data-tips-type="warning">When configuring an HTTPS listener, note the following information:</div>


   * <div data-tips="true" data-tips-type="warning">The port number configured using <code>loadbalancer-protocol-port</code> (<code>443</code> in this example) must be declared in the <code>spec.ports</code> field. The <code>spec.ports.protocol</code> field for that port must be set to <code>TCP</code>.</div>


   * <div data-tips="true" data-tips-type="warning">If the configured port number (in this example, <code>443</code>) is not declared in the <code>spec.ports</code> field, the <code>HTTP:443</code> specified in the annotation will be ignored.</div>


   * <div data-tips="true" data-tips-type="warning">If the configured port number is declared while the <code>spec.ports.protocol</code> field is set to <code>UDP</code>, the <code>HTTPS:443</code> specified in the annotation will be ignored.</div>



Annotations for LoadBalancer services can be used to create HTTPS listeners running on CLB instances. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # Required. ID of an existing LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port: "HTTPS:443" # Required. Configuration of Layer 7 protocol listener, including protocol (HTTP, HTTPS) and port number
    service.beta.kubernetes.io/volcengine-loadbalancer-cert-source: "clb" # Required. The location where the HTTPS certificate is obtained. Available values: clb and cert_center (Certificate Center)
    service.beta.kubernetes.io/volcengine-loadbalancer-cert-id: "cert-22jti***" # Required. HTTPS certificate ID for servers
    service.beta.kubernetes.io/volcengine-loadbalancer-security-policy-id: "default_policy" # Optional.  ID of security policy
    service.beta.kubernetes.io/volcengine-loadbalancer-ca-enabled: "on" # Optional. Whether to enable two-way authentication. Available value: on (enabled), off (disabled)
    service.beta.kubernetes.io/volcengine-loadbalancer-ca-cert-id: "cert-22jti***" # Required when two-way authentication is enabled. Enter a CA certificate ID for bidirectional authentication
    service.beta.kubernetes.io/volcengine-loadbalancer-keepalive-timeout: "75" # Optional. The idle timeout period of client connections. Specify an integer from 0 to 900. Default value: 75. Unit: seconds. A value of 0 indicates that persistent client connections are disabled.
    service.beta.kubernetes.io/volcengine-loadbalancer-client-header-timeout: "60" # Optional. The timeout period for client request headers. Specify an integer from 30 to 120. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-client-body-timeout: "30" # Optional. The timeout period for client request bodies. Specify an integer from 30 to 120. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-send-timeout: "60" # Optional. The timeout period for forwarding responses to clients. Specify an integer from 1 to 1300. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-proxy-read-timeout: "60" # Optional. The timeout period for backend responses. Specify an integer from 30 to 3600. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-proxy-send-timeout: "60" # Optional. The timeout period for forwarding requests to backends. Specify an integer from 30 to 3600. Default value: 60. Unit: seconds.
    service.beta.kubernetes.io/volcengine-loadbalancer-proxy-connect-timeout: "4" # Optional. The timeout period for establishing backend connections. Specify an integer from 4 to 120. Default value: 4. Unit: seconds.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 443
    protocol: TCP
    targetPort: 443
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-protocol\-port |String |Yes |The Layer 7 protocol and port number for the listener. You can specify multiple values separated by commas (`,`), for example, `https:443,http:80`.<br><br><div data-tips="true" data-tips-type="danger">Warning</div><br><br><br><div data-tips="true" data-tips-type="danger">This annotation can be altered or deleted at any time. The system will remove the old listener and rebuild a new one according to the changes when the annotation is updated. Modify this annotation with caution, as it will cause an interruption of network traffic.</div><br> |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cert\-source |String |Yes |Certificate source. Available values:<br><br><br>* **clb**: certificate from the CLB console.<br><br>* **cert_center**: certificate from the Certificate Center. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cert\-id |String |Yes |Server certificate ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">CCM does not actively verify the validity of the certificate ID. If the certificate ID is invalid, the listener cannot be created successfully.</div><br> |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-security\-policy\-id |String |No |Select an encryption policy to enable TLS protocols. Valid values:<br><br><br>* **default_policy**: supports SSL v3, TLS v1.0, TLS v1.1, TLS v1.2.<br><br>* **tls_cipher_policy_1_0**: supports TLS v1.0, TLS v1.1, TLS v1.2.<br><br>* **tls_cipher_policy_1_1**: supports TLS v1.1, TLS v1.2.<br><br>* **tls_cipher_policy_1_2**: supports TLS v1.2.<br><br>* **tls_cipher_policy_1_2_strict**: supports TLS v1.2. |default_policy |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-ca\-enabled |String |No |Whether to enable mutual authentication:<br><br><br>* **on**: It is enabled.<br><br>* **off**: Disable this setting. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-ca\-cert\-id |String | Required when mutual authentication is enabled |The CA certificate ID used for mutual authentication.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">CCM does not actively verify the validity of the certificate ID. If the certificate ID is invalid, the listener cannot be created successfully.</div><br> |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-keepalive\-timeout |String |No |The timeout period for persistent connections between clients and CLB. If no access requests are sent within the timeout period, CLB terminates the current connection and establishes a new connection when the next request arrives.<br><br><br>* The value is an integer. Valid values: 0 to 900.<br><br>* Unit: seconds.<br><br>* A value of 0 indicates that persistent connections are disabled. |75 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-client\-header\-timeout |String |No |The timeout period for reading client request headers. A client sends a request to CLB. If the client does not transmit the complete header within the timeout period, CLB returns the 408 error code, indicating a request timeout.<br><br><br>* The value is an integer. Valid values: 30 to 120.<br><br>* Unit: seconds. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-client\-body\-timeout |String |No |The timeout period for reading client request bodies. A client sends a request to CLB. If the client does not send any request body within the timeout period, CLB returns the 408 error code to indicate a request timeout.<br><br><br>* The value is an integer. Valid values: 30 to 120.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-send\-timeout |String |No |The timeout period for CLB to send responses to clients. CLB sends a response to a client. If the client does not receive any content within the timeout period, the connection is closed.<br><br><br>* The value is an integer. Valid values: 1 to 3600.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-proxy\-read\-timeout |String |No |The timeout period for CLB to read responses from backend servers. CLB sends a request to a backend server. If the backend server that receives the request does not respond within the timeout period, the connection is closed.<br><br><br>* The value is an integer. Valid values: 30 to 3600.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-proxy\-send\-timeout |String |No |The timeout period for CLB to transmit requests to backend servers. CLB sends a request to a backend server. If the backend server does not receive any content within the timeout period, the connection is closed.<br><br><br>* The value is an integer. Valid values: 30 to 3600.<br><br>* Unit: seconds.<br><br>* This timeout applies only to the interval between two consecutive write operations, not to the entire response transmission process. |60 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-proxy\-connect\-timeout |String |No |The timeout period for establishing connections between CLB and backend servers. If CLB does not establish a connection to a backend server within the timeout period, the connection establishment operation is terminated.<br><br><br>* The value is an integer. Valid values: 4 to 120.<br><br>* Unit: seconds.<br><br>* We recommend setting this value to be greater than the health check timeout period. |4 |Yes |


<span id=".6YWN572u6LCD5bqm566X5rOV"></span>
### Specifying scheduling algorithm

Annotations for LoadBalancer services can be used to specify scheduling algorithms for CLB instances. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-scheduler: "wrr" # Required. The scheduling algorithm for the listener. Available values: wrr, wlc, and sh
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP 
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-scheduler |String |Yes |Configuring the scheduling algorithm for the listener. Valid values:<br><br><br>* **wrr**: weighted round robin. The higher the weight of the backend server, the more frequently (probabilistically) it is selected as the forwarding destination.<br><br>* **wlc**: weighted least connections. This distributes requests to the backend server with the smallest ratio of `current connections to weight`.<br><br>* **sh**: source IP hash. Requests with source IP addresses that have the same hash value are forwarded to the same backend server. |None |Yes |


<span id=".6YWN572u6LaF5pe25pe26Ze0"></span>
### Configuring timeout

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Timeout is only applicable to TCP and UDP listeners.</div>


Annotations for LoadBalancer services can be used to set timeout for CLB instances. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-established-timeout: "100" # Required. Timeout of listener
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-established\-timeout |String |Yes |Configure the connection timeout of the listener, currently only effective for TCP and UDP listeners. Available values:<br><br><br>* TCP: 10 to 900 seconds, default is 900 seconds.<br><br>* UDP: 1 to 300 seconds, default is 90 seconds. |None |Yes |


<span id=".6YWN572u5bim5a695bOw5YC8"></span>
### Configuring maximum bandwidth

Annotations for LoadBalancer services can be used to set the maximum bandwidth for CLB instances. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-listener-bandwidth: "10" # Required. Maximum bandwidth of the listener
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-listener\-bandwidth |String |Yes |Configure the maximum bandwidth for the listener in Mbps.<br><br><br>*  **\-1**: This listener does not exclusively occupy CLB bandwidth. It shares the non\-exclusive bandwidth of the CLB instance with other listeners.<br><br>* Value range: 1 to the CLB bandwidth that is not used exclusively. For details about bandwidth specifications for CLB instances, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). |None |Yes |


<span id=".6YWN572u5Lya6K-d5L-d5oyB"></span>
### Configuring session persistence

Annotations for LoadBalancer services can be used to configure session persistence for CLB instances. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-persistence-timeout: "3600" # Required. Session persistence for the listener
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-persistence\-timeout |String |Yes |Configure session persistence and timeout for the listener. Sessions will be preserved based on source IPs if session persistence is configured. The range of values is 0 to 3600 seconds. Details:<br><br><br>* Setting it to 0 means session persistence is disabled.<br><br>* Setting it to a value from 1 to 3600 means session persistence is enabled with a specified timeout. |None |Yes |


<span id=".6YWN572u5YGl5bq35qOA5p-l"></span>
### Configuring health check

<span id="7yVXCbXK"></span>
#### Configuring TCP health checking

LoadBalancer Services support configuring health checking for TCP listeners via annotations. An example and description are as follows:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: "on" # Required. Whether to enable health check
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-connect-timeout: "2" # Optional. Response time to wait for a health check
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-interval: "2" # Optional. Health check interval
    service.beta.kubernetes.io/volcengine-loadbalancer-healthy-threshold: "3" # Optional. Number of health checks indicating the backend server is healthy
    service.beta.kubernetes.io/volcengine-loadbalancer-unhealthy-threshold: "3" # Optional. Number of health checks  indicating the backend server is unhealthy
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP  # Port communication protocol. In this example, the value is TCP, indicating the creation of a TCP listener.
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-flag |String |Yes |Whether to enable health check. Valid values:<br><br><br>* **on**: It is enabled.<br><br>* **off**: Disable this setting. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-interval |String |No |Health check interval.<br><br><br>* Value range: 1 to 300<br><br>* Unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-connect\-timeout |String |No |Health check timeout.<br><br><br>* Value range: 1–60<br><br>* Unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-healthy\-threshold |String |No |The number of consecutive health check requests required to determine that the back\-end server is running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-unhealthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is not running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |


<span id="HeQgZrAH"></span>
#### Configuring UDP health checking

LoadBalancer Services support configuring health checking for UDP listeners via annotations. An example and description are as follows:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: "on" # Required. Whether to enable health check
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-connect-timeout: "2" # Optional. Response time to wait for a health check
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-interval: "2" # Optional. Health check interval
    service.beta.kubernetes.io/volcengine-loadbalancer-healthy-threshold: "3" # Optional. Number of health checks indicating the backend server is healthy
    service.beta.kubernetes.io/volcengine-loadbalancer-unhealthy-threshold: "3" # Optional. Number of health checks  indicating the backend server is unhealthy
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-udp-request: "healthcheckrequest" # Optional. The string used in health check requests. Effective only if the listener protocol is UDP.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-udp-expect: "ok" # Optional. The string expected in health check responses. Effective only if the listener protocol is UDP.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: UDP  # Port communication protocol. In this example, the value is UDP, indicating the creation of a UDP listener.
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-flag |String |Yes |Whether to enable health check. Valid values:<br><br><br>* **on**: It is enabled.<br><br>* **off**: Disable this setting. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-interval |String |No |Health check interval.<br><br><br>* Value range: 1 to 300<br><br>* Unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-connect\-timeout |String |No |Health check timeout.<br><br><br>* Value range: 1–60<br><br>* unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-healthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-unhealthy\-threshold |String |No |The number of consecutive health check requests required to determine that the back\-end server is not running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-udp\-request |String |No |Request string for health check. It is only applicable to UDP listeners.<br><br><br>* It needs to be used together with `volcengine-loadbalancer-health-check-udp-expect`.<br><br>* Only letters and numbers are allowed, with 64 characters at most. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-udp\-expect |String |No |Request string for health check. It is only applicable to UDP listeners.<br><br><br>* It needs to be used together with `volcengine-loadbalancer-health-check-udp-request`.<br><br>* It can contain only letters and numbers. The maximum length is 64 characters. |None |Yes |


<span id="ZOkQR1a8"></span>
#### Configuring HTTP health checking

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You need to upgrade the cloud\-controller\-manager add\-on to v1.42.3 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


LoadBalancer Services support configuring health checking for HTTP listeners via annotations. An example and description are as follows:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: "on" # Required. Whether to enable health check
    service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port: "HTTP:80" # Required. Configuration of Layer 7 protocol listener, including protocol (HTTP, HTTPS) and port number
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-method: "GET" # Optional. Method for health check, including GET (default value) and HEAD. Effective only if the listener protocol is HTTP/HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-domain: "example.com" # Optional. Domain name for health check. It can be left empty. Effective only if the listener protocol is HTTP or HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-uri: "/" # Optional. The path for health checks. Effective only if the listener protocol is HTTP or HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-http-code: "http_2xx" # Optional. Status code indicating a successful health check. Effective only if the listener protocol is HTTP or HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-connect-timeout: "2" # Optional. Response time to wait for a health check
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-interval: "2" # Optional. Health check interval
    service.beta.kubernetes.io/volcengine-loadbalancer-healthy-threshold: "3" # Optional. Number of health checks indicating the backend server is healthy
    service.beta.kubernetes.io/volcengine-loadbalancer-unhealthy-threshold: "3" # Optional. Number of health checks  indicating the backend server is unhealthy
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP # Port communication protocol. When configuring HTTP health checks, this must be set to TCP.
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-flag |String |Yes |Whether to enable health check. Valid values:<br><br><br>* **on**: It is enabled.<br><br>* **off**: Disable this setting. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-protocol\-port |String |Yes |The Layer 7 protocol and port number for the listener. You can configure multiple values separated by commas (`,`), for example, `http:80,http:8080`. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-method |String |No |The method of health check. It is only applicable to HTTP/HTTPS listeners. Valid values:<br><br><br>* **GET**<br><br>* **HEAD** |GET |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-domain |String |No |The domain name for health check, only applicable to HTTP/HTTPS listeners.<br><br><br>* An empty domain name is allowed. If it is empty, the system will use the intranet IP of the backend server group to perform health check.<br><br>* If any domain name is configured, you need to ensure it is compliant with the convention, e.g., `example.com`. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-uri |String |No |Health check path, only applicable to HTTP/HTTPS listeners. |`/` |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-http\-code |String |No |The status code for normal health checks. You can configure multiple HTTP status codes separated by commas (`,`). It is only applicable to HTTP/HTTPS listeners. Available values:<br><br><br>* http_2xx<br><br>* http_3xx<br><br>* http_4xx<br><br>* http_5xx |http_2xx |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-interval |String |No |Health check interval.<br><br><br>* Value range: 1 to 300<br><br>* Unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-connect\-timeout |String |No |Health check timeout.<br><br><br>* Value range: 1–60<br><br>* unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-healthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-unhealthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is not running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |


<span id="gC0N2Y73"></span>
#### Configure HTTPS health checking

<div data-tips="true" data-tips-type="warning">Note</div>



* <div data-tips="true" data-tips-type="warning">You need to upgrade the cloud\-controller\-manager add\-on to v1.42.3 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


* <div data-tips="true" data-tips-type="warning">Before creating an HTTPS listener, first log in to your BytePlus account, click <a href="https://console.byteplus.com/iam/service/attach_role/?ServiceName=clb">Service authorization</a>, then click <strong>Authorize Now</strong> on the page to complete cross\-service authorization.</div>


* <div data-tips="true" data-tips-type="warning">The CA and server certificate need to be uploaded first to the CLB console or Certificate Center before getting started. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Certificate-management">Certificate management</a>, <a href="https://docs.byteplus.com/en/docs/6638/118034">Creating SSL certificate</a>, and <a href="https://docs.byteplus.com/en/docs/6638/118039">Uploading SSL certificate</a>.</div>


* <div data-tips="true" data-tips-type="warning">When configuring an HTTPS listener, note the following information:</div>


   * <div data-tips="true" data-tips-type="warning">The port number configured using <code>loadbalancer-protocol-port</code> (<code>443</code> in this example) must be declared in the <code>spec.ports</code> field. The <code>spec.ports.protocol</code> field for that port must be set to <code>TCP</code>.</div>


   * <div data-tips="true" data-tips-type="warning">If the configured port number (in this example, <code>443</code>) is not declared in the <code>spec.ports</code> field, the <code>HTTP:443</code> specified in the annotation will be ignored.</div>


   * <div data-tips="true" data-tips-type="warning">If the configured port number is declared while the <code>spec.ports.protocol</code> field is set to <code>UDP</code>, the <code>HTTPS:443</code> specified in the annotation will be ignored.</div>



LoadBalancer Services support configuring health checking for HTTPS listeners via annotations. An example and description are as follows:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: "on" # Required. Whether to enable health check
    service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port: "HTTPS:443" # Required. Configuration of Layer 7 protocol listener, including protocol (HTTP, HTTPS) and port number
    service.beta.kubernetes.io/volcengine-loadbalancer-cert-source: "clb" # Required. The location where the HTTPS certificate is obtained. Available values: clb and cert_center (Certificate Center)
    service.beta.kubernetes.io/volcengine-loadbalancer-cert-id: "cert-22jti***" # Required. HTTPS certificate ID for servers
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-method: "GET" # Optional. Method for health check, including GET (default value) and HEAD. Effective only if the listener protocol is HTTP/HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-domain: "example.com" # Optional. Domain name for health check. It can be left empty. Effective only if the listener protocol is HTTP or HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-uri: "/" # Optional. The path for health checks. Effective only if the listener protocol is HTTP or HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-http-code: "http_2xx" # Optional. Status code indicating a successful health check. Effective only if the listener protocol is HTTP or HTTPS.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-connect-timeout: "2" # Optional. Response time to wait for a health check
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-interval: "2" # Optional. Health check interval
    service.beta.kubernetes.io/volcengine-loadbalancer-healthy-threshold: "3" # Optional. Number of health checks indicating the backend server is healthy
    service.beta.kubernetes.io/volcengine-loadbalancer-unhealthy-threshold: "3" # Optional. Number of health checks  indicating the backend server is unhealthy
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 443
    protocol: TCP # Port communication protocol. When configuring HTTP health checks, this must be set to TCP.
    targetPort: 443
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-flag |String |Yes |Whether to enable health check. Valid values:<br><br><br>* **on**: It is enabled.<br><br>* **off**: Disable this setting. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-protocol\-port |String |Yes |The Layer 7 protocol and port number for the listener. You can specify multiple values separated by commas (`,`), for example, `https:443,http:80`. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cert\-source |String |Yes |Certificate source. Available values:<br><br><br>* **clb**: certificate from the CLB console.<br><br>* **cert_center**: certificate from the Certificate Center. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cert\-id |String |Yes |Server certificate ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">CCM does not actively verify the validity of the certificate ID. If the certificate ID is invalid, the listener cannot be created successfully.</div><br> |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-method |String |No |The method of health check. It is only applicable to HTTP/HTTPS listeners. Valid values:<br><br><br>* **GET**<br><br>* **HEAD** |GET |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-domain |String |No |The domain name for health check, only applicable to HTTP/HTTPS listeners.<br><br><br>* An empty domain name is allowed. If it is empty, the system will use the intranet IP of the backend server group to perform health check.<br><br>* If any domain name is configured, you need to ensure it is compliant with the convention, e.g., `example.com`. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-uri |String |No |Health check path, only applicable to HTTP/HTTPS listeners. |`/` |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-http\-code |String |No |The status code for normal health checks. You can configure multiple HTTP status codes separated by commas (`,`). It is only applicable to HTTP/HTTPS listeners. Available values:<br><br><br>* http_2xx<br><br>* http_3xx<br><br>* http_4xx<br><br>* http_5xx |http_2xx |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-interval |String |No |Health check interval.<br><br><br>* Value range: 1 to 300<br><br>* Unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-connect\-timeout |String |No |Health check timeout.<br><br><br>* Value range: 1–60<br><br>* unit: seconds |2 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-healthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-unhealthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is not running properly.<br><br><br>* Value range: 3 to 10<br><br>* Unit: times |3 |Yes |


<span id="jSMhk1fk"></span>
### Configuring access control

Annotations for LoadBalancer services can be used to configure access control for listeners. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-acl-status: "on" # Required. Whether to enable access control for the listener
    service.beta.kubernetes.io/volcengine-loadbalancer-acl-type: "white" # Required. Access control method. Values: white (indicating allowlist) and black (indicating blocklist).
    service.beta.kubernetes.io/volcengine-loadbalancer-acl-id: "acl-3cj44nv0jhhxc6c6rrtet****,acl-2febxt4pu0zy85oxruw0t****" # Required. ID of the access control policy group bound with the listener
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-acl\-status |String |Yes |Whether to enable access control for the listener. Valid values:<br><br><br>* **on**: It is enabled.<br><br>* **off**: Disable this setting. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-acl\-type |String |Yes |The method to apply access control for the listener. Available methods:<br><br><br>* **black**: blocklist. The listener denies requests from IP addresses or subnets set in the specified access control policy group.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the access control policy group is empty, the listener will forward all requests.   </div><br>   <br><br>* **white**: allowlist. The listener forwards requests from IP addresses or subnets set in the specified access control policy group.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the access control policy group is empty, the listener will deny all requests.   </div><br>    |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-acl\-id |String |Yes |ID of the access control policy group bound to the listener. For details about policy groups, see [Management of access control policy groups](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups).<br><br>You can specify at most five policy group IDs. If you specify multiple policy group IDs, separate them with commas (`,`). |None |Yes |


<span id="bMvolloe"></span>
### Configuring Proxy Protocol to forward source IPs

Annotations for LoadBalancer services can be used to configure source IP forwarding for listeners. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-proxy-protocol: "standard" # Required. Allow source IP to be forwarded by using Proxy Protocol headers
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-proxy\-protocol |String |Yes |Whether to enable Proxy Protocol to forward source IPs. Available values:<br><br><br>* **standard**: Enable this setting.<br><br>* **off**: Disable this setting. |None |Yes |


<span id="mGSEqLqs"></span>
### Configuring graceful connection termination

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You need to upgrade the cloud\-controller\-manager to version 1.43.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


LoadBalancer Services allow you to configure graceful connection termination for listeners by using annotations. If this feature is enabled, when backend servers are deleted or their health checks are abnormal, existing connections can still work normally within the graceful termination period. The following YAML content provides an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-connection-drain: "on" # (Required) Specify whether to enable graceful connection termination. Values include on and off.
    service.beta.kubernetes.io/volcengine-loadbalancer-connection-drain-timeout: "100" # Configure the graceful termination timeout. Required when graceful connection termination is enabled. 
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-connection\-drain |String |Yes |Whether to enable graceful connection termination. Valid values:<br><br><br>* **on**: It is enabled.<br><br>* **off**: Disable this setting. |None |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-connection\-drain\-timeout |String |No |The period during graceful connection termination applies. The value is an integer within the range of 0 to 900. The time is measured in seconds.<br><br>When the value is 0, a Reset packet is sent immediately to terminate the connection if the backend server is deleted or fails the health check.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when graceful connection termination is enabled.</div><br> |None |Yes |


<span id=".5YW25LuW6YWN572u"></span>
## Server group configuration

<span id="HIqDJY41"></span>
### Configuring IPv6 backend server group

The LoadBalancer service supports configuring the IP version of backend server groups via Annotation, allowing IPv6 backend server groups running in an IPv4/IPv6 dual\-stack cluster.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only IPv4/IPv6 dual\-stack network clusters support IPv6 type backend server groups. For how to configure dual\-stack clusters, see <a href="https://docs.byteplus.com/en/docs/vke/Deploying-an-IPv4_IPv6-dual-stack-cluster-using-VKE">Creating IPv4/IPv6 dual\-stack clusters</a>.</div>


* <div data-tips="true" data-tips-type="warning">To obtain the client's real source IP address, you can enable the Proxy Protocol feature on the listener of the CLB instance. For details, see <a href="https://docs.byteplus.com/en/docs/90/21682#bMvolloe">Configuring source IP passthrough in Proxy Protocol</a>.</div>




<Tabs>
<Tab zoneid="OvrnlfHZtK" title="Binding to existing CLB instances">
<TabTitle>Binding to existing CLB instances</TabTitle>

The following configuration example and description show you how to connect to an existing CLB instance and configure an IPv6 backend server group.

<div data-tips="true" data-tips-type="warning">Note</div>


<div data-tips="true" data-tips-type="warning">When using annotations to connect to an existing CLB instance, the instance must be dual\-stack. For details, see <a href="https://docs.byteplus.com/en/docs/clb/CLB-instances-01">Creating CLB instances</a>.</div>


```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-5gt7c99436dc73***" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-backend-ip-version: "ipv6" # Required. It is the IP version that the backend server group applies. In this scenario, it must be set to ipv6.
    service.beta.kubernetes.io/volcengine-loadbalancer-pass-through: "true" # Required. In this scenario, the LB-to-pod direct access mode needs to be enabled for the load balancer, and the Pod ENI needs to be mounted to the CLB backend server group.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  ipFamilyPolicy: PreferDualStack  # Preferred protocol stack. In this scenario, it must be set to PreferDualStack, i.e., dual protocol stacks.
  ipFamilies: # It is the communication protocol to use. In this scenario, both IPv4 and IPv6 must be configured.
  - IPv6
  - IPv4
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```





</Tab>
<Tab zoneid="tSBftlnMmC" title="Creating CLB instances">
<TabTitle>Creating CLB instances</TabTitle>

The following configuration example and description show you how to create a CLB instance and configure an IPv6 backend server group:

<div data-tips="true" data-tips-type="warning">Note</div>



* <div data-tips="true" data-tips-type="warning">Use the <code>spec.ipFamilyPolicy</code> and <code>spec.ipFamilies</code> fields to enable dual protocols for the Service.</div>


* <div data-tips="true" data-tips-type="warning">When creating a new CLB instance, the network type must be set to <code>PRIVATE</code>. To provide public network access, you can manually bind an EIP to the CLB instance in the CLB console after the instance is created. For details, see <a href="https://docs.byteplus.com/en/docs/clb/CLB-instances-05">Binding/Unbinding EIP</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information about configuration parameters for creating CLB Instances, see <a href="https://docs.byteplus.com/en/docs/90/21682#ptOYn7Gt">Creating CLB Instances</a>.</div>



```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-name: "clb-demo" # Optional. Name of the newly created LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-subnet-id: "subnet-mizw4xqzpssg5smt1b******" # Required. Subnet ID of the LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-address-type: "PRIVATE" # Required. It is the network type of the load balancer instance. In this scenario, it must be set to PRIVATE
    service.beta.kubernetes.io/volcengine-loadbalancer-backend-ip-version: "ipv6" # Required. It is the IP version that the backend server group applies. In this scenario, it must be set to ipv6.
    service.beta.kubernetes.io/volcengine-loadbalancer-pass-through: "true" # Required. In this scenario, the LB-to-pod direct access mode needs to be enabled for the load balancer, and the Pod ENI needs to be mounted to the CLB backend server group.
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  ipFamilyPolicy: PreferDualStack  # Preferred protocol stack. SingleStack indicates single stack. PreferDualStack indicates dual stacks.
  ipFamilies: # The communication protocols actually used. The single stack supports IPv4. The dual stacks support IPv4&IPv6 and IPv6&IPv4.
  - IPv6
  - IPv4
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```





</Tab>
</Tabs>


The following table describes the annotations.


|Field |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-backend\-ip\-version |String |Yes |Configure the IP version of the Backend server group. Valid values:<br><br><br>* **ipv4**: Backend server group applies IPv4.<br><br>* **ipv6**: Backend server group applies IPv6. |ipv4 |Yes |


<span id="J8Mq9ida"></span>
## Other configurations

<span id=".55u06YCaLXBvZC3mqKHlvI8="></span>
### LB\-to\-pod direct access mode

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This mode can be enabled for an existing CLB instance or a new CLB instance. The following examples will use an existing CLB instance.</div>


* <div data-tips="true" data-tips-type="warning">It can only be enabled (by setting the annotation to <code>true</code>) for clusters using the VPC\-CNI network model. Modify this annotation with caution, as it will cause an interruption of network traffic.</div>


* <div data-tips="true" data-tips-type="warning">If the LoadBalancer Service is associated with workloads deployed on VCI, you must enable LB\-to\-pod direct access mode. Otherwise, the service will be unavailable.</div>



Annotations for LoadBalancer services can be used to configure LB\-to\-pod direct access mode. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-pass-through: "true" # Required. Whether to enable LoadBalancer-to-pod direct access mode
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Key |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-pass\-through |String |Yes |Whether to enable LB\-to\-pod direct access mode for LoadBalancer. Valid values:<br><br><br>* **true**: It is enabled. The pod is running as the direct backend of the LoadBalancer.<br><br>* **false**: Disabled. |false |Yes |


<span id=".5bGV56S65YWs572RLWNsYi3nmoTnp4HnvZEtaXAt5Zyw5Z2A"></span>
### Displaying the private IP of the CLB on the Internet

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature can be enabled for an existing CLB instance or a new CLB instance. The following examples will use an existing CLB instance.</div>


* <div data-tips="true" data-tips-type="warning">This feature is only applicable to the CLB that is accessible on the Internet. For private CLB instances, only internal IPs can be viewed no matter whether the feature is enabled.</div>


* <div data-tips="true" data-tips-type="warning">It is not applicable to IPv4/IPv6 dual\-stack clusters.</div>



Annotations for LoadBalancer services can be used to allow or disallow the display of private IPs of Internet\-accessible CLB. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-display-internal-ip: "true" # Required. Whether to display the private IP address of the CLB accessible on the Internet
  name: clb-service
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP
    targetPort: 80
  type: LoadBalancer # Service type
```


The following table describes the annotations.


|Key |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-display\-internal\-ip |String |Yes |Whether to display the private IP address of the public CLB. Valid values:<br><br><br>* **true**: Enabled If the CLB can be accessed on the Internet, both the public and private IPs are displayed.<br><br>* **false**: Disabled. If the CLB can be accessed on the Internet, only the private IP is displayed.<br><br>* Missing this parameter indicates it is disabled. It means if the CLB can be accessed on the Internet, only the private IP is displayed. |false |Yes |


The public and private IP addresses can be found on the console page or in the YAML editor after configuration is finished.

<span id=".5Li66LSf6L295Z2H6KGh5re75Yqg6aKd5aSW5qCH562-"></span>
### Adding extra labels to LoadBalancer services

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Labels can be added only when creating a new CLB instance. Doing it with an existing CLB will lead to errors.</div>


* <div data-tips="true" data-tips-type="warning">It should be added when creating a new service. Leaving the annotation value empty indicates existing labels will be removed.</div>


* <div data-tips="true" data-tips-type="warning">Existing extra labels cannot be updated by using annotations.</div>



Annotations for LoadBalancer services can be used to add extra labels. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-name: "clb-demo"
    # Optional. Name of the newly created LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-subnet-id: "subnet-mizw4xqzpssg5smt1b******"
    # Required. Subnet ID of the LoadBalancer instance
    service.beta.kubernetes.io/volcengine-loadbalancer-additional-resource-tags: "key1=value1,key2=value2"
    # Required. Add extra labels to the LoadBalancer
  name: clb-service # The name of the service.
  namespace: default # The namespace to which the service belongs.
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx # Bind the Service to backend pods through the label selector.
  ports:
  - name: test # The name of the port mapping policy.
    port: 80 # The service port.
    protocol: TCP  # The communication protocol TCP/UDP.
    targetPort: 80 # The container port.
  type: LoadBalancer # Service type.
```


The following table describes the annotations.


|Key |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-additional\-resource\-tags |String |Yes |Add extra labels for LoadBalancer. The value must be in the form of `key=value`. You can configure multiple labels separated by commas (`,`). |None |No |


The extra labels of the CLB instance can be found on the CLB console page.

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [The event "lb is provisioning" occurs when configuring layer-4 LoadBalancer using annotations](https://docs.byteplus.com/en/docs/vke/Event-lb-is-provisioning-occurs-when-configuring-a-layer-4-load-balancer-by-using-annotations)

* [The event "loadbalancer for service not found" occurs when configuring layer-4 LoadBalancer using annotations](https://docs.byteplus.com/en/docs/vke/Event-loadbalancer-for-service-not-found-occurs-when-configuring-a-layer-4-load-balancer)

* [The event "InvalidServerGroupListener.InUse" occurs when configuring layer-4 LoadBalancer using annotations](https://docs.byteplus.com/en/docs/vke/Event-InvalidServerGroupListener_InUse-occurs-when-deleting-a-Service)
