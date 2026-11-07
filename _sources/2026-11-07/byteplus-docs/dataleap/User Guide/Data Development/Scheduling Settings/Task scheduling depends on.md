---
title: "Task scheduling depends on"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/scheduling_dependencies"
---

DataLeap task scheduling depends on different tasks, forming upstream and downstream dependency relationships through configuration operations. You can configure the upstream and downstream dependencies of tasks according to the actual business logic required to complete the data lineage construction. After the upstream tasks are executed and produce data, the downstream tasks will start executing to ensure that the downstream tasks can normally obtain the data produced upstream, ensuring data quality and improving data development efficiency. This article will introduce the configuration description of scheduling dependencies.

<span id="90da0b79"></span>
## 1 Usage Restrictions

Currently, only task types such as EMR Serverless Spark SQL, ByteHouse CE SQL, and ByteHouse CDW SQL support the automatic recommendation of upstream task information needed for setting dependencies based on SQL logic.

<span id="e72be6ce"></span>
## 2 Dependency Considerations

After configuring the upstream and downstream node dependencies, the downstream task must meet the following conditions before it can continue:


1. All upstream nodes on which it depends have been executed and are not in a failed state;

2. It has reached the scheduling execution time set in the scheduling attributes of the downstream task. If the set execution time has been reached but the upstream has not completed, the downstream will not start.

3. Once all upstream tasks are completed and the current time has reached the downstream's set execution time, sufficient scheduling resources must be available to commence the downstream task.


<span id="_2-功能入口"></span>
## **3 Dependency Configuration Entry**


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In the **Overview** interface, the projects you joined are displayed. Click on **IDE development** to enter the corresponding project.

3. In the **Data Development** interface, in the left navigation bar, double\-click to open a batch task and enter the node editing interface.

4. Click the **Schedule** button on the right\-side navigation bar, and find the **Dependencies** section to configure.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c9fb9268e8d4a238dc4fc3412b50f08~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-1-任务上游依赖设置"></span>
## 4 **Upstream Dependency Settings**

Establishing task dependencies complete the construction of data lineage. Generally, when a task is executed successfully, the data table partition is ready.

Upstream dependencies can be set through **Dependency Recommendations** or **manually adding**.

<span id="50209991"></span>
### 4.1 **Dependency Recommendations**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a72d7439aff46758176be2b93314af0~tplv-goo7wpa0wc-image.image) </span>

EMR Serverless Spark SQL, EMR StarRocks SQL, ByteHouse CE SQL, and ByteHouse CDW SQL tasks can automatically recommend the information of upstream tasks required based on SQL logic.

Click the **Dependency Advice** button:


* If the referenced table name you need to depend on already has a corresponding output task, you can directly select the task you need from the recommended task list returned in the pop\-up.

* If the referenced table name you need is not found to have a corresponding output task, you can perform the following operations:

   * Check if the SQL code logic of the current task complies with the requirements.

   * Apart from the upstream of some data integration tasks, for other types of tasks, you also need to confirm that the upstream dependent tasks have configured the specific output database table information of the tasks in the "Register the data produced by the task"; if the upstream tasks cannot configure the "Register the data produced by the task", you can manually add the dependency relationship through the "Add Manual" method.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Some target data sources for data integration tasks have the capability of automatic output registration. The specific data sources that support automatic output registration are as follows:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When the job type is script mode (DSL) and the target data source is Hive, ByteHouse CDW, or ByteHouse CE, automatic output registration is supported;      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When the job type is visualization mode and the target data source is Hive, ByteHouse CDW, ByteHouse CE, or HDFS, automatic output registration is supported.      </div>
      

   * If parts of the SQL code being edited have SQL parsing exceptions, such as tasks using **Schedule Settings \> Input parameters** with **Project parameters** type and the parameter settings checked for **encryption**, non **Project Administrators** during task parsing will be unable to parse those encrypted parameters. When clicking on **Dependency Recommendations**, the system will notify you that the recommended task is incomplete or exceptional, requiring you to **add manually** the dependencies.

      At this moment, you can click the "**add manually**" button to manually search and operate the task dependencies. See details below [4.2 Add Manual](https://docs.byteplus.com/docs/dataleap/scheduling_dependencies#375a5b96).


<span id="375a5b96"></span>
### 4.2 Add **Manual**

The Dependency Recommendations function can significantly reduce the workload in task dependency configuration, but it has its limitations. If the task returned by Dependency Recommendations lacks some data update tasks for tables currently used by your task, you can also use the **manual addition** mode to manually adjust the dependencies.


1. Click the **add manually** button, on the dependency task search page, search by Task name, Task ID, table, or HDFS path, and add the needed upstream dependencies.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Tasks that have been closed in the Operations Center are not supported for addition as upstream dependencies.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Quasi\-real\-time tasks can only depend on tasks of the same quasi\-real\-time frequency, and cannot depend on tasks with a minute\-level frequency or higher. Therefore, you must pay special attention to whether there is an upstream and downstream dependency relationship in the current task when switching between quasi\-real\-time and other execution frequencies, which will clear the dependencies of the current task.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c318d69878a842aea3d7aafd8576db4c~tplv-goo7wpa0wc-image.image) </span>

2. After selecting the dependent tasks, click the **OK** button to complete adding the dependencies manually.


<span id="7b07ce0e"></span>
## 5 Dependency Configuration Methods

After finding the corresponding upstream tasks and adding dependencies, you can proceed with the subsequent **Dependency Configuration Methods** settings, which support **Specifying Offset** and **Nearest Dependence** methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are default dependency configuration methods used by the project, and when creating a project, you can specify the default configuration method for task dependency as <strong>Specified Offset</strong> or <strong>Nearest Dependence</strong>. See details <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a>.</div>


<span id="b85898e3"></span>
### 5.1 Specify Offset

When the offset in tasks dependent on different scheduling frequencies or scheduled dates varies, manual setting of the offset is required.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When specifying the offset configuration method, the system defaults to filling in the offset parameters. However, the default offset settings are only suitable for typical cases. If the default values are unsuitable for the current task scenario, you may manually adjust the offset parameters.</div>



1. Choose from the **Configuration method dropdown:** Specify Offset;

2. Choose **Set** or **Interval** as the offset form to set the dependency offset parameter. The dependency implementation mechanism varies for upstream and downstream tasks with different frequencies, which are specifically divided into the following three main categories:

   
   |Upstream and downstream frequency types |Dependency implementation mechanism |Instance cases |Offset setting examples (interval/set, offset, offset units) |
   |---|---|---|---|
   |Same frequency dependence |Current task instance business time + Offset \* Offset unit = Business time of the upstream task instance. |* Daily task depends on daily task, dependent on the instance executed on the same day by the upstream task<br><br>* Daily task depends on daily task, dependent on the instance executed the previous day by the upstream task |* Set: 0 Days<br><br>* Set: \-1 Days |
   |High frequency dependent on low frequency |Current task instance business time + Offset \* Offset unit + Business time compensation value = Business time of the upstream task instance<br><br>PS: service time compensation value = (same execution time, low frequency task instance corresponding to business time) \- (same execution time, high frequency task instance corresponding to service time);<br><br>Example: When a daily task is dependent on an hourly task, business time compensation value = 23 hours. |Daily task depends on hourly task, depending on the 24\-hour instances executed by the upstream task yesterday |Interval: \-23,0 hours |
   |Low frequency dependent on high frequency |Depends on all instances executed by upstream tasks within the time range "Current task instance business time \- Offset \* Offset unit ~ Current task instance business time";<br><br>PS: The above time range is left\-open and right\-closed. |Hourly tasks depend on daily tasks, relying on instances executed within the last 2 days. |Set: \-1,0 days |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Description for different frequency upstream tasks with corresponding offset units:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Monthly task: Offset unit = Month, representing 1 month; Offset unit = Day, representing 1 day.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Weekly task: Offset unit = Week(s), representing 1 week; Offset unit = Day, representing 1 day.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Daily task: Offset unit = Day, representing 1 day.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Hourly task: Offset unit = Hour, representing 1 hour.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By Minute task: Offset unit = Minute, representing 5 minutes; (Currently, the minimum frequency for tasks by minute is: Execute every 5 minutes).   </div>
   

3. After the offset parameters are set, you can click the **Dependency preview** button to view the instance dependencies under the specified business dates of upstream and downstream tasks according to the current dependency settings, and select the specified business time based on the actual situation to conveniently verify whether the offset settings meet expectations.


<span id="da78ebe1"></span>
### 5.2 Nearest Dependence

When selecting **Nearest dependence** from the Configuration method dropdown, no further offset parameters need to be configured, as downstream instances will follow the principle of Nearest when searching for upstream instance dependencies, which means depending on the upstream instance closest to (or earlier than) its scheduled execution time.

<span id="45a7c7eb"></span>
#### 5.2.1 Same Frequency Dependence

Same frequency dependence refers to operations occurring at the same frequency:


* The number of instances in the upstream and downstream cycles is equal: the instances in the upstream and downstream cycles correspond one\-to\-one and directly depend on each other.

   
   |Scenario |Task Description |Dependency Diagram |
   |---|---|---|
   |Hour B is dependent on Hour A |Hourly tasks A/B generate 24 instances each day, with the upstream and downstream instance numbers being consistent, and the first instance is scheduled at 0:30 |Upstream and downstream instances A/B correspond one\-to\-one.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e362c8d6913046b98dc6b6b5390cf044~tplv-goo7wpa0wc-image.image) </span> |
   ||Hourly tasks A/B generate 4 instances a day, with consistent numbers of upstream and downstream instances:<br><br><br>* Task A's first instance is scheduled at 0:00<br><br>* Task B's first instance is scheduled at 4:59 |Upstream and downstream instances A/B correspond sequentially according to the order of instance creation.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1dbb476f03d496d83f944b50fb41ed5~tplv-goo7wpa0wc-image.image) </span> |
   

* The number of instances in the upstream and downstream cycles is unequal: it depends on the nearest instance on the left side of the upstream; if there is none, then it depends on the far left instance (the first instance of the upstream task).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The definition of left\-side instances: For instance A with a scheduled execution time of x, any upstream instance that is scheduled earlier than x is referred to as a left\-side instance of A.   </div>
   

   
   |Scene |Task Description |Dependency Diagram |
   |---|---|---|
   |Hour B depends on Hour A |* Hourly task A generates 4 instances, scheduled at: 4:00, 8:00, 12:00, 16:00<br><br>* Hourly task B generates 8 instances, scheduled at: 0:00, 3:00, 6:00, 9:00, 12:00, 15:00, 18:00, 21:00 |Instance B relies on the nearest Instance A in terms of scheduled times, either concurrent or prior to Instance B's scheduled execution time.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8f7977788fc459c8492d3974feb6719~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="d7a5f9f4"></span>
#### 5.2.2 Dependency with different frequencies upstream and downstream

Depend on the nearest instance on the left side of the upstream; if there is none, then depend on the far left instance (the first instance of the upstream task).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Definition of an upstream instance: If the scheduled execution time of Instance A is x, an upstream instance with a scheduled time earlier than x is referred to as a left\-hand instance of A.</div>



* High frequency dependent on low frequency

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a high\-frequency task depends on all low\-frequency instances before the current scheduled time, enable the <strong>Cross\-cycle Dependencies</strong> option for hours tasks. For example, a daily task instance scheduled at 3:00 requires dependencies on all hourly instances scheduled before 3:00; hence, you need to enable <strong>Cross\-cycle Dependencies</strong> for hourly tasks. See details <a href="https://docs.byteplus.com/docs/dataleap/scheduling_dependencies#30453928">Task Self\-Dependency Settings</a>.   </div>
   

   
   |Scene |Task Description |Dependency Schematic |
   |---|---|---|
   |The daily task B depends on the hourly task A |* Hourly task A generates 24 instances, with the first instance at 00:00<br><br>* Daily task B generates one instance, scheduled for 3:00 |Instance B depends on the nearest instance A, dependent on the upstream instance A closest in time to the scheduled execution time of instance B (equal to or earlier than the scheduled time of instance B), i.e., the 3:00 daily instance depends on the 3:00 hourly instance, with other hourly instances A having no downstream dependencies.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0886697fcad9482d952ab669afa86617~tplv-goo7wpa0wc-image.image) </span> |
   |Hourly task B depends on minute task A |* Minute task A, with a 15\-minute frequency, starts at 0:00 and generates a total of 96 instances<br><br>* Hourly task B generates 6 instances, with scheduled times at: 00:00, 4:00, 8:00, 12:00, 16:00, 20:00 |The daily task relies on the hourly task to be consistent, and Nearest dependence relies only on the upstream instance A that is closest to (or earlier than) the scheduled execution time of instance B<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4edecac606f74f59b661762c6272101f~tplv-goo7wpa0wc-image.image) </span> |
   

* Low frequency dependent on high frequency

   
   |Scenario |Task Description |Dependency Diagram |
   |---|---|---|
   |Hourly task B depends on daily task A |* Daily task A generates one instance, with the first instance at 3:00<br><br>* Hourly task B generates 24 instances, with scheduled times at 0:00 |Instance B relies on Nearest to instance A, since upstream only generates a 3:00 daily instance, all downstream hourly instances will depend on this single upstream instance<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13ea849e4eb04785ae35f65e4404a8d2~tplv-goo7wpa0wc-image.image) </span> |
   |Minute task B depends on hourly task A |* Hourly task A generates 6 instances, with scheduled times at: 0:07, 4:07, 8:07, 12:07, 16:07, 20:07<br><br>* 15\-minute task B, with a frequency of every 15 minutes, starting at 0:05 and generating a total of 96 instances |Instance B depends on the nearest upstream Instance A, which is the closest (equal to or earlier than) to the scheduled execution time of Instance B.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae196fb00c6e4589bf4293581c65bca6~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="17dde504"></span>
#### 5.2.3 Dependency Preview

After setting up Nearest dependence, you can click **Dependency Preview** button to view the instance dependencies of upstream and downstream tasks for the specified business date, based on the current Nearest dependent settings, and choose the actual situation to confirm whether the dependency settings meet the expectations timely.

<span id="30453928"></span>
## **6 Task Self\-Dependency Settings**

If the task needs to depend on the output of its own previous cycle, you can use the Self\-dependent Settings.

Cross\-cycle Dependencies only support the setting of dependencies on oneself across cycles. If the task requires dependence on its own data output from the previous cycle, such as today's task execution depending on yesterday's results of the current task, you can **choose Cross\-cycle Dependencies** set to **Yes**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96d089025cdd4aea951e145fcb3c2e47~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When cross\-cycle dependencies are enabled, you need to set "Earliest backfill time" in <strong>Scheduling attribute</strong>, so that the instance corresponding to the earliest backfill time does not check the operation of the previous scheduling period and can start directly from the instance of the earliest backfill time.</div>


<span id="bf22337e"></span>
## 7 Subsequent Operations

After configuring the task scheduling dependencies, if your upstream and downstream tasks involve scenarios with input and output parameter transfer, you can continue to configure **Input and Output Parameters**. See details [Input and Output Parameter Settings](https://docs.byteplus.com/docs/dataleap/input_and_output_parameter_settings).
