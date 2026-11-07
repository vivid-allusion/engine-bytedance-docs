---
title: "Task Template"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/task_template"
---

The task template function provides a convenient way to create project\-level task templates for managing common task logic standards, thereby reducing the maintenance cost of commonly used code. You can quickly reference ready\-made task templates. By modifying a few parameters, you can reuse the core data processing logic, reduce repetitive code development, and enhance development efficiency. This document will introduce the operating instructions for task templates.

<span id="_3-新建任务模板"></span>
## 1 Create New Task Template


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc) **.** 

2. In the **Overview** interface, displayed joined projects, click on **IDE Development** to enter the corresponding project.

3. In the **Data Development** interface, click on **List of templates** in the left navigation bar to enter the **Task Template** interface.

4. In the **More** button on the right side of the template list, create a new subdirectory or a new task template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd568ef6dd934c509d837349571f0355~tplv-goo7wpa0wc-image.image) </span>

5. In the window for creating a new task template, enter the following parameters to create a template:

   
   |Parameters |Description |
   |---|---|
   |Template name |Input template name information. Only periods (.), letters, numbers, underscores, [],【】,（）, (), and Chinese characters are supported, cannot exceed 200 characters. |
   |Template description |Enter the description information for this task template for ease of subsequent management and use. |
   |Directory |Select the file path where the task template will be stored. |
   |Supported task types |Select the corresponding task type for the task template. Currently, only Shell tasks are supported. |
   

6. After configuring the parameters, click the **OK** button to complete the creation of the new task template.


<span id="_4-模板列表管理"></span>
## 2 List of Templates Management

<span id="_4-1-任务模板筛选"></span>
### 2.1 Task Template Filtering

In the task template directory tree, the following filtering methods are supported:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3693be91bd244f3bcfe22d3be56426a~tplv-goo7wpa0wc-image.image) </span>


1. Select the "**Mine**" button to filter out task templates created by the current account under the project.

2. You can enter task template name information in the text box for fuzzy search.

3. Click the **collapse** button, and the filtering box on the right will appear, where you can filter by **task type, template owner** via multiple selections; you can also click the **Reset** button to clear all filters and display all task templates.


<span id="_4-2-子目录文件夹管理"></span>
### 2.2 Subdirectory Folder Management

You can click the **More** button to the right of the folder name. You can **create a new subdirectory, create a new task template, move the folder position, delete the folder, rename the folder** and other actions under the folder.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Delete subdirectory folders, confirm whether there are still subnodes under the current folder, clear the subnodes first, then proceed with the deletion.</div>


<span id="_4-3-任务模板管理"></span>
### 2.3 Task Template Management

You can click the **More** button to the right of the task template name to perform actions such as **rename, move to another folder directory, delete, copy** and other operations on the task template.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Delete the task template, confirm whether the current template is referenced by online tasks; if references exist, deletion fails and a pop\-up reminder appears. You must first remove the online task references before continuing with the deletion.</div>



* When you hover over the name of the task template, it will display detailed information such as the template name, creator, creation time, and more. You can also directly reference the current task template on the detailed information interface; see details [6 Reference task mode](https://docs.byteplus.com/docs/dataleap/69494#1).


<span id="_5-编辑任务模板"></span>
## 3 Edit Task Template

Click on the task template name to open the template editor, where you can enter generic code logic or select generic parameter information.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When updating an existing task template, confirm whether the updates affect the referenced tasks, and view the template version referenced in <strong>Reference records</strong> on the right. Update the task template cautiously.</div>


<span id="_5-4-shell"></span>
### 3.1 Shell Template


1. In the code development and editing interface of the task template, write a generic Shell script, with a simple script example as follows:

   ```shell
   #! /bin/bash
   function commonFunction() {
    ARGS=`getopt -a -o u:p: -l yarn_cluster:,yarn_queue:, -- "$@"`
    if [ $? != 0 ];
        then echo "Terminating"
        exit 1
    fi
    eval set -- "${ARGS}"
    while true; do
            case "$1" in
                -u|--yarn_cluster)
                    yarn_cluster="$2"
                    shift
                    ;;
                -p|--yarn_queue)
                    yarn_queue="$2"
                    shift
                    ;;
                --)
                    shift
                    break
                    ;;
                
            esac
        shift
    done
   
    echo ${yarn_cluster}
    echo ${yarn_queue}
   }
   
   commonFunction
   ```
   

2. Image Address:

   Supported custom images are recommended, suggest using BytePlus [Container Registry](https://www.byteplus.com/en/product/cr), with the following example fill\-in:

   * Johor location: dataleap\-johor\-ap\-southeast\-1.cr.bytepluses.com/studio/spark:online

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Custom image must install Python3 to function properly.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Basic image address only contains the most basic Linux and Python commands; for simple scenarios, you can also base on the basic image address and supplement some dependencies.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Basic image address: dataleap\-johor\-ap\-southeast\-1.cr.bytepluses.com/studio/runtime_light:online   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your custom image file contains files that need to be encrypted and you want this image file to be accessible only to fixed tasks, you can create a private image type and add the <strong>image repository address, username</strong> and <strong>password</strong> and other private image configuration information to the <strong>exclusive computing resource group</strong>, accessing the image file through the <strong>exclusive computing resource group</strong>. See details for modifying the resource group image configuration operation in <a href="https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group">Exclusive Computing Resource Group Management</a> the description.   </div>
   

   4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to manually fill in the specific image version corresponding <strong>network address</strong> information in the <strong>OCI artifact repository</strong> for the private image address. If omitted, the default basic image address will be accessed.   </div>
   

3. Parameter Settings

   You can operate below to **Add Parameter Group**:

   * Parameter group name: Enter the parameter group name; multiple parameter names are allowed under one parameter group name.

      1. New parameter: Add multiple parameter configurations under the current parameter group name.

      2. Settings: Customize the prefix content of parameters; the connectors between parameters and parameter content should match.

      3. Delete: Supports deleting the entire content of the parameter group.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce0ebf5b92864f9faa7af7f7ae144775~tplv-goo7wpa0wc-image.image) </span>

   * Parameter name: Information on **parameter name, default value, field type (including String and JSON types), and parameter description** etc. required in custom scripts.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The parameter replacement logic for Shell task template is as follows:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the parameter settings, add the parameter names used in the script: yarn_cluster, yarn_queue, fill in the default values according to the actual scenario, or you can choose not to fill them in and replace them directly when referencing the template in the shell task.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The parameters and parameter values entered will be concatenated in the last line of the script, for example, in the code above, after the shell task is referenced, the last line of the script is replaced with: commonFunction \-yarn_cluster=chris \-yarn_queue=script, overall by reading the parameter values and calling the commonFunction function method, using getopt to parse and execute.   </div>
   


<span id="1"></span>
## 4 Reference task mode

After the task template configuration is complete, you can reference it using the following two methods:


1. The function area of the task development node (Shell task types)

   1. In the **task development** interface, click **Data Development** in the left navigation bar.

   2. Enter the editor interface for the task type corresponding to the template, and click **Task Template** in the top navigation function area.

   3. Enter the **Task Template** prompt and select whether to use the task template. If you choose to use it, complete the following configuration information:

   
   |Parameters |Description |
   |---|---|
   |Choose Template |Select the task template corresponding to the task type, and the dropdown will display the template name information for the types of projects below. |
   |Version |You can specify a version number, or **always use the latest**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When you choose <strong>Always use latest</strong>: if the task template is updated later, the associated online tasks will be updated synchronously, so use this option with caution.</div><br> |
   |Parameter Setting |When you need to replace parameters in task templates, you can fill in specific parameter values through **Single line edit mode** or **Script edit mode**. |
   |Preview Results |The preview results will display the complete final code logic, and you can confirm again if the logic is correct. |
   

2. Direct reference to task templates

   1. Before referencing, you need to open the editor interface for the corresponding task type first; if it does not match the template task type, referencing is not supported.

   2. Move the mouse over the task template name, and directly click on "Reference" in the details on the right side. In the pop\-up, click the **OK** button to implement the task template reference, which can support multiple task references.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a32aff0b8fd446cb874aa94544235433~tplv-goo7wpa0wc-image.image) </span>


<span id="_7-其他信息"></span>
## 5 Other Information

In the **Task Template** interface, after creating the template, you can view the **Basic Info, Versions, Reference Record** and other information in the right navigation pane.


* Basic Info: View the template name/ID, template description, and information about the task type.

* Versions: After saving or updating the template, each version's updates are recorded. You can also perform the following actions:

   * View: Access code settings, custom parameters, and other information of the task template.

   * Restore as Draft: You can restore to a historical draft version, facilitating a timely rollback of the task template code.

   * Version Comparison: You can select two historical versions to compare and view the differences in their code, parameter configuration, and other information.

* Reference Records:

   * You can view which tasks have applied the current task template. Click the **View** button to jump to the corresponding task development interface.

   * When a batch task is activated but later closed, the corresponding reference records are deleted.

   * After a streaming task is closed, the reference records are not cleared and still exist.
