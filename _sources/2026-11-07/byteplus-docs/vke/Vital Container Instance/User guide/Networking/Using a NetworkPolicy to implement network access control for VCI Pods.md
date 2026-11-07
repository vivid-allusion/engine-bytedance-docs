---
title: "Using a NetworkPolicy to implement network access control for VCI Pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_a_NetworkPolicy_to_implement_network_access_control_for_VCI_Pods"
---

A Kubernetes NetworkPolicy implements policy\-based network access control. This topic describes how to use a NetworkPolicy to implement Pod network access control in VCI scenarios.

<span id="T5r8xTHv"></span>
## Background

VCI uses a nodeless architecture, so Pods do not run on nodes that you can view or manage. Traditional NetworkPolicy solutions that rely on node DaemonSets, such as calico\-node, cannot be used directly in VCI scenarios. A VCI NetworkPolicy uses the capabilities of a centralized control plane and Cello/Cilium to inject and enforce access policies directly at the pod network layer. It provides the following capabilities:


* **Alignment with Kubernetes standards**: This resource is fully compatible with NetworkPolicy resources of `networking.k8s.io/v1`, allowing you to migrate existing policies from other Kubernetes environments at no cost.

* **Adaptation to the nodeless architecture**: Policies take effect dynamically with the Pod lifecycle. You do not need to deploy additional agents on Pods or nodes.

* **L3/L4 access control**: The resource supports Ingress and Egress rules based on Pod labels, namespace labels, and CIDR. You can specify TCP/UDP ports and port ranges.


For basic concepts, field meanings, and complete YAML syntax of Kubernetes NetworkPolicies, see the [Kubernetes community documentation](https://kubernetes.io/zh-cn/docs/concepts/services-networking/network-policies/).

<span id="yGC9qKxR"></span>
## Usage instructions


* The following describes the capabilities supported by VCI NetworkPolicies.

   * Ingress and Egress policies. You can use `podSelector`, `namespaceSelector`, and `ipBlock` (CIDR) to select traffic sources and destinations.

   * Port and port range matching based on TCP and UDP.

   * Combining multiple `from`/`to` rules in a single policy. You can specify `ipBlock`, `podSelector`, and `namespaceSelector` in the same rule. These rules apply the OR relationship.

* VCI NetworkPolicy cannot be used in hybrid deployment scenarios that combine regular nodes (ECS nodes) and virtual nodes. For information on how to use NetworkPolicies in regular node scenarios in VKE clusters, see [Using a NetworkPolicy to implement network access control](https://docs.byteplus.com/en/docs/vke/Using-NetworkPolicies-for-network-access-control).

* VCI NetworkPolicies, VPC security groups, and network ACLs for VCI scenarios apply access control at different layers. Traffic must pass through multiple layers of checks in sequence. They work together and cannot replace each other:

   * NetworkPolicy: Applies at the VCI Pod level, aligns closely with application semantics, and dynamically follows the VCI pod lifecycle.

   * Security group: Applies at the VCI instance (ENI) level, with instance\-level granularity.

   * Network ACL: Applies at the subnet level and has the coarsest granularity.

* For specialized capabilities such as Web Application Firewall (WAF) and Cloud Firewall, we recommend using the corresponding professional cloud security services. NetworkPolicies focus on L3/L4 traffic within clusters.

* VCI NetworkPolicy is consistent with its Kubernetes\-native object and uses the following default behavior:

   * If no policy selects a Pod in a specific direction (Ingress/Egress), all traffic in that direction is allowed.

   * Once a policy in a certain direction (Ingress/Egress) selects a Pod and that direction is defined, only traffic that explicitly matches allow rules is allowed. All other traffic is denied.


<span id="4HNaC6U1"></span>
## Prerequisites


* A cluster required by the VCI service has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* The vci\-virtual\-kubelet add\-on has been installed in the cluster. For detailed instructions, see [vci-virtual-kubelet](https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet-add-on).


<span id="3o8ESATz"></span>
## Procedure

<span id="dxA5B6TR"></span>
### Step 1: Enable NetworkPolicy in the workload

To enable VCI NetworkPolicy, add the Pod annotation to your workloads that are deployed by using VCI.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A VCI NetworkPolicy supports only workloads fully deployed using VCI and does not support hybrid deployment scenarios combining VCI and ECS.</div>



<Tabs>
<Tab zoneid="MzKYuGqR0p" title="Use the console">
<TabTitle>Use the console</TabTitle>

When creating or updating a workload deployed using the **VCI** method, in the **Advanced settings** step, add the following **instance annotation**: `vci.volcengine.com/network-policy-enabled: "true"`. For detailed instructions, see [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments?lang=en) and [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63da048606be10375d3581ed5b86d188.png) </span>


</Tab>
<Tab zoneid="Jd6VcYRqfP" title="Use a YAML configuration">
<TabTitle>Use a YAML configuration</TabTitle>

When creating or updating workloads fully deployed using the VCI method (`vke.volcengine.com/burst-to-vci: enforce`), add the following Pod annotation: `vci.volcengine.com/network-policy-enabled: "true"`. The following example uses a Deployment YAML file for demonstration. For more workload types and methods to create or update their YAML files, see [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments?lang=en) and [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f4191e4b30f3606981bfd4f1f2bff88.png) </span>

A complete sample YAML file is shown below.

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-deployment  # Deployment name.
  namespace: default  # The namespace of the Deployment.
spec:
  replicas: 2
  selector:
    matchLabels:
      app: demo-deployment
  template:
    metadata:
      annotations:
        vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
        vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1nai****  # Specify the ID of a subnet. You can specify multiple subnets within the same availability zone. To do so, separate them with commas (,).
        vci.vke.volcengine.com/preferred-instance-family: vci.u1  # Specify the instance family of the VCI.
        vci.volcengine.com/network-policy-enabled: "true"  # Whether to enable the VCI NetworkPolicy feature. Values: true (enabled) and false (disabled).
      labels:
        app: demo-deployment
    spec:
      containers:
      - name: demo-deployment
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # The address and version of the container image. Replace the value with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
        ports:
        - containerPort: 80
        resources:
          requests:  # Specify the container vCPU and memory.
            cpu: "500m"      
            memory: "1024Mi"
          limits:
            cpu: "1"      
            memory: "2048Mi"
```



</Tab>
</Tabs>


<span id="Uewjwbfx"></span>
### Step 2: Write a NetworkPolicy YAML file

Write a standard Kubernetes NetworkPolicy YAML file based on your business requirements. For the complete semantics of fields and YAML syntax, see the [Kubernetes NetworkPolicy documentation](https://kubernetes.io/zh-cn/docs/concepts/services-networking/network-policies/).

The following examples use the ai\-agent\-prod namespace in the AI Agent production environment to demonstrate common policy combinations. Replace the values of selectors such as `app` with your actual information. All IP addresses in the examples are placeholders. Replace them with your actual target CIDR blocks.


<Tabs>
<Tab zoneid="jfy3WkFd" title="Scenario 1: Deny all traffic by default">
<TabTitle>Scenario 1: Deny all traffic by default</TabTitle>

Before defining fine\-grained policies, you can first place the workload in an isolated environment as a baseline for zero\-trust (a security architecture) to ensure business security.

The following example policy selects all Pods in the ai\-agent\-prod namespace, declares both Ingress and Egress directions, but provides no allow rules, denying all inbound/outbound traffic for Pods in this namespace.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all  # NetworkPolicy object name.
  namespace: ai-agent-prod  # Target namespace where the NetworkPolicy takes effect.
spec:
  podSelector: {}  # Pod label selector. {} indicates all Pods in the target namespace.
  policyTypes:  # Policy type. This example defines two policy types: Ingress and Egress, but does not provide any rules that allow traffic. Therefore, based on the default behavior of the VCI NetworkPolicy, this policy will deny all ingress and egress traffic for all Pods in this namespace.
  - Ingress
  - Egress
```



</Tab>
<Tab zoneid="XaxYl2zA" title="Scenario 2: Implement multi-agent communication">
<TabTitle>Scenario 2: Implement multi-agent communication</TabTitle>

In scenarios where multiple agents do not directly access each other, you can configure a central control service in a NetworkPolicy to restrict direct access between agents.

The following sample policy assumes that two groups of agents, `analyzer-agent` and `retriever-agent`, interact through the `control-center` control service. The policy precisely allows both groups of agents to access port 8080 of `control-center` and blocks any other Pods from accessing `control-center`. Together with the default deny policy in scenario 1, the two agents cannot communicate directly with each other.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-access-to-control-center  # NetworkPolicy object name.
  namespace: ai-agent-prod  # Target namespace where the NetworkPolicy takes effect.
spec:
  podSelector:  # Pod label selector. Allow Pods that match this label to access resources in the target namespace.
    matchLabels:
      app: control-center
  policyTypes:
  - Ingress
  ingress:
  - from:  # Allow traffic from analyzer-agents and retriever-agents.
    - podSelector:
        matchLabels:
          app: analyzer-agent
    - podSelector:
        matchLabels:
          app: retriever-agent
    ports:
    - protocol: TCP
      port: 8080
```



</Tab>
<Tab zoneid="5TAKOdtm" title="Scenario 3: Restrict access to external services">
<TabTitle>Scenario 3: Restrict access to external services</TabTitle>

In scenarios where an AI agent needs to access external LLM endpoints or vector databases, you can configure a NetworkPolicy to limit the egress traffic. This prevents the agent from accessing malicious websites or leaking data.

The following sample policy limits the outbound traffic of the AI agent `analyzer-agent`, allowing access only to the internal `control-center` service, DNS, the specified external LLM endpoint, and the vector database. All other outbound traffic is denied.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">DNS\-related egress rules are required in almost all egress allowlist scenarios. Omitting these rules will cause domain name resolution to fail, resulting in abnormal connections.</div>


```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-egress-for-analyzer-agents  # NetworkPolicy object name.
  namespace: ai-agent-prod  # Target namespace where the NetworkPolicy takes effect.
spec:
  podSelector:  # Pod label selector. Allow Pods that match this label to access resources in the target namespace.
    matchLabels:
      app: analyzer-agent
  policyTypes:
  - Egress
  egress:
  # Access the internal control-center service.
  - to:
    - podSelector:
        matchLabels:
          app: control-center
    ports:
    - protocol: TCP
      port: 8080
  # Allow DNS resolution (required).
  - to:
    - namespaceSelector: {}
      podSelector:
        matchLabels:
          k8s-app: kube-dns
    ports:
    - protocol: UDP
      port: 53
    - protocol: TCP
      port: 53
  # Access the specified external service.
  - to:
    - ipBlock:    # External service address.
        cidr: 10.XX.XX.XX/32    # Assume this is the IP address of an LLM endpoint.
    - ipBlock:    # Allow DNS resolution (required).
        cidr: 10.XX.XX.0/24     # Here, assume this is the VPC subnet of the vector database.
    ports:
    - protocol: TCP
      port: 443
```



</Tab>
<Tab zoneid="TLTNlbZ6" title="Scenario 4: Isolate data from different environments">
<TabTitle>Scenario 4: Isolate data from different environments</TabTitle>

NetworkPolicy follows an allowlist model, where only traffic from allowlisted namespaces is allowed and access from all other namespaces not on the allowlist is implicitly denied, achieving strict data isolation.

The following is an example policy that allows pods only within the `ai-agent-prod` namespace to access production environment data in `prod-database` and automatically denies cross\-namespace traffic.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-staging-access-to-prod-db  # NetworkPolicy object name.
  namespace: ai-agent-prod  # Target namespace where the NetworkPolicy takes effect.
spec:
  podSelector:  # Pod label selector. Allow Pods that match this label to access resources in the target namespace.
    matchLabels:
      app: prod-database
  policyTypes:
  - Ingress
  ingress:
  - from:
  # Only allow traffic from the namespace for the production environment.
  # Block any traffic from the test environment.
  # Caution: A NetworkPolicy follows an allowlist model, so this setting defines the allowed objects, not denied objects.
    - podSelector: {}
      namespaceSelector:
        matchLabels:
          kubernetes.io/metadata.name: ai-agent-prod
```



</Tab>
</Tabs>


<span id="LmTYPJnw"></span>
### Step 3: Deliver the policy to the cluster


1. Use kubectl to connect to the target VCI cluster. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to deliver the policy to the target namespace.

   ```Bash
   kubectl apply -f <policy.yaml> -n <namespace>
   # Replace <policy.yaml> with the name of the YAML file that you wrote in Step 1, and replace <namespace> with the target namespace name.
   ```
   

   After delivery, the policy will take effect in the cluster for VCI Pods that have this Pod annotation: `vci.volcengine.com/network-policy-enabled: "true"`. Newly scheduled Pods to VCI will automatically match against existing policy rules during the network initialization stage.


<span id="GwBFypkU"></span>
### Step 4: Verify that the policy takes effect


1. Run the following command to confirm whether the policy has been created.

   ```Bash
   kubectl get networkpolicy -n <namespace>
   # Replace <namespace> with the target namespace name.
   ```
   

   The expected result is that the response includes the target policy name, and `POD-SELECTOR` matches the labels of the target Pods you expect to select.

   ```Bash
   NAME                             POD-SELECTOR     AGE
   allow-access-to-backend          app=backend      2m
   ```
   

2. Run the following command to confirm whether the rule meets expectations.

   ```Bash
   kubectl describe networkpolicy <policy-name> -n <namespace>
   # Replace <policy-name> with the NetworkPolicy object name defined in the YAML file that you wrote in Step 1, and replace <namespace> with the target namespace name.
   ```
   

   The expected result is that the response includes `PodSelector`, allowed Ingress/Egress traffic, traffic source or destination selectors, and port information.

   ```Bash
   Name:         allow-access-to-backend
   Namespace:    ai-agent-prod
   PodSelector:  app=backend
   Policy Types: Ingress
   Ingress:
     To Port: 8080/TCP
     From:
       PodSelector: app=frontend
   ```
   

3. Run the following command to confirm which Pods are selected by the rule.

   ```Bash
   kubectl get pods -l <POD-SELECTOR> -n <namespace> -o wide --show-labels
   # Replace <POD-SELECTOR> with the actual Pod label, and replace <namespace> with the target namespace name.
   ```
   

   The expected response is as follows:

   ```Bash
   NAME        READY   STATUS    RESTARTS   AGE   IP             NODE     LABELS
   backend-0   1/1     Running   0          10m   10.XX.XX.12    <none>   app=backend
   ```
   

4. Run the following command to verify whether the selected Pod has the VCI NetworkPolicy annotation.

   ```Bash
   kubectl describe networkpolicy <policy-name> -n <namespace>
   kubectl get pod <pod-name> -n <namespace> \
     -o jsonpath='{.metadata.annotations["vci.volcengine.com/network-policy-enabled"]}{"\n"}'
   # Replace <pod-name> with the actual Pod name, and replace <namespace> with the target namespace name.
   ```
   

   The expected response is `true`.

5. Initiate access from the source Pod allowed by the policy and confirm whether the connection is successful.

   ```Bash
   kubectl exec -n <namespace> frontend-0 -- \
     curl -m 5 -s -o /dev/null -w "%{http_code}\n" \
     http://<allowed-source-pod-ip>:8080/healthz
   
   # Replace <namespace> with the target namespace name. Replace <allowed-source-pod-ip> with the source Pod IP address that will be denied.
   ```
   

   If `200` is returned, access is successful.

6. Initiate access from a source Pod that is expected to be denied by the policy and confirm whether the connection times out or is denied.

   ```Bash
   kubectl exec -n <namespace> other-0 -- \
     curl -m 5 -v \
     http://<deny-source-pod-ip>:8080/healthz
   
   # Replace <namespace> with the target namespace name. Replace <deny-source-pod-ip> with the IP address of the source Pod to be denied.
   ```
   

   The expected result is a connection timeout, no response, or connection refusal.


<span id="0tEzxlOX"></span>
## What to do next

<span id="PfPma3PC"></span>
### Change the policy


1. Directly update the corresponding YAML.

2. Run the following command to recreate the policy. The policy will be recalculated in the cluster and applied to the matching Pods.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend first verifying changes to default deny baseline policies in the test environment to avoid accidentally blocking production traffic.   </div>
   

   ```Bash
   kubectl apply -f <policy.yaml> -n <namespace>
   
   # Replace <policy.yaml> with the YAML file name of the policy, and replace <namespace> with the name of the namespace to which the policy applies.
   ```
   


<span id="FMrtehxu"></span>
### Delete the policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After the policy is deleted, traffic that was restricted by the policy may be allowed again.</div>


* <div data-tips="true" data-tips-type="warning">If other policies still select the same Pod, the final effect is based on the allowed rules after all policies are merged. Make sure that the deletion does not expand access to production traffic.</div>



NetworkPolicies are a standard Kubernetes resource. To delete a NetworkPolicy, follow the steps below.


* Deleting a namespace will automatically clean up all NetworkPolicy resources under it.

* Use the following command to delete a single NetworkPolicy resource.

   ```Bash
   kubectl delete networkpolicy <name> -n <namespace>
   
   Replace <name> with the NetworkPolicy resource name, and <namespace> with the name of the namespace where the policy takes effect.
   ```
