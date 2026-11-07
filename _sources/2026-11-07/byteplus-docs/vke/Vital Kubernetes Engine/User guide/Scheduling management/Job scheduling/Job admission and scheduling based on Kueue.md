---
title: "Job admission and scheduling based on Kueue"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Job_admission_and_scheduling_based_on_Kueue"
---

This topic mainly describes how to use Kueue in a VKE cluster to implement the All\-or\-Nothing scheduling capability.

<span id="14TPj5Cm"></span>
## Background

As a Kubernetes\-native system, Kueue is used to manage quotas and control how jobs use quotas. In clusters that are shared among multiple teams or services, where complete batch job governance, such as governance on quotas, queues, priorities, and preemption, is required, All\-or\-Nothing can be achieved through the quota mechanism of Kueue (ClusterQueue) and gang admission (Workload). When the quota is insufficient to accommodate the entire job, the job remains suspended and does not schedule any pods.

<span id="y12tFd7z"></span>
## Prerequisites


* A managed VKE cluster running Kubernetes v1.30 or later has been created. For details, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The KubeConfig of the target cluster has been downloaded and configured in the local `$HOME/.kube/config` file. For details, see [Connecting to clusters using kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* The Helm tool has been installed in the local terminal. For details, see the [official Helm documentation](https://helm.sh/zh/docs/intro/install/).


<span id="fKepKliy"></span>
## Procedure

<span id="4BqnEeyK"></span>
### Step 1: Install Kueue


1. Configure the KubeConfig path in the local terminal.

   ```Bash
   export KUBECONFIG=${your_kubeconfig_path}
   ## Replace ${your_kubeconfig_path} with the local path of KubeConfig.
   ## For example, if the local path of KubeConfig is /Users/bytedance/.kube/config, the complete command is as follows:
   ## export KUBECONFIG=/Users/bytedance/.kube/config
   ```
   

2. Use the Helm tool to install Kueue.

   ```Bash
   helm install kueue oci://registry.k8s.io/kueue/charts/kueue \
     --version 0.18.1 \
     --namespace kueue-system --create-namespace \
     --wait
   ```
   

3. Confirm the Kueue installation status.

   1. Confirm the Helm release status.

      ```Bash
      helm list -n kueue-system
      ```
      

      The expected output is as follows: `STATUS` is `deployed`.

      ```Bash
      NAME    NAMESPACE       REVISION        UPDATED                                 STATUS   CHART           APP VERSION
      kueue   kueue-system    1               2026-06-15 18:55:25.549036 +0800 CST    deployed kueue-0.18.1    v0.18.1
      ```
      

   2. Confirm the running status of the controller Pods.

      ```Bash
      kubectl get pods -n kueue-system -o wide
      ```
      

      The expected output is as follows: `READY` is `1/1`, and `STATUS` is `Running`.

      ```Bash
      NAME                                       READY   STATUS    RESTARTS   AGE     IP              NODE            NOMINATED NODE   READINESS GATES
      kueue-controller-manager-9c54ccf47-k5vmf   1/1     Running   0          4m10s   192.168.123.8   192.168.123.4   <none>           <none>
      ```
      

   3. Check the registered CRDs.

      ```Bash
      kubectl get crd | grep kueue.x-k8s.io
      ```
      

      The expected output is as follows: CRDs such as `clusterqueues`, `localqueues`, `workloads`, and `resourceflavors` are visible.

      ```Bash
      admissionchecks.kueue.x-k8s.io                         2026-06-15T10:55:33Z
      clusterqueues.kueue.x-k8s.io                           2026-06-15T10:55:33Z
      cohorts.kueue.x-k8s.io                                 2026-06-15T10:55:33Z
      localqueues.kueue.x-k8s.io                             2026-06-15T10:55:33Z
      multikueueclusters.kueue.x-k8s.io                      2026-06-15T10:55:33Z
      multikueueconfigs.kueue.x-k8s.io                       2026-06-15T10:55:33Z
      provisioningrequestconfigs.kueue.x-k8s.io              2026-06-15T10:55:33Z
      resourceflavors.kueue.x-k8s.io                         2026-06-15T10:55:33Z
      topologies.kueue.x-k8s.io                              2026-06-15T10:55:33Z
      workloadpriorityclasses.kueue.x-k8s.io                 2026-06-15T10:55:33Z
      workloads.kueue.x-k8s.io                               2026-06-15T10:55:33Z
      ```
      


<span id="NV3aD5rB"></span>
### Step 2: Perform job admission and scheduling

After Kueue is installed, use Kueue in the VKE cluster to verify the All\-or\-Nothing scheduling capability.


1. Create a queue and set the quota.

   This topic configures a ClusterQueue quota of only 4 CPU cores. This is used to verify later that an entire Job is not admitted when the quota is insufficient. Run the following commands to create ResourceFlavor, ClusterQueue, and LocalQueue.

   ```Bash
   cat <<'EOF' | kubectl apply -f -
   apiVersion: kueue.x-k8s.io/v1beta1
   kind: ResourceFlavor
   metadata:
     name: default-flavor  # The ResourceFlavor name. It is referenced by ClusterQueue.
   ---
   apiVersion: kueue.x-k8s.io/v1beta1
   kind: ClusterQueue
   metadata:
     name: cluster-queue  # The ClusterQueue name.
   spec:
     namespaceSelector: {}
     resourceGroups:
     - coveredResources: ["cpu", "memory"]
       flavors:
       - name: default-flavor  # Reference the ResourceFlavor defined above.
         resources:
         - name: "cpu"
           nominalQuota: 4  # The CPU quota of ClusterQueue. Set the value to 4 to test the insufficient quota scenario.
         - name: "memory"
           nominalQuota: 8Gi
   ---
   apiVersion: kueue.x-k8s.io/v1beta1
   kind: LocalQueue
   metadata:
     name: user-queue  # The LocalQueue name.
     namespace: default   # The namespace of the LocalQueue. Jobs must be submitted in the same namespace.
   spec:
     clusterQueue: cluster-queue  # Associate the LocalQueue with the ClusterQueue. Use the label kueue.x-k8s.io/queue-name on the job to specify this LocalQueue.
   EOF
   ```
   

2. Submit two jobs to verify gang admission.

   Each job requires 3 CPU cores (`parallelism=3`). However, the queue quota is only 4 cores, which can only accommodate one job. Add the label `kueue.x-k8s.io/queue-name=user-queue` to the two jobs and set `suspend to true` to let Kueue manage jobs.

   ```Bash
   cat <<'EOF' | kubectl apply -f -
   apiVersion: batch/v1
   kind: Job
   metadata:
     name: job-a  # The job name.
     namespace: default   # The job namespace. It needs to be consistent with the LocalQueue namespace.
     labels:
       kueue.x-k8s.io/queue-name: user-queue # Specify the LocalQueue used by the job so that the job can be managed by Kueue.
   spec:
     parallelism: 3  # The number of parallel pods. The job requires a total of 3 CPU cores.
     completions: 3  # The number of Pods that must complete.
     suspend: true   # Set the value to true. The job remains suspended, awaiting Kueue admission before being scheduled.
     template:
       spec:
         containers:
         - name: dummy
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
           resources:
             requests:
               cpu: "1"    # Each pod requests 1 core. Three pods request a total of 3 cores.
               memory: "1Gi"
         restartPolicy: Never
   ---
   apiVersion: batch/v1
   kind: Job
   metadata:
     name: job-b   # The job name.
     namespace: default   # The job namespace. It needs to be consistent with the LocalQueue namespace.
     labels:
       kueue.x-k8s.io/queue-name: user-queue   # Use the same queue as job-a to share the 4-core quota.
   spec:
     parallelism: 3    # Three cores are required. The two jobs require a total of 6 cores, which is greater than the 4-core quota. Therefore, only one job can be accommodated.
     completions: 3
     suspend: true    # Set the value to true. The job remains suspended, awaiting Kueue admission.
     template:
       spec:
         containers:
         - name: dummy
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
           resources:
             requests:
               cpu: "1"
               memory: "1Gi"
         restartPolicy: Never
   EOF
   ```
   


<span id="GZbDx2RF"></span>
## Validate results

View workload and job status.

```Bash
kubectl get workloads -n default
kubectl get jobs -n default
kubectl get pods -n default -o wide
```


The expected result is as follows:


* One job is admitted (`ADMITTED` of the corresponding workload is `True`), and after the job is resumed (`suspend` is set to false), all 3 pods simultaneously enter the `Running` state.

* The other job remains in the `Suspended` state, due to insufficient quota, and its corresponding workload is in the `Pending` state and does not schedule any pods.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1087be26ba0d9e961d52407c1917f48a.png) </span>

The preceding results prove that when the queue quota cannot accommodate all jobs, Kueue admits each entire job as a whole. This prevents resource waste where half of a job occupies quota and the other half waits in queue and achieves the job\-level All\-or\-Nothing capability.

<span id="gu0naJCz"></span>
## Clean up resources

After validation is complete, run the following commands to clean up the jobs, queues, and Kueue add\-on created in this topic.

```Bash
## Delete jobs
kubectl delete job job-a job-b -n default --ignore-not-found

## Delete queues and quotas
kubectl delete localqueue user-queue -n default --ignore-not-found
kubectl delete clusterqueue cluster-queue --ignore-not-found
kubectl delete resourceflavor default-flavor --ignore-not-found

## Uninstall Kueue
helm uninstall kueue -n kueue-system
kubectl delete ns kueue-system --ignore-not-found
```
