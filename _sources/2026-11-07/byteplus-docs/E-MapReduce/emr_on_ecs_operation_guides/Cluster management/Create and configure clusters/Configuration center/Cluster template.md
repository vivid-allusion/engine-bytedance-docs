---
title: "Cluster template"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Cluster_template"
---

Cluster template is a module in the EMR Configuration Center. Users can save the cluster configuration information provided when creating an EMR cluster as a cluster template, so that it can be reused as cluster configuration information. After creating a cluster template, users can create new clusters based on the cluster configuration information in the cluster template. Users can also manage cluster templates in the Configuration Center.

<span id="创建集群模版"></span>
## Create cluster template

Cluster templates are maintained in the Configuration Center. Users can create cluster templates in two ways:


* Create cluster template in the Configuration Center

* Save cluster configuration as cluster template when creating a cluster


<span id="在配置中心创建集群模版"></span>
### Create cluster template in the Configuration Center

Users can create cluster templates in the Configuration Center. The steps are as follows:


1. On the EMR page, use the left navigation bar to go to **Configuration Center** \- **Cluster template**. The page displays the user's cluster template list.

2. Click the **Create template** button on the right side of the title bar of the cluster template page. The page displays information related to creating a cluster template.

3. Fill in each configuration item in the cluster configuration information of the cluster template in sequence. For the meaning of each configuration item, refer to the corresponding configuration item when creating a cluster using the **Create custom**Custom creation method.

4. After confirming that the information is correct, at the bottom of the \*\*Preview confirmation \*\* page, click the **Create template** button.


After the cluster template is created successfully, it will appear in the cluster template list on the **Configuration Center** \- **Cluster template** page.

<span id="创建集群时将集群配置保存为集群模版"></span>
### Save cluster configuration as cluster template when creating a cluster

Users can save the configuration filled in when creating a cluster as a cluster template. The steps are as follows:


1. Go to the **Create cluster** page, use the **Custom creation** method, and fill in each configuration item in sequence.

2. At the bottom of the **Preview and confirm** page, click the **Save as cluster template** button.

3. The **Save as Cluster Template** dialog box appears. Enter the cluster template name in the dialog box, and click the **OK** button.


After the cluster template is saved successfully, you can return to the Create Cluster page to continue creating a cluster. The successfully saved cluster template will appear in the cluster template list on the **Configuration Center** \- **Cluster Template** page.

<span id="基于集群模版创建集群"></span>
## Create a cluster based on a cluster template

After creating a cluster template, users can create clusters based on the cluster template. The steps are as follows:


1. In the EMR page, use the left navigation bar to go to **Configuration Center** \- **Cluster Template**. The page displays the user's cluster template list.

2. Find the required cluster template in the cluster template list, and in the **Actions** column of the corresponding row, click **Create Cluster.** 

3. A dialog box appears. After reading and confirming the content in the dialog box, click the **OK** button.


The successfully submitted cluster will appear on the **Cluster Management** \- **Cluster List** page. The name of a cluster created based on a cluster template includes the cluster template name and the creation time information.

<span id="管理集群模版"></span>
## Manage cluster templates

On the list page of **Configuration Center** \- **Cluster Template**, you can manage cluster templates. The following operations are currently supported:


* **Search Cluster Template**: Use the search box on the right side of the cluster template page title bar to search for the required cluster template.

* **View Cluster Template Details**: In the **Template Name/ID** column of the corresponding row, click the cluster template ID.

* **Edit Cluster Template**: In the **Actions** column of the corresponding row, click **Edit**. For specific editing methods, refer to creating a cluster template.

* **Clone Cluster Template**: In the **Actions** column of the corresponding row, click **Clone** and enter a new cluster template name.

* **Delete Cluster Template**: In the **Actions** column of the corresponding row, click **Delete.** 


<span id="注意事项"></span>
## Important notes


* Users must be assigned the EMRFullAccess access policy to access the Configuration Center.

* Currently, only Hadoop and Flink cluster types support creating cluster templates; other cluster types do not support creating cluster templates.

* A single user can create up to 50 cluster templates.

* Cluster templates only support the Pay\-As\-You\-Go payment type and do not support the Subscription payment type.

* Editing or deleting cluster templates does not affect clusters created from those templates.
