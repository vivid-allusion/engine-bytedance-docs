---
title: "RayJob Quick Start"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/RayJob_Quick_Start"
---

In the Ray on VKE scenario, you can submit Ray jobs using the RayJob method. When using RayJob, KubeRay automatically creates a RayCluster and submits the Ray job once the cluster is ready. It also supports automatically deleting the RayCluster after the Ray job completes.

This section provides a detailed example of using RayJob, in which a simple Python code snippet is executed to help you get started and use RayJob quickly.

<span id="_1-准备条件"></span>
## 1. Prerequisites


1. Deploy the Ray service in the EMR on VKE product.

2. To run RayJob jobs using the kubectl command, you need to install the kubectl tool (see [Install and configure kubectl](https://kubernetes.io/docs/tasks/tools/)), and configure the connection information for the Volcano Engine VKE cluster (see [Connect to a VKE cluster](https://www.volcengine.com/docs/6460/100919#%E6%AD%A5%E9%AA%A4%E4%BA%8C%EF%BC%9A%E8%BF%9E%E6%8E%A5%E9%9B%86%E7%BE%A4)).


<span id="_2-使用指导"></span>
## 2. Usage guide


1. Prepare the YAML file for RayJob: rayjob.sample.yaml

   ```yaml
   apiVersion: ray.io/v1
   kind: RayJob
   metadata:
     name: rayjob-sample
   spec:
     entrypoint: python /home/ray/samples/sample_code.py
         
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
                   image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-1.2.0
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
               self.name = "counter_name"
               self.counter = 0
   
           def inc(self):
               self.counter += 1
   
           def get_counter(self):
               return "{} got {}".format(self.name, self.counter)
   
       counter = Counter.remote()
   
       for _ in range(5):
           ray.get(counter.inc.remote())
           print(ray.get(counter.get_counter.remote()))
   ```
   


In this YAML file:


* Define the RayJob name as "`rayjob-sample`"

* Specify the job entry point as "`python /home/ray/samples/sample_code.py` "

* In HeadGroupSpec, define the head information of the RayCluster: specify the image name, ports, resource limits, and mount volumes.

* In WorkerGroupSpecs, define the worker information of the RayCluster.

* In the final Python script,

   * Define a `Counter` class, which is a Ray remote object that includes methods for incrementing the counter and retrieving the current count.

   * Create a remote instance of `Counter`, perform five remote increment operations, and print the current count after each increment.

2. Execute the above YAML file

   ```shell
   kubectl apply -f rayjob.sample.yaml -n <命名空间>
   ```
   

3. Check the RayJob execution status

   You can see the created RayCluster and the pods used by RayJob in the VKE cluster.

4. Delete the RayJob

   ```shell
   kubectl delete -f rayjob.sample.yaml -n <命名空间>
   ```
