---
title: "Removing data nodes"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/reducing-data-nodes"
---

When your business runs into off\-peak time of traffic, or the volume of data stored in your instance decreases, you can reduce the number of data nodes by removing data nodes from the instance to better match the current business status.

This topic describes how to remove data nodes from an instance.

<span id="fcb20afc"></span>
## Precautions


* Removing the number of data nodes involves data migration which has some impact on read and write performance. We recommend that you perform the operation of removing data nodes during the off\-peak time of business workloads.

* Whether to remove data nodes is evaluated from the following three aspects of instance running status after data node removal during peak hours:

   * CPU utilization is below 80%

   * memory utilization is below 70%

   * disk utilization is below 80%

      Only when the above three thresholds are met, removing data nodes is recommended. For more information about how to monitor the above data, please see [Viewing monitoring overview](https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring).

* During the data migration process, the number of data nodes cannot be increased, but other configurations of upgrade and downgrade operations are allowed.

* After the data migration is completed, it is necessary to confirm the order of reducing the number of data nodes on the page.

* The execution time of a data migration task mainly depends on the size of the data volume. If a large amount of data needs to be migrated, it may take a long time to complete the migration process.

* Single\-node instances cannot perform data node removing.


<span id="c9cb7722"></span>
## Reducing the number of data nodes

The process of removing the number of data nodes involves data migration, which can be divided into three steps as shown in the following figure.


1. Enter the functional entry.

   1. Log into the [BytePlus Cloud Search console](https://console.byteplus.com/es).

   2. In the top menu bar, select the Project and Region where the desired instance resides.

   3. On the **Instances** page, find the desired instance, click `...` in the **Actions** column, and then choose **Remove data nodes**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f04f5ae6da184ca2983b1a37d5471b86~tplv-goo7wpa0wc-image.image) </span>

2. Execute data migration tasks.

   1. In the dialog box that appears, confirm the message, and click **OK**.

   2. On the **Remove data nodes** page, set the node number to the desired number, and click **Confirm order**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e07aceaf20054f68a7bf59097fd1eed5~tplv-goo7wpa0wc-image.image) </span>

      The system verifies removal requests. If the verification succeeds, the system removes nodes and migrates data. If the verification fails, follow the instructions on the page to handle exceptions before proceeding with the next step.

      
      |**Check Item** |**Normal Status** |
      |---|---|
      |Cluster health status |The cluster status is green. |
      |Index allocation configuration |Index allocation is set to all or is not configured.<br><br>`cluster.routing.allocation.enable: all` indicates that shards of all types are allocated to their respective nodes. |
      |Index replica distribution |Different replicas are distributed to different nodes. |
      |Number of remaining nodes after the removal |The number of nodes is larger than or equal to two. For an instance across multiple Availability Zones, make sure that each Availability Zone contains the same remaining number of nodes, and each Availability Zone must have at least two nodes. |
      |Node CPU load after data migration |The CPU load for 5 minutes does not exceed 3.5. |
      |Disk size of the destination node for data migration |If data needs to be migrated before the removal, ensure that the disk usage of the destination node does not exceed 75%. |
      |Memory of the destination node for data migration |If data needs to be migrated before the removal, ensure that the memory usage of the destination node does not exceed 70%. |
      |Number of shards |The node to be removed has 0 shards. |
      

   3. After the removing request verification is passed, click **Confirm order** again, and then in the dialog box, click **OK** to start the data migration.

   4. In the pop\-up dialog box showing operation estimated duration , click **OK**.

   5. On the **Migration details** page, confirm change details, read and agree to Terms of data migration, and then click **Confirm migration** to confirm the migration again.

      You can also view migration details and stop the migration task.

      * **Details**: View the details of the migration task.

      * **Stop**: Stop the migration task. After you stop the migration task, the data is migrated back.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The execution time of a data migration task mainly depends on the size of the data volume. If a large amount of data needs to be migrated, it may take a long time to complete the migration.      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the migration task takes a long time, you can exit the migration task page to handle other work. You can later re\-enter the data migration task on the instance list page. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/cloudsearch/reducing-data-nodes#6490bb47">Viewing migration tasks</a>.      </div>
      

   6. Confirm that the migration task is complete and start to remove the data node.

      On the data migration task page, view the migration progress. When the data migration task shows **Data migration complete**, click **Confirm to change** to enter the data node remove order page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2732b8d2b294f29b69674d5f7be4542~tplv-goo7wpa0wc-image.image) </span>

3. Confirm the data node capacity reduction order.

   1. On the **Order details** page, view the numbers of data nodes before and after the change, read and confirm the Terms of Service, and then click **Buy now**.

   2. Return to the **Instances** page to verify the operation. If the instance status changes from **Changing** to **Running**, the operation succeeds.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/129a7e8f1f534d79a4d531dccf7c0311~tplv-goo7wpa0wc-image.image) </span>


<span id="e627b85e"></span>
### Viewing migration tasks

On the **Instances** page, you can view the progress of a migration task.

The progress of a migration task is indicated by a circle icon. To view the progress, hover your mouse pointer over the icon. To view migration task details, including progress and remaining time, click the circle icon. You also stop the migration task.
