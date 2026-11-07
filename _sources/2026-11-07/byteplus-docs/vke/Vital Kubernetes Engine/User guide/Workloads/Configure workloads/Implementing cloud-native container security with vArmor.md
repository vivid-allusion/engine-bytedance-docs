---
title: "Implementing cloud-native container security with vArmor"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Implementing_cloud-native_container_security_with_vArmor"
---

vArmor provides ‌container hardening and runtime protection‌ for workloads in Kubernetes clusters. It is designed for scenarios that require security policy configuration and protection validation for cloud\-native applications using AppArmor, BPF, and Seccomp. This topic provides the ‌configuration instructions and considerations‌ for implementing cloud\-native container security with vArmor.

<span id="2Z9ixsxC"></span>
## Background

vArmor is an open\-source cloud\-native container sandbox system developed by ByteDance. It leverages Linux technologies [AppArmor LSM](https://en.wikipedia.org/wiki/AppArmor), [BPF LSM](https://docs.kernel.org/bpf/prog_lsm.html), and [Seccomp](https://en.wikipedia.org/wiki/Seccomp) for container hardening. You can manage security policies in Kubernetes clusters via vArmor CRDs to harden containers where specific workloads run. vArmor aims to ‌reduce the complexity and cost‌ of container hardening by leveraging existing technologies, thereby balancing security risks and protection costs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details about vArmor, see <a href="https://docs.volcengine.com/docs/6507/2582778?lang=zh">What is container hardening</a> and <a href="https://varmor.org/">the official website</a>.</div>


vArmor employs different hardening technologies to secure cloud\-native containers. Key concepts and working principles are as follows:


|Hardening technology |Basic knowledge |How it works |
|---|---|---|
|AppArmor Enforcer |A security enforcement engine based on the Linux kernel's AppArmor module. It is a mature mandatory access control system. |When a Pod is created, vArmor converts defined security policies into AppArmor Profiles and injects them into container configurations via the Webhook mechanism. The Linux kernel then takes control, restricting container processes' file read/write operations, network access, and system calls based on these profiles. |
|BPF Enforcer |A next\-generation security engine based on ‌eBPF (Extended Berkeley Packet Filter)‌ technology. |Instead of injecting static configurations, it dynamically attaches lightweight eBPF sandbox programs to kernel security hooks (LSM Hooks) or tracepoints. When container processes initiate system calls, eBPF programs perform ‌real\-time kernel\-space checks‌ to block unauthorized operations. |
|Behavior modeling mode |An ‌allowlist\-based policy generation mode‌ built on dynamic feature collection. |When this mode is enabled, vArmor enters an ‌"observation period‌" without immediately blocking operations. It silently logs target container behaviors during normal operation (such as processes started, file paths accessed, network calls made) in the background. After the observation period ends, it automatically generates a dedicated allowlist policy. |


The following table compares different hardening technologies.


|**Comparison dimension** |**AppArmor Enforcer** |**BPF Enforcer** |**Behavior modeling mode** |
|---|---|---|---|
|Feature category |Enforcer module (interception engine). |Enforcer module (interception engine). |Policy mode (behavior data collector). |
|‌Working mechanism |Statistically injects profiles and relies on in\-kernel modules to perform interception. |Dynamically attaches eBPF programs to implement real\-time control at the system call layer. |Silently observes container runtime behaviors, then automatically summarizes and generates allowlist policies. |
|Key advantages |Mature ecosystem, high stability, and troubleshooting procedures. |No reliance on a single kernel module, strong cross\-system compatibility, and finer\-grained interception. |No manual configuration, preventing service interruptions caused by misconfigurations. |
|Dependencies and limitations |The host kernel must support AppArmor and have it enabled. |The host kernel version must meet eBPF feature requirements. |Business traffic during observation must be sufficient to avoid incomplete allowlists. |
|Application scenario |Routine isolation for workloads on veLinux/Ubuntu nodes. |Nodes incompatible with AppArmor or performance\-critical deep protection. |Scenarios where security engineers cannot manually determine explicit permission requirements during the initial launch phase of complex services. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">AppArmor Enforcer and BPF Enforcer differ partially in access control capabilities. However, the two do not conflict and can be used simultaneously in the same cluster if needed.</div>


* <div data-tips="true" data-tips-type="default">The behavior modeling mode forms an upstream\-downstream collaboration relationship with the two enforcers. Behavior modeling generates policies, which must eventually be enforced by the AppArmor or BPF enforcer.</div>



<span id="HbEEX5gb"></span>
## Prerequisites

The [varmor add-on](https://docs.byteplus.com/en/docs/vke/varmor-add-on) has been installed.

<span id="k49BKF55"></span>
## Operation guide

<span id="d0KUjBaz"></span>
### Step 1: Configure a VarmorPolicy

After installing the varmor add\-on and its related CRD resources in the cluster, you can customize container security policies by using the VarmorPolicy resource. A VarmorPolicy consists of two main sections:


* `target`: Specifies which Pods or workloads the policy applies to, using resource types and label selectors.

* `policy`: Defines the protection method, for example, enforcer selection (AppArmor or BPF), protection mode, and high\-risk behaviors to intercept.


The following content provides an example configuration and a description of key fields.

```YAML
apiVersion: crd.varmor.org/v1beta1
kind: VarmorPolicy
metadata:
  name: demo-policy # Security policy name.
  namespace: default # Namespace of security policy.
spec:
  target: # Target selector. It specifies the objects that use the security policy.
    kind: Pod # Specify the resource type that uses this security policy.
    selector:
      matchLabels:
        app: varmor-test  # Specify labels of Pods to which this security policy applies.
  policy: # Security policy details.
    enforcer: AppArmor      # Use AppArmor technology to achieve isolation and restriction.
    mode: EnhanceProtect    # Enhanced protection mode: Kernel directly denies and returns "Permission denied" for any container behavior matching rules below.
    enhanceProtect: # Core protection rule configurations.
      auditViolations: true # Whether to log policy violation audits. Values: true (logs audits when the policy takes effect) and false (no audit logs. Whether to block violations depends on the policy mode. For example, EnhanceProtect still blocks rule violations.)
      attackProtectionRules: # Rules details.
      - rules: # Rule 1: Globally blocks file permission modification.
        - disable-chmod
      - rules: # Rule 2: Applies targeted prevention of SA Token leakage.
        - mitigate-sa-leak
        targets:
        - "/bin/bash"
        - "/bin/dash"
        - "/bin/sh"
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can also configure the VarmorPolicy policy for a specified cluster by using the Cloud Security Center. For details, see <a href="https://docs.volcengine.com/docs/6507/2582780?lang=zh">Container hardening instructions</a>.</div>


* <div data-tips="true" data-tips-type="default">For more details and examples of custom vArmor rule configuration, see the <a href="https://www.varmor.org/zh-cn/docs/main/guides/policies_and_rules/custom_rules">official documentation</a>.</div>



<span id="J1kE94AB"></span>
### Step 2: Harden workloads

When you create a workload, you need to add labels that match `target.selector.matchLabels` to the Pod to ensure the VarmorPolicy selects the target Pod. If Webhook injection has been enabled for the add\-on, you also need to add matching labels as required by the add\-on, such as `sandbox.varmor.org/enable: "true"`. This topic uses a Deployment as an example. The sample and instructions are as follows:


1. Create the YAML file of a workload. The code of the sample file `deployment-demo.yaml` is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-demo # Workload name.
     namespace: default # The namespace to which the workload belongs.
   spec: 
     replicas: 1
     selector: 
       matchLabels: 
         app: varmor-test # Specify the security policy using the label of the VarmorPolicy.
     template: 
       metadata: 
         labels: 
           app: varmor-test # Specify the security policy using the label of the VarmorPolicy.
           sandbox.varmor.org/enable: "true" # Webhook matching label. This setting must be consistent with that of the varmor add-on.
       spec:
         containers:
         - name: demo
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           ports:
           - containerPort: 80
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl apply -f deployment-demo.yaml
   ```
   


<span id="E3s6eK2L"></span>
## Result validation

<span id="nuPl5TZh"></span>
### Confirming configurations


<Tabs>
<Tab zoneid="cDx3XFcm1R" title="Use the VKE console">
<TabTitle>Use the VKE console</TabTitle>

1. In the left navigation bar, click **Workload** \> **Resource Explorer**.

2. Select **CRD** from the **Category** drop\-down list and search for `varmorpolicy`.

3. Click the resource name to enter the resource details page, where you can see the VarmorPolicy configuration.

4. In the **Actions** column, click **Edit Yaml** to view or modify the VarmorPolicy configuration, or click **Delete** to delete it.


</Tab>
<Tab zoneid="c54CQFKu9P" title="Via the Cloud Security Center console">
<TabTitle>Via the Cloud Security Center console</TabTitle>

1. Log in to the [Cloud Security Center console](https://console.byteplus.com/security-center).

2. In the left navigation pane, click **Risk management** \> **Container hardening**.

3. Click the **Policy configuration** tab to view the VarmorPolicy details.

4. Click **Edit** or **Delete** in the **Actions** column to manage the VarmorPolicy policy.


</Tab>
</Tabs>


<span id="ThEAYcv7"></span>
### Validate the policy

In the VarmorPolicy provided in this topic, the global prohibition on file permission modification‌ is enabled. You can use the following sample commands to test whether the policy takes effect in the Pod.

```Bash
touch /tmp/a
chmod 777 /tmp/a
```


The expected result is that the `chmod` command fails because the global prohibition on file permission modification‌ is enabled in the Pod.

```Bash
bash: /bin/chmod: Permission denied
```


<span id="JQzpRCjW"></span>
### Viewing logs

The "Violation logs" page allows you to view audit records of policy violations triggered by specified clusters or workloads. It helps quickly identify ‌which Pod‌ violated rules, which rule‌ was triggered, and what behavior‌ was blocked (for example, access file paths, filtered system calls, and network access targets). Logs can be filtered by ‌cluster, policy, time range‌, and other dimensions, helping with policy tuning and security incident tracing.


1. Log in to the [Cloud Security Center console](https://console.byteplus.com/security-center).

2. In the left navigation pane, click **Risk management** \> **Container hardening**.

3. On the **Violation logs** tab, view violation logs for the specified cluster or Pod.


&nbsp;
