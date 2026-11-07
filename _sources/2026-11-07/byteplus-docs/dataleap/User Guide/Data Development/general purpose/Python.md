---
title: "Python"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/python"
---

Python tasks suit scenarios with small data volumes and simple logic, supporting Python 3.7 for development business needs.

<span id="84d56150"></span>
## 1 Usage restrictions


* When a sub\-user logs in to create a task, if they manually select the network environment, they must have either the VPCReadOnlyAccess or VPCFullAccess permission policy for the private network. A sub\-user can ask the primary account to add the corresponding permission policy to [Access Control](https://console.byteplus.com/iam/identitymanage/user). For details, see [Access Control](https://docs.byteplus.com/en/docs/vpc/IAM-Overview).

* When configuring upstream dependencies for Python tasks, the **dependency recommendation** feature in scheduling properties is not supported. Upstream dependencies can only be added manually using **manual addition**. For details, see [Task scheduling depends on](https://docs.byteplus.com/docs/dataleap/scheduling_dependencies).


<span id="_2-前提条件"></span>
## **2 prerequisite**


* DataLeap service activated, see [DataLeap service activation](https://docs.byteplus.com/docs/undefined/689b492cf611e0051a33f318).

* When Python tasks access private network services or resources, they must use an **exclusive computing resource group**. The Python task interface does not support modifying network settings separately.


<span id="_3-1-创建任务"></span>
## **3 create task**


1. Log in to the [DataLeap tenant console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/overview?), enter the project’s **IDE development** interface, and **create a task**.

2. Click the **New Task** button, then choose **Data Development \> Generic \> Python** as the task type.

3. Fill in the basic task info by entering the task name, for example: python_task, and select the target folder to save the task. Click the **Confirm** button to complete task creation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Task name information allows characters: periods, letters, numbers, underscores, hyphens, [], 【】, （）, (), and Chinese characters, and must be within 127 characters.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40918c2be9ab40a4a85e99b618e8219f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-编辑使用"></span>
## **4 edit task**

After the task is created successfully, enter the code development and editing interface.

<span id="_3-2-1-开发代码编辑"></span>
### 4.1 develop code editing


1. Supported languages: Python, as shown below:

   ```python
   print ("Hello, Python!")
   ```
   

2. Parameters: time parameters like ${date}, ${hour} are supported; refer to more parameters at:[Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252)

   ```python
   print ('${date}')
   ```
   

3. Example of installing third\-party dependencies using command line:

   ```Python
   import os
   os.system('pip install numpy(Replace the required third-party package name) -i https://pypi.tuna.tsinghua.edu.cn/simple')
   ```
   

   See [Using third-party dependency packages in Python tasks](https://docs.byteplus.com/docs/dataleap/using_third-party_dependency_packages_in_python_tasks) more installation methods for details.


<span id="_3-2-2-资源设置"></span>
### 4.2 resource settings


1. Dependency packages: third\-party packages referenced in the code; manually input third\-party package dependencies here. To specify a specific version, add it in the format "plcga==1.6"; use semicolons to separate multiple dependencies.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When configuring dependency packages, it is recommended to include the corresponding package version to ensure consistent runtime environments.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is not recommended to add configurations for packages not required in the code.   </div>
   

2. Environment variables: when setting system environment variables in Python scripts, avoid overwriting system variables directly. Append variables using the format PATH=$PATH:/usr/local/bin/python; separate multiple variables with semicolons.


<span id="_3-2-3-网络配置（可选）"></span>
### 4.3 network configuration (optional)

When a task accesses public network, private network (VPC) resources, or image repository addresses with network access restrictions in the script, you need to configure the network by selecting a private network, subnet, and security group information that can communicate with your resources.

There are two methods:


* You can manually select the private network (VPC), subnet, security group, and other network information where the task resources and data sources reside.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a sub\-account logs in to create a task, selecting the network environment requires relevant service permissions. At this point, the primary account needs to add the <strong>VPCReadOnlyAccess</strong> or <strong>VPCFullAccess</strong> permission to the sub\-user in <a href="https://console.byteplus.com/iam/identitymanage/user">IAM Control</a>. See <a href="https://docs.byteplus.com/en/docs/vpc/IAM-Overview">IAM Overview</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f488bd0472854595aca827126ab7864d~tplv-goo7wpa0wc-image.image) </span>

* Alternatively, when the project is bound to an **exclusive computing resource group**, you can use the [exclusive computing resource group](https://www.volcengine.com/docs/6260/71656) to access resources and services in the private network, enabling network communication.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fef5503c69b24d84be70e500634d662b~tplv-goo7wpa0wc-image.image) </span>

   You can [enable public network](https://docs.byteplus.com/en/docs/natgateway/Internet-NAT-Gateway-Getting-Started) access for the VPC where the exclusive computing resource group is located, or ensure its VPC information matches the VPC information of your resources. If they differ, you can use [CEN](https://docs.byteplus.com/en/docs/cen/Getting-Started-Overview) to connect the networks.

   After selecting an **exclusive computing resource group**, all network configuration information here comes from the exclusive computing resource group. Direct modification in the network configuration interface is not supported. You can configure the corresponding private network information when creating the exclusive computing resource group. See details [Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group).


<span id="_3-2-4-任务产出数据登记"></span>
### 4.4 Register the data produced by the task

Registering produced data records the task's data lineage and does not affect code logic. If the Shell task outputs data from engine library tables, it is strongly recommended to fill this in to facilitate future maintenance of the task's data lineage.


1. Engine type: Select the type of data engine of the output based on actual conditions, such as EMR (EMR Hadoop, EMR Doris, EMR StarRocks engines), ByteHouse, EMR Serverless Spark, EMR Serverless StarRocks, Default (no output registration), etc.

2. Associated instance: select instance information under the corresponding engine.

3. Data type: select the output data type under the corresponding engine type.

4. Database table: select the detailed name of the database and table output under the corresponding engine.


<span id="_3-2-5-执行设置"></span>
### 4.5 Execution settings


1. Click to open the **Execution settings** window on the right sidebar.

2. Select computing resource group: supports selecting common computing resource groups, [Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group).

3. Image address:

   Supports custom images. It is recommended to use BytePlus image repository, dataleap\-{region}.cr.bytepluses.com/studio/spark:online, where the {region} value should be replaced with the actual region, such as johor\-ap\-southeast\-1.

   Complete example: Beijing region: dataleap\-johor\-ap\-southeast\-1.cr.bytepluses.com/studio/spark:online

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The DataLeap common computing resource group cannot access the public network. If the image repository address you provide (such as a third\-party image repository) requires access through the public network or a specified private network (VPC), configure network connectivity via the <strong>Network configuration</strong> above. Try the following solutions:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enable <strong>public network</strong> access for both your image repository address and the VPC you configured;   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The VPC where your image repository is located must match the VPC you configured, or they must be connected through <a href="https://docs.byteplus.com/en/docs/cen/Getting-Started-Overview">CEN</a>.   </div>
   

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">See details <a href="https://docs.byteplus.com/docs/dataleap/python#_3-2-3-%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE%EF%BC%88%E5%8F%AF%E9%80%89%EF%BC%89">4.3 network configuration (optional)</a>.      </div>
      

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Python 3 must be installed in custom images for proper functionality.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The basic image address includes only the most fundamental Linux and Python commands. In simple scenarios, you can use the basic image address and add some dependencies as needed.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To check dependencies included in the basic image, follow these steps:   </div>
   

         1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Create a Python task;   </div>
   

         2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Execute the following script;   </div>
   

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">         ```Python
         import os
         os.system("pip freeze")
         ```
                  </div>
         

         3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After execution, check the log to see the included dependencies.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Basic image address: dataleap\-{region}.cr.bytepluses.com/studio/runtime_light:online, where the value of {region} should be replaced with the specific region information based on the actual situation, such as johor\-ap\-southeast\-1.   </div>
   

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Complete example: dataleap\-johor\-ap\-southeast\-1.cr.bytepluses.com/studio/runtime_light:online      </div>
      

   4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your customized image files contain encrypted files and you want the image file to be accessible only by fixed tasks, you can create a private image type and add the <strong>image repository address, username</strong> and <strong>password</strong> along with other private image configuration information to the <strong>exclusive computing resource group</strong>. Access the image file through the <strong>exclusive computing resource group</strong>. For the operation of modifying resource group image configuration, see <a href="https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group">Exclusive Computing Resource Group Management</a>.   </div>
   

   5. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to manually fill in the specific image version's network address information in the OCI artifac<strong>network address information in the OCI artifact repository</strong> for the private image address. The actual filled image address shall prevail. If omitted, the system will access the default basic image address.   </div>
   

4. Resource configuration: resources can be configured according to actual needs, measured in CUs, with the default set to 1CU (1CU = 1 Core 4GB). More resource specifications are available in the dropdown menu.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The 0.25CU and 0.5CU specifications are selectable only by the exclusive computing resource group.   </div>
   

5. Resource selection:

   Python tasks support using **generic resources** in task editing by accessing resources like Jar, File, and Zip to improve data development efficiency.

   Select the resources required for the task from the **resource selection** dropdown. If no resources are created yet, click the **new resource** button to create one in the resources library. See [Resources Library](https://docs.byteplus.com/docs/undefined/682aa9fee638492ec7c94266) for details on creating resources.


<span id="_3-2-6-调度设置"></span>
## 5 schedule settings

Go to the right sidebar **schedule settings** and configure node scheduling properties. See [scheduling settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings) for setup details.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Python task upstream dependency settings do not support the <strong>dependency recommendation</strong> feature and can only add upstream dependencies through <strong>manual addition</strong>.</div>


<span id="_3-3-保存任务"></span>
## 6 save and debug task

After configuration, click the **save** and **debug** icons in the top action bar to execute the edited Python command. After successful execution, view running logs and results at the bottom of the interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Debug operation: Directly use production data for debugging. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Debug log data in the Data Development interface is retained for 15 days, during which you can view the details of the debug logs.</div>


* <div data-tips="true" data-tips-type="warning">This task type supports sending message notifications after a task debug run succeeds or fails. You can go to <strong>Project Console \> Configuration \> Message notification settings</strong> to choose whether to enable <strong>Task debug run successful</strong> or <strong>failed</strong> notifications, based on your business needs. The default notification method is email. You need to link the appropriate <strong>Security Email</strong> in advance in the Account Management section.</div>



<span id="_3-5-提交发布任务"></span>
## 7 submit release task

After configuring the required parameters and successfully debugging the task, submit the task for release to execute it in the Operations Center batch task maintenance.

Click the **Save** and **Commit for Deploy** buttons in the action bar above. In the **Commit for Deploy** dialog, select parameters such as **backfill data, monitor settings, commit settings**. Finally, click the **Confirm** button to complete the job submission. See deploy instructions for details: [4.1 Submit Batch Task](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-1-%E7%A6%BB%E7%BA%BF%E4%BB%BB%E5%8A%A1%E6%8F%90%E4%BA%A4).

See batch task maintenance for follow\-up operations: [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).
