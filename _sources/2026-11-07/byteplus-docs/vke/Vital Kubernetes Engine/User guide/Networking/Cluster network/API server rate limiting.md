---
title: "API server rate limiting"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/API_server_rate_limiting"
---

API Priority and Fairness (APF) is Kubernetes' native request\-traffic management mechanism designed to ensure control plane stability when the API Server load increases. This topic describes the basic principles of APF and how to view and mitigate APF rate limiting.

<span id="MNG1iTEi"></span>
## Background

<span id="JHEBw5f1"></span>
### Overview of API server rate limiting

As the sole API entry point for Kubernetes clusters, the API Server handles requests initiated by nodes, controllers, O&M scripts, and business\-side clients. To prevent control plane resource depletion and API service unavailability due to abnormal traffic from certain clients, Kubernetes implements a request\-throttling mechanism: before requests enter the API Server processing flow, they undergo an admission check by the rate\-limiting component. Requests that fail the admission check are directly rejected (status code 429). In VKE clusters, rate limiting for the API Server is primarily implemented based on APF.

<span id="SHQLEhG4"></span>
### APF overview

<span id="kQW9eB49"></span>
#### What is APF?

APF is a Kubernetes\-native request traffic management mechanism designed to classify, prioritize, queue, and reject requests sent to the API Server. Its core working logic is as follows:


1. Request grouping: APF first matches requests to a specific **FlowSchema** based on attributes such as the request source, requested resource, and request verb.

2. Seat allocation: After request matching, requests are then mapped to a specific **PriorityLevelConfiguration**. This PriorityLevelConfiguration determines how many concurrency seats this type of request can occupy and whether requests are queued or rejected when the concurrency limit is exceeded.


The following table describes common APF concepts:


|**Term** |**Function** |Meaning |
|---|---|---|
|FlowSchema |Request classification |Defines which flow a request belongs to. The classification conditions are usually related to attributes such as the request source, target resource, and namespace.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more information about the FlowSchema resource and its configuration fields, see the <a href="https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#flowschema">official documentation</a>.</div><br> |
|PriorityLevelConfiguration |Priority configuration |Specifies the processing capacity allocated to a given flow category, as well as the handling policy (queuing or rejection) when seats are insufficient.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">For more information about the PriorityLevelConfiguration resource and its configuration fields, see the <a href="https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#prioritylevelconfiguration">official documentation</a>.</div><br> |
|Seats |Concurrency seats |The basic unit of concurrent processing capacity allocated to a priority level. By default, APF allocates one seat to a request but may assign multiple seats in certain scenarios. When all seats are occupied, new requests cannot be executed immediately. |
|Queue |Queuing |When seats are temporarily insufficient, requests will first enter a queue and wait there. If the waiting time exceeds the threshold or the queue reaches full capacity, the requests will be rejected. |


<span id="lRBp2RHj"></span>
#### APF workflow

When a request enters the API Server, the APF operates using the workflow below:


1. APF first determines which flow the request belongs to according to FlowSchema rules.

2. APF assigns the request to the corresponding PriorityLevelConfiguration.

   1. If the PriorityLevelConfiguration still has available concurrency seats, the request is executed directly.

   2. If the PriorityLevelConfiguration has no available concurrency seats and queuing is allowed, the request enters the queue.

   3. If all concurrency seats are occupied and the queue cannot continue accepting requests, the request is rejected with a `429 Too Many Requests` response.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">APF rate limiting ‌focuses not on equal distribution, but on ‌prioritizing critical traffic when the control plane is under stress. For example, requests from system components and node heartbeat requests generally should not compete for the same priority level as regular batch query requests.</div>


<span id="WFzx4S60"></span>
### Default configurations in VKE

In VKE clusters, a single API Server has a default concurrency limit of 600 simultaneous requests. The control plane of a VKE cluster adopts a highly available architecture with at least two API Server replicas deployed, doubling the cluster's overall concurrent request capacity. If the control plane is further scaled out (by adding more replicas), the overall concurrent capacity increases linearly. In addition, the control plane of VKE clusters supports dynamic specification upgrade based on actual load. When the specification is upgraded, the concurrency limit of a single API Server will be automatically increased.

<span id="qwsgi1Uh"></span>
### View APF resources

To check which APF rules are currently applied in your cluster, view the FlowSchema and PriorityLevelConfiguration objects in the cluster.


1. [Use kubectl to connect to the clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to view the FlowSchema objects in the cluster.

   ```Bash
   kubectl get flowschema
   ```
   

   The following is the expected result (listing existing FlowSchema objects in the cluster).

   ```Bash
   NAME                           PRIORITYLEVEL      MATCHINGPRECEDENCE   DISTINGUISHERMETHOD   AGE    MISSINGPL
   exempt                         exempt             1                    <none>                4d3h   False
   probes                         exempt             2                    <none>                4d3h   False
   system-leader-election         leader-election    100                  ByUser                4d3h   False
   system-node-high               node-high          400                  ByUser                4d3h   False
   system-nodes                   system             500                  ByUser                4d3h   False
   vke-cello-list                 vke-lowest-limit   505                  ByUser                4d3h   False
   vke-list-limit                 vke-list-limit     511                  ByUser                4d3h   False
   kube-controller-manager        workload-high      800                  ByNamespace           4d3h   False
   kube-scheduler                 workload-high      800                  ByNamespace           4d3h   False
   kube-system-service-accounts   workload-high      900                  ByNamespace           4d3h   False
   service-accounts               workload-low       9000                 ByUser                4d3h   False
   global-default                 global-default     9900                 ByUser                4d3h   False
   catch-all                      catch-all          10000                ByUser                4d3h   False
   ```
   

   The key fields are described in the following table.

   
   |Field |Description |
   |---|---|
   |NAME |FlowSchema name. |
   |PRIORITYLEVEL |PriorityLevelConfiguration that is mapped to the current FlowSchema. |
   |MATCHINGPRECEDENCE |Matching precedence. The lower the value, the higher the matching precedence. |
   |DISTINGUISHERMETHOD |The method of splitting requests into queues. Available options include:<br><br><br>* `ByUser`: Isolates by user.<br><br>* `ByNamespace`: Isolates by namespace.<br><br>* `<none>`: No isolation is applied. All requests share the same queue. |
   |AGE |The duration for which the FlowSchema has existed. |
   |MISSINGPL |Whether the associated PriorityLevelConfiguration is missing. Valid values:<br><br><br>* `False`: The associated queue exists and is normal.<br><br>* `True`: The associated queue does not exist and is abnormal. |
   

4. Run the following command to view PriorityLevelConfiguration objects in the cluster.

   ```Bash
   kubectl get prioritylevelconfiguration
   ```
   

   The following is the expected result (listing existing PriorityLevelConfiguration objects in the cluster).

   ```Bash
   NAME               TYPE      NOMINALCONCURRENCYSHARES   QUEUES   HANDSIZE   QUEUELENGTHLIMIT   AGE
   catch-all          Limited   5                          <none>   <none>     <none>             4d3h
   exempt             Exempt    <none>                     <none>   <none>     <none>             4d3h
   global-default     Limited   20                         128      6          50                 4d3h
   leader-election    Limited   10                         16       4          50                 4d3h
   node-high          Limited   40                         64       6          50                 4d3h
   system             Limited   30                         64       6          50                 4d3h
   vke-list-limit     Limited   10                         64       4          50                 4d3h
   vke-lowest-limit   Limited   1                          64       4          50                 4d3h
   workload-high      Limited   40                         128      6          50                 4d3h
   workload-low       Limited   100                        128      6          50                 4d3h
   ```
   

   The key fields are described in the following table.

   
   |Field |Description |
   |---|---|
   |NAME |PriorityLevelConfiguration name. |
   |TYPE |Resource type. Valid values:<br><br><br>* `Exempt`: Requests are exempt from rate limiting and can pass through directly.<br><br>* `Limited`: Requests are rate\-limited‌ and subject to queuing. |
   |NOMINALCONCURRENCYSHARES |The concurrency share. It determines how many concurrency seats a queue at the corresponding priority level can be allocated. This value is a relative weight, not an absolute value. It indicates the relative weight of this PriorityLevelConfiguration among all Limited PriorityLevelConfigurations. Generally, a larger value means more concurrency seats can be allocated to this PriorityLevelConfiguration. However, it is not equivalent to a fixed absolute concurrency limit. |
   |QUEUES |Queue count. Requests can be distributed across sub\-queues via ByUser and ByNamespace. |
   |HANDSIZE |Shuffling hand size. When a request arrives, N sub\-queues are randomly selected, and the request is routed to the shortest sub\-queue. The larger this value is, the more precise the load balancing effect will be. |
   |QUEUELENGTHLIMIT |Maximum queuing length limit per sub\-queue. Requests will be rejected directly with a `429 Too Many Requests` response if the queue length exceeds this threshold. |
   |AGE |The duration for which the PriorityLevelConfiguration has existed. |
   


<span id="bfArX14u"></span>
## Check for APF rate limiting

Rate limiting is triggered when request traffic to the API Server exceeds the allowed concurrency seats. You can determine whether rate limiting occurs in the cluster through the following methods:


* Check whether the client frequently receives `429 Too Many Requests` responses. If yes, the requests have been rejected by the server.  This is usually the most direct signal of rate limiting.

* Use the cloud\-native observability feature of VKE to directly check APF\-related metrics and the dashboard for the API Server. For details, see [Control plane service observability](https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability).


<span id="wgCAy5FP"></span>
## Mitigate APF rate limiting

<span id="p9v8xiWJ"></span>
### Step 1: Optimize client behavior

When client requests are rate\-limited by APF, we recommend optimizing client behavior first. For details, see [Large-scale cluster limits and recommendations](https://docs.byteplus.com/en/docs/vke/Large-scale_cluster_limits_and_suggestions).

<span id="6HHXciYK"></span>
### Step 2: Adjust APF configurations

If all the following conditions are met, consider modifying APF configurations to mitigate rate\-limiting issues:


* Rate\-limited traffic originates from ‌stable, business\-critical workloads‌.

* You have implemented basic client\-side optimizations, such as avoiding frequent list/watch operations, adding a backoff mechanism for retries, and reducing unnecessary full\-data queries. Adjusting APF configurations is only recommended if `429 Too Many Requests` errors persist after the above optimizations are implemented.

* The current default APF rules still cannot meet business requirements.


<span id="UytAOpZX"></span>
#### Method 1: Adjust existing PriorityLevelConfigurations

You can allocate more concurrency seats to specified requests by adjusting the `nominalConcurrencyShares` field in a PriorityLevelConfiguration. If necessary, you can also evaluate and adjust the number of queues and the queue length limit.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Be cautious when modifying FlowSchemas and PriorityLevelConfigurations. Misconfiguration may cause ‌API Server request loss and server service disruption.</div>


* <div data-tips="true" data-tips-type="warning">If you need to modify the default APF objects, set <code>apf.kubernetes.io/autoupdate-spec</code> to <code>false</code> to prevent the system from automatically reverting the configuration to the default settings later.</div>



The following is a configuration example. In this example, you can allocate more concurrency shares for this type of request by adjusting the `nominalConcurrencyShares` field in the PriorityLevelConfiguration.

```YAML
apiVersion: flowcontrol.apiserver.k8s.io/v1
kind: PriorityLevelConfiguration
metadata:
  name: global-default
  annotations:
    apf.kubernetes.io/autoupdate-spec: "false" # Set it to false to prevent the system from automatically reverting the configuration to the default settings later.
spec:
  type: Limited
  limited:
    nominalConcurrencyShares: 40 # Set the concurrency share for this type of request. This value is a relative weight, not an absolute value.
    lendablePercent: 50
    limitResponse:
      type: Queue
      queuing:
        queues: 128
        handSize: 6
        queueLengthLimit: 50
```


The key fields are described in the following table.


|Field |Description |
|---|---|
|**Basic field** ||
|name |PriorityLevelConfiguration name. A FlowSchema references the PriorityLevelConfiguration by its name. |
|apf.kubernetes.io/autoupdate\-spec |The APF auto\-update toggle switch. When you set it to `false`, the system will skip auto\-update for this resource. This prevents the system from automatically reverting the configuration to the default settings. |
|**spec fields** ||
|type |Resource type. Valid values:<br><br><br>* `Exempt`: Requests are exempt from rate limiting and can pass through directly.<br><br>* `Limited`: Requests are rate\-limited‌ and subject to queuing. |
|limited.nominalConcurrencyShares |The concurrency share. It determines how many concurrency seats a queue at the corresponding priority level can be allocated. This value is a relative weight, not an absolute value. It indicates the relative weight of this PriorityLevelConfiguration among all Limited PriorityLevelConfigurations. Generally, a larger value means more concurrency seats can be allocated to this PriorityLevelConfiguration. However, it is not equivalent to a fixed absolute concurrency limit.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can use the <code>kubectl get prioritylevelconfiguration</code> command to view all PriorityLevelConfigurations in the cluster. In this example, the total relative weight of Limited PriorityLevelConfigurations is 256. For details, see <a href="https://docs.byteplus.com/en/docs/90/110465#qwsgi1Uh">View APF Resources</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Assume the total number of concurrency seats is 600. When the global\-default PriorityLevelConfiguration has a concurrency weight of 20, seats allocated to this PriorityLevelConfiguration (among all Limited ones) are approximately 20 / 256 × 600 = 46.</div><br> |
|limited.lendablePercent |Proportion of lendable concurrency seats. It indicates the percentage of this PriorityLevelConfiguration's concurrency seats that may be borrowed by other PriorityLevelConfigurations when this one is idle. This field enables APF's elastic borrowing mechanism, which avoids wasting idle resources in PriorityLevelConfigurations.<br><br><br>* In this example, the field is set to 50, meaning this PriorityLevelConfiguration allows up to 50% of its seats to be lent.<br><br>* When requests for this PriorityLevelConfiguration increase, the lent seats will be recalled. |
|limitResponse.type |Processing policy for requests that exceed the concurrency limit. Valid values:<br><br><br>* `Queue`: Requests will enter a queue and await processing.<br><br>* `Reject`: Requests will be rejected directly with a `429 Too Many Requests response`. |
|queuing.queues |The number of sub\-queues. In this example, the value is set to 128. Requests are distributed across sub\-queues based on the `distinguisherMethod` in the FlowSchema, preventing requests from a user or namespace from blocking the entire queue. |
|queuing.handSize |Shuffling hand size. In this example, the value is set to 6. This means the system randomly selects 6 from all sub\-queues (128 in this example) and puts a request into the shortest sub\-queue. |
|queuing.queueLengthLimit |The maximum length for a single sub\-queue. In this example, the value is set to 50. It means that when there are already 50 queued requests in a sub\-queue, new incoming requests targeting this sub\-queue will be directly rejected with a `429 Too Many Requests` response and will not be added to the sub\-queue. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For information about other PriorityLevelConfiguration fields, see the <a href="https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#prioritylevelconfiguration">official documentation</a>.</div>


<span id="J7NRGIi7"></span>
#### Method 2: Add a custom FlowSchema

If the currently rate\-limited business\-critical requests are mixed with other common requests, you can also add a finer\-grained FlowSchema to match critical requests to a separate PriorityLevelConfiguration. This prevents these critical requests from being permanently governed by default rules and competing with other request traffic for resources.

In the following example, a new FlowSchema is created to specifically match List requests and is associated with the workload\-high PriorityLevelConfiguration, which has a higher `nominalConcurrencyShares` value. Meanwhile, the `matchingPrecedence` field is set to 9000. This ensures its matching precedence is higher than that of the FlowSchema that the requests would originally hit (the global\-default FlowSchema in this example).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating a custom FlowSchema, pay special attention to the <code>matchingPrecedence</code> field. Requests will hit the new rule first only if the new rule has a higher matching precedence.</div>


```YAML
apiVersion: flowcontrol.apiserver.k8s.io/v1
kind: FlowSchema
metadata:
  name: requests-from-demo-sa
spec:
  matchingPrecedence: 9000 # The matching precedence. The smaller the value, the higher the matching precedence.
  distinguisherMethod: # The method of splitting requests into queues. Valid values: ByUser (queue isolation by user), ByNamespace (queue isolation by namespace), <none> (no isolation, with a single queue used)
    type: ByUser
  priorityLevelConfiguration:
    name: workload-high
  rules:
    - subjects:
        - kind: ServiceAccount
          serviceAccount:
            name: demo-service-account
            namespace: demo-namespace
      resourceRules:
        - verbs: ["list"]
          apiGroups: ["*"]
          resources: ["pods"]
          namespaces: ["default"]
```


The key fields are described in the following table.


|Field |Description |
|---|---|
|**Basic field** ||
|name |FlowSchema name. It is used for FlowSchema identification and management. |
|**spec fields** ||
|matchingPrecedence |Matching precedence. The lower the value, the higher the matching precedence. |
|distinguisherMethod.type |The method of splitting requests into queues. Valid values:<br><br><br>* `ByUser`: Isolates by user.<br><br>* `ByNamespace`: Isolates by namespace.<br><br>* `<none>`: No isolation is applied. All requests share the same queue. |
|priorityLevelConfiguration.name |The associated PriorityLevelConfiguration. In this example, requests matching this FlowSchema will be assigned to the `workload-high` PriorityLevelConfiguration. |
|**rule matching fields** ||
|subjects |Request initiators. In this example, the values of the fields are described as follows:<br><br><br>* `kind: ServiceAccount`: Matches identities of the ServiceAccount type<br><br>* `name: demo-service-account`: Specifies the ServiceAccount name.<br><br>* `namespace: demo-namespace`: Specifies the namespace where the ServiceAccount is located. |
|resourceRules |The ‌operation scope of request matching. In this example, the following values are specified:<br><br><br>* `verbs`: Only matches `list` operations. You can also specify other values, such as `get`, `watch`, `create`, and `delete`. You can use the wildcard `*` to specify all operations.<br><br>* `apiGroups`: Matches all API groups.<br><br>* `resources`: Only matches operations on Pod resources.<br><br>* `namespaces`: Only matches requests occurring in the default namespace. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about FlowSchema fields, see the <a href="https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#flowschema">official documentation</a>.</div>


<span id="TEEAwU4m"></span>
### Validate results

After completing client\-side optimizations or APF configuration adjustments, you can use the following steps to confirm whether APF rate limiting has been mitigated.


1. Check whether `429 Too Many Requests` responses on the client side have significantly decreased.

2. Confirm whether the growth rate of the `apiserver_flowcontrol_rejected_requests_total` metric on the dashboard has slowed. For details, see [Control plane service observability](https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability).

3. Check whether the concurrency seat occupancy of the target PriorityLevelConfiguration has returned to a controllable range.

4. Verify whether ‌waiting times and success rates for business\-critical requests are normal.
