---
title: "Tag-based bill splitting"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Tag-based-bill-splitting-for-instances"
---

VCI supports bill splitting based on tags added to instances. This addresses the need for financial cost sharing.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* When using tags for bill splitting, you need to **enable** bill tags in the Billing Center console at [Billing Management - Bill Tags](https://console.byteplus.com/finance/bill/tag/) and apply relevant tags to bill details. For more information, see [Cost Tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

* VCI pods created by VKE have the following system tags by default:

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Enabled</strong> system tags will be automatically synchronized to split bills, but there may be up to an 8\-hour delay.   </div>
   

   
   |System tag |Description |
   |---|---|
   |sys:vke:cluster\-id\-{real cluster ID} |The ID of the VKE cluster to which the VCI pod belongs. Example: `sys:vke:cluster-id-ccofrscb915********`. |
   |sys:vke:namespace |The namespace where the VCI pod is located. |
   |sys:vke:zone\-id |The ID of the availability zone where the VCI pod is located, for example, `cn-beijing-a`. |
   |sys:vke:pod\-name |The name of the VCI pod. |
   |sys:vke:owner\-reference\-kind |The kind of workload that the VCI pod belongs to, such as Deployment and Job. |
   |sys:vke:owner\-reference\-name |The name of the workload (for example, Deployment, and Job) to which the VCI pod belongs. |
   |sys:vke:instance\-type |Specifications of the VCI pod. For example, `sys:vke:instance-type: vci.u1.2c-4gi`. |
   


<span id=".5re75Yqg5qCH562-"></span>
## Adding tags

Enable tag\-based bill splitting in VCI pods via pod annotations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can add resource tags in the BytePlus <a href="https://console.byteplus.com/resourcemanager">Resource management console</a>, or directly add resource tags when creating VCI pods. The system will synchronize the tags to the <a href="https://console.byteplus.com/resourcemanager/tag/list">Resource management console \- Tags</a> page.  For details, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Resource_Tag">Resource Tag</a>.</div>



|Annotation Key |Annotation sample value |Description |
|---|---|---|
|vci.vke.volcengine.com/resource\-tags |"app:nginx,env:test" |Specify custom tags for the VCI pod to enable bill splitting of VCI resources by tag. The requirements for custom tags are as follows:<br><br><br>* The supported format is string.<br><br>* Each tag consists of a key\-value pair in the `key:value` format. Multiple tags are separated by commas (`,`). For example, `"app:nginx,env:test"` means that two tags are set for the VCI pod: `app:nginx` and `env:test`.<br><br>* The requirements for a tag key are as follows:<br><br>   * It must not start with `volc:` in any case.<br><br>   * It can only contain language characters, digits, spaces, and the following special characters: `_./=+-@`.<br><br>   * The length is limited to 1 to 128 characters.<br><br>* The requirements for a tag value are as follows:<br><br>   * This can be left blank.<br><br>   * It can only contain letters, digits, spaces, and the following special characters: `_./=+-@`.<br><br>   * Its length does not exceed 256 characters.<br><br>* A single VCI pod supports up to 50 tags.<br><br>* Adding a tag with the same key as an existing tag key by using the annotation will overwrite the original tag value.<br><br>* Tag keys and values do not allow leading or trailing spaces. |


The following sample code creates a VCI pod. For more information about creating VCI pods, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance):

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: demo-vci-pod  # Pod Name.
  namespace: default  # Namespace to which the pods belong.
  annotations:
    vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
    vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1n******** # Specify the ID of a subnet. You can specify multiple subnets within the same availability zone. To do so, separate them with commas (,).
    vci.vke.volcengine.com/preferred-instance-family: vci.u1 # Specify the instance family of the VCI.
    vci.vke.volcengine.com/resource-tags: "app:nginx,env:test"  # Custom tags for the VCI pod.
spec:
  containers:
  - image: cr-cn-beijing.volces.com/tw/nginx:1.0 # The address and version of the container image. Replace the value with your actual information.
    imagePullPolicy: Always
    name: nginx
    resources:
      requests:  # Specify the vCPU, memory, and GPU settings for the container as needed.
        cpu: 2
        nvidia.com/gpu: 2 # Specify the number of GPUs for the container as needed (same as native one). You can specify both limits and requests, but the values must be equal.
      limits:
        cpu: 2
        nvidia.com/gpu: 2
```


<span id=".5YiG6LSm5ZCO5p-l55yL6K-05piO"></span>
## Viewing results after configuring bill splitting

Custom VCI tags will only be shown in the **Tags** column on the **Split bills** page. You can follow the steps below to view the result:


1. Log in to the BytePlus [Cost Center](https://console.byteplus.com/finance).

2. Select **Bill management** \> **Split Bills** in the left navigation bar.

3. On the **Split bills** page, use the **Tags** search box at the top of the page to search for the custom VCI pod tags that you have set.
