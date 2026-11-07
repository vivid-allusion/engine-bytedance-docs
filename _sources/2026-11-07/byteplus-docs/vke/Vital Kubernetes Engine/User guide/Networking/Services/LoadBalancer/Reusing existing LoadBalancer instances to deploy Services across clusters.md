---
title: "Reusing existing LoadBalancer instances to deploy Services across clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Reusing_a_LoadBalancer_to_achieve_cross-cluster_deployment_of_services"
---

Cross\-cluster service deployment can provide better disaster tolerance and reliability for business, and realize high\-level security isolation. However, creating an individual LoadBalancer instance to realize a load balancing service for each cluster will lead to a waste of resources. You can use a single LoadBalancer instance to provide service across multiple clusters by mounting the internal endpoints of those clusters to the instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">The annotations in YAML files are case\-sensitive.</div>


* <div data-tips="true" data-tips-type="warning">It is highly recommended that you first read <a href="https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_usage_precautions">Considerations for using LoadBalancer services</a> carefully before getting started.</div>



<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5Zy65pmv5LiA77ya5bCG5rWB6YeP6L2s5Y-R6Iez6ZuG576k5ZKM5aSW6YOo56uv54K5"></span>
### Scenario 1: Forwarding traffic to a cluster and external endpoints

You can mount the services running in the cluster and the endpoints (for example, ECS) working outside the cluster onto the same CLB or NLB instance, so that the business deployed on clusters and ECS instances can share the same entry.

<span id=".5Zy65pmv5LqM77ya5bCG5rWB6YeP6L2s5Y-R6Iez5aSa5Liq6ZuG576k5YaF55qELXNlcnZpY2U="></span>
### Scenario 2: Forwarding traffic to the services running in multiple clusters

You can mount the services running in different clusters onto an existing CLB or NLB instance to provide the same entry. The services reusing the same CLB or NLB instance need to share the same listener and back\-end server group. Therefore, you need to manually configure the listener and back\-end server group for the CLB or NLB instance, so that those services can reuse the group. Moreover, the listener needs to be listening to the ports on which those services are running.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Only the CLB or NLB instances manually created can be reused. In other words, CLB or NLB instances automatically created for LoadBalancer Services cannot be reused.

* You cannot add, delete, or modify the `service.beta.kubernetes.io/volcengine-loadbalancer-id` field on an existing service.

* You cannot add, delete, or modify the `service.beta.kubernetes.io/volcengine-loadbalancer-server-group-id` field on an existing service.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A CLB or NLB instance, listener, and back\-end server group have been created.

   * For information about how to configure CLB instances, see [Creating CLB instances](https://docs.byteplus.com/en/docs/clb/CLB-instances-01), [Creating listeners](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener), and [Creating back-end server groups](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group).

   * For information about how to configure NLB instances, see [Creating NLB instances](https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance?lang=zh), [Adding listeners](https://docs.byteplus.com/en/docs/clb/NLB-Adding-a-listener), and [Creating back-end server groups](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group).

* To connect to an NLB instance, make sure that the cloud\-controller\-manager add\-on is upgraded to v1.45.1 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="caaPjzBrGm" title="Reusing CLB instances">
<TabTitle>Reusing CLB instances</TabTitle>

Use the following YAML configuration to create a service and reuse the manually created CLB instance in a VKE (Vital Kubernetes Engine) cluster.

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "clb-mim02n8g5kw05smt1b******"
    # (Required) ID of an existing CLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-server-group-id: "rsp-22j***:80,rsp-22j***:443"
    # Required. Existing backend server group ID and port number
    service.beta.kubernetes.io/volcengine-loadbalancer-weight: "10"
    # Required. Weight of backend server group 
  name: clb-service # The name of the service.
  namespace: default # The namespace to which the service belongs.
spec:
  externalTrafficPolicy: Cluster
  selector:
    app: nginx # Bind the service to back-end pods through the label selector.
  ports:
  - name: test # The name of the port mapping policy.
    port: 80 # The service port.
    protocol: TCP  # The communication protocol TCP/UDP.
    targetPort: 80 # The container port.
  type: LoadBalancer # Service type.
```





</Tab>
<Tab zoneid="ZbHhQWhx6q" title="Reusing NLB instances">
<TabTitle>Reusing NLB instances</TabTitle>

Use the following YAML configuration to create a Service and reuse a manually created CLB instance in the VKE cluster.

```YAML
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/volcengine-loadbalancer-id: "nlb-138jkmmlh2xa858j***"
    # (Required) The ID of an existing NLB instance.
    service.beta.kubernetes.io/volcengine-loadbalancer-server-group-id: "rsp-138k***:80,rsp-22j***:443"
    # Required. Existing backend server group ID and port number
    service.beta.kubernetes.io/volcengine-loadbalancer-weight: "10"
    # Required. Weight of backend server group 
  name: nlb-service # The name of the service.
  namespace: default # The namespace to which the service belongs.
spec:
  loadBalancerClass: "volcengine.com/nlb" # Use the NLB instance.
  externalTrafficPolicy: Local
  selector:
    app: nginx # Bind the service to back-end pods through the label selector.
  ports:
  - name: test # The name of the port mapping policy.
    port: 80 # The service port.
    protocol: TCP # The communication protocol TCP/UDP.
    targetPort: 80  # The container port.
  type: LoadBalancer # Service type.
```





</Tab>
</Tabs>


The following table describes the annotations.


|Key |Type |Required |Description |Default value |Changeable |
|---|---|---|---|---|---|
|service.beta.kubernetes.io/volcengine\-loadbalancer\-id |String |Yes |The ID of an existing CLB or NLB instance. |No |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-server\-group\-id |String |Yes |Group ID and port number of the existing backend server.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The IDs and port numbers of the backend server groups. Note that the port numbers need to be correspondingly consistent with the <code>port</code> under the <code>spec.ports</code> of the service, instead of the <code>targetPort</code> or <code>nodePort</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple pairs of ID and port need to be separated with commas. You can add as many pairs as you want.</div><br> |No |No |
|service.beta.kubernetes.io/volcengine\-loadbalancer\-weight |String |Yes |The weight on the back\-end server.<br><br><br>* The value is an integer from 0 to 100. A greater weight means that the back\-end server will receive more requests.<br><br>* A value of 0 indicates that the server will no longer accept new requests.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about weights on back\-end servers, see <a href="https://docs.byteplus.com/en/docs/clb/Adding-a-server">Adding or removing back\-end servers</a>.</div><br> |No |No |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For different network models, the objects mounted in the back\-end server group of CLB or NLB instances differ:</div>



* <div data-tips="true" data-tips-type="default">VPC\-CNI:</div>


   * <div data-tips="true" data-tips-type="default">The LB\-to\-pod direct access mode is not enabled by default for connecting to CLB instances. That means the cluster will mount the node where the pod of the back\-end service is located as a back\-end server in the back\-end server group. To enable LB\-to\-pod direct access, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations">Configuring CLB services based on annotations</a>.</div>


   * <div data-tips="true" data-tips-type="default">The LB\-to\-pod direct access mode is enabled by default for connecting to NLB instances. That means the cluster will directly mount the pod of the back\-end service in the NLB server group.</div>


* <div data-tips="true" data-tips-type="default">Flannel:</div>


   * <div data-tips="true" data-tips-type="default">If a CLB or NLB instance is associated with a workload that is deployed using ECS, the cluster mounts the node where the pod of the back\-end service is located as a back\-end server in the CLB or NLB back\-end server group.</div>


   * <div data-tips="true" data-tips-type="default">If a CLB or NLB instance is associated with a workload that is deployed using VCI, the cluster mounts the pod directly to the back\-end server group of the CLB or NLB instance.</div>



<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results


1. Execute the following command to view the service created.

   ```bash
   kubectl get svc -n default
   ```
   

   The information below is what will be printed on the screen. The `EXTERNAL-IP` is the public IP address of the CLB or NLB instance to which the service is attached.

   ```bash
   NAME          TYPE           CLUSTER-IP        EXTERNAL-IP      PORT(S)         AGE
   clb-service   LoadBalancer   172.xxx.xxx.xxx   14.xxx.xxx.xxx   80:30891/TCP    44s
   ```
   

2. Execute the following command to view the service created.

   ```bash
   kubectl describe svc clb-service -n default
   ```
   

   The information below is what will be printed on the screen. The Annotations field displays information about the manually created CLB or NLB instance, including the instance ID and backend server group ID. This information is consistent with the CLB or NLB instance you created manually.

   ```bash
   Name:                     clb-service
   Namespace:                default
   Labels:                   service.beta.kubernetes.io/volcengine-loadbalancer-id=clb-22j***
   Annotations:              service.beta.kubernetes.io/system-volcengine-loadbalancer-last-applied-annotations:
                               {"service.beta.kubernetes.io/volcengine-loadbalancer-id":"clb-22j***","service.beta.kubernetes.io/volcengine-loadbalanc...
                             service.beta.kubernetes.io/volcengine-loadbalancer-id: clb-22j***
                             service.beta.kubernetes.io/volcengine-loadbalancer-server-group-id: rsp-22j***:80
                             service.beta.kubernetes.io/volcengine-loadbalancer-weights: 10
   Selector:                 app=nginx
   Type:                     LoadBalancer
   IP Family Policy:         SingleStack
   IP Families:              IPv4
   IP:                       172.21.xxx.xxx
   IPs:                      172.21.xxx.xxx
   LoadBalancer Ingress:     14.xxx.xxx.xxx
   Port:                     test  80/TCP
   TargetPort:               80/TCP
   NodePort:                 test  30036/TCP
   Endpoints:                192.168.0.44:80
   Session Affinity:         None
   External Traffic Policy:  Cluster
   Events:
     Type    Reason                Age                    From                Message
     ----    ------                ----                   ----                -------
     Normal  EnsuringLoadBalancer  2m19s (x2 over 2m22s)  service-controller  Ensuring load balancer
     Normal  EnsuredLoadBalancer   2m18s (x2 over 2m19s)  service-controller  Ensured load balancer
   ```
   

3. Log in to the [load balancer console](https://console.byteplus.com/clb) to view the corresponding CLB or NLB instance and back\-end server group list. You can view the newly added back\-end servers and their weights in the back\-end server group.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For more information about how to configure LoadBalancer Services with annotations, see [Using annotations to configure CLB Services](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations) and [Using annotations to configure NLB Services](https://docs.byteplus.com/en/docs/vke/Configuring_an_NLB_Service_using_annotations).
