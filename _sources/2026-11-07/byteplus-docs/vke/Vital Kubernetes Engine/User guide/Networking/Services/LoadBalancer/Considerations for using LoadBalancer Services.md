---
title: "Considerations for using LoadBalancer Services"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_usage_precautions"
---

For each LoadBalancer service (a service with field type: LoadBalancer), the Cloud Controller Manager (CCM) add\-on of VKE creates or reuses a CLB/NLB instance for the service. This topic describes the key considerations in configuring a LoadBalancer Service.

<span id=".5paw5bu6LeWkjeeUqOi0n-i9veWdh-ihoeWunuS-iw=="></span>
## Creating or reusing an LB instance

You can either create a new CLB/NLB instance or reuse an existing one when configuring a service through the console or YAML settings. The following table shows the differences between creating and reusing CLB/NLB instances.


|Resource object |Creating CLB/NLB instance |Reusing CLB/NLB instance |
|---|---|---|
|CLB/NLB |* The controller will automatically create a CLB/NLB instance, a listener, and a backend server group based on the configurations in the Annotation field or in the console.<br><br>* When you delete the Service, the controller will delete the automatically created CLB/NLB instance. |* Specify the ID of the CLB/NLB instance to be reused in the annotation field service.beta.kubernetes.io/volcengine\-loadbalancer\-id.<br><br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><div data-tips="true" data-tips-type="danger">Do not reuse a CLB instance of a cluster API server, regardless of whether it is the CLB instance of the API server for the current cluster or another cluster. Otherwise, cluster exceptions may occur.</div><br><br><br><br>* The controller will create a listener and a backend server group for the CLB/NLB instance based on the other configurations in the Annotation field.<br><br>* When you delete the Service, the controller will delete the listener and backend server group created for the reused CLB/NLB instance. It will not delete the CLB/NLB instance.<br><br><br>&nbsp;<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the CLB/NLB instances that are created in the CLB/NLB console can be reused. This means that the CLB/NLB instances that are automatically created by the LoadBalancer Service of VKE cannot be reused.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">CLB/NLB instances achieve load balancing in virtual private clouds (VPCs). Therefore, the reused CLB/NLB instance must be deployed in the same VPC as the cluster.</div><br> |
|Listener |* The controller will automatically create a listener and a backend server group based on the configurations in the Annotation field or in the console.<br><br>* When you delete the Service, the controller will delete the created listener and backend server group. |* The controller will automatically create a listener and a backend server group based on the configurations in the Annotation field.<br><br>* The controller cannot create a listener on a port that already exists on a reused CLB/NLB instance. |


<span id=".Y2NtLeiwg-iwkOacuuWItg=="></span>
## CCM tuning mechanism

For each LoadBalancer service, i.e., the service with field `type: LoadBalancer`, Cloud Controller Manager (CCM) add\-on of VKE will create a new CLB/NLB or reuse the resources of an existing one, including the instance, listener, and backend server group.

Additionally, the CCM add\-on starts tuning in the following scenarios:


* Changes occur in the backend when you create, delete, and modify the Service. For example, pod IP addresses change, or pods are created or deleted.

* The configuration fields of the Service change, including Annotation, spec, and status.

* The controller pod is restarted.


<span id=".6YWN572u5rOo5oSP5LqL6aG5"></span>
## Configuration considerations


* We recommend specifying the parameters of the CLB/NLB instance either in the VKE console or through YAML. If you modify resources or configurations managed by the Service (such as forwarding rules) in the CLB/NLB console, your changes may be overwritten by the controller.

* If you manually modify the configurations of the CLB/NLB instance in the CLB/NLB console, the controller cannot detect the changes. Therefore, the controller cannot write the updated configurations in the CLB/NLB console into the Annotation field of the Service. When the Service triggers tuning, the updated configurations in the CLB/NLB console may be refreshed by the controller based on the configurations in the Annotation field.

* Part of the configurations for the CLB/NLB instance can be specified both through the Annotation field of the Service and the CLB/NLB console. Therefore, to avoid mutual overwriting of configurations that will cause business failures, you need to configure the CLB/NLB instance in VKE by the following logic:

   * When you configure the CLB/NLB instance for the first time, if related configurations (such as the access control of the listener) exist in the Annotation field of the Service, keep the CLB/NLB instance configurations the same as those in the Annotation field.

   * After you manually modify the configurations of the CLB/NLB instance in the CLB/NLB console, the configurations of the CLB/NLB instance remain consistent with those manual changes until the next tuning of the Service. When the Service is tuned again, the system will refresh the configurations based on the updated configurations in the spec and Annotation fields of the Service:

      * If the spec and Annotation fields of the Service do not change during the next tuning, the configurations of the CLB/NLB instance will not be refreshed. In this case, the actual configurations of the CLB/NLB instance remain consistent with the updated configurations in the CLB/NLB console.

      * If the spec field or the Annotation field of the Service changes during the next tuning, the configurations of the CLB/NLB instance will be refreshed based on the Annotation field. In this case, the updated configurations in the CLB/NLB console will be overwritten.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">Warning         </div>
         

         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">After you modify the spec field or the Annotation field of the Service, Service tuning may cause the manually updated configurations of the CLB/NLB instance in the CLB/NLB console to be overwritten. To prevent the preceding issues, when you modify the configurations of the CLB/NLB instance through the Annotation field of the Service, make sure that all configurations are consistent with those in the CLB/NLB console.         </div>
         

<span id=".5YW25LuW5rOo5oSP5LqL6aG5"></span>
## Other considerations


* Do not change the CLB instance, listener, backend server group, or forwarding rule created or managed by the Service in the CLB/NLB console without authorization. Otherwise, exceptions may occur in the LoadBalancer Service within the cluster.

* Do not modify any content prefixed with `k8s_` in the name of a listener or backend server group.

* Do not modify any content prefixed with `k8s_` in the description of a forwarding rule.

* Basic cloud resource fees will be incurred for the use of the CLB service. For detailed information, refer to [CLB Billing overview](https://docs.byteplus.com/en/docs/clb/Billing-01) and [NLB Billing overview](https://docs.byteplus.com/en/docs/clb/NLB-Billing).
