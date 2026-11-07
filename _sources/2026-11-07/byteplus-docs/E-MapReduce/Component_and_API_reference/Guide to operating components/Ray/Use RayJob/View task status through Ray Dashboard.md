---
title: "View task status through Ray Dashboard"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/View_task_status_through_Ray_Dashboard"
---

Ingress controllers are used in Kubernetes to manage routing for external access to cluster services. This section describes how to provide the RayCluster Dashboard UI via Ingress, enabling you to view task status through Ray's UI.

<span id="_1-准备条件"></span>
## 1. Prerequisites


1. Same prerequisites as in [RayJob Quick Start](https://docs.byteplus.com/docs/E-MapReduce/109441)


<span id="_2-使用指导"></span>
## 2. Usage guide


1. Prepare the yaml file: rayjob.ingress.yaml


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
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-1.2.0
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


In the yaml file, `nginx.ingress.kubernetes.io/rewrite-target: /$1` is an annotation specifically for the Nginx Ingress controller. It designates a new URL target path for requests routed through Ingress. `/$1` means the Nginx Ingress controller will capture the first segment of the incoming request URI (usually the first part of the path) and pass it as a parameter to the backend service.


2. Apply the yaml file

   ```bash
   kubectl apply -f rayjob.ingress.yaml -n <命名空间>
   ```
   

3. Access the Ray Dashboard UI

   You can obtain the endpoint information for ingress access using the following method:

   ```bash
   kubectl get ingress -n <命名空间>
   kubectl describe ingress ingress名称 -n <命名空间>
   ```
   

   Combine the above information to form the final URL. For example, as shown in the figure: http:///rayjob\-sample\-raycluster\-c59cq/ to access the Dashboard.

4. Delete the RayJob

   ```bash
   kubectl delete -f rayjob.ingress.yaml -n <命名空间>
   ```
