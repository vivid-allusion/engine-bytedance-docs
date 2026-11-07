---
title: "Task Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Task_Management___"
---

The intelligent marking function relies on advanced AI large\-scale model technology to help you automate the marking process in the data processing process. By using this function, you can significantly reduce the workload of manual marking and effectively improve the accuracy of marking tasks. This function is widely applicable to a variety of business scenarios, such as analyzing social media data, mining hotspots, organizing user comment data, and listening to user voices. This article will introduce in detail how to start with the preparation work, step by step to complete the creation and operation of the intelligent marking task, and finally manage and optimize the final result, covering the entire process of the entire operation.

<span id="353285c7"></span>
# Preparation


* The intelligent marking data source comes from the dataset of the customer data platform CDP, so you need to build the dataset before building the intelligent marking task. See [Data Set ](https://www.volcengine.com/docs/6356/81302?lang=zh)for details.

* Add your AI large model to the intelligent marking function to provide the core capabilities of data analytics and marking for subsequent intelligent marking tasks. The specific operation is as follows:

   1. Enter the smart marking function.

   2. On the **Task Management** page, click **Model Management**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36944aae86f94ab0b286ae6a41acd74b~tplv-goo7wpa0wc-image.image) </span>

   3. In the upper right corner of the **Model Management** page, click **New Model** .

   4. Configure the large model parameters and save them.

      * **Basic information** : According to the actual situation, customize the version ID, name, whether it is enabled, whether it is public, and configure the model and access point you need to access. You can obtain a list of models and access point information from the connected AI platform.

      * **Default configuration** : Configure the Temperature, MaxToken, TopP, RateLimit of the model connection.

      * **Ability configuration** : Select whether to enable thinking mode, Multi\-modality model. If there is an extension configuration, it can be configured in JSON format.


<span id="5b32cbdc"></span>
# Create task


1. Log into the Customer Data Platform and select **Smart Marking** \> **Task Management** in the top menu bar.

   If the page width is insufficient, select **More** \> **Smart Marking** \> **Task Management** .

2. On the right side of the **Task Management** page, click **New Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d35c09842074b50b1d43d3f0ccbed77~tplv-goo7wpa0wc-image.image) </span>

3. On the **New Task** Flow page, complete the following configurations.

   1. Configure **basic information** and click **Next** .

      * **Task name** : Custom task name that identifies the current task.

      * **Task type** : Currently only supports selecting **offline marking tasks** .

      * **Task update method** :

         * **Manual update** : After the task is created, manually run the task to update the data.

         * **Timely update** : configure the update frequency and specific time, and the system regularly runs the task to update the data.

      * **Monitoring Configuration** : Supports configuring one or more monitors. After configuration, when a task fails or times out, the system will trigger an alarm in time to help you quickly detect and handle task abnormalities and avoid affecting the data processing progress.

   2. Configure the **profiling object** and click **Next** .

      * **Object type** : Currently only **datasets are supported** .

      * **Datasets** : From the list of CDP datasets, select the dataset that requires smart marking.

   3. Configure the **smart marking configuration** and click **Next** .

      * Intelligent marking comes with a wealth of AI applications to process marking data.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d05f760880743ba906534e0bad16d02~tplv-goo7wpa0wc-image.image) </span>

      * Click Advanced Settings in the upper right corner of the specified app card to perform the following actions:

         * Management prompt words: The system has provided prompt words by default. If you need to adjust them dynamically based on business, you can customize the editing and support AI help writing.

         * Data output configuration: including whether to allow the large model to expand the label, filter the emotion in the result, and whether the output result contains the marking reason field.

         * Debugging and preview: Support input field values to debug whether the running results of the AI application meet expectations.

      * To use **principal recognition** and **tag recognition** applications, you need to go to Create relevant tag libraries, see details [Manage Label Library](https://docs.byteplus.com/docs/dataagent/Manage_Label_Library).

      * **Custom applications** can flexibly set the following data for business processing.

         * Content to be analyzed: You can directly select fields from the input dataset as the analysis content, or you can refer to the marking results of other configured applications in this task as input to achieve multi\-step chain analysis.

         * Supports multi\-modal input and sets the URL of images or videos that have been stored in TOS.

         * Prompt words, support AI to help write.

         * Output field structure.

   4. Configure the **output table structure configuration** , and click **Next** .

      1. According to the selected application, set the fields to be output in the analysis results, and support adding fields from the dataset to merge into the output fields.

      2. Set the output result to save the object. Currently, only the specified dataset is supported.

   5. In the last step of **performance testing** , configure the test sample and perform the marking test. Click **Finish** when expected.

      The created tasks can be viewed in the task management list.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca30e722ae864bb1929e2490118cc9b3~tplv-goo7wpa0wc-image.image) </span>


<span id="2f79c0db"></span>
# View task results

In the task management list, you can view the running results and running records of the specified task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b89d753fb2df44d29efb4984010817e1~tplv-goo7wpa0wc-image.image) </span>


* At the top of the page, you can jump to view the data set information corresponding to the analysis object and the output result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e15344c59264a7fbe96b9db1eca09fb~tplv-goo7wpa0wc-image.image) </span>

* Support multiple selection of wrong results and import wrong question management.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65a6190aa5f94461bf47258a0c1a6fde~tplv-goo7wpa0wc-image.image) </span>

* On the **Run Log** tab, the following operations are supported:

   * Refresh the running record or run the task.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67d65a6413c84daebf69331897c32cae~tplv-goo7wpa0wc-image.image) </span>

   * In the Actions column, it is supported to rerun the task, view the current running view, or log.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/663b30d05f6b4416adb823d1d431a345~tplv-goo7wpa0wc-image.image) </span>


<span id="1948e082"></span>
# Management Wrong Questions and Prompt Word Tuning

In the task management list, you can view the wrong question and prompt word tuning configuration for a given task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d11a26398c04ef7848548525c0d63c3~tplv-goo7wpa0wc-image.image) </span>


* In the **wrong question management** page tab, support adding wrong questions. When entering the wrong question, you need to fill in the wrong field, the unique identification of the output result and the correct content. The system will intelligently optimize the prompt word according to the wrong question information you enter.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2fd14d592244da8be44e3e1f9328307~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b46de7b25f94e0e98b488552e9c1e53~tplv-goo7wpa0wc-image.image) </span>

* In the **prompt word version** tab, you can query the optimized version of the prompt word for different AI applications. The default prompt word is V1 version, and the version number will be + 1 for each optimization.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/265ff81c094d414788fd4084c6bc79bf~tplv-goo7wpa0wc-image.image) </span>


<span id="558f989e"></span>
# Edit or delete tasks

In the action column of the task management list, editing or deleting the specified task is supported.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once the task is deleted, it cannot be restored. Please proceed with caution.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cee5ee10c7604bc6b6370a990bfcc7e0~tplv-goo7wpa0wc-image.image) </span>
