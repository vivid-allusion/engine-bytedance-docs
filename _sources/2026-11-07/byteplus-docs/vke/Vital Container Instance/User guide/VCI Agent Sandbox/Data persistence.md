---
title: "Data persistence"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Data_persistence"
---

This topic mainly describes how to achieve sandbox data persistence in VCI Agent Sandbox.

<span id="ziwct9R8"></span>
## System volume

For system volume snapshots, **SandboxSnapShot** (Namespaced) and **SandboxSnapShotClass** (Cluster\-scoped) are introduced to abstract the snapshot capability of sandboxes in a unified manner.


* **SandboxSnapShot**: Creates a snapshot for a specific sandbox and records the snapshot status, ID, retention duration, and other information.

* **SandboxSnapShotClass**: Describes the underlying snapshot generation parameters and the default deletion policy.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The time required to create a system volume snapshot is related to the size of temporary data generated in the system volume. Therefore, you need to avoid restoring sandboxes before the system volume snapshot is created.</div>


<span id="Hrao1nsq"></span>
### SandboxSnapShot

At the namespace level, it creates a snapshot for a specific sandbox and records the snapshot status, ID, retention duration, and other information.

```YAML
apiVersion: extensions.agents.x-k8s.io/v1alpha1
kind: SandboxSnapShot
metadata:
  name: demo-sandbox-snap-001
  namespace: default
spec:
  sandboxRef: # Specify the Sandbox Reference used for creating the snapshot.
    apiVersion: agents.x-k8s.io/v1alpha1
    kind: Sandbox
    name: demo-sandbox
    namespace: default

  snapshotClassName: vci-provider-class  # The type of snapshot storage service used. It is optional.
  deletionPolicy: Delete    # The snapshot deletion policy. Valid values: Delete and Retain. If you set the value to Delete, underlying snapshots are also deleted after SandboxSnapShot is deleted. If you set the value to Retain, underlying snapshots are retained after SandboxSnapShot is deleted.
  retentionDays: 15  # The snapshot retention duration. Default value: 15 days.

status: 
  phase: Completed  # The snapshot status. Valid values: Pending (The snapshot creation task has not been submitted), InProgress (The snapshot is being created), Completed (The snapshot is created), and Failed (The snapshot fails to be created).
  snapshotID: vci-snap-123456  # The snapshot ID.
  sizeBytes: 40GB # The snapshot size.
  
  creationTime: "2025-12-04 12:00:00"  # The snapshot creation time.
  expirationTime: "2025-12-19 12:00:00"  # The snapshot expiration time.
  conditions:  # This field records the snapshot status, which indicates whether the current snapshot is Ready, and records snapshot error information.
    - type: Ready
      status: "True"
      lastTransitionTime: "2025-12-04T12:00:10Z"
      reason: SnapshotCreated
      message: "Snapshot successfully created by VCI provider"
    - type: Error
      status: "False"
```


<span id="41aGGjyK"></span>
### SandboxSnapShotClass

It describes parameters related to snapshot creation and the snapshot deletion policy.

```YAML
apiVersion: extensions.agents.x-k8s.io/v1alpha1
kind: SandboxSnapShotClass
metadata:
  name: vci-snapshot-class

spec:
    driver: sandbox.agent.io/vci   # The snapshot back-end provider. Currently only "vci" is supported.
    deletionPolicy: Delete   # The snapshot deletion policy. Valid values: Delete and Retain. If you set the value to Delete, underlying snapshots are also deleted after SandboxSnapShot is deleted. If you set the value to Retain, underlying snapshots are retained after SandboxSnapShot is deleted.
    retentionDays: 20
```


<span id="M9TWHXMc"></span>
## Data volume

Data volumes can be mounted on NAS. This allows users to share data across multiple sandboxes.

Data generated during the sandbox lifecycle can be stored in persistent storage (PV and PVC). After a Pod is deleted and recreated, the data from the PVC can still be mounted into the container. The Sandbox CRD defines a volumeClaimTemplates template, which allows users to specify the `accessmode`, `storage size`, and `storageClassName` of the Volume. This is similar to the way the StatefulSet CRD is used.

The data retention policy for data volumes is determined by the retention policy of the Volume:


* **Retain**: After the PVC is released, the PV remains Released and is not automatically deleted or reclaimed.

* **Delete**: After the PVC is released, the PV and its underlying storage resources are automatically deleted.

* **Recycle**: After the PVC is released, the PV is reclaimed into the unbound PV pool and can be reused by other PVCs.


```YAML
apiVersion: agents.x-k8s.io/v1alpha1
kind: Sandbox
metadata:
  name: demo-sandbox
spec:
  replicas: 1
  volumeClaimTemplates:
  - metadata:
      name: nginx-data
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 5Gi
      storageClassName: sandbox-nfs
  podTemplate:
    spec:
      tolerations:
      - key: "vci.vke.volcengine.com/node-type"
        operator: "Exists"
        effect: "NoSchedule"
      containers:
      - name: ubuntu-sshd
        image: vke-qa-cn-beijing.cr.volces.com/qa/ubuntu-sshd:12.04
        command: ["/usr/sbin/sshd", "-D"]
        ports:
        - containerPort: 22
        volumeMounts:
        - name: nginx-data
          mountPath: /usr/share/nginx/html
```
