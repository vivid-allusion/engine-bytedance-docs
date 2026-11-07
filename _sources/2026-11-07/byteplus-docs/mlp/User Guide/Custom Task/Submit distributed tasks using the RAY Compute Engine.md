---
title: "Submit distributed tasks using the RAY Compute Engine"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Submit_distributed_tasks_using_the_RAY_Compute_Engine"
---

Ray On MLP is a new distributed computing engine option available on the BytePlus Machine Learning Platform. With this powerful engine, algorithm engineers can easily perform large\-scale data processing and distributed model training with Python and Ray AI Runtime. BytePlus Machine Learning Platform (MLP) focuses on providing end\-to\-end machine learning services to help customers build reliable and efficient machine learning processes. Now we take it a step further and integrate the Ray framework [(ray.io) ](https://www.ray.io/)with the custom tasks module to help you easily create and run Ray jobs, enabling flexible scheduling of jobs and on\-demand execution.

When using Ray On MLP, you don't need to make any code changes or adjust any resources. You can simply use a pre\-configured Ray image or a custom image that carries a Ray Runtime to run a Ray job with one click. You can also connect to your Ray engine through the Dev boxes module in MLP for related task development and debugging. Ray On MLP Preview is now available in all regions, which means you can take advantage of this powerful distributed computing engine on a global scale to easily address distributed challenges in different geographies and scenarios.

<span id="功能限制"></span>
# functional limitations


1. Task diagnostics are not supported, but automatic retries are supported.

2. Countdown display is not supported in the instance retention time function.

3. Enabling the Metrics feature in Ray Dashboard requires users to interface with their own Grafana.


<span id="页面交互"></span>
# page interaction

<span id="创建-ray-集群"></span>
## Create a Ray cluster


1. Click "custom tasks" to enter the list page, and click "create custom tasks".

2. Configure the tasks in turn, and the image needs to select to ensure that there are Ray\-related binary files and meet the version requirements (2.2.0~ 2.32.0)

3. Select the Ray frame and select the corresponding model. You can fill in the RuntimeEnv for the running environment your driver needs, and mount the corresponding storage according to the job requirements.

   1. **Note: The** current version does not support task diagnostics and fault tolerance.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac95f2ceb27c408ca944da625a331d0a~tplv-goo7wpa0wc-image.image) </span>


4. Once created, you can view the corresponding Ray task in the console and view the required information


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d496b20e3764003969b3350af6aa745~tplv-goo7wpa0wc-image.image) </span>

<span id="访问-ray-dashboard"></span>
## Visit Ray Dashboard

<span id="方式一：通过-dashboard-入口直接访问"></span>
### Method 1: Direct access through the DashBoard entrance


1. Enter the task details page, the basic information module provides Ray DashBoard public/private network access portal.

2. Click on the corresponding "Public Network"/"Private Network" to enter the "Dashboard" according to your access needs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>How to choose public network/private network access:</strong> When the queue resource group to which the task belongs and its configured VPC has public network access enabled in [global configuration], the task can access the Ray Dashboard through the public network; otherwise, it only supports access through the private network.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93c996cd82394d5e95789d2a92d4c6a5~tplv-goo7wpa0wc-image.image) </span>

<span id="方式二：通过-dashboard-的-port-信息访问"></span>
### Method 2: Access to port information through Dashboard


1. On the task details page, select Live Log to view the port information that Ray Dashboard accessed.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b7c614efd6867f9540ec2a821ed5728.png) </span>


2. Switch back to the "Overview Information" page, select "Head Instance", click "WebIDE", open "New Terminal", and switch to "Ports".

3. Enter the port you just viewed on the log page, the example here is "8265", and click "Local Address" to access "Ray Dashboard".


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d07ffc84cd40ec3971d47d8ad291a506.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d370e5ba5fdf5bdbf98cfae6916ba650.png) </span>

<span id="访问日志-监控"></span>
## Access log/monitoring


1. You can view the full log and related monitoring through the "Log" portal provided by the platform. You can view relevant logs and monitoring information based on the "Ray Dashboard" in the previous step.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f42a28649e246999f5a9e2776d9f8a4~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eae457e4de30442eaaef223b3b3cc8fc~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef8507995674428c9afc889224f6130c~tplv-goo7wpa0wc-image.image) </span>

<span id="容错能力"></span>
## fault tolerance

The worker instances created by Ray are fault tolerant. When a worker encounters a failure, it can recover and rejoin the cluster in minutes.
