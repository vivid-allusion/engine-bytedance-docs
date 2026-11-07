---
title: "Node load details"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Node_load_details"
---

The platform provides additional node load details dashboards for **resource group administrators** . When the load in the resource group is queued due to fragmentation, the resource group administrator can query the load fragmentation on this page. This function supports querying resource group GPU resource usage, node load details (including GPU, CPU and memory usage of Dev boxes, custom tasks and inference services), free nodes and fragmented node information.

<span id="使用步骤"></span>
## Procedure

If you need to use this feature, you need to follow these steps:


1. Click "Resource Group" \- "Node Load Details".

2. Select the load task type that needs to be queried, the default is "Dev boxes", and enter the load ID under the corresponding type to search.

3. After the ID is entered into the query, the actual resources required for the load will be displayed in the lower panel, including the corresponding GPU model, the Node list under the resource group, and the actual resource usage (GPU, CPU, and memory).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only load information with query status <code>in queue</code>is supported.</div>


* <div data-tips="true" data-tips-type="tip">Only load information on GPU servers is supported.</div>


* <div data-tips="true" data-tips-type="tip">Nodes that have gone offline in the past day will still appear in the Node list.</div>


* <div data-tips="true" data-tips-type="tip">Querying for fragmentation information for a service deployment is currently supported only if there is at least one "queued" instance in the deployment.</div>



<span id="最佳实践"></span>
## Best practices

What happens when you submit a custom task with 8 GPU/112 vCPU/1960 GiB memory \* 2, there is a quota in the queue, but the task is always `in the queue`?


1. Enter "Resource Group" \- "Node Load Details", select the load type as "custom tasks", and enter the full load ID of the task.

2. After clicking, you can view the required resource specifications for the load and the actual resource usage, which is displayed here as the specification usage for a single instance.

3. In the "Free Nodes" below, you can see the number of idle nodes of the whole machine, and in the "Fragment Nodes", you can view the actual consumption of resources and the idle resource usage of each fragment node.

4. Depending on the resource usage of the load (single instance specification usage \* number of instances), click "IP" in the list of fragmented nodes. View the load details on the current shard node and choose to migrate the shard load.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25a9d34271944230b9b1de35d7d49805~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In the "Node Load Details" Pod list, the beginning of "t" represents custom tasks, the beginning of "s" represents inference services, and the beginning of "di" represents Dev boxes.</div>


* <div data-tips="true" data-tips-type="tip">Migration method description: According to the load ID, you can contact the task creator to perform the task migration operation. For specific migration methods, please refer to the "Operation Guide" section of the <a href="https://docs.byteplus.com/docs/undefined/67e296e40ae76c0503e97085">Node Fault Notification and Load Migration Guide</a>.</div>
