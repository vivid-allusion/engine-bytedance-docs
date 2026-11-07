---
title: "Configuring an NLB Service using annotations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_an_NLB_Service_using_annotations"
---

Services support more comprehensive Layer 4 network load balancing (NLB) capabilities through annotations. This topic describes how to configure load balancing services using annotations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Annotations are case\-sensitive.</div>


* <div data-tips="true" data-tips-type="warning">Before configuring a LoadBalancer Service, be sure to carefully read <a href="https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_usage_precautions">Considerations for using LoadBalancer Services</a>.</div>



<span id="8LDzqvnQ"></span>
## Prerequisites

To connect to an NLB instance, make sure that the cloud\-controller\-manager add\-on is upgraded to v1.46.0 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="8LDzqvnQ"></span>
## Creating instances

<span id="s1dVJVFc"></span>
### Connecting to an existing NLB instance

Create a Service and associate it with an existing NLB instance by defining the configuration in a YAML manifest. The following configuration serves as an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-138jkmmlh2xa858***" # (Required) The ID of an existing NLB instance.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-id |String |Yes |The ID of the existing NLB instance. |No |


<span id="fHKNEAKs"></span>
### Creating public\-network NLB instances

Create a Service and provision a public load balancer instance by defining the configuration in a YAML manifest. The following configuration serves as an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-name: "nlb-demo" # (Optional) The name of the NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-address-type: "internet" # (Required) The network type of the NLB instance. Valid values include internet and intranet.
    service.beta.kubernetes.io/volcengine-loadbalancer-security-groups: "sg-1a1j6dj8hx***" # (Required) The ID of the security group associated with the NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-zone-maps: | # The network configuration of the NLB instance. At least two availability zones are required.
      [
        {
          "zoneId": "cn-beijing-a",
          "subnetId": "subnet-ivz80f***",
          "eipId": "eip-13eoqxduidce***"
        },
        {
          "zoneId": "cn-beijing-b",
          "subnetId": "subnet-1a1j6uw***"
        }
      ]
    service.beta.kubernetes.io/volcengine-loadbalancer-cross-zone-enabled: "true" # (Optional) Whether to enable cross-AZ forwarding for the NLB instance. Valid values include true and false.
    service.beta.kubernetes.io/volcengine-loadbalancer-project-name: "default" # (Optional) The name of the project to which the NLB instance belongs. If this field is not specified, the project of the cluster is used.
    service.beta.kubernetes.io/volcengine-loadbalancer-additional-resource-tags: "key1=val1,key2=val2" # (Optional) Custom labels for the NLB instance.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-name |String |No |The name of the NLB instance. If you do not specify a name, it defaults to the instance ID. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-address\-type |String |Yes |The network type of the NLB instance. Valid values:<br><br><br>* **internet**: Public network.<br><br>* **intranet**: Private network. |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-security\-groups |String |Yes |The ID of the security group associated with the NLB instance. You can specify a comma\-separated list of security groups.`` |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-zone\-maps |Array of zoneMaps |Yes |The network configuration of the NLB instance.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">At least two availability zones are required.</div><br> |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cross\-zone\-enabled |String |No |Whether to enable cross\-AZ forwarding for the NLB instance. Valid values:<br><br><br>* **true** (default): Yes.<br><br>* **false**: No. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-project\-name |String |No |The name of the project to which the NLB instance belongs. If this field is not specified, the project of the cluster is used. |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-additional\-resource\-tags |String |No |Custom labels for the NLB instance. A label follows the `key1=val1` format. You can specify multiple labels separated with commas (`,`). |Yes |


**zoneMaps**


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|zoneId |String |Yes |The ID of the AZ, for example, `cn-beijing-a`. |No |
|subnetId |String |Yes |The subnet ID, for example, `subnet-bp12mw1f8k3jgy****`. |No |
|eipId |String |No |EIP instance ID. For example, `eip-13eoqxduidce***`. If this field is not configured, a new EIP will be purchased. |No |


<span id="exm4w7r6"></span>
### Creating private\-network NLB instances

Create a Service and provision a private load balancer instance by defining the configuration in a YAML manifest. The following configuration serves as an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-name: "nlb-demo" # (Optional) The name of the NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-address-type: "intranet" # (Required) The network type of the NLB instance. Valid values include internet and intranet.
    service.beta.kubernetes.io/volcengine-loadbalancer-security-groups: "sg-1a1j6dj8hx***" # (Required) The ID of the security group associated with the NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-zone-maps: | # (Required) The network configuration of the NLB instance. At least two availability zones are required.
      [
        {
          "zoneId": "cn-beijing-a",
          "subnetId": "subnet-ivz80fesq3***",
          "ipv4Address": "192.168.1.10"
        },
        {
          "zoneId": "cn-beijing-b",
          "subnetId": "subnet-1a1j6uwpamw***"
        }
      ]
    service.beta.kubernetes.io/volcengine-loadbalancer-cross-zone-enabled: "true" # (Optional) Whether to enable cross-AZ forwarding for the NLB instance. Valid values include true and false.
    service.beta.kubernetes.io/volcengine-loadbalancer-project-name: "default" # (Optional) The name of the project to which the NLB instance belongs. If this field is not specified, the project of the cluster is used.
    service.beta.kubernetes.io/volcengine-loadbalancer-additional-resource-tags: "key1=val1,key2=val2" # (Optional) Custom labels for the NLB instance.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-name |String |No |The name of the NLB instance. If no custom name is specified, it defaults to the instance ID. |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-address\-type |String |Yes |The network type of the load balancer instance. Valid values:<br><br><br>* **internet**: Public network.<br><br>* **intranet**: Private network. |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-security\-groups |String |Yes |The ID of the security group associated with the NLB instance. You can specify a comma\-separated list of security groups.`` |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-zone\-maps |Array of zoneMaps |Yes |The network configuration of the NLB instance.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">At least two availability zones are required.</div><br> |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cross\-zone\-enabled |String |No |Whether to enable cross\-AZ forwarding for the NLB instance. Valid values:<br><br><br>* **true**: Yes.<br><br>* **false**: No. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-project\-name |String |No |The name of the project to which the NLB instance belongs. If this field is not specified, the project of the cluster is used. |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-additional\-resource\-tags |String |No |Custom labels for the NLB instance. A label follows the `key1=val1` format. You can specify multiple labels separated with commas (`,`). |Yes |


**zoneMaps**


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|zoneId |String |Yes |The ID of the AZ, for example, `cn-beijing-a`. |No |
|subnetId |String |Yes |The subnet ID, for example, `subnet-bp12mw1f8k3jgy****`. |No |
|ipv4Address |String |No |The IPv4 address of the private network. For example, `192.168.1.10`. If this field is not configured, the system automatically allocates an available IPv4 address from the subnet. |No |


<span id="WXGK1HZP"></span>
## Back\-end server group configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can configure a back\-end server group when you associate an existing NLB instance or create a new NLB instance. The following example uses an existing NLB instance for demonstration.</div>


<span id="mJExeirQ"></span>
### Specifying a scheduling algorithm

An NLB service allows you to specify a scheduling algorithm for back\-end server groups through annotations. The following configuration serves as an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-scheduler: "wrr" # (Required) The scheduling algorithm of the back-end server group. Valid values include wrr, wlc, and sh.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-scheduler |String |Yes |The scheduling algorithm used by the back\-end server group. Valid values:<br><br><br>* **wrr**: Weighted Round Robin (default). Back\-end servers with higher weight values are polled ‌more frequently (with a higher probability)‌.<br><br>* **wlc**: Weighted Least Connections. ‌The algorithm extends the least connections algorithm‌ by assigning different weights to servers based on their ‌processing capacity‌, enabling each server to handle a number of service requests proportional to its weight.<br><br>* **sh**: Source IP Hash. ‌The algorithm uses consistent hashing‌ based on source IP addresses. Requests from the same source address ‌are directed to‌ the same back\-end server. |Yes |


<span id="z5lSGlRN"></span>
### Configuring back\-end security group bypass

An NLB service allows you to bypass security groups for back\-end server groups through annotations. The following configuration serves as an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-bypass-security-group-enabled: "true" # (Required) Whether to bypass back-end security groups. Valid values include true and false.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-bypass\-security\-group\-enabled |String |Yes |Whether to bypass back\-end security groups:<br><br><br>* **true**: Enabled Traffic from the NLB instance is no longer subject to the security group rules of the back\-end ECS or its ENI and is always allowed.<br><br>* **false**: No (default). |Yes |


<span id="vuR4V4oa"></span>
### Configuring TCP health checking

An NLB service allows you to configure TCP health checking for back\-end server groups through annotations. The following configuration serves as example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: "on" # (Required) Whether to enable health checking for back-end server groups. The value is on or off.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-type: "TCP" # (Optional) Health check protocol. Valid options include TCP, UDP, and HTTP.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-port: "80" # (Optional) The health check port. The value is an integer within the range of 1 to 65,535.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-connect-timeout: "8" # (Optional) Health check response timeout (in seconds). The value range is 1 to 60.
    service.beta.kubernetes.io/volcengine-loadbalancer-healthy-threshold: "4" # (Optional) Health threshold for health checking. The value is an integer within the range of 2 to 10.
    service.beta.kubernetes.io/volcengine-loadbalancer-unhealthy-threshold: "4" # (Optional) Unhealthy threshold for health checks. The value is an integer within the range of 2 to 10.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-interval: "5" # (Optional) The time interval (in seconds) of health checks. The value is an integer within the range of 1 to 300.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-flag |String |No |Whether to enable health checking. Valid values:<br><br><br>* **on**: Yes (Default).<br><br>* **off**: Disable this setting. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-type |String |No |The health check protocol. Valid values:<br><br><br>* **TCP** (default)<br><br>* **UDP**<br><br>* **HTTP**<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration must be consistent with the <code>protocol</code> configuration in the <code>spec.ports</code> field.</div><br> |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-port |String |No |The health check port. The value is an integer within the range of 1 to 65535. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-connect\-timeout |String |No |The timeout in seconds for health checks. The value is an integer within the range of 1 to 60. The default value is 3.<br><br>‌If the back\-end server fails to respond within the timeout period, its health check status is marked as abnormal. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-healthy\-threshold |String |No |The health threshold for health checking. The value is an integer within the range of 2 to 10. The default value is 3.<br><br>The threshold is the number of consecutive health checks: if that many consecutive checks on a back\-end server pass, the server is considered healthy. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-unhealthy\-threshold |String |No |The unhealthy threshold for health checks. The value is an integer within the range of 2 to 10. The default value is 3.<br><br>The threshold is the number of consecutive health checks: if all the consecutive checks on a back\-end server fail, the server is considered unhealthy. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-interval |String |No |The time interval (seconds) of health checking. The value is an integer within the range of 1 to 300. The default interval is 10 seconds. |Yes |


<span id="jQXS33zR"></span>
### Configuring UDP health checking

An NLB Service allows you to configure UDP health checking for backend server groups by using annotations. The following is an example and description:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: "on" # (Required) Whether to enable health checking for back-end server groups. The value is on or off.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-type: "UDP" # (Optional) Health check protocol. Valid options include TCP, UDP, and HTTP.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-port: "80" # (Optional) The health check port. The value is an integer within the range of 1 to 65,535.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-connect-timeout: "8" # (Optional) Health check response timeout (in seconds). The value range is 1 to 60.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-udp-request: "request123" # (Optional) UDP health check request string. The string can contain only letters and numbers. The maximum string length is 64 characters. This setting and check-udp-expect must be either both empty or both non-empty.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-udp-expect: "expect123" # (Optional) The expected response string for UDP health checking. The string can contain only letters and numbers. The maximum string length is 64 characters. This setting and check-udp-request must be either both empty or both non-empty.
    service.beta.kubernetes.io/volcengine-loadbalancer-healthy-threshold: "4" # (Optional) Health threshold for health checking. The value is an integer within the range of 2 to 10.
    service.beta.kubernetes.io/volcengine-loadbalancer-unhealthy-threshold: "4" # (Optional) Unhealthy threshold for health checks. The value is an integer within the range of 2 to 10.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-interval: "5" # (Optional) The time interval (in seconds) of health checks. The value is an integer within the range of 1 to 300.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: UDP
    targetPort: 80
  type: LoadBalancer
```


The following table describes the annotations.


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-flag |String |No |Whether to enable health checking. Valid values:<br><br><br>* **on**: Yes (Default).<br><br>* **off**: Disable this setting. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-type |String |No |The health check protocol. Valid values:<br><br><br>* **TCP** (default)<br><br>* **UDP**<br><br>* **HTTP**<br><br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration must be consistent with the <code>protocol</code> configuration in the <code>spec.ports</code> field.</div><br> |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-port |String |No |The health check port. The value is an integer within the range of 1 to 65,535. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-connect\-timeout |String |No |The timeout in seconds for health checks. The value is an integer within the range of 1 to 60. The default value is 3.<br><br>‌If the back\-end server fails to respond within the timeout period, its health check status is marked as abnormal. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-udp\-request |String |No |The request string for UDP health checking.<br><br><br>* It can contain only letters and numbers. The maximum length is 64 characters.<br><br>* This setting and `check-udp-expect` must be either both empty or both non\-empty. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-udp\-expect |String |No |The expected response string for UDP health checking.<br><br><br>* It can contain only letters and numbers. The maximum length is 64 characters.<br><br>* This setting and `check-udp-request` must be either both empty or both non\-empty. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-healthy\-threshold |String |No |The health threshold for health checking. The value is an integer within the range of 2 to 10. The default value is 3.<br><br>The threshold is the number of consecutive health checks: if that many consecutive checks on a back\-end server pass, the server is considered healthy. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-unhealthy\-threshold |String |No |The unhealthy threshold for health checks. The value is an integer within the range of 2 to 10. The default value is 3.<br><br>The threshold is the number of consecutive health checks: if all the consecutive checks on a back\-end server fail, the server is considered unhealthy. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-interval |String |No |The time interval (seconds) of health checking. The value is an integer within the range of 1 to 300. The default interval is 10 seconds. |Yes |


<span id="bnerl0xT"></span>
### Configuring HTTP health checking

An NLB Service allows you to configure HTTP health checking for backend server groups by using annotations.  The following is an example and description:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-flag: "on" # (Required) Whether to enable health checking for back-end server groups. The value is on or off.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-type: "HTTP" # (Optional) Health check protocol. Valid options include TCP, UDP, and HTTP.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-port: "80" # (Optional) The health check port. The value is an integer within the range of 1 to 65,535.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-connect-timeout: "8" # (Optional) Health check response timeout (in seconds). The value range is 1 to 60.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-uri: "/" # (Optional) The health check path. The default value is "/".
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-domain: "example.com" # (Optional) The domain name for health checking.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-method: "GET" # (Optional) The health check method. Valid values include GET and HEAD.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-http-code: "http_2xx,http_3xx" # (Optional) The status code for a normal health check. Valid values include http_2xx, http_3xx, http_4xx, and http_5xx.
    service.beta.kubernetes.io/volcengine-loadbalancer-healthy-threshold: "4" # (Optional) Health threshold for health checking. The value is an integer within the range of 2 to 10.
    service.beta.kubernetes.io/volcengine-loadbalancer-unhealthy-threshold: "4" # (Optional) Unhealthy threshold for health checks. The value is an integer within the range of 2 to 10.
    service.beta.kubernetes.io/volcengine-loadbalancer-health-check-interval: "5" # (Optional) The time interval (in seconds) of health checks. The value is an integer within the range of 1 to 300.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-flag |String |No |Whether to enable health checking. Valid values:<br><br><br>* **on**: Yes (Default).<br><br>* **off**: Disable this setting. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-type |String |No |The health check protocol. Valid values:<br><br><br>* **TCP** (default)<br><br>* **UDP**<br><br>* **HTTP** |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-port |String |No |The health check port. The value is an integer within the range of 1 to 65,535. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-connect\-timeout |String |No |The timeout in seconds for health checks. The value is an integer within the range of 1 to 60. The default value is 3.<br><br>‌If the back\-end server fails to respond within the timeout period, its health check status is marked as abnormal. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-uri<br><br> |String |No |The health check path.<br><br><br>* It must start with a forward slash (`/`).<br><br>* It can contain letters, digits, hyphens (`-`), underscores (`_`), forward slashes (`/`), periods (`.`), percent signs (`%`), question marks (`?`), hash signs (`#`), ampersands (`&`), and equal signs (`=`).<br><br>* The length is limited to 1 to 128 characters.<br><br>* If this field is not configured, the default is `/`. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-domain |String |No |The domain name for health checking.<br><br><br>* It must contain at least one period (`.`) and cannot start or end with a period (`.`).<br><br>* It can contain uppercase and lowercase letters, digits, hyphens (`-`), and periods (`.`). It cannot start or end with hyphens (`-`).<br><br>* It can contain 1 to 80 characters.<br><br>* If this field is not configured, health checking uses the private IP address of the back\-end server. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-method |String |No |The health check method. Valid values:<br><br><br>* **GET**: This is the default method. To use the GET method, ensure that the server supports this method.<br><br>* **HEAD**: The HEAD method allows the server to return only the headers and thereby reduces backend overhead. To use the HEAD method, ensure that your server supports this method. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-http\-code |String |No |The HTTP status code for a normal health check. Available values:<br><br><br>* **http_2xx**<br><br>* **http_3xx**<br><br>* **http_4xx**<br><br>* **http_5xx** |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-healthy\-threshold |String |No |The health threshold for health checking. The value is an integer within the range of 2 to 10. The default value is 3.<br><br>The threshold is the number of consecutive health checks: if that many consecutive checks on a back\-end server pass, the server is considered healthy. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-unhealthy\-threshold |String |No |The unhealthy threshold for health checks. The value is an integer within the range of 2 to 10. The default value is 3.<br><br>The threshold is the number of consecutive health checks: if all the consecutive checks on a back\-end server fail, the server is considered unhealthy. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-health\-check\-interval |String |No |The time interval (seconds) of health checking. The value is an integer within the range of 1 to 300. The default interval is 10 seconds. |Yes |


<span id="99KzWcOl"></span>
### Configure client IP retention

<div data-tips="true" data-tips-type="warning">Note</div>



* <div data-tips="true" data-tips-type="warning">To use this feature, upgrade the cloud\-controller\-manager add\-on to v1.50.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading the add\-on</a>.</div>


* <div data-tips="true" data-tips-type="warning">This annotation is configured at the Service level. When a single Service includes multiple ports, the configuration applies to all backend server groups of the NLB instance.</div>



An NLB load Service allows you to configure client IP retention for backend server groups by using annotations. The following is an example and description:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-preserve-client-ip-enabled: "false" # (Required) Whether to enable the client IP retention feature. Valid values: true (enabled, default) and false (disabled)
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-preserve\-client\-ip\-enabled |String |Yes |Whether to enable client IP retention. Valid values:<br><br><br>* **true** (default): Yes. The NLB instance forwards requests to the backend server group with the client's source IP address. The backend server can obtain the client's source IP address without additional settings. After the server group is created, you can view this information on the details page.<br><br>* **false**: Disable it.<br><br>* If this annotation is not configured or its value is empty, the backend server group configuration is not modified.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When this annotation is deleted, the backend server group retains the configuration that existed before the deletion. To modify the configuration, first explicitly set this annotation to true or false, then remove the annotation.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Client IP retention is unavailable in the following scenarios:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the client and the server group use different IP versions, client IP retention does not take effect.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the server group is of <strong>IP type</strong>, you cannot enable this feature.</div><br> |Yes |


<span id="390kSbGS"></span>
## Configure listeners

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A listener can be created for an existing NLB instance or a new NLB instance. The following example uses an existing NLB instance for demonstration.</div>


<span id="Y5JxKwlQ"></span>
### Creating a TCP listener

If you do not use the `service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port` field to configure the load balancing protocol of the listener, the system configures the listener protocol based on the `spec.ports` field in the YAML file. For example, if `protocol` is set to TCP in `spec.ports`, the system creates a TCP listener. The example is as follows:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing LoadBalancer instance.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: TCP # Listener protocol. In this example, TCP is configured, which indicates that a TCP listener is created.
    targetPort: 80
  type: LoadBalancer
```


<span id="T80y0iby"></span>
### Creating UDP listeners

To specify the protocol for the listener, you can use` spec.ports` in the YAML file instead of the annotation `service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port`. For example, with the `protocol` under `spec.ports` set to UDP, the system will create a UDP listener accordingly. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing LoadBalancer instance.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
  selector:
    app: nginx
  ports:
  - name: test
    port: 80
    protocol: UDP # Listener protocol. In this example, the protocol is UDP, which indicates that a UDP listener is created.
    targetPort: 80
  type: LoadBalancer
```


<span id="DKWvwMdg"></span>
### Creating TLS listeners

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before you create an HTTPS listener, upload a CA certificate or SSL certificate to the Certificate Center. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Certificate-management">Managing certificates</a>, <a href="https://docs.byteplus.com/en/docs/6638/118034">Creating SSL certificates</a>, and <a href="https://docs.byteplus.com/en/docs/6638/118039">Uploading SSL certificates</a>.</div>


* <div data-tips="true" data-tips-type="warning">When you configure a TLS listener, take note of the following information:</div>


   * <div data-tips="true" data-tips-type="warning">The port number configured using <code>loadbalancer-protocol-port</code> (<code>443</code> in this example) must be declared in the <code>spec.ports</code> field. The <code>spec.ports.protocol</code> field for that port must be set to <code>TCP</code>.</div>


   * <div data-tips="true" data-tips-type="warning">If the configured port number (in this example, <code>443</code>) is not declared in the <code>spec.ports</code> field, the <code>TLS:443</code> specified in the annotation will be ignored.</div>


   * <div data-tips="true" data-tips-type="warning">If the configured port number is declared, but the <code>spec.ports.protocol</code> field is set to <code>UDP</code>, the <code>TLS:443</code> specified in the annotation will be ignored.</div>


   * <div data-tips="true" data-tips-type="warning">To configure both a UDP 443 port and a TLS 443 port, set <code>loadbalancer-protocol-port</code> to <code>TLS:443</code> and declare both the TCP 443 port and UDP 443 port in the <code>spec</code> field.</div>



Annotations for LoadBalancer services can be used to create TLS listeners on NLB instances. The following configuration provides an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-11ztoo3erqn***" # (Required) The ID of an existing LoadBalancer instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-protocol-port: "TLS:443" # (Required) The Layer 7 listener configuration, including a protocol (TLS in this example) and port number.
    service.beta.kubernetes.io/volcengine-loadbalancer-cert-source: "SSL" # (Required) The source of the HTTPS server certificate. Valid values include SSL and .
    service.beta.kubernetes.io/volcengine-loadbalancer-cert-id: "cert-9bb2ce26f05a456***" # (Required) The ID of the HTTPS certificate for servers.
    service.beta.kubernetes.io/volcengine-loadbalancer-security-policy-type: "system" # (Required) The type of security policy for the TLS listener. Valid values include system and custom.
    service.beta.kubernetes.io/volcengine-loadbalancer-security-policy-id: "tls_cipher_policy_1_0" # (Required) The TLS security policy.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
  selector:
    app: nginx # Bind the Service to backend pods through the label selector.
  ports:
  - name: test # The name of the port mapping policy.
    port: 443 # The service port.
    protocol: TCP  # Port communication protocol TCP/UDP. For a TLS listener, you must set the protocol to TCP.
    targetPort: 443 # The container port.
  type: LoadBalancer # Service type.
```


The following table describes the annotations.


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-protocol\-port |String |Yes |The Layer 7 protocol and port number for the listener. In this example, it is `TLS:443`. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cert\-source |String |No |The server certificate source. Valid values:<br><br><br>* **SSL**: (default) SSL certificate from the Certificate Center. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-cert\-id |String |No |Server certificate ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">CCM does not actively verify the validity of the certificate ID. If the certificate ID is invalid, the listener cannot be created successfully.</div><br> |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-tls\-security\-policy\-type |String |Yes |The security policy type of the TLS listener. Valid values:<br><br><br>* **custom**: Custom policy.<br><br>* **system** (default): System policy. |Yes |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-security\-policy\-id |String |Yes |The TLS security policy. You can select a system policy or a custom policy.<br><br><br>* For a system policy, the value can be one of the following:****<br><br>   * tls_cipher_policy_1_0<br><br>   * tls_cipher_policy_1_1<br><br>   * tls_cipher_policy_1_2<br><br>   * tls_cipher_policy_1_2_strict<br><br>   * tls_cipher_policy_1_2_strict_with_1_3<br><br>* For a custom policy, set the value to the ID of the custom policy.**** |Yes |


<span id="c57hXjwy"></span>
## Other configurations

<span id="bfMugA8j"></span>
### LB\-to\-pod direct access mode

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature can be enabled for an existing NLB instance or a new NLB instance. The following example uses an existing NLB instance for demonstration.</div>


* <div data-tips="true" data-tips-type="warning">Modify this annotation with caution, as it will cause an interruption of network traffic.</div>


* <div data-tips="true" data-tips-type="warning">If the LoadBalancer Service is associated with workloads deployed on VCI, you must enable LB\-to\-pod direct access mode. Otherwise, the service will be unavailable.</div>



Annotations for LoadBalancer services can be used to configure LB\-to\-pod direct access mode. Here is an example:

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-138jkmmlh2xa858***" # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-pass-through: "true" # (Optional) Whether to enable LB-to-pod direct access.
  name: nlb-service
  namespace: default
spec:
  loadBalancerClass: "volcengine.com/nlb" # Load balancer type. Specify that this Service uses NLB as the LoadBalancer implementation.
  externalTrafficPolicy: Local
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


|Field |Type |Required |Description |Changeable |
|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-pass\-through |String |No |Whether to enable LB\-to\-pod direct access mode. Valid values:<br><br><br>* **true**: Enabled Pods are specified as the backend servers of the load balancer.<br><br>* **false**: No.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This configuration is optional. If this configuration is not present, the default value differs by cluster network model:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For clusters that use the VPC\-CNI network model, the default value is <code>true</code>, which means LB\-to\-pod direct access mode is enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For clusters that use the Flannel network model, the default value is <code>false</code>, which means LB\-to\-pod direct access mode is not enabled.</div><br> |Yes |
