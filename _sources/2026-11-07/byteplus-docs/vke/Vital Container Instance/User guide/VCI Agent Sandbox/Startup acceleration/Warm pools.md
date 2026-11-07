---
title: "Warm pools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Warm_pools"
---

The warm pool capability of VCI Agent Sandbox eliminates cold\-start latency by pre\-creating and caching ready instances, enabling resource delivery within seconds. This topic describes the warm pool capability and its operational workflow.

## Feature introduction

The warm pool (SandboxWarmPool) is a core VCI Agent Sandbox extension.  Without it, each sandbox creation requires a full workflow of steps, including scheduling, image pulling, container startup, and health check. This process can take up to tens of seconds. A warm pool completes these steps in advance, stores ready Pods in the cache pool, and directly allocates resources from the pool when workloads request sandboxes, achieving sub\-second provisioning.

### Advantages

|**Pain point** |**No warm pool** |**Warm pool** |
|---|---|---|
|Cold\-start latency |A single Pod takes approximately tens of seconds to start, and the duration is further prolonged if image pulling is required, resulting in interrupted interactions. |Ready Pods are pre\-created for direct delivery upon request, reducing latency to the sub\-second level. |
|Resource waste |Idle sandboxes can occupy resources for a long time, leading to resource idleness. |Idle resources are automatically reclaimed after an idle timeout and replenished on demand, improving resource utilization by over 50%. |
|Response to concurrency spikes |Sandbox creation lags in high\-concurrency scenarios, causing queued requests. |Elastic scaling dynamically matches workload demands, enabling seamless, user\-transparent scale\-out during peak periods. |
|Multi\-tenant security isolation |Shared environments are prone to data leaks and permission control challenges. |It leverages Kata\-based strong isolation, with each sandbox running in an independent environment. |

### Core CRD resources

A warm pool relies on four core CRDs:

|**CRD resources** |**Function** |**Key capabilities** |
|---|---|---|
|SandboxTemplate |Defines sandbox configuration templates (image, resources, security policies, and more). |Configuration reuse, unified specification, and version management. |
|SandboxWarmPool |Manages warm pool resources. It is responsible for pre\-creating and maintaining the pool of ready Pods. |Pre\-creation of ready Pods, automatic replenishment, elastic scaling, and idle resource reclamation. |
|SandboxClaim |Serves as the sandbox creation request resource. Workloads obtain sandbox instances via this CRD. |Request for sandboxes from the pool or template, dynamic configuration overriding, and timeout control |
|Sandbox |Sandbox instances (corresponding to the running Pods). |Lifecycle management, status reporting, and environment isolation. |

## Usage limits

The warm pool capability is temporarily incompatible with the system disk state persistence (Snapshot) capability, and the two cannot be used simultaneously. This is because the warm pool manages a set of ready sandbox instances with fully identical states, whereas system disk snapshots are designed to save the independent runtime state of individual sandboxes. To use the system volume snapshot recovery capability, see the snapshot\-related description in [Lifecycle management](https://docs.byteplus.com/en/docs/vke/Lifecycle_management).

## Prerequisites

Before using the warm pool solution to accelerate VCI Agent Sandbox startup, ensure the following prerequisites are met:

* The VCI Agent Sandbox has been installed. For details, see the [Installation guide](https://docs.byteplus.com/en/docs/vke/Installation_guide?lang=en).

* The container image used by the sandbox has been created and pushed to an accessible image registry. You can push images to CR. For details, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

## Procedure

### Step 1: Create a SandboxTemplate

A SandboxTemplate defines the basic sandbox configurations, such as environment, resource limits, and security context. It serves as the template for the warm pool to create Pods.

1. Create a SandboxTemplate manifest. The following YAML file `sandbox-template.yaml` serves as an example.

   ```YAML
   apiVersion: extensions.agents.x-k8s.io/v1alpha1
   kind: SandboxTemplate
   metadata:
     name: code-interpreter-template  # Sandbox template name.
     namespace: default  # Namespace of the sandbox template.
   spec:
     podTemplate:  # Configuration template for sandbox Pods. The syntax follows standard Kubernetes PodSpec.
       metadata:
         annotations:
           agent.sandbox.io/snapshot-max-num: "2"  # Maximum number of snapshots associated with a single sandbox. The value is a positive integer, which is a string.
           vci.vke.volcengine.com/enable-auto-create-imc: "true"  # Whether to enable automatic image caching to accelerate image pulls. Values: false (disabled) and true (enabled).
           vci.vke.volcengine.com/preferred-instance-family: vci.u1,vci.n3i  # Specify the VCI instance family.
           vci.volcengine.com/persistent-container: "true"  # Whether to persist writable layer data. Values: false (no) and true (yes).
           vci.volcengine.com/tls-enable: "false"  # Whether to collect VCI container logs to TLS. Values: false (disable log collection) and true (enable log collection).
           vci.volcengine.com/usable-disk-capacity: "40"  # Specify the writable layer size of the system volume (unit: GiB).
           vke.volcengine.com/burst-to-vci: enforce  # Forced scheduling to VCI.
       spec:
         containers:
         - name: sandbox
           image: vke-cn-beijing.cr.volces.com/vke/nginx:latest # The address and version of the container image. Replace the value with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
           resources:
             limits:
               cpu: "2"
               memory: "4Gi"
           env:  # Environment variable settings. The default settings are recommended.
           - name: SANDBOX_TIMEOUT  # Key of the sandbox timeout.
             value: "3600"  # Value of the sandbox timeout in seconds.
           - name: MAX_EXECUTION_TIME  # Key of the maximum sandbox template creation duration.
             value: "600"  # Value of the maximum sandbox template creation duration in seconds.
           volumeMounts:  # Volume mounting configuration. The default is recommended.
           - name: workspace
             mountPath: /workspace
         volumes:  # Volume mounting configuration. The default is recommended.
         - name: workspace
           emptyDir: {}
   ```

2. Run the following command to create the SandboxTemplate.

   ```Bash
   kubectl apply -f sandbox-template.yaml
   ```

### Step 2: Create a SandboxWarmPool

A SandboxWarmPool defines the scale of the warm pool. The controller will pre\-create the specified number of ready Pods according to the configuration.

1. Create a SandboxWarmPool manifest. The following YAML file `sandbox-warmpool.yaml` serves as an example:

   ```YAML
   apiVersion: extensions.agents.x-k8s.io/v1alpha1
   kind: SandboxWarmPool
   metadata:
     name: sandbox-warm-pool  # Warm pool name.
     namespace: default  # Namespace of the warm pool.
   spec:
     sandboxTemplateRef:
       name: code-interpreter-template  # Associated SandboxTemplate name. The warm pool will create Pods based on this template.
     replicas: 200 # Number of ready Pods maintained in the warm pool. Configure this field appropriately based on your concurrency level. An excessive quantity leads to resource waste.
   ```

2. Run the following command to create the SandboxWarmPool.

   ```Bash
   kubectl apply -f sandbox-warmpool.yaml
   ```

### Step 3: Create a SandboxClaim

Workloads apply for a sandbox via a SandboxClaim. The system ‌prioritizes allocating ready Pods from the warm pool‌ for immediate binding and delivery.

1. Create a SandboxClaim manifest. The following YAML file `sandbox-claim.yaml` serves as an example:

   ```YAML
   apiVersion: extensions.agents.x-k8s.io/v1alpha1
   kind: SandboxClaim
   metadata:
     name: sandbox-claim  # SandboxClaim name.
     namespace: default  # Namespace of the SandboxClaim.
   spec:
     sandboxTemplateRef:
       name: code-interpreter-template  # Template name used by the SandboxClaim. ‌The controller prioritizes allocating ready Pods from the warm pool associated with the template.‌ If no Pods are available in the pool, it creates new Pods using the template configuration.
   ```

2. Run the following command to create the SandboxClaim.

   ```Bash
   kubectl apply -f sandbox-claim.yaml
   ```

## Validate results

1. After creating the SandboxClaim, run the following command to view the status of the sandbox claim.

   ```Bash
   kubectl get sandboxclaim sandbox-claim -o yaml
   ```

   When the `status.phase` of the SandboxClaim is Bound, a sandbox instance has been successfully obtained from the warm pool. You can view the name of the bound sandbox by checking `status.sandboxRef`.

   ```YAML
   status:
     phase: Bound
     sandboxRef:
       name: sandbox-warm-pool-xxxxx
   ```

2. Run the following command to view the warm pool status and confirm that the number of instances in the pool meets expectations.

   ```Bash
   kubectl get sandboxwarmpool sandbox-warm-pool -o yaml
   ```

   The expected response is as follows:

   ```YAML
   apiVersion: extensions.agents.x-k8s.io/v1alpha1
   kind: SandboxWarmPool
   metadata:
     name: sandbox-warm-pool
     namespace: default
     uid: 8f3c9d2a-1b4e-4c7a-******
     creationTimestamp: "2026-07-14T06:30:00Z"
     generation: 1
   spec:
     replicas: 5                      # Expected number of sandbox instances in the warm pool. 
     template:
       spec:
         image: sandbox-runtime:v1.2.0
         resources:
           requests:
             cpu: "500m"
             memory: 1Gi
           limits:
             cpu: "1"
             memory: 2Gi
   status:
     phase: Ready                     # Overall status of the warm pool. The status "Read" indicates the pool is ready.
     replicas: 5                      # Total number of instances in the pool.
     availableReplicas: 5             # Number of ready instances available for claim.
     boundReplicas: 1                 # Number of instances bound by SandboxClaim.
     idleReplicas: 4                  # Number of idle and available instances.
     conditions:
     - type: Ready
       status: "True"
       reason: PoolReady
       message: "Warm pool has reached desired replicas"
       lastTransitionTime: "2026-07-14T06:31:20Z"
   ```
