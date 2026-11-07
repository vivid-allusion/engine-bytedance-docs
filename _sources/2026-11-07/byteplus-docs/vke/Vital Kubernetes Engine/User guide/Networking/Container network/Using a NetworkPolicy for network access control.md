---
title: "Using a NetworkPolicy for network access control"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-NetworkPolicies-for-network-access-control"
---

A Kubernetes NetworkPolicy implements policy\-based network access control. You can use a NetworkPolicy to control pod traffic by IP address or port. This topic describes the configuration methods and use cases of NetworkPolicies.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a><strong>]</strong>: This feature is currently in beta. To use it, submit an application.</div>


* <div data-tips="true" data-tips-type="tip">For details about NetworkPolicies in Kubernetes, see <a href="https://kubernetes.io/docs/concepts/services-networking/network-policies/#networkpolicy-resource">Network Policies</a>.</div>



<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* VKE NetworkPolicies are supported only in clusters that use the VPC\-CNI network model.

* The vpc\-cni add\-on must be upgraded to version v1.6.4 or later.

* NetworkPolicy implementation for VCI differs from that for VKE and requires independent configuration. For details, see [Using a NetworkPolicy to implement network access control for VCI Pods](https://docs.byteplus.com/en/docs/vke/Using_a_NetworkPolicy_to_implement_network_access_control_for_VCI_Pods).

* When using a NetworkPolicy to control traffic, consider cluster scale limitations. For details, see [Limit](https://docs.byteplus.com/en/docs/vke/Limits).

* A NetworkPolicy does not support the following [scenarios](https://github.com/kubernetes/kubernetes/blob/master/test/e2e/network/netpol/network_policy.go).

   * should allow egress access to server in CIDR block

   * should deny ingress access to updated pod

   * should allow ingress access from updated pod

   * should enforce except clause while egress access to server in CIDR block

   * should enforce ingress policy allowing any port traffic to a server on a specific protocol  [Feature:UDP]

   * should ensure an IP overlapping both IPBlock.CIDR and IPBlock.Except is allowed

   * should properly isolate pods that are selected by a policy allowing SCTP, even if the plugin doesn't support SCTP

   <span id="3qv15e31"></span>
   ## Procedure

<span id=".5q2l6aqk5LiA77ya5byA5ZCvLW5ldHdvcmtwb2xpY3k="></span>
### Step 1: Enable NetworkPolicy


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. In the left navigation bar, click **Addons**.

4. On the **Network** tab, find the **vpc\-cni** add\-on, move the mouse over the add\-on card, click **Configuration**, and enable the **NetworkPolicy** feature.

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It takes about 1 minute for <strong>NetworkPolicy </strong>to take effect after being enabled (or disabled).   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Modifying this configuration causes the add\-on to restart. Perform this operation during off\-peak hours.   </div>
   

5. Click **Confirm**.


<span id="z3JVtLb8"></span>
### Step 2: Configure a NetworkPolicy

After enabling the NetworkPolicy feature, you can specify a network policy for specific pods by configuring a NetworkPolicy. In the NetworkPolicy, you define traffic direction by using ingress and egress, and you filter ingress and egress targets (namespaces and pods) by using ipBlock, namespaceSelector, and podSelector.

The following content provides an example configuration and a description of key fields.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: network-policy-demo # NetworkPolicy name.
  namespace: default # NetworkPolicy namespace.
spec:
  podSelector: # Pod selector. Use labels to select pods that require network control. If no specific label is specified, all pods in the cluster are selected.
    matchLabels:
      app: nginx
  policyTypes: # Traffic direction in which the network policy takes effect. Specify Ingress for inbound control or Egress for outbound control.
  - Ingress
  - Egress
  ingress: # Inbound policy configuration.
  - from: # Traffic source in the inbound policy. Only specified source objects can access the specified pods.
    - ipBlock: # Source CIDR block for inbound traffic. This field supports only IP addresses external to the cluster and does not support internal cluster addresses (such as node IP addresses).
        cidr: 192.168.1.0/24
        except: # Exclude IP addresses or sub-CIDR blocks from the source CIDR block for inbound traffic control. These IP addresses within the CIDR block are not allowed to access Pods.
        - 192.168.1.100/32
    - namespaceSelector: # Namespace selector. It allows pods in namespaces with specified labels to access specified pods.
        matchLabels:
          namespace: doc-demo
    - podSelector: # Pod selector. It allows pods with specified labels to access specified pods.
        matchLabels:
          app: nginx
    ports: # The allowed ports.
    - protocol: TCP # Allowed port protocol.
      port: 6379 # The allowed port number.
  egress: # Egress policy configuration.
  - to: # Traffic destination in the egress policy. Pods can only access specified destination objects.
    - ipBlock: # Target CIDR block for outbound traffic. This field supports only IP addresses external to the cluster and does not support internal cluster addresses (such as node IP addresses).
        cidr: 10.0.0.0/24
        except: # Exclude IP addresses or sub-CIDR blocks from the destination CIDR for outbound traffic to deny Pod access
        - 10.0.1.100/32
    - namespaceSelector: # Namespace selector. It allows only specified pods to access other pods in namespaces with specified labels.
        matchLabels:
          namespace: doc-demo
    - podSelector: # Pod selector. It allows only specified pods to access other pods with specified labels.
        matchLabels:
          app: nginx
    ports: # The allowed ports.
    - protocol: TCP # Allowed port protocol.
      port: 5978 # The allowed port number.
```


Key fields are described in the table below:


|Parameter |Description |
|---|---|
|policyTypes |Specify the traffic control direction in the NetworkPolicy policy. Options include:<br><br><br>* **Ingress**: Ingress traffic policy for controlling external traffic entering specified pods.<br><br>* **Egress**: Egress traffic policy for controlling access to external destinations by specified pods. |
|ipBlock |Static CIDR block. This field is used to specify IP addresses external to the cluster. Traffic between pods and specified external IP addresses will be controlled by the NetworkPolicy policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field only supports IP addresses external to the cluster and does not support internal cluster addresses, such as IP addresses of nodes.</div><br> |
|namespaceSelector |Namespace selector. It selects, by label, the namespaces that require network traffic control. All pods in the matched namespaces are governed by the NetworkPolicy. |
|podSelector |Pod selector. It selects pods that need network traffic control by label. Pods that meet the filter conditions are governed by the NetworkPolicy. |


<span id="zcQ1lVOb"></span>
## Validating results

<span id="jRQ1wfuh"></span>
### Confirming configurations


1. In the left navigation bar, click **Workload** \> **Resource Explorer**.

2. From the **Category** drop\-down list, select **API Group** and use the name `networking.k8s.io` to search for the resource object.

3. Click the resource name to enter the resource details page, where you can see the NetworkPolicy resource category.

4. Click the name of the NetworkPolicy resource to enter the resource details page, where you can view, modify, or delete the NetworkPolicy configuration.


<span id="45VZT00g"></span>
### Checking traffic

After the configuration is complete, you can create multiple workloads in the cluster and verify whether the configured traffic rules in the NetworkPolicy are applied effectively to pods. For example, if you allow only mutual access within the same namespace, deploy multiple pods in different namespaces. Log in to a pod and run the ping command to verify that it can access only other pods in the same namespace and cannot access pods in other namespaces. The example is as follows:

```Bash
root@deployment-demo-a-7796***:/# ping 192.168.2.159
PING 192.168.2.159 (192.168.2.159) 56(84) bytes of data.
64 bytes from 192.168.2.159: icmp_seq=1 ttl=64 time=0.021 ms
64 bytes from 192.168.2.159: icmp_seq=2 ttl=64 time=0.030 ms
64 bytes from 192.168.2.159: icmp_seq=3 ttl=64 time=0.027 ms
64 bytes from 192.168.2.159: icmp_seq=4 ttl=64 time=0.021 ms
--- 192.168.2.159 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3057ms
rtt min/avg/max/mdev = 0.021/0.024/0.030/0.004 ms
root@deployment-demo-a-7796***:/# ping 192.168.2.157
PING 192.168.2.157 (192.168.2.157) 56(84) bytes of data.

```


<span id="ksr9LESe"></span>
## Configuration examples

<span id="pIH8lbrO"></span>
### Allowing mutual access within the same namespace

The following YAML configuration example defines a NetworkPolicy that only allows pods within the same namespace to access each other and prevents pod access across namespaces.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: demo-1  # NetworkPolicy resource name.
  namespace: default  # Namespace to which the NetworkPolicy belongs.
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector: {}
```


<span id="kj51pmsU"></span>
### Denying all inbound traffic

The following YAML configuration example defines a NetworkPolicy that denies any inbound traffic (pods cannot be accessed by any object).

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: demo-2  # NetworkPolicy resource name.
  namespace: default  # Namespace to which the NetworkPolicy belongs.
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress: []
```


<span id="IyfXKiCL"></span>
### Allowing access only from a specified namespace

The following YAML configuration example defines a NetworkPolicy that only allows pods in the namespace with the `name: demo-workspace` label to access other pods in the cluster.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: demo-3 # NetworkPolicy resource name.
  namespace: default  # Namespace to which the NetworkPolicy belongs.
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress:
  - from:
    - namespaceSelector:  # Namespace selector.
        matchLabels:  # Namespace labels for matching.
          name: demo-workspace
```


<span id="vblsBtVT"></span>
### Allowing access only to a specified namespace

The following YAML configuration example defines a NetworkPolicy that only allows pods in the cluster to access pods in the namespace with the `name: demo-workspace` label.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: demo-4  # NetworkPolicy resource name.
  namespace: default  # Namespace to which the pod belongs.
spec:
  podSelector: {}
  policyTypes:
  - Egress
  egress:
  - to:
    - namespaceSelector:  # Namespace labels for matching.
        matchLabels:
          name: demo-workspace
```


<span id="PXz1VZpl"></span>
### Allowing access only to a specified CIDR block

The following YAML configuration example defines a NetworkPolicy that only allows pods in the cluster to access external objects within the CIDR block `172.16.0.0/16`, over `TCP`, and on port `8080`. It prevents access to other network objects or ports.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: demo-5  # NetworkPolicy resource name.
  namespace: default  # Namespace to which the pod belongs.
spec:
  podSelector: {}
  policyTypes:
  - Egress
  egress:
  - to:
    - ipBlock:
        cidr: 172.16.0.0/16  # Pod CIDR
    ports:  # Specified ports.
    - protocol: TCP  # Port protocol.
      port: 8080  # Port number.
```


<span id="7tI3KbNO"></span>
### Allowing access only from a specified CIDR block

The following YAML configuration example defines a NetworkPolicy that only allows pods in the cluster to be accessed by external objects within the CIDR block `172.16.0.0/16` via `TCP` and port `80`.

```YAML
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: demo-6  # NetworkPolicy resource name.
  namespace: default  # Namespace to which the pod belongs.
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress:
  - from:
    - ipBlock:
        cidr: 172.16.0.0/16  # Pod CIDR
    ports:  # Specified ports.
    - protocol: TCP  # Port protocol.
      port: 80  # Port number.
```
