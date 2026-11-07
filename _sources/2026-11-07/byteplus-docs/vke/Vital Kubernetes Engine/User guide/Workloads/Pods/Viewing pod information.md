---
title: "Viewing pod information"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Viewing-pod-details"
---

This topic primarily describes how to view basic information, event information, log information, and YAML configuration information related to pods.

## Viewing information in the console

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the left navigation bar, click **Workload** \> **Pod**.

4. On the **Pod** page, select the target namespace to view the basic information of pods.

5. Click the pod name to go to the **pod details page**. Switch between tabs to view detailed information about the pod.

   |Tab |Description |
   |---|---|
   |Overview |Displays the basic information, network configuration, status, and associated storage information of the pod. |
   |Container list |Displays the list of all containers for the pod and the basic information about each container. |
   |Access method |Displays the information about the service associated with the pod. You can access the pod by using the access address of the service and the internal and external endpoints. For service\-related descriptions, see [Service overview](https://docs.byteplus.com/en/docs/vke/Service-overview). |
   |Event |Shows pod events from the last hour. Please check them promptly. The events older than one hour are not available for viewing. |
   |Log |Displays the logs of each container in the pod and the logs of exited containers. You can select a container and the number of displayed logs based on your business requirements. You can also download logs.<br><br>> **tip**<br><br><br>> The logs of exited containers refer to the logs generated during the last running of the containers before a restart.<br> |

6. (Optional) On the **container details page**, click the buttons in the upper\-right corner to perform related operations on the pod.

   |Operation button |Description |
   |---|---|
   |Console |Click **Console** to log in to the container. This is equivalent to running the the `kubectl exec -it {your_container_name} -- /bin/bash` command in the cluster. |
   |More operations |You can edit or export the YAML configuration of the pod, view monitoring data, and delete the pod. For a detailed description, see [Managing pods](https://docs.byteplus.com/en/docs/vke/Managing-pods). |

## Viewing information by using the kubectl command

1. Connect to the cluster where the pod is located. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the kubectl command to view pod information.

   > **tip**

   > Replace the variable symbol `${variable}` in the command with the actual pod\-related value. Take the command used to view pod details as an example. If `${pod-name}` is `demo-pod` and `${pod-namespace}` is `default`, the complete command is as follows:

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```bash
   kubectl get pod demo-pod -n default -o wide
   ```
      </div>
   

   * View pod details

      ```bash
      kubectl get pod ${pod-name} -n ${pod-namespace} -o wide
      ```

   * View pod events

      ```bash
      kubectl describe pod ${pod-name} -n ${pod-namespace}
      ```

   * View pod logs

      * View the log of the first or the only container in a pod:

         ```bash
         kubectl logs ${pod-name} -n ${pod-namespace}
         ```

      * View the log of the specified container in a pod:

         ```bash
         kubectl logs ${pod-name} -n ${pod-namespace} [-c ${container-name}]
         ```

      * View the logs of all containers in a pod:

         ```bash
         kubectl logs ${pod-name} -n ${pod-namespace} --all-containers
         ```

      * View the logs of exited containers in a pod:

         ```bash
         kubectl logs ${pod-name} -c ${container-name} --previous
         ```

   * View pod YAML configurations

      ```bash
      kubectl get pod ${pod-name} -n ${pod-namespace} -o yaml
      ```
