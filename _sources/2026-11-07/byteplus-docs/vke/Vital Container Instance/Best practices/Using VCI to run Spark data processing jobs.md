---
title: "Using VCI to run Spark data processing jobs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-VCI-to-run-Spark-data-processing-Jobs"
---

When you use VCI to run Spark data processing jobs, you can flexibly create pods based on your business requirements without the limitations on the node computing capacity of VKE clusters. This effectively reduces computing costs. This topic mainly describes how to install Spark Operator in a VKE cluster and use VCI to run Spark data processing jobs.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

This topic describes how to use VCI to run Spark jobs by using the native Kubernetes Spark Operator. The main steps are as follows:


1. Create a cluster.

2. Connect to the cluster.

3. Install spark\-operator.

4. Test spark\-operator.


To use more advanced features of VCI, you can configure VCI by specifying annotations. For details, see [Pod annotations](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

The following content introduces the proven practices of VCI. To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/VCI-limits) of VCI, you need to perform operations by following the solution described in this topic or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The kubectl tool has been installed in the local environment. For detailed instructions, see [Installing kubectl](https://kubernetes.io/docs/tasks/tools/).

* The Helm tool has been installed in the local environment. For detailed instructions, see [Installing Helm](https://helm.sh/zh/docs/intro/install/).

* Before you create a cluster, make sure that the preparations are complete. For details, see [Preparations](https://docs.byteplus.com/en/docs/vke/Preparations).

* VCI has been activated. For detailed instructions, see [VCI quick guide](https://docs.byteplus.com/en/docs/vke/VCI-quick-guide).


<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXZwYy1jbmkt5a655Zmo572R57uc5qih5Z6L55qE6ZuG576k"></span>
## Step 1: Create a VPC\-CNI cluster


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the top navigation bar, select the region closest to your business.

3. In the left navigation bar, click **Cluster**. On the page that appears, click **Create cluster**.

4. In the **Create cluster** dialog box, click **Create now** in the **Custom managed clusters** section.

5. On the **Create cluster** page, create a cluster that uses the VPC\-CNI network model by following the wizard. The configurations of some parameters are as follows.  For other parameters, see the instructions in [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you add nodes during cluster creation, select appropriate node specifications based on your business requirements. Ensure the specifications meet the requirements for installing and running Spark Operator. This ensures that the vCPUs and memory of the nodes meet your needs.   </div>
   

6. It takes 15 to 20 minutes to create a cluster. You can view the creation progress and check whether the cluster has been created in the **cluster list**.


<span id=".5q2l6aqk5LqM77ya6L-e5o6l6ZuG576k"></span>
## Step 2: Connect to the cluster


1. On the **Cluster** page of the [VKE console](https://console.byteplus.com/vke), find the cluster created in **Step 1**, and click its name.

2. On the **Overview** page of the cluster, click the **Connection** tab.

3. Obtain the cluster access credentials on the **Public network access configuration** tab.

4. Log in to the kubectl client, access the `.kube` directory, and modify the `config` file.

   ```bash
   cd .kube
   vi config
   ```
   

5. Import the obtained cluster access credentials into the `config` file, press the **ESC** key to exit edit mode, and then run the `:wq` command to save the file.

6. Verify whether the cluster is connected.

   ```bash
   kubectl get nodes
   ```
   

   If you see messages similar to the following, kubectl is successfully connected to the cluster.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0401bd7fd11eb5d3a6aa94c77522f256.png) </span>


<span id=".5q2l6aqk5LiJ77ya5a6J6KOFLXNwYXJrLW9wZXJhdG9y"></span>
## Step 3: Install Spark Operator

Install Spark Operator by using the kubectl client.


1. Create a serviceaccount.

   ```bash
   kubectl create serviceaccount spark
   kubectl create clusterrolebinding spark-role --clusterrole=edit --serviceaccount=default:spark --namespace=default
   ```
   

2. Create a namespace named **spark\-operator** in the cluster.

   ```bash
   kubectl create namespace spark-operator
   ```
   

3. Install Spark Operator.

   ```bash
   helm repo add spark-operator https://googlecloudplatform.github.io/spark-on-k8s-operator
   helm install my-release spark-operator/spark-operator --namespace spark-operator --set enableBatchScheduler=true --set enableWebhook=true
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you fail to pull the spark\-operator image when installing Spark Operator, you can go to the <strong>Deployment</strong> page of the target cluster in the <a href="https://console.byteplus.com/vke">VKE</a> console, and update the image address of the <strong>my\-release</strong> workload under the <strong>spark\-operator</strong> namespace to <code>doc-cn-beijing.cr.volces.com/vke/spark:v1beta2-1.3.8-3.1.1</code>. This ensures that Spark Operator can be installed.   </div>
   

<span id=".5q2l6aqk5Zub77ya5L2_55SoLXZjaS3ov5DooYwtc3Bhcmst5Lu75Yqh"></span>
## Step 4: Use VCI to run Spark jobs

This topic provides an example of how to create a Deployment named **spark\-pi ** via a YAML file.


1. On the **Cluster** page of the [VKE](https://console.byteplus.com/vke) console, find the cluster created in **Step 1**, and click its name.

2. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

3. Click **Create with Yaml**. On the page that appears, select **Custom** from the **Type** drop\-down list, enter the following sample code in the **Yaml** code editor, and then click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Pulling images directly from Git is often unstable. CR is an effective solution to this issue. In this example, you can directly use the following image address:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```Bash
   cr-share-cn-shanghai.cr.volces.com/spark/spark-operator:v3.1.1
   ```
      </div>
   

   ```YAML
   # Copyright 2017 Google LLC
   #
   # Licensed under the Apache License, Version 2.0 (the "License");
   # you may not use this file except in compliance with the License.
   # You may obtain a copy of the License at
   #
   #     https://www.apache.org/licenses/LICENSE-2.0
   #
   # Unless required by applicable law or agreed to in writing, software
   # distributed under the License is distributed on an "AS IS" BASIS,
   # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   # See the License for the specific language governing permissions and
   # limitations under the License.
   
   
   apiVersion: "sparkoperator.k8s.io/v1beta2"
   kind: SparkApplication
   metadata:
     name: spark-pi
     namespace: default
   spec:
     type: Scala
     mode: cluster
     image: "cr-share-cn-shanghai.cr.volces.com/spark/spark-operator:v3.1.1" #Use the CR URL of BytePlus as the official URL.
     imagePullPolicy: Always
     mainClass: org.apache.spark.examples.SparkPi
     mainApplicationFile: "local:///opt/spark/examples/jars/spark-examples_2.12-3.1.1.jar"
     sparkVersion: "3.1.1"
     restartPolicy:
       type: Never
     volumes:
       - name: "test-volume"
         hostPath:
           path: "/tmp"
           type: Directory
     driver:
       cores: 1
       coreLimit: "1200m"
       memory: "512m"
       labels:
         version: 3.1.1
       serviceAccount: spark
       volumeMounts:
         - name: "test-volume"
           mountPath: "/tmp"
     executor:
       annotations:
         vke.volcengine.com/burst-to-vci: enforce  #Specify that the Spark job runs on the VCI.
       cores: 1
       instances: 1
       memory: "512m"
       labels:
         version: 3.1.1
       volumeMounts:
         - name: "test-volume"
           mountPath: "/tmp"
   ```
   

4. Run the following command to verify the result.

   ```Shell
   kubectl get sparkapplication
   ```
   

   If information similar to the following content is returned, it indicates that the Spark job has been run.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d5040e3435217f395b0427f7f0e5bbf.png) </span>

   After the Spark job is run, you can run the following command to obtain the details about the Spark job.

   ```Bash
   kubectl describe sparkapplication spark-pi
   ```
   

   Expected response:

   ```Bash
   Name:         spark-pi
   Namespace:    default
   Labels:       <none>
   Annotations:  <none>
   API Version:  sparkoperator.k8s.io/v1beta2
   Kind:         SparkApplication
   Metadata:
     Creation Timestamp:  2023-11-27T15:45:20Z
     Generation:          1
     Resource Version:    24933
     UID:                 ad8fa50c-1d45-4a33-97bd-2c1de4155f7b
   Spec:
     Driver:
       Core Limit:  1200m
       Cores:       1
       Labels:
         Version:        3.1.1
       Memory:           512m
       Service Account:  spark
       Volume Mounts:
         Mount Path:  /tmp
         Name:        test-volume
     Executor:
       Annotations:
         vke.volcengine.com/burst-to-vci:  enforce
       Cores:                              1
       Instances:                          1
       Labels:
         Version:  3.1.1
       Memory:     512m
       Volume Mounts:
         Mount Path:         /tmp
         Name:               test-volume
     Image:                  cr-share-cn-shanghai.cr.volces.com/spark/spark-operator:v3.1.1
     Image Pull Policy:      Always
     Main Application File:  local:///opt/spark/examples/jars/spark-examples_2.12-3.1.1.jar
     Main Class:             org.apache.spark.examples.SparkPi
     Mode:                   cluster
     Restart Policy:
       Type:         Never
     Spark Version:  3.1.1
     Type:           Scala
     Volumes:
       Host Path:
         Path:  /tmp
         Type:  Directory
       Name:    test-volume
   Status:
     Application State:
       State:  COMPLETED
     Driver Info:
       Pod Name:             spark-pi-driver
       Web UI Address:       10.234.70.207:0
       Web UI Port:          4040
       Web UI Service Name:  spark-pi-ui-svc
     Execution Attempts:     1
     Executor State:
       spark-pi-4a08948c1174fd43-exec-1:  FAILED
     Last Submission Attempt Time:        2023-11-27T15:45:23Z
     Spark Application Id:                spark-aadd883935dd422eb0526412b846c9b1
     Submission Attempts:                 1
     Submission ID:                       923c3ed6-50de-4b65-a0e2-7c506b72dd2a
     Termination Time:                    2023-11-27T15:48:10Z
   Events:
     Type     Reason                     Age   From            Message
     ----     ------                     ----  ----            -------
     Normal   SparkApplicationAdded      18m   spark-operator  SparkApplication spark-pi was added, enqueuing it for submission
     Normal   SparkApplicationSubmitted  18m   spark-operator  SparkApplication spark-pi was submitted successfully
     Normal   SparkDriverRunning         18m   spark-operator  Driver spark-pi-driver is running
     Normal   SparkExecutorPending       18m   spark-operator  Executor [spark-pi-4a08948c1174fd43-exec-1] is pending
     Normal   SparkExecutorRunning       16m   spark-operator  Executor [spark-pi-4a08948c1174fd43-exec-1] is running
     Normal   SparkDriverCompleted       16m   spark-operator  Driver spark-pi-driver completed
     Normal   SparkApplicationCompleted  16m   spark-operator  SparkApplication spark-pi completed
     Warning  SparkExecutorFailed        15m   spark-operator  Executor [spark-pi-4a08948c1174fd43-exec-1 %!s(int=-1) Unknown (Container not Found)] failed with ExitCode: %!d(MISSING), Reason: %!s(MISSING)
   ```
   


<span id=".c3Bhcmst5Lu75Yqh5pel5b-X5pS26ZuG"></span>
## Spark job log collection

You can collect VCI logs by using TLS of BytePlus. For more information, see [Collecting VCI container logs](https://docs.byteplus.com/en/docs/vke/Collecting-VCI-container-logs-using-Torch-Log-Service).

<span id=".5L2_55So6ZWc5YOP57yT5a2Y"></span>
## Image cache usage

If the Spark image is large (over 2 GB), pulling it takes a long time. You can speed up image pulling with image cache. For more information, see [Image caches](https://docs.byteplus.com/en/docs/vke/Image-Cache).
