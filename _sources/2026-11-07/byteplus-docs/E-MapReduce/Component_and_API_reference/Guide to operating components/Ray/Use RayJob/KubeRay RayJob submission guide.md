---
title: "KubeRay RayJob submission guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/KubeRay_RayJob_submission_guide"
---

In the Ray on VKE scenario, Ray jobs can be submitted using the RayJob method. When using RayJob, KubeRay automatically creates a RayCluster and submits the Ray job once the cluster is ready. It also supports automatically deleting the RayCluster after the Ray job completes. This section introduces the YAML file versions and usage examples of RayJob in various scenarios.

<span id="场景一：提交简单的rayjob"></span>
## Scenario 1: Submit a simple RayJob

The following YAML is a demo example for a simple test scenario. In this example, the Ray job code is mounted to the RayCluster via a ConfigMap, which is suitable for simple code testing scenarios.

```yaml
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
spec:
  entrypoint: python /home/ray/samples/sample_code.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 300

  runtimeEnvYAML: |
    env_vars:
      counter_name: "test_counter"
      
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.9.3' # should match the Ray version in the image of the containers
    # Ray head pod template
    headGroupSpec:
      rayStartParams:
        dashboard-host: '0.0.0.0'
      template:
        spec:
          containers:
            - name: ray-head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
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
                  cpu: "200m"
              volumeMounts:
                - mountPath: /home/ray/samples
                  name: code-sample
          volumes:
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
                lifecycle: 
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                  requests:
                    cpu: "200m"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import ray
    import os
    import requests

    ray.init()

    @ray.remote
    class Counter:
        def __init__(self):
            self.name = os.getenv("counter_name")
            assert self.name == "test_counter"
            self.counter = 0

        def inc(self):
            self.counter += 1

        def get_counter(self):
            return "{} got {}".format(self.name, self.counter)

    counter = Counter.remote()

    for _ in range(5):
        ray.get(counter.inc.remote())
        print(ray.get(counter.get_counter.remote()))

    assert requests.__version__ == "2.31.0"
```


The execution status of the above job can be viewed by checking the logs of the job pod:

```plain
INFO cli.py:36 -- Job submission server address: http://rayjob-sample-raycluster-xg4mb-head-svc.test1.svc.cluster.local:8265
SUCC cli.py:60 -- ------------------------------------------------
SUCC cli.py:61 -- Job 'rayjob-sample-2m42f' submitted successfully
SUCC cli.py:62 -- ------------------------------------------------
INFO cli.py:285 -- Next steps
INFO cli.py:286 -- Query the logs of the job:
INFO cli.py:288 -- ray job logs rayjob-sample-2m42f
INFO cli.py:290 -- Query the status of the job:
INFO cli.py:292 -- ray job status rayjob-sample-2m42f
INFO cli.py:294 -- Request the job to be stopped:
INFO cli.py:296 -- ray job stop rayjob-sample-2m42f
INFO cli.py:303 -- Tailing logs until the job exits (disable with --no-wait):
INFO worker.py:1405 -- Using address 192.168.6.48:6379 set in the environment variable RAY_ADDRESS
INFO worker.py:1540 -- Connecting to existing Ray cluster at address: 192.168.6.48:6379...
INFO worker.py:1715 -- Connected to Ray cluster. View the dashboard at 192.168.6.48:8265  
test_counter got 1
test_counter got 2
test_counter got 3
test_counter got 4
test_counter got 5
SUCC cli.py:60 -- -----------------------------------
SUCC cli.py:61 -- Job 'rayjob-sample-2m42f' succeeded
SUCC cli.py:62 -- -----------------------------------
```


Since the ttlSecondsAfterFinished parameter above is set to 300 seconds, the RayCluster will be automatically released after 300 seconds.

<span id="场景二：rayjob中配置ingress透出dashboard"></span>
## Scenario 2: Configure Ingress in RayJob to expose the Dashboard

In real\-world operation scenarios, it may be necessary to view the Dashboard corresponding to the RayCluster for better task monitoring. The Dashboard can be exposed using the following method:

```yaml
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
  annotations:
    # This annotation must be added, otherwise accessing the dashboard will result in a 404 error
    nginx.ingress.kubernetes.io/rewrite-target: /$1 
spec:
  entrypoint: python /home/ray/samples/sample_code.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 3000

  runtimeEnvYAML: |
    env_vars:
      counter_name: "test_counter"
      
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.9.3' # should match the Ray version in the image of the containers
    # Ray head pod template
    headGroupSpec:
      # Enable ingress
      enableIngress: true
      rayStartParams:
        dashboard-host: '0.0.0.0'
      template:
        spec:
          containers:
            - name: ray-head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
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
                  cpu: "200m"
              volumeMounts:
                - mountPath: /home/ray/samples
                  name: code-sample
          volumes:
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
                lifecycle:
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                  requests:
                    cpu: "200m"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import ray
    import os
    import requests

    ray.init()

    @ray.remote
    class Counter:
        def __init__(self):
            self.name = os.getenv("counter_name")
            assert self.name == "test_counter"
            self.counter = 0

        def inc(self):
            self.counter += 1

        def get_counter(self):
            return "{} got {}".format(self.name, self.counter)

    counter = Counter.remote()

    for _ in range(5):
        ray.get(counter.inc.remote())
        print(ray.get(counter.get_counter.remote()))

    assert requests.__version__ == "2.31.0"
```


The endpoint information for ingress access can be obtained as follows:

```yaml
kubectl get ingress -n +上述yaml部署的namespace名称
kubectl describe ingress ingress名称 -n +上述yaml部署的namespace名称
```


Combine the above information to form the final URL. For example, as shown in the figure: http://VIP/rayjob\-sample\-raycluster\-c59cq/ can be used to access the Dashboard.

<span id="场景三：rayjob中挂载pvc"></span>
## Scenario 3: Mount a PVC in RayJob

In certain RayJob development scenarios, the disk space of the pod's mount path may be insufficient. In such cases, a PVC needs to be mounted to the RayJob.

The following is an example of using the csi\-ebs plugin:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
 name: test-pvc
spec:
 storageClassName: ebs-essd
 accessModes:
   - ReadWriteOnce
 resources:
   requests:
     storage: 40Gi
---
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
spec:
  entrypoint: python /home/ray/samples/sample_code.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 300

  runtimeEnvYAML: |
    env_vars:
      counter_name: "test_counter"
      
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.9.3' # should match the Ray version in the image of the containers
    # Ray head pod template
    headGroupSpec:
      rayStartParams:
        dashboard-host: '0.0.0.0'
      template:
        spec:
          containers:
            - name: ray-head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
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
                  cpu: "200m"
              volumeMounts:
                - mountPath: /home/ray/samples
                  name: code-sample
                - mountPath: "/var/data/"
                  name: esb
          volumes:
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
            - name: esb
              persistentVolumeClaim:
                claimName: test-pvc
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
                lifecycle:
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                  requests:
                    cpu: "200m"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import ray
    import os
    import requests

    ray.init()

    @ray.remote
    class Counter:
        def __init__(self):
            self.name = os.getenv("counter_name")
            assert self.name == "test_counter"
            self.counter = 0

        def inc(self):
            self.counter += 1

        def get_counter(self):
            return "{} got {}".format(self.name, self.counter)

    counter = Counter.remote()

    for _ in range(5):
        ray.get(counter.inc.remote())
        print(ray.get(counter.get_counter.remote()))

    assert requests.__version__ == "2.31.0"
```


In the above demo, the cloud disk is mounted to the /var/data directory. The code can write some intermediate data to this directory for use by subsequent RayJob tasks.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_202a787ae6aa0175ad54aefb20435465.png) </span>

Caution: Since the default reclaim policy of the StorageClass in VKE is Delete, the PV will also be deleted when the above PVC is deleted. Customers can orchestrate a series of tasks using Airflow and clear the PVC at the end of the workflow to enable reuse of intermediate results. Additionally, customers can modify the reclaim policy of the above StorageClass so that the PV remains when the PVC is cleared. However, in this case, customers need to manage when to clear the data themselves.

<span id="场景四：通过git拉取业务源码到rayjob中"></span>
## Scenario 4: Pull business source code into RayJob via Git

In real business scenarios, job code is typically managed in a Git repository. The following describes how to conveniently pull a Git repository for job testing using an InitContainer:

```yaml
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
  annotations:
    # This annotation must be added, otherwise accessing the dashboard will result in a 404 error
    nginx.ingress.kubernetes.io/rewrite-target: /$1 
spec:
  entrypoint: python /app/apiserver/test/e2e/resources/counter_sample.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 3000

  runtimeEnvYAML: |
    env_vars:
      counter_name: "test_counter"
      
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.9.3' # should match the Ray version in the image of the containers
    # Ray head pod template
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
                  git clone https://github.com/ray-project/kuberay /app
              volumeMounts:
                 - name: code
                   mountPath: /app
          containers:
            - name: ray-head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
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
                  cpu: "200m"
              volumeMounts:
               - name: code 
                 mountPath: /app   
          volumes:
            - name: code
              emptyDir: {}
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
                lifecycle:
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                  requests:
                    cpu: "200m"
```


For actual company scenarios, it is usually necessary to configure the key information required to pull the Git repository. You can follow the steps below:

```yaml
kubectl create secret generic ssh-key-secret --from-file=ssh-privatekey=id_ras的绝对路径

# Make the following changes to the above initContainer section:
initContainers:
- name: git-clone
  image: alpine/git
  command:
     - /bin/sh
     - -c
     - |
     git clone GitHub - ray-project/kuberay: A toolkit to run Ray applications on Kubernetes /app
     sed -i 's/2.26.0/2.31.0/g' /app/apiserver/test/e2e/resources/counter_sample.py                
  volumeMounts:
     - name: code
       mountPath: /app
     - name: ssh-key-volume
       mountPath: /root/.ssh
  
  # In the volumes section, mount the secret created above
volumes:
  - name: code
    emptyDir: {}
  - name: ssh-key-volume
    secret:
      secretName: ssh-key-secret
```


<span id="场景五：rayjob支持gpu类型作业"></span>
## Scenario 5: RayJob supports GPU\-type jobs

```yaml
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
spec:
  entrypoint: python /home/ray/samples/sample_code.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 300
 
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.9.3' # should match the Ray version in the image of the containers
    # Ray head pod template
    enableInTreeAutoscaling: true
    headGroupSpec: 
      rayStartParams:
        dashboard-host: '0.0.0.0'
      template:
        spec:
          containers:
            - name: ray-head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
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
                  nvidia.com/gpu: 1
                requests:
                  cpu: "200m"
                  nvidia.com/gpu: 1
              volumeMounts:
                - mountPath: /home/ray/samples
                  name: code-sample
          volumes:
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
                lifecycle:  
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                    nvidia.com/gpu: 1
                  requests:
                    cpu: "200m"
                    nvidia.com/gpu: 1
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import ray
    import os
    import torch

    ray.init()
    print(torch.cuda.is_available())
```


You can check the logs to see that cuda available is True

```plain
INFO cli.py:36 -- Job submission server address: http://rayjob-sample-raycluster-drs78-head-svc.test2.svc.cluster.local:8265
SUCC cli.py:60 -- ------------------------------------------------
SUCC cli.py:61 -- Job 'rayjob-sample-rb8g5' submitted successfully
SUCC cli.py:62 -- ------------------------------------------------
INFO cli.py:285 -- Next steps
INFO cli.py:286 -- Query the logs of the job:
INFO cli.py:288 -- ray job logs rayjob-sample-rb8g5
INFO cli.py:290 -- Query the status of the job:
INFO cli.py:292 -- ray job status rayjob-sample-rb8g5
INFO cli.py:294 -- Request the job to be stopped:
INFO cli.py:296 -- ray job stop rayjob-sample-rb8g5
INFO cli.py:303 -- Tailing logs until the job exits (disable with --no-wait):
INFO worker.py:1405 -- Using address 192.168.0.11:6379 set in the environment variable RAY_ADDRESS
INFO worker.py:1540 -- Connecting to existing Ray cluster at address: 192.168.0.11:6379...
INFO worker.py:1715 -- Connected to Ray cluster. View the dashboard at 192.168.0.11:8265  
True
SUCC cli.py:60 -- -----------------------------------
SUCC cli.py:61 -- Job 'rayjob-sample-rb8g5' succeeded
SUCC cli.py:62 -- -----------------------------------
```


<span id="场景六：rayjob中实现autoscaler功能"></span>
## Scenario 6: Implementing the AutoScaler feature in RayJob

For a principle overview, refer to: [Enable Autoscaler for RayCluster](https://docs.byteplus.com/docs/undefined/69aa38e166ca14055c32e83c)

```yaml
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
  annotations:
  # This annotation must be added, otherwise accessing the dashboard will result in a 404 error
    nginx.ingress.kubernetes.io/rewrite-target: /$1 
spec:
  entrypoint: python /home/ray/samples/sample_code.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 300
 
  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
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
          containers:
            - name: ray-head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
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
                - mountPath: /home/ray/samples
                  name: code-sample
          volumes:
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-20240402
                lifecycle:  
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                  requests:
                    cpu: "1"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import ray
    ray.init()

    import time
    @ray.remote
    def square(x):
        time.sleep(100)
        return x * x


    futures = [square.remote(i) for i in range(40)]
    print(ray.get(futures))
```


The result is as follows (kubectl logs ray\-cluster pod name autoscaler \-n namespace where rayCluster is located):

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c054560c5f00d6f0fc47cfd1c4479d30.png) </span>

By viewing the AutoScaler logs, you can see that the AutoScaler initiates a scaling\-out request when resources are tight. Additionally, after the task is completed and the idleTimeoutSeconds period has passed, idle pods will go through the scale\-down process.
