---
title: "Lifecycle management"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Lifecycle_management"
---

This topic mainly describes how to manage sandboxes across their lifecycle in VCI Agent Sandbox, such as creating, suspending, restoring, deleting, and modifying sandboxes.

## Creating a sandbox

You can use VCI resources to create a sandbox.

> **tip**

* > A sandbox is a Sandbox Custom Resource.

* > VCI containers use Kata Containers to achieve strong isolation.

### Prerequisites

* A StorageClass has been created in a VCI\-based cluster, which is used for dynamically creating a PVC for the sandbox data volume. For details, see [Using dynamic EBS PVs](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes), [Using dynamic FileNAS PVs](https://docs.byteplus.com/en/docs/vke/Using-dynamic-NAS-Volumes), and [Using dynamic vePFS PVs](https://docs.byteplus.com/en/docs/vke/Using-dynamic-PFS-volumes).

* To define a deletion/retention policy for a sandbox snapshot by using SandboxSnapShotClass ** ** , create a related custom resource in advance. The following YAML file serves as an example. For details, see [Data persistence](https://docs.byteplus.com/en/docs/vke/Data_persistence).

   ```YAML
   apiVersion: extensions.agents.x-k8s.io/v1alpha1
   kind: SandboxSnapShotClass
   metadata:
     name: class-for-retain-snapshot # The SandboxSnapShotClass name.
   spec:
       deletionPolicy: Retain  # The sandbox snapshot deletion/retention policy. Valid values: retain and delete.
       driver: sandbox.agent.io/vci  # The backend provider of the snapshot. Currently, only the vci provider type is supported.
   ```

* An image required to run the sandbox has been created. Make sure that the nodes in the cluster where the sandbox is located can pull the image. You can also upload the image to CR. For details, see [Pushing and pulling images by using Docker](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

* When you create a sandbox by using an existing snapshot, you can obtain the snapshot ID by using one of the following two methods:

   * Use the snapshot ID automatically created by VCI during the shutdown of an existing sandbox.

   * Use the Snapshot\-type Custom Resource created by the user.

### Creating sandboxes for the first time

If you create a sandbox in VCI Agent Sandbox for the first time, use the following sample code.

```YAML
apiVersion: agents.x-k8s.io/v1alpha1
kind: Sandbox
metadata:
  annotations:
    agent.sandbox.io/snapshot-class: "class-for-retain-snapshot" # Optional. The name of the SandboxSnapShotClass associated with the sandbox. If the snapshot deletion policy is specified both here and in snapshot-deletion-policy, the policy specified in snapshot-deletion-policy takes precedence.
    agent.sandbox.io/snapshot-deletion-policy: Delete # Optional. Specify whether to delete the snapshot when the sandbox is being deleted. If it is not specified, the deletion policy of SandboxSnapShotClass will be used. Valid values: delete and retain.
    agent.sandbox.io/snapshot-retention-days: "3" # Optional. The retention period of the snapshot. Unit: days. The snapshot will be automatically deleted when the period elapses. If it is not specified, the retention period of SandboxSnapShotClass will be used. The value is a positive integer, which is a string.
    agent.sandbox.io/snapshot-max-num: "3" # Optional. The maximum number of snapshots associated with a sandbox. The value is a positive integer, which is a string.
  name: test-sandbox-example  # The sandbox name.
spec:
  replicas: 1  # The number of running Pod replicas for the sandbox. You can only set the value to 0 or 1. 0 indicates that no computing resources exist and the sandbox is paused. 1 indicates that one VCI Pod computing resource is provided, and the sandbox starts.
  volumeClaimTemplates:  # The PVC template of the data volume.
    - spec: 
        accessModes:
          - ReadWriteMany
        resources:
          requests:
            storage: 20Gi
        storageClassName: test-storage-class  # The StorageClass name, which is used for dynamically creating a PVC for the sandbox data volume.
        volumeMode: Filesystem
      metadata:
        name: generated-name
  podTemplate:  # The VCI Pod template that corresponds to the sandbox.
    metadata:
      annotations:
        vci.volcengine.com/tls-enable: "false" # Specify whether to enable log collection. Valid values: true (enable) and false (disable).
        vke.volcengine.com/burst-to-vci: enforce # Forced scheduling to VCI.
        vci.vke.volcengine.com/enable-auto-create-imc: "true"  # Enable automatic image caching.
        vci.volcengine.com/usable-disk-capacity: "40"  # Specify the available space of the system volume (writable layer space). Unit: GiB.
        vci.volcengine.com/persistent-container: "true" # Specify whether to enable persistence for the container writable layer data. Valid values: true (enable) and false (disable).
        vci.volcengine.com/image-restart-policy: "in-place" # Specifies the image update policy. Allowed value: in-place (updates the image in place).
      labels:
        app: test-server
    spec:
      containers:
      - image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # The image required to run the sandbox.
        imagePullPolicy: IfNotPresent
        name: test-server
        resources: { }
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      terminationGracePeriodSeconds: 30
```

If the `status.phase` of the CRD changes to **Running**, it indicates that the sandbox has been created. The sample code snippet is as follows:

```YAML
status:
  conditions:
  - lastTransitionTime: "2025-11-18T02:21:30Z" # The status transition time, which is the time when the status changes from False/Unknown to True.
    message: Pod is Ready; Service Exists
    observedGeneration: 1
    reason: DependenciesReady # It indicates that the resources that the sandbox depends on, such as Pod, Service, PV, and PVC resources, have been created and are ready.
    status: "True" # If status is True, it indicates the sandbox is ready. If status is False, it indicates the sandbox is not ready.
    type: Ready
  replicas: 1 # The number of running Pod replicas for the sandbox. You can only set the value to 0 or 1. 0 indicates that no computing resources exist and the sandbox is paused. 1 indicates that one VCI Pod computing resource is provided, and the sandbox starts.
  phase: Running # It indicates that the sandbox is created.
  selector: agents.x-k8s.io/sandbox-name-hash=e6b82627 # The Pod that corresponds to the sandbox can be queried through this label selector.
  service: demo-sandbox  # The name of the Service associated with the sandbox.
  serviceFQDN: ubuntu-sshd.default.svc.cluster.local   # The fully qualified domain name (FQDN) of the corresponding Service within the cluster. Clients within the cluster can use the FQDN to directly access the sandbox via protocols, such as ssh and http, which depend on the Service port configuration.
```

### Create a sandbox by using an existing snapshot

When you create a sandbox by using an existing snapshot in VCI Agent Sandbox, add the annotation `vci.volcengine.com/snapshot-id` based on the sample code displayed in the **Creating sandboxes for the first time** section. The complete sample code is as follows.

```YAML
apiVersion: agents.x-k8s.io/v1alpha1
kind: Sandbox
metadata:
  name: test-sandbox-example  # The sandbox name.
spec:
  replicas: 1  # The number of running Pod replicas for the sandbox. You can only set the value to 0 or 1. 0 indicates that no computing resources exist and the sandbox is paused. 1 indicates that one VCI Pod computing resource is provided and the sandbox starts.
  volumeClaimTemplates:  # The PVC template of the data volume.
    - spec:
        accessModes:
          - ReadWriteMany
        resources:
          requests:
            storage: 20Gi
        storageClassName: test-storage-class  # The StorageClass name, which is used for dynamically creating a PVC for the sandbox data volume.
        volumeMode: Filesystem
      metadata:
        name: generated-name
  podTemplate:  # The VCI Pod template that corresponds to the sandbox.
    metadata:
      annotations:
        vci.volcengine.com/tls-enable: "false"
        vke.volcengine.com/burst-to-vci: enforce # Forced scheduling to VCI.
        vci.vke.volcengine.com/enable-auto-create-imc: "true"  # Enable automatic image caching.
        vci.volcengine.com/usable-disk-capacity: "40"  # Specify the available space of the system volume (writable layer space). Unit: GiB.
        vci.volcengine.com/persistent-container: "true"  # Specify whether to enable persistence for the container writable layer data. Valid values: true and false.
        vci.volcengine.com/snapshot-id: "snapshot-1" # The ID of an existing snapshot. This parameter only takes effect when the sandbox is created for the first time by default.
      labels:
        app: test-server
    spec:
      containers:
      - image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # The image required to run the sandbox. This image must be consistent with that used by the existing snapshot specified in snapshot-id.
        imagePullPolicy: IfNotPresent
        name: test-server
        resources: { }
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      terminationGracePeriodSeconds: 30
```

## Suspending a sandbox

### Automatically create snapshots

To suspend a sandbox, set its `replicas` to 0. By default, when the sandbox is suspended, VCI Agent Sandbox will automatically generate a snapshot. The sample code snippet is as follows:

```YAML
apiVersion: agents.x-k8s.io/v1alpha1
kind: Sandbox
metadata:
  annotations:
  name: test-sandbox-example
spec:
  replicas: 0 # If you set the number of replicas to 0, VCI Pods will be released and stop billing, but the metadata will be retained. As a result, the sandbox is suspended.
```

If the `status.phase` of the CRD changes to **Paused**, it indicates that the sandbox has been suspended. The sample code snippet is as follows:

```YAML
status:
  conditions:
  - lastTransitionTime: "2026-02-05T06:24:40Z"
    message: Pod does not exist, replicas is 0; Service Exists
    observedGeneration: 2
    reason: DependenciesReady
    status: "True"
    type: Ready
  phase: Paused # It indicates that the sandbox is being suspended.
  replicas: 0 # When the number of replicas is 0, VCI Pod resources are released, and billing stops, but metadata is retained, and the sandbox is suspended.
  service: test-sandbox-example
  serviceFQDN: test-sandbox-example.default.svc.cluster.local
  snapShotId: fake-id # Record the snapshot ID at shutdown, which will be used when the sandbox is started again.
```

### Do not create snapshots

If you do not want a snapshot to be automatically created when the sandbox is suspended, you can disable this feature by configuring the annotation `agent.sandbox.io/auto-create-snapshot: "false"`.

```YAML
apiVersion: agents.x-k8s.io/v1alpha1
kind: Sandbox
metadata:
  annotations:
    agent.sandbox.io/auto-create-snapshot: "false"  # Whether a snapshot is generated when the sandbox is suspended. Valid values: false and true.
  name: test-sandbox-example
spec:
  replicas: 0 # If you set the number of replicas to 0, VCI Pods will be released and stop billing, but the metadata will be retained. As a result, the sandbox is suspended.
```

If the `status.phase` of the CRD changes to **Paused**, it indicates that the sandbox has been suspended and no snapshots will be automatically generated. The sample code snippet is as follows:

```YAML
status:
  conditions:
  - lastTransitionTime: "2026-02-05T06:24:40Z"
    message: Pod does not exist, replicas is 0; Service Exists
    observedGeneration: 2
    reason: DependenciesReady
    status: "True"
    type: Ready
  phase: Paused # It indicates that the sandbox is being suspended.
  replicas: 0 # When the number of replicas is 0, VCI Pod resources are released, and billing stops, but metadata is retained, and the sandbox is suspended.
  service: test-sandbox-example
  serviceFQDN: test-sandbox-example.default.svc.cluster.local
```

## Restoring a sandbox

To restore a sandbox, set its `replicas` to 1. The snapshot generated from the previous shutdown will be used for restoring the sandbox. The sample code snippet is as follows:

```YAML
apiVersion: agents.x-k8s.io/v1alpha1
kind: Sandbox
metadata:
  annotations:
  name: test-sandbox-example
spec:
  podTemplate:
    spec:
      containers:
      - command:
        - /usr/sbin/sshd
        - -D
        image: vke-cn-beijing.cr.volces.com/vke/nginx:latest
        name: ubuntu-sshd
        ports:
        - containerPort: 22
          protocol: TCP
        volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: nginx-data
      tolerations:
      - effect: NoSchedule
        key: vci.vke.volcengine.com/node-type
        operator: Exists
  replicas: 1 # If you set the number of replicas to 1, one VCI Pod will be occupied and start billing. The system volume snapshot that was last suspended will be used for restoring the sandbox.
```

If the `status.phase` of the Custom Resource changes to **Running**, it indicates that the sandbox has been restored.

## Updating a sandbox

### Update through recreation

When updating the CPU, memory, or GPU configuration of the sandbox, you need to first suspend the sandbox and then update the `resources` within the `podTemplate`. After the configuration is complete, resume the sandbox. This process will destroy the original Pod and then recreate a Pod to update the sandbox configuration.

1. Suspend the sandbox by setting `replicas` to 0. The sandbox is suspended if `status.phase` is **Paused**.

2. Update the `resources` field in `podTemplate`.

   ```YAML
   spec:
     replicas: 1  # The number of running Pod replicas for the sandbox. You can only set the value to 0 or 1. 0 indicates that no computing resources exist and the sandbox is paused. 1 indicates that one VCI Pod computing resource is provided and the sandbox starts.
     podTemplate:
       spec:
         containers:
         - name: ubuntu-sshd   # Set the container name.
           image: vke-cn-beijing.cr.volces.com/vke/nginx:latest   # Configure the container image.
           command: ["/usr/sbin/sshd", "-D"]
           ports:
           - containerPort: 22
           resources:   # Set the CPU, memory, and GPU specification of the container.
             requests:
               cpu: 2
               memory: 4Gi
             limits:
               cpu: 2
               memory: 4Gi
     volumeClaimTemplates:
     - metadata:
         name: nginx-data
       spec:
         accessModes:
         - ReadWriteOnce
         resources:
           requests:
             storage: 5Gi
         storageClassName: sandbox-nfs    # Declare a Volume template for containers to mount NAS volumes.
   ```

3. Restore the sandbox by setting `replicas` to 1. The Custom Resource is restored if `status.phase` is **Running**.

### In\-place update

You can perform an in\-place update on a sandbox image without rebuilding the Pod. It means that you can update the sandbox image on the existing Pod without destroying the Pod. This shortens the time required for configuration changes.

1. Configure the annotation `vci.volcengine.com/persistent-container: "true"` in the sandbox YAML file.

   ```YAML
   apiVersion: agents.x-k8s.io/v1alpha1
   kind: Sandbox
   metadata:
     annotations:
       agent.sandbox.io/snapshot-class: "class-for-retain-snapshot" # Optional. The name of the SandboxSnapShotClass associated with the sandbox. If the snapshot deletion policy is specified both here and in snapshot-deletion-policy, the policy specified in snapshot-deletion-policy takes precedence.
       agent.sandbox.io/snapshot-deletion-policy: Delete # Optional. Specify whether to delete the snapshot when the sandbox is being deleted. If it is not specified, the deletion policy of SandboxSnapShotClass will be used. Valid values: delete and retain.
       agent.sandbox.io/snapshot-retention-days: "3" # Optional. The retention period of the snapshot. Unit: days. The snapshot will be automatically deleted when the period elapses. If it is not specified, the retention period of SandboxSnapShotClass will be used. The value is a positive integer, which is a string.
       agent.sandbox.io/snapshot-max-num: "3" # Optional. The maximum number of snapshots associated with a sandbox. The value is a positive integer, which is a string.
       agent.sandbox.io/auto-create-snapshot: "false" # Optional. Whether to generate a snapshot when the sandbox is suspended. Valid values: false and true.
     name: test-sandbox-example  # The sandbox name.
   spec:
     replicas: 1  # The number of running Pod replicas for the sandbox. You can only set the value to 0 or 1. 0 indicates that no computing resources exist and the sandbox is paused. 1 indicates that one VCI Pod computing resource is provided, and the sandbox starts.
     volumeClaimTemplates:  # The PVC template of the data volume.
       - spec: 
           accessModes:
             - ReadWriteMany
           resources:
             requests:
               storage: 20Gi
           storageClassName: test-storage-class  # The StorageClass name, which is used for dynamically creating a PVC for the sandbox data volume.
           volumeMode: Filesystem
         metadata:
           name: generated-name
     podTemplate:  # The VCI Pod template that corresponds to the sandbox.
       metadata:
         annotations:
           vci.volcengine.com/tls-enable: "false" # Specify whether to enable log collection. Valid values: true (enable) and false (disable).
           vke.volcengine.com/burst-to-vci: enforce # Forced scheduling to VCI.
           vci.vke.volcengine.com/enable-auto-create-imc: "true"  # Enable automatic image caching.
           vci.volcengine.com/usable-disk-capacity: "40"  # Specify the available space of the system volume (writable layer space). Unit: GiB.
           vci.volcengine.com/persistent-container: "true" # Specify whether to enable persistence for the container writable layer data. Valid values: true (enable) and false (disable).
           vci.volcengine.com/image-restart-policy: "in-place" # The image update policy. The value in-place indicates updating the container image in place without recreating the Pod.
         labels:
           app: test-server
       spec:
         containers:
         - image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # The image required to run the sandbox.
           imagePullPolicy: IfNotPresent
           name: test-server
           resources: { }
           terminationMessagePath: /dev/termination-log
           terminationMessagePolicy: File
         dnsPolicy: ClusterFirst
         restartPolicy: Always
         schedulerName: default-scheduler
         terminationGracePeriodSeconds: 30
   ```

2. Subsequent updates to the image configured in `podTemplate` can be performed directly via YAML, and the VCI Agent Sandbox will update the container image in place.

3. After the update is complete, if the `status.phase` of the custom resource is **Running** and the container image has switched to the target version, the in\-place update of the sandbox is complete.

## Deleting a sandbox

If you no longer need a sandbox, you can directly delete the corresponding Sandbox resource. When you delete the sandbox, its corresponding VCI Pod, Snapshot, Custom Resource, and PVC resources will be automatically deleted.

The data retention policy of a data volume is determined by the retention policy of the StorageClass.

* **Retain**: After the PVC is released, the PV remains Released and is not automatically deleted or reclaimed.

* **Delete**: After the PVC is released, the PV and its underlying storage resources are automatically deleted.

To delete the sandbox at a scheduled time, you can specify shutdownTime. The sample code is as follows.

```YAML
spec:
  podTemplate:
    spec:
      containers:
      - image: vke-cn-beijing.cr.volces.com/vke/nginx:latest
        name: nginx
        ports:
        - containerPort: 80
          protocol: TCP
        volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: nginx-data
  replicas: 1  # The number of running Pod replicas for the sandbox. You can only set the value to 0 or 1. 0 indicates that no computing resources exist and the sandbox is paused. 1 indicates that one VCI Pod computing resource is provided and the sandbox starts.
  shutdownTime: "2024-11-17T20:44:05Z" # After this time point, the Pod that corresponds to the sandbox will be deleted, but the Sandbox resource will be retained.
```
