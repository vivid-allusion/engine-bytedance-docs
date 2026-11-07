---
title: "Replace the K8S Default Scheduler with Volcano Scheduler to run Spark and Ray jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Replace_the_K8S_Default_Scheduler_with_Volcano_Scheduler_to_run_Spark_and_Ray_jobs"
---

EMR On VKE supports running Spark and Ray jobs with the K8S default scheduler. To achieve better job performance, consider using Volcano Scheduler instead of the K8S default scheduler if you have the following requirements:


1. Fair scheduling among multiple jobs: Prevent a single job's Driver/Executor from consuming excessive resources, which can cause starvation for other jobs.

2. Queue capabilities: Distinguish available quotas for tasks and set min/max resource limits for different types of jobs.

3. Resource reservation: Prevent resource deadlocks caused by all Drivers occupying all resources during high concurrency jobs.

4. Batch scheduling: Supports batch scheduling capabilities.


<span id="_1-安装-volcano-scheduler"></span>
## 1. Install Volcano Scheduler

<span id="方式一：直接使用-yaml-文件安装"></span>
### Method 1: Install directly using a YAML file

```bash
kubectl apply -f https://raw.githubusercontent.com/volcano-sh/volcano/master/installer/volcano-development.yam
```


<span id="方式二：使用-helm-chart-安装"></span>
### Method 2: Install using a Helm chart

> The example uses the source code installation method. Source code reference: https://github.com/volcano\-sh/volcano


```bash
helm install volcano installer/helm/chart/volcano --namespace volcano-system --create-namespace

# list helm release
helm list -n volcano-system
```


<span id="_2-使用-volcano-调度-spark-作业"></span>
## 2. Use Volcano to schedule Spark jobs

<span id="_2-1-修改-sparkoperator-配置以支持使用-volcano-scheduler"></span>
### 2.1 Modify the SparkOperator configuration to support Volcano Scheduler

Update using the Helm installation directory


1. Locate the agent pod of EMR and enter it. You can find the agent using the following command:


```bash
kubectl get pods -n {您的emr集群ID}

kubectl exec -it {上一步的agent pod名称} /bin/bash -n {您的emr集群ID}

cd /tmp/SPARK/1.0.0/client/charts
```



2. (Optional) If your cluster version is < EMR\-VKE\-1.4.0, manually perform the following upgrade:

   1. Modify /tmp/SPARK/1.0.0/client/charts/SparkOperator/templates/webhook\-cleanup\-job.yaml as follows (differences highlighted in red):

   ```yaml
   {{ if .Values.webhook.enable }}
   apiVersion: batch/v1
   kind: Job
   metadata:
     name: {{ include "spark-operator.fullname" . }}-webhook-cleanup
     annotations:
       {{- toYaml .Values.webhook.cleanupAnnotations | nindent 4 }}
     labels:
       {{- include "spark-operator.labels" . | nindent 4 }}
   spec:
     template:
       metadata:
         name: {{ include "spark-operator.fullname" . }}-webhook-cleanup
         {{- if .Values.istio.enabled }}
         annotations:
           "sidecar.istio.io/inject": "false"
         {{- end }}
         {{- if .Values.webhook.cleanupPodLabels }}
         labels:
           {{- toYaml .Values.webhook.cleanupPodLabels | nindent 8 }}
         {{- end }}
       spec:
         serviceAccountName: {{ include "spark-operator.serviceAccountName" . }}
         restartPolicy: OnFailure
         {{- with .Values.imagePullSecrets }}
         imagePullSecrets:
           {{- toYaml . | nindent 8 }}
         {{- end }}
         containers:
         - name: clean-secret
           image: {{ .Values.image.repository }}:{{ default .Chart.AppVersion .Values.image.tag }}
           imagePullPolicy: {{ .Values.image.pullPolicy }}
           securityContext:
             {{- toYaml .Values.securityContext | nindent 10 }}
           command:
           - "/bin/sh"
           - "-c"
           - "curl -ik \
             -X DELETE \
             -H \"Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)\" \
             -H \"Accept: application/json\" \
             -H \"Content-Type: application/json\" \
             https://kubernetes.default.svc/api/v1/namespaces/{{ .Release.Namespace }}/secrets/{{ include "spark-operator.fullname" . }}-webhook-certs \
             && \
             curl -ik \
             -X DELETE \
             -H \"Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)\" \
             -H \"Accept: application/json\" \
             -H \"Content-Type: application/json\" \
             --data \"{\\\"kind\\\":\\\"DeleteOptions\\\",\\\"apiVersion\\\":\\\"batch/v1\\\",\\\"propagationPolicy\\\":\\\"Foreground\\\"}\" \
             https://kubernetes.default.svc/apis/batch/v1/namespaces/{{ .Release.Namespace }}/jobs/{{ include "spark-operator.fullname" . }}-webhook-init"
           resources:
             {{- toYaml .Values.webhook.cleanupResources | nindent 10 }}
         {{- with .Values.tolerations }}
         tolerations:
           {{- toYaml . | nindent 8 }}
         {{- end }}
         {{- with .Values.nodeSelector }}
         nodeSelector:
           {{- toYaml . | nindent 8 }}
         {{- end }}
   {{ end }}
   ```
   

3. Execute the upgrade command


```bash
helm upgrade spark-operator ./SparkOperator --namespace {您的emr spark 所在 namespace} --set batchScheduler.enable=true --set webhook.enable=true
```


<span id="_2-2-提交-spark-作业，并指定使用-volcano-调度器调度"></span>
### 2.2 Submit Job for Spark and specify scheduling with Volcano Scheduler

```bash
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: spark-wordcount
spec:
  type: Scala
  sparkVersion: 3.2.1
  batchScheduler: "volcano"
  mainClass: org.apache.spark.examples.SparkPi
  mainApplicationFile: "tos://xxx/spark-examples_2.12-3.3.3.jar"
  arguments:
    - "1000"
  driver:
    cores: 1
    coreLimit: 1000m
    memory: 8g
  executor:
    cores: 1
    coreLimit: 1000m
    memory: 4g
    memoryOverhead: 2g
    instances: 1
```


After submitting the job, you can check the scheduling status through the driver pod event:

```bash
Events:
  Type    Reason     Age   From                  Message
  ----    ------     ----  ----                  -------
  Normal  Scheduled  27s   volcano               Successfully assigned emr-3ia0hq36gf3bd5my2wxh-spark/spark-wordcount-driver to 172.16.2.27
```


You can also check resource allocation by viewing Volcano's default queue.

<span id="进阶功能"></span>
#### Advanced features

To restrict and control a job using a specific queue, you can manually create a Volcano queue:

```bash
cat << EOF > sparkQ.yaml
apiVersion: scheduling.volcano.sh/v1beta1
kind: Queue
metadata:
  name: sparkqueue
spec:
  weight: 1
  reclaimable: false
  capability:
    cpu: 4
    memory: 16Gi
EOF

kubectl apply -f sparkQ.yaml
```


A Volcano queue is an entity that contains a group of **podgroup**, serving as the foundation for resource isolation and as the basis for this group of podgroups to acquire cluster resources. You can Submit Job for Spark/Ray to the queue. Modify the above SparkApplication YAML to create a job using a queue:

```bash
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: spark-wordcount-2
spec:
  type: Scala
  sparkVersion: 3.2.1
  batchScheduler: "volcano"
  batchSchedulerOptions:
    queue: "sparkqueue"
  mainClass: org.apache.spark.examples.SparkPi
  mainApplicationFile: "tos://{ 您的 bucket }/SparkJobs/spark-examples_2.12-3.3.3.jar"
  arguments:
    - "1000"
  driver:
    cores: 1
    coreLimit: 1000m
    memory: 8g
  executor:
    cores: 1
    coreLimit: 1000m
    memory: 4g
    memoryOverhead: 2g
    instances: 1
```


You can obtain job scheduling information by querying the usage details of the Volcano Queue:

```bash
kubectl describe queue {上述创建的 queue 名称} -n { 你的命名空间 }
...
Spec:
  Capability:
    Cpu:        5
    Memory:     15Gi
  Reclaimable:  false
  Weight:       4
Status:
  Allocated:
    Cpu:                        2
    Memory:                     15155Mi
    Pods:                       2
    vke.volcengine.com/eni-ip:  2
```


<span id="_3-使用-volcano-调度-ray-作业"></span>
## 3. Use Volcano to schedule Ray jobs

<span id="修改-rayoperator-配置以支持使用-volcano-scheduler"></span>
### Modify the RayOperator configuration to support Volcano Scheduler

Update using the Helm installation directory


1. Locate the agent pod of EMR and enter it. You can find the agent using the following command:


```bash
kubectl get pods -n {您的emr集群ID}

kubectl exec -it {上一步的agent pod名称} /bin/bash -n {您的emr集群ID}

cd /tmp/RAY/1.0.0/client/charts
```



2. (Optional) If your cluster version is < EMR\-VKE\-1.4.0, manually perform the following upgrade:

   1. Modify /tmp/RAY/1.0.0/client/charts/kuberay\-operator/templates/rolebinding.yaml as follows (differences highlighted in red):

   ```yaml
   {{- if .Values.rbacEnable }}
   kind: ClusterRoleBinding
   apiVersion: rbac.authorization.k8s.io/v1
   metadata:
     labels:
   {{ include "kuberay-operator.labels" . | indent 4 }}
     name: {{ include "kuberay-operator.fullname" . }}
   subjects:
   - kind: ServiceAccount
     name: {{ .Values.serviceAccount.name  }}
     namespace: {{ .Release.Namespace }}
   roleRef:
     kind: ClusterRole
     name: {{ include "kuberay-operator.fullname" . }}
     apiGroup: rbac.authorization.k8s.io
   {{- end }}
   ```
   

   3. Modify /tmp/RAY/1.0.0/client/charts/kuberay\-operator/templates/role.yaml as follows:

   ```yaml
   {{- if .Values.rbacEnable }}
   kind: ClusterRole
   apiVersion: rbac.authorization.k8s.io/v1
   metadata:
     labels:
   {{ include "kuberay-operator.labels" . | indent 4 }}
     name: {{ include "kuberay-operator.fullname" . }}
   rules:
   - apiGroups:
     - batch
     resources:
     - jobs
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - coordination.k8s.io
     resources:
     - leases
     verbs:
     - create
     - get
     - list
     - update
   - apiGroups:
     - ""
     resources:
     - events
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ""
     resources:
     - pods
     verbs:
     - create
     - delete
     - deletecollection
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ""
     resources:
     - pods/status
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ""
     resources:
     - serviceaccounts
     verbs:
     - create
     - delete
     - get
     - list
     - watch
   - apiGroups:
     - ""
     resources:
     - services
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ""
     resources:
     - services/status
     verbs:
     - get
     - patch
     - update
   - apiGroups:
     - extensions
     resources:
     - ingresses
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - networking.k8s.io
     resources:
     - ingressclasses
     verbs:
     - get
     - list
     - watch
   - apiGroups:
     - networking.k8s.io
     resources:
     - ingresses
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ray.io
     resources:
     - rayclusters
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ray.io
     resources:
     - rayclusters/finalizers
     verbs:
     - update
   - apiGroups:
     - ray.io
     resources:
     - rayclusters/status
     verbs:
     - get
     - patch
     - update
   - apiGroups:
     - ray.io
     resources:
     - rayjobs
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ray.io
     resources:
     - rayjobs/finalizers
     verbs:
     - update
   - apiGroups:
     - ray.io
     resources:
     - rayjobs/status
     verbs:
     - get
     - patch
     - update
   - apiGroups:
     - ray.io
     resources:
     - rayservices
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   - apiGroups:
     - ray.io
     resources:
     - rayservices/finalizers
     verbs:
     - update
   - apiGroups:
     - ray.io
     resources:
     - rayservices/status
     verbs:
     - get
     - patch
     - update
   - apiGroups:
     - rbac.authorization.k8s.io
     resources:
     - rolebindings
     verbs:
     - create
     - delete
     - get
     - list
     - watch
   - apiGroups:
     - rbac.authorization.k8s.io
     resources:
     - roles
     verbs:
     - create
     - delete
     - get
     - list
     - update
     - watch
   - apiGroups:
     - route.openshift.io
     resources:
     - routes
     verbs:
     - create
     - delete
     - get
     - list
     - patch
     - update
     - watch
   {{- if .Values.batchScheduler.enabled }}
   - apiGroups:
     - scheduling.volcano.sh
     resources:
     - podgroups
     verbs:
     - create
     - delete
     - get
     - list
     - update
     - watch
   - apiGroups:
     - apiextensions.k8s.io
     resources:
     - customresourcedefinitions
     verbs:
     - get
   {{- end }}
   {{- end }}
   ```
   

3. Run the upgrade command to allow ray to use batchScheduler


```bash
helm upgrade kuberay-operator ./kuberay-operator --namespace {您 rayOperator 部署的 namespace} --set batchScheduler.enabled=true
```



4. Create a queue:


```bash
cat << EOF > sparkQ.yaml
apiVersion: scheduling.volcano.sh/v1beta1
kind: Queue
metadata:
  name: rayqueue
spec:
  weight: 1
  reclaimable: false
  capability:
    cpu: 5
    memory: 10Gi
EOF

kubectl apply -f sparkQ.yaml
```



5. Create a RayCluster and use Volcano for scheduling


```bash
apiVersion: ray.io/v1
kind: RayCluster
metadata:
  name: ray-volcano-cluster
  labels:
    ray.io/scheduler-name: volcano
    volcano.sh/queue-name: rayqueue
spec:
  rayVersion: '2.7.0'
  headGroupSpec:
    rayStartParams: {}
    template:
      spec:
        containers:
          - name: ray-head
            image: 您的 ray 镜像地址
            resources:
              limits:
                cpu: "1"
                memory: "2Gi"
              requests:
                cpu: "1"
                memory: "2Gi"
  workerGroupSpecs:
    - groupName: worker
      rayStartParams: {}
      replicas: 2
      minReplicas: 2
      maxReplicas: 2
      template:
        spec:
          containers:
            - name: ray-head
              image: 您的 ray 镜像地址
              resources:
                limits:
                  cpu: "1"
                  memory: "1Gi"
                requests:
                  cpu: "1"
                  memory: "1Gi"
```



6. Create a Ray Job and use Volcano for scheduling


```bash
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample-0702
  labels:
    ray.io/scheduler-name: volcano
    volcano.sh/queue-name: rayqueue
  annotations:
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
              image: 您的 ray 镜像地址
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
                image: 您的 ray 镜像地址
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



7. You can view the Volcano scheduling status through queues or container information:


RayHead：

```bash
Events:
  Type    Reason     Age   From                  Message
  ----    ------     ----  ----                  -------
  Normal  Scheduled  36s   volcano               Successfully assigned emr-3ia0hq36e35exzu87met-ray/ray-volcano-cluster-head-74v9n to 172.16.2.25
```


Queue:

```bash
Spec:
  Capability:
    Cpu:        5
    Memory:     15Gi
  Reclaimable:  false
  Weight:       4
Status:
  Allocated:
    Cpu:                        3
    Memory:                     4Gi
    Pods:                       3
    vke.volcengine.com/eni-ip:  3
```
