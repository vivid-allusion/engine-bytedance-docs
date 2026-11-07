---
title: "User guide for submitting Ray jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/User_guide_for_submitting_Ray_jobs"
---

In the VKE scenario, you can submit Ray jobs using RayCluster in the following ways. You can also refer to the [official documentation](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started.html) for more information:


1. Submitting via kubectl: You need to install the kubectl tool and configure the Kubernetes connection information.

2. Submitting using the Ray Client SDK (such as JobSubmissionClient): You need to deploy the Ray environment.


<span id="_1通过-kubectl-命令提交"></span>
## 1. **Submit via kubectl command**


1. Refer to [Connecting to a VKE cluster](https://www.volcengine.com/docs/6460/100919#%E6%AD%A5%E9%AA%A4%E4%BA%8C%EF%BC%9A%E8%BF%9E%E6%8E%A5%E9%9B%86%E7%BE%A4) to install kubectl and configure the VKE cluster connection information

2. Obtain the name of the pod where the Head of the RayCluster is located


```shell
export NAMESPACE=<命名空间>
APPNAME=<RayCluster应用名称>
HEAD_POD=$(kubectl get pods --selector=ray.io/node-type=head -o custom-columns=POD:metadata.name --no-headers  -n $NAMESPACE |grep $APPNAME) 

echo $HEAD_POD
```


In the example, NAMESPACE is the namespace in the VKE cluster where the RayCluster resides. APPNAME is the name of the RayCluster.


3. Connect to the Head pod to submit a Ray job and obtain resource information


```shell
# 打印集群资源信息
kubectl exec -it $HEAD_POD  -n $NAMESPACE -- python -c "import ray; ray.init(); print(ray.cluster_resources())"
```



4. Connect to the Head pod to submit a Ray job and execute the Python file


```shell
# 将本地python文件上传到head pod中
echo '
import ray
ray.init()
print(ray.cluster_resources())' > test.py
kubectl exec -it $HEAD_POD -n $NAMESPACE -c ray-head -- mkdir -p /home/ray/work_dir
kubectl cp  test.py -n $NAMESPACE -c ray-head $HEAD_POD:/home/ray/work_dir

# 执行python文件
kubectl exec -n $NAMESPACE -it $HEAD_POD -- ray job submit --working-dir /home/ray/work_dir  -- python /home/ray/work_dir/test.py
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e169270c5d10d515db1b9efaecc6befd.png) </span>


5. You can view the Ray execution status on the Ray Dashboard page, or use the following command to check the job execution status


```shell
kubectl exec -n $NAMESPACE -it $HEAD_POD -- ray job status <jobID>
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d309da27869c5631ffaca8c626d94fd3.png) </span>

<span id="采用ray-client-sdk（如jobsubmissionclient）提交"></span>
## Submitting using the Ray Client SDK (such as JobSubmissionClient)


1. Install the Ray environment. EMR provides [Ray image list](https://docs.byteplus.com/docs/E-MapReduce/109430), which allows you to deploy the Ray environment in Docker.

   When installing the Ray environment, the Ray version must be consistent with the version used by RayCluster.

2. Use the following command to obtain the IP address of the Head of the RayCluster, or manually obtain the Head's IP address:

   ```shell
   export NAMESPACE=<命名空间>
   APPNAME=<RayCluster应用名称>
   HEAD_POD=$(kubectl get pods --selector=ray.io/node-type=head -o custom-columns=POD:metadata.name --no-headers  -n $NAMESPACE |grep $APPNAME) 
   IP=$(kubectl describe pod $HEAD_POD -n $NAMESPACE |grep IP |awk '{print $2}' | head -1)
   ```
   


In the example, NAMESPACE and APPNAME need to be filled in according to the actual situation.


3. Enter the Ray environment and configure `export IP=<Head's IP address>`. Then run the Python command and use the interactive mode to execute the following Python code block

   ```python
   import ray
   import os
   
   head_ip = os.getenv("IP")
   ray.init(address="ray://{}:10001".format(head_ip))
   print(ray.cluster_resources())
   ```
   

   The IP address here is the Head's IP. Ensure that the execution environment can access the RayCluster. You can use the command `telnet $IP 10001` to confirm whether the network is connected.

4. Submit the following code block using JobSubmissionClient. You can also submit using the Ray CLI method.

   1. Create a directory and place the job script in this directory:

      ```python
      mkdir -p /tmp/ray_working_dir
      cd /tmp/ray_working_dir
      ```
      

   2. Write the Ray job script: ray_data_demo.py

      ```python
      import ray
      
      ds = ray.data.range(100)
      ds.show(limit=10)
      ```
      

   3. Define the SDK\-based job submission: job_submmiter.py

      ```python
      import os
      from ray.job_submission import JobSubmissionClient
      
      os.makedirs("/tmp/ray_working_dir", exist_ok=True)
      
      head_ip = os.getenv("IP")
      dashboard_url="http://{}:8265".format(head_ip)
      client = JobSubmissionClient(dashboard_url)
      job_id = client.submit_job(
          # Entrypoint shell command to execute
          entrypoint="python ray_data_demo.py",
          # Path to the local directory that contains the script.py file
          runtime_env={
              "working_dir": "/tmp/ray_working_dir",
          }
      )
      print(job_id)
      
      # Check status
      job_status = client.get_job_status(job_id)
      print(job_status)
      ```
      

   4. Run job_submmiter.py

      ```shell
      python job_submmiter.py
      ```
      

   After submitting the Ray job, a Job ID will be returned. You can use the following shell command to check the job status

   6. Check the task execution status

   ```python
   export RAY_ADDRESS=http://$IP:8265
   ray job status <jobID>
   ```
