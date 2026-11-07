---
title: "Monitor RayJob using EMR"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Monitor_RayJob_using_EMR"
---

In Kubernetes, Prometheus can be used for metric collection. This section describes how to configure Prometheus\-related parameters in the YAML file of RayJob, so that RayJob metrics can be collected into the Ray service of EMR.

<span id="_1-准备条件"></span>
## 1 Prerequisites


1. Same as the prerequisites in [RayJob Quick Start](https://docs.byteplus.com/docs/E-MapReduce/109441)

2. Compatible with EMR product version 1.4.0 and above


<span id="_2-使用指导"></span>
## 2 Usage guide


1. Prepare the YAML file: rayjob.metrics.yaml

   ```yaml
   apiVersion: ray.io/v1
   kind: RayJob
   metadata:
     name: rayjob-lxy-online
   spec:
     entrypoint: python /home/ray/samples/sample_code.py
     shutdownAfterJobFinishes: false
     runtimeEnvYAML: |
       pip:
         - requests==2.26.0
         - pendulum==2.1.2
       env_vars:
         counter_name: "test_counter"
     rayClusterSpec:
       rayVersion: "2.9.3"
       # Enable autoscaler
       enableInTreeAutoscaling: true
       headGroupSpec:
         rayStartParams:
           dashboard-host: "0.0.0.0"
         #pod template
         template:
           metadata:
             annotations:
               prometheus.io/path: /metrics
               prometheus.io/port: "8080"
               prometheus.io/scrape: "true"
           spec:
             imagePullSecrets:
               - name: lxy-docker-secret
             containers:
               - name: ray-head
                 image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.9.3-py3.9-ubuntu20.04-1.2.0
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
               # You set volumes at the Pod level, then mount them into containers inside that Pod
               - name: code-sample
                 configMap:
                   name: ray-job-code-sample
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
           rayStartParams: {}
           #pod template
           template:
             metadata:
               annotations:
                 prometheus.io/path: /metrics
                 prometheus.io/port: "8080"
                 prometheus.io/scrape: "true"
             spec:
               imagePullSecrets:
                 - name: lxy-docker-secret
               containers:
                 - name: ray-worker # must consist of lower case alphanumeric characters or '-', and must start and end with an alphanumeric character (e.g. 'my-name',  or '123-abc'
                   image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.9.3-py3.9-ubuntu20.04-1.2.0
                   lifecycle:
                     preStop:
                       exec:
                         command: ["/bin/sh", "-c", "ray stop"]
                   resources:
                     limits:
                       cpu: "1"
                     requests:
                       cpu: "200m"
     submitterPodTemplate:
       spec:
         imagePullSecrets:
           - name: lxy-docker-secret
         restartPolicy: Never
         containers:
           - name: my-custom-rayjob-submitter-pod
             image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.9.3-py3.9-ubuntu20.04-1.2.0
     ######################Ray code sample#################################
   # this sample is from https://docs.ray.io/en/latest/cluster/job-submission.html#quick-start-example
   # it is mounted into the container and executed to show the Ray job at work
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
               # Used to verify runtimeEnv
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
   ```
   


The following three annotations in this YAML file are related to the Prometheus monitoring system:


* `prometheus.io/path: /metrics` specifies the path that Prometheus should access when scraping metrics. In this example, `/metrics` is the HTTP endpoint where the container exposes metrics. The Prometheus server will periodically request this path to obtain metric data.

* `prometheus.io/port: "8080"`: Specifies the port that Prometheus should use when scraping metrics. In this example, the port is `8080`. This means that Prometheus will attempt to connect to port `8080` of the Ray cluster node to obtain metrics.

* `prometheus.io/scrape: "true"`: Specifies whether Prometheus should scrape the specified endpoint. Setting it to `"true"` indicates that Prometheus needs to scrape metrics from this endpoint.

2. Execute the YAML file

   ```bash
   kubectl apply -f rayjob.metrics.yaml -n <命名空间>
   ```
   

3. Ray monitoring metric information can be viewed in cluster monitoring in the EMR cluster

4. Delete RayJob

   ```bash
   kubectl delete -f rayjob.metrics.yaml -n <命名空间>
   ```
