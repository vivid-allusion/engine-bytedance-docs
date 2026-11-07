---
title: "Expanding by using dynamically provisioned EBS volumes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Dynamically-expanding-EBS-Volumes"
---

VKE supports online expansion of PVs and their corresponding Elastic Block Storage (EBS) file systems. When the file system of an EBS volume is not mounted, expansion can be implemented with a pod restart. When the file system of an EBS volume is already mounted to a node, expansion can be implemented without requiring a pod restart. This topic describes the steps of expanding EBS capacity as dynamically provisioned PersistentVolumes (PV).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VKE cluster that uses v1.20.15\-vke.11 or later has been created, and the csi\-ebs add\-on in the cluster has been upgraded to the latest version.

* Dynamically provisioned EBS PVs have already been used, with the `allowVolumeExpansion:true` setting included in the StorageClass. For details, see [Using EBS as dynamic PersistentVolumes](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes#.6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So).

* To avoid data loss caused by expansion failure, we recommend that you back up data in advance. For details, see [Using EBS snapshots](https://docs.byteplus.com/en/docs/vke/Using-EBS-volume-snapshots).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5pa55byP5LiA77yI5o6o6I2Q77yJ77ya6YeN5ZCvLXBvZC3lrp7njrDnprvnur_mianlrrk="></span>
### Method 1 (recommended): Offline expansion with a pod restart

An unmounted file system during EBS volume expansion helps prevent volume and file system expansion errors. **This expansion method is recommended to ensure file system stability.** 


1. Run the `kubectl exec [pod_name] df [data volume mount path]` command to view the file system status before expansion. Run the `kubectl get pv [pv_name]` command to view the PV status. The following is an example (both the PV size and the file system size are 20 GiB):


```bash
$ kubectl exec deployment-nginx-mlt-7db45f9b6-5jckg df /usr/share/nginx/html
Filesystem     1K-blocks   Used     Available  Use%   Mounted on
/dev/vdc       20511312    45080    20449848   1%     /usr/share/nginx/html

$ kubectl get pv pvc-6c98cd01-dd32-4636-ac11-794ce9fff540 
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                    STORAGECLASS     REASON   AGE
pvc-6c98cd01-dd32-4636-ac11-794ce9fff540   20Gi       RWO            Delete           Bound    default/pvc-for-sc-mlt   sc-ebs-ssd-mlt            3m55s
```



2. Run the `kubectl label pv [pv_name] topology.kubernetes.io/zone=nozone` command to add an invalid zone label to the PV. The purpose of this operation is to prevent the pod from being scheduled to any node after it restarts. The example is as follows:


```bash
$ kubectl label pv pvc-6c98cd01-dd32-4636-ac11-794ce9fff540 topology.kubernetes.io/zone=nozone
persistentvolume/pvc-6c98cd01-dd32-4636-ac11-794ce9fff540 labeled
```



3. Run the `kubectl delete pod [pod_name]` command to delete the current pod, which will cause a new pod to be started. Because the zone label of the PV for the pod is invalid, the newly started pod will remain in the Pending state. The example is as follows:


```bash
$ kubectl delete pod deployment-nginx-mlt-7db45f9b6-5jckg
pod "deployment-nginx-mlt-7db45f9b6-5jckg" deleted

$ kubectl get pod deployment-nginx-mlt-7db45f9b6-frqvb           # Query pod status.
NAME                                   READY   STATUS    RESTARTS   AGE
deployment-nginx-mlt-7db45f9b6-frqvb   0/1     Pending   0          28s

$ kubectl describe pod deployment-nginx-mlt-7db45f9b6-frqvb      # View pod details.
Events:
  Type     Reason            Age                From               Message
  ----     ------            ----               ----               -------
  Warning  FailedScheduling  52s                default-scheduler  0/6 nodes are available: 2 node(s) had no available volume zone, 4 node(s) had volume node affinity conflict.
  Warning  FailedScheduling  50s (x1 over 52s)  default-scheduler  0/6 nodes are available: 2 node(s) had no available volume zone, 4 node(s) had volume node affinity conflict.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you run the <code>kubectl delete</code> command, a new pod is created with a different name.</div>



1. Run the `kubectl patch pvc [pvc_name] -p '{"spec":{"resources":{"requests":{"storage":"[expanded capacity]"}}}}'` command to change the capacity of the PVC to 30 GiB. The example is as follows:


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend configuring expanded PVC capacity in multiples of 10.</div>


```bash
$ kubectl patch pvc pvc-for-sc-mlt  -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
persistentvolumeclaim/pvc-for-sc-mlt patched
```



5. Run the `kubectl label pv [pv_name] topology.kubernetes.io/zone-` command to remove the label previously set on the PV. After the label is removed, the pod can be scheduled successfully. The example is as follows:


```bash
$ kubectl label pv pvc-6c98cd01-dd32-4636-ac11-794ce9fff540 topology.kubernetes.io/zone-
persistentvolume/pvc-6c98cd01-dd32-4636-ac11-794ce9fff540 unlabeled
```



6. Run the following command to validate the expansion result. The response shows that the pod status is Running and that the corresponding PV and file system have already been expanded from 20 GiB to 30 GiB. The example is as follows:


```bash
$ kubectl get pod deployment-nginx-mlt-7db45f9b6-frqvb      # View pod status.
NAME                                   READY   STATUS    RESTARTS   AGE
deployment-nginx-mlt-7db45f9b6-frqvb   1/1     Running   0          3m39s

$ kubectl get pv pvc-6c98cd01-dd32-4636-ac11-794ce9fff540   # View PV storage capacity.
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                    STORAGECLASS     REASON   AGE
pvc-6c98cd01-dd32-4636-ac11-794ce9fff540   30Gi       RWO            Delete           Bound    default/pvc-for-sc-mlt   sc-ebs-ssd-mlt            9m46s

$ kubectl get pvc pvc-for-sc-mlt                           # View PVC storage capacity.
NAME             STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS     AGE
pvc-for-sc-mlt   Bound    pvc-6c98cd01-dd32-4636-ac11-794ce9fff540   30Gi       RWO            sc-ebs-ssd-mlt   10m

$ kubectl exec deployment-nginx-mlt-7db45f9b6-frqvb df /usr/share/nginx/html   # View file system status.
Filesystem      1K-blocks  Used   Available   Use%   Mounted on
/dev/vdc        30832548   45036  30771128    1%     /usr/share/nginx/html
```


<span id=".5pa55byP5LqM77ya5LiN6YeN5ZCvLXBvZC3lrp7njrDlnKjnur_mianlrrk="></span>
### Method 2: Online expansion without a pod restart

When the file system of the EBS volume is mounted on a node, I/O processes during expansion may cause file system expansion to encounter errors. Please take precautions to avoid this.


1. Run the` kubectl exec [pod_name] df [data volume mount path]` command to view the file system status before expansion. Run the `kubectl get pv [pv_name]` command to view the PV status. The following is an example (both the PV size and the file system size are 20 GiB):


```bash
$ kubectl exec deployment-nginx-mlt-7db45f9b6-5jckg df /usr/share/nginx/html
Filesystem     1K-blocks   Used     Available  Use%   Mounted on
/dev/vdc       20511312    45080    20449848   1%     /usr/share/nginx/html

$ kubectl get pv pvc-6c98cd01-dd32-4636-ac11-794ce9fff540 
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                    STORAGECLASS     REASON   AGE
pvc-6c98cd01-dd32-4636-ac11-794ce9fff540   20Gi       RWO            Delete           Bound    default/pvc-for-sc-mlt   sc-ebs-ssd-mlt            3m55s
```



2. Run the `kubectl patch pvc [pvc_name] -p '{"spec":{"resources":{"requests":{"storage":"[capacity after expansion]"}}}}'` command to change the capacity of the PVC to 30 GiB. The example is as follows:


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend configuring expanded PVC capacity in multiples of 10.</div>


```bash
$ kubectl patch pvc pvc-for-sc-mlt  -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
persistentvolumeclaim/pvc-for-sc-mlt patched

```



3. Repeat the command in Step 1 to validate the expansion result. The response shows the corresponding PV and file system have already been expanded from 20 GiB to 30 GiB. The example is as follows:


```bash
$ kubectl exec deployment-nginx-mlt-7db45f9b6-5jckg df /usr/share/nginx/html
Filesystem      1K-blocks  Used   Available   Use%   Mounted on
/dev/vdc        30832548   45036  30771128    1%     /usr/share/nginx/html

$ kubectl get pv pvc-6c98cd01-dd32-4636-ac11-794ce9fff540
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                    STORAGECLASS     REASON   AGE
pvc-6c98cd01-dd32-4636-ac11-794ce9fff540   30Gi       RWO            Delete           Bound    default/pvc-for-sc-mlt   sc-ebs-ssd-mlt            9m46s

```
