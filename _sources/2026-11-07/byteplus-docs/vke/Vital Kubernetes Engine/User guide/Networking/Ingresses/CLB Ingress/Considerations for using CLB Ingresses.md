---
title: "Considerations for using CLB Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Precautions_for_using_CLB_Ingress"
---

When configuring CLB Ingresses, the system will create or reuse a LoadBalancer (Classic Load Balancer, CLB) instance for the Ingress through add\-ons. This topic introduces the key considerations when configuring CLB Ingresses.

<span id=".5paw5bu6LeWkjeeUqOi0n-i9veWdh-ihoeWunuS-iw=="></span>
## Creating or reusing CLB instances

You can choose to create a new CLB or reuse an existing one when configuring CLB Ingresses for a VKE cluster on the console or through YAML configuration. The following table shows the differences between creating and reusing CLB instances.


|Resource object Object |Creating CLB Instance |Reusing CLB Instance |
|---|---|---|
|CLB |* The controller will automatically create a CLB, a listener, and a backend server group according to the configurations in the annotations.<br><br>* When deleting the Ingress, the controller will delete the CLB that was automatically created. |* Specify the ID of the reused CLB instance in the annotation `ingress.vke.volcengine.com/loadbalancer-id`.<br><br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><div data-tips="true" data-tips-type="danger">Do not reuse a CLB instance of a cluster API server, regardless of whether it is the CLB instance of the API server for the current cluster or another cluster. Otherwise, cluster failures may occur.</div><br><br><br><br>* The controller will create a listener and a backend server group for the CLB instance based on the other configurations in the Annotation field.<br><br>* When deleting an Ingress, the controller will delete the listeners and backend server groups created along with the reused CLB, but will not delete the CLB instance.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the CLB created through the LoadBalancer console can be reused. The CLB automatically created along with VKE Ingresses cannot be reused.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The reused CLB needs to be in the same VPC as the cluster to provide load\-balancing service.</div><br> |
|Listener |* The controller will automatically create a listener and a backend server group based on the configurations in the Annotation field.<br><br>* When deleting the Ingress, the controller will delete the related listeners and backend server groups. |* The controller will automatically create a listener and a backend server group according to the configurations in the annotations.<br><br>* The controller cannot create a listener on a port that already exists on a reused CLB instance. |


<span id=".6YWN572u5rOo5oSP5LqL6aG5"></span>
## Configuration considerations


* We recommend configuring CLB instance parameters uniformly, either in the VKE console or via YAML. If resources or configurations specified or maintained by Ingress (such as forwarding rules) are modified in the LoadBalancer console, there is a risk that the configuration may be overwritten.

* The controller cannot detect the changes made through the LoadBalancer console to the configurations of CLB instances. In other words, the controller cannot save the changes made on LoadBalancer console into the annotations of Ingresses. When the Ingress triggers reconciliation, the changes made through the LoadBalancer console may be updated by the controller according to the configurations in the annotations.


<span id=".5YW25LuW5L2_55So6ZmQ5Yi2"></span>
## Other considerations


* Do not change the CLB instances associated with the CLB Ingress you created, or other related resources such as listeners, backend server groups, and forwarding rules. Otherwise, CLB services may malfunction, and you will be fully responsible for any consequences of your actions.

* Do not modify any content prefixed with `k8s_` in the name of a listener or backend server group.

* If you modify resources or configurations specified or maintained by the CLB Ingress on the server side, the configurations may be overwritten.

* There are fees for using LoadBalancer (Classic Load Balancer, CLB) products. For details, see [Billing overview](https://docs.byteplus.com/en/docs/clb/Billing-07).
