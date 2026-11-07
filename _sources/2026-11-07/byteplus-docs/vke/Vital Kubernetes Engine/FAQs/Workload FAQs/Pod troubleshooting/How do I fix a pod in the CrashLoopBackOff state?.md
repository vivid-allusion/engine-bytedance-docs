---
title: "How do I fix a pod in the CrashLoopBackOff state?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pod-in-the-CrashLoopBackOff-state"
---

## Issue description

If a pod remains in the **CrashLoopBackOff** state for an extended period, it means the container repeatedly crashes after a restart.

## Cause analysis

The CrashLoopBackOff state indicates a container startup problem. Possible reasons are as follows:

* Voluntary container process exit

* System OOM

* cgroup OOM

* Health check failure

## Solution

### Voluntary container exit

When the container process exits voluntarily, the exit code is generally from 0 to 128. A normal exit has an exit code of 0. An exit code from 1 to 127 indicates the program exited due to an abnormal event. The cause of the abnormal event may be an application bug or other reasons. You can view the pod event information to confirm the exit code.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

5. From the **Namespace** drop\-down list, select the namespace where the target pod is located. In the pod list, click the name of the target pod to enter the pod details page.

6. In the upper\-right corner of the **Overview** tab, click `...` \> **Edit Yaml** to confirm whether the container startup command and related settings are correct.

   > **tip**

   > You can also use the following kubectl command to view container configuration information: `kubectl get pod <pod-name> -n <pod-namespace> -o yaml`.

7. Click the **Event** tab to view the event details of the pod.

   > **tip**

   > You can also use the following kubectl command to view pod events: `kubectl describe pod <pod-name> -n <pod-namespace>`.

   The following is an example response:

   ```YAML
   Containers:
   demo:
   Container ID:   containerd://83c6dd7f7930e***
   Image:          nginx:latest
   Image ID:       docker.io/library/nginx@sha256:104c7c***
   Port:           <none>
   Host Port:      <none>
   State:          Waiting
     Reason:       CrashLoopBackOff
   Last State:     Terminated
     Reason:       Completed
     Exit Code:    127
     Started:      Mon, 04 Sep 2023 16:28:17 +0800
     Finished:     Mon, 04 Sep 2023 16:28:17 +0800
   Ready:          False
   Restart Count:  9
   Environment:    <none>
   ```

9. Click the **Log** tab to view the details of the pod logs and troubleshoot the problem based on the log content.

   > **tip**

   > You can also use the following kubectl command to view container log information: `kubectl logs <pod-name> -n <pod-namespace> [-c CONTAINER]`.

### System OOM

If a system OOM occurs, the container in the pod will have an exit code of 137, indicating it was stopped by the SIGKILL signal. At the same time, the kernel logs the following error message:

```yaml
Out of memory: Kill process ...
```

This exception is usually caused by excessive memory consumption from other non\-container processes deployed on the node (for example, kubelet and kube\-proxy), or because the memory allocated by kubelet parameters \-\-kube\-reserved and \-\-system\-reserved is too small, leaving insufficient space for other non\-container processes to run.

Solution: Adjust the reserved memory space appropriately according to actual requirements.

### cgroup OOM

If the process is stopped due to cgroup OOM, you can see `OOMKilled` as the `Reason` in the pod event, which means the actual memory usage of the container has exceeded its configured limit. Additionally, the kernel log will report the `Memory cgroup out of memory` error.

Solution: Adjust the memory limit of the container according to your needs.

### Health check failure

A health check failure can also cause the pod to enter the CrashLoopBackOff state. For details, see [How do I fix pod health check failures?](https://docs.byteplus.com/en/docs/vke/Pod-health-check-failed)
