---
title: "RayJob submission guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/RayJob_submission_guide"
---

<span id="_1-环境准备"></span>
## 1 Environment preparation


1. Deploy the Ray service in the EMR on VKE product.

2. To run RayJob jobs using the kubectl command, you need to install the kubectl tool (see [Install and configure kubectl](https://kubernetes.io/docs/tasks/tools/)), and configure the connection information for the Volcano Engine VKE cluster (see [Connect to a VKE cluster](https://www.volcengine.com/docs/6460/100919#%E6%AD%A5%E9%AA%A4%E4%BA%8C%EF%BC%9A%E8%BF%9E%E6%8E%A5%E9%9B%86%E7%BE%A4)).


<span id="_2-rayjob提交指导"></span>
## 2 RayJob submission guide

After enabling the Ray service in the Volcano Engine EMR on VKE product, you can submit RayJob jobs by following these steps:


1. Write the RayJob configuration file: First, create a configuration file in YAML format, defining the resource requirements for RayJob, the configuration of the Ray cluster, and the entry point for the job. You can refer to the RayJob YAML template provided below.

2. Apply the RayJob configuration: Use the `kubectl` command\-line tool to apply the RayJob configuration file to the Volcano Engine VKE cluster. Open a terminal or command\-line interface and execute the following command:


```bash
kubectl apply -f <RayJob配置文件的名称>
```



3. Verify whether RayJob is running: Use the following command to check the status of RayJob:


```bash
kubectl get rayjob

# Or obtain more detailed status information:
kubectl describe rayjob <RayJob名称>
```



4. View logs: You can use `kubectl` to view the logs of the Pod.


```bash
kubectl logs <RayJob生成的Pod名称>
```


If Ingress is enabled in the RayJob configuration, locate the corresponding cluster in the EMR management console, use quick connect to open the Ray Dashboard UI, and view job execution information.


5. Cleanup: After the job is completed, if you do not want automatic cleanup (if `shutdownAfterJobFinishes: true` is configured), you need to manually delete RayJob and related Kubernetes resources. Use the following command to delete RayJob and all associated resources:


```bash
kubectl apply -f <RayJob配置文件的名称>

# Or use the following command
kubectl delete rayjob <rayjob-name>
```


Additionally, if your RayJob needs to interact with external storage or services, ensure that the corresponding storage classes, PVCs, Secrets, and so on are pre\-configured in the Volcano Engine VKE cluster.

The following introduces the YAML template used for RayJob. You can add, remove, or modify it according to different scenarios.

<span id="_3-rayjob使用的yaml模版"></span>
## 3 **YAML template for RayJob usage**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
 name: pvc名称
spec:
 storageClassName: ebs-essd # Use cloud disk. Volcano Engine also supports NAS, CloudFS, and TOS.
 accessModes:
   - ReadWriteOnce
 resources:
   requests:
     storage: 40Gi # Configure according to actual requirements.
---
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
  annotations:
    # This annotation must be added, otherwise accessing the dashboard will return a 404 error.
    nginx.ingress.kubernetes.io/rewrite-target: /$1 
spec:
  entrypoint: python ***.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 300
 
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    # Enable ingress
    enableIngress: true
    rayVersion: '2.9.3' # should match the Ray version in the image of the containers
    # If enableInTreeAutoscaling is true, the autoscaler sidecar will be added to the Ray head pod.
    enableInTreeAutoscaling: true
    autoscalerOptions:
      # upscalingMode is "Default" or "Aggressive" or "Conservative"
      # Conservative: Upscaling is rate-limited; the number of pending worker pods is at most the size of the Ray cluster.
      # Default: Upscaling is not rate-limited.
      # Aggressive: An alias for Default; upscaling is not rate-limited.
      upscalingMode: Conservative
      # idleTimeoutSeconds is the number of seconds to wait before scaling down a worker pod which is not using Ray resources.
      idleTimeoutSeconds: 60
      # imagePullPolicy optionally overrides the autoscaler container's default image pull policy (IfNotPresent).
      imagePullPolicy: IfNotPresent
      # Optionally specify the autoscaler container's securityContext.
      securityContext: {}
      env: []
      envFrom: []
    headGroupSpec:
      # Enable ingress
      enableIngress: true
      rayStartParams:
        dashboard-host: '0.0.0.0'
      template:
        spec:
          initContainers:
            - name: git-clone
              image: alpine/git
              command:
                 - /bin/sh
                 - -c
                 - |
                  git clone 代码仓库地址 /app
              volumeMounts:
                 - name: esb
                   mountPath: /app
          containers:
            - name: ray-head
              image: 镜像地址
              ports:
                - containerPort: 6379
                  name: gcs-server
                - containerPort: 8265 # Ray dashboard
                  name: dashboard
                - containerPort: 10001
                  name: client
              resources:
                limits:
                  cpu: "1"
                requests:
                  cpu: "1"
              volumeMounts:
                - name: esb
                  mountPath: /app                
          volumes:
            - name: esb
              # Code can be placed on a cloud disk or directly configured as emptyDir.
              persistentVolumeClaim:
                claimName: pvc名称
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: autoscaling-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            imagePullSecrets:
              - name: 拉取镜像密钥
            containers:
              - name: ray-worker
                image: 镜像仓库地址
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                    nvidia.com/gpu: 1 
                  requests:
                    cpu: "1"
                    nvidia.com/gpu: 1
```


Key parameter descriptions:


|Parameter name |Note |
|---|---|
|enableIngress |Whether to enable Ingress.<br><br>When setting this parameter, you also need to add the following annotations in meta:<br><br>nginx.ingress.kubernetes.io/rewrite\-target: /$1 |
|enableInTreeAutoscaling |Whether to enable autoscaling.<br><br>After enabling, autoscaling will run as a sidecar container in the Head pod and be responsible for cluster scaling tasks.<br><br>After enabling autoscaling, the minReplicas and maxReplicas in workerGroupSpecs set the upper and lower limits for scaling. |
|shutdownAfterJobFinishes |Whether to release RayCluster after the job is completed |
|ttlSecondsAfterFinished |How long after the job is completed to release RayCluster, Unit: seconds |
|idleTimeoutSeconds |Waiting time before scaling down idle workers, Unit: seconds |
|storageClassName |Configure the StorageClass for PVC.<br><br>Currently supports ebs\-essd, ebs\-ssd, and more |


The Ray image address and image key can be filled in as described in [Ray image list](https://docs.byteplus.com/docs/E-MapReduce/109430), or you can use a custom image.
