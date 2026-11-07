---
title: "One-click deployment"
product: "Seedream"
product_code: "seedream"
source: "https://docs.byteplus.com/en/docs/seedream/one-click-deployment"
---

<span id="4maIm7QS"></span>
# Detailed Steps for One\-Click Deployment

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Only available for users with specific subscrption.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131256-925575560999.png) </span>


&nbsp;

1. ## Lumina Workflow Creation <span id="eeFir5pD"></span>


[https://ai.byteplus.com/lumina/workflow-as-room/modal](https://ai.byteplus.com/lumina/workflow-as-room/modal)

You can create a workflow using one of the following methods

Option a. Create a workflow by creating a new canvas pro<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930083341-559921273372.png) </span>

&nbsp;

Option b. Import a workflow from a workflow template<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930083444-511233236311.png) </span>

&nbsp;

Option c. Import an existing workflow file

Drag and drop the saved workflow file into the blank canvas pro to import<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930083607-956198625630.png) </span>

 
&nbsp;

2. ## Workflow Parameter Definition (Slotting) <span id="C2mjKL3B"></span>


Parameter Definition, commonly known as Slotting, refers to defining which nodes in the workflow are exposed externally. It exposes the parameters in the workflow as parameter information in the algorithm service API. The node parameters that are not slotted will be uniformly encapsulated.

<div style="text-align: center">
</div>



|<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131014-131802589229.png" width="2406px" /><strong>Example</strong></div><br> |Common Slotting Parameters:<br><br><br>1. loadimage+saveimage：Input image, output result image<br><br>2. ksample：<br><br>   1. denoise<br><br>   2. seed<br><br>3. prompt: Confirm the exact slotting node with the designer<br><br><br><div data-tips="true" data-tips-type="warning">This means that in subsequent API access:</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>The above parameters will show default values and can be adjusted.</strong></div><br><br><br><div data-tips="true" data-tips-type="warning">In actual deployment, you only need to open the corresponding parameters according to business requirements.</div><br> |
|---|---|


**Slotting Process：** 


|<div style="text-align: center"><br><strong>Steps</strong></div><br> |<div style="text-align: center"><br><strong>Schematic diagram</strong></div><br> |
|---|---|
|1. Right‑click on the node<br><br>2. Select Slot tagging<br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131012-1635867202778.png" width="828px" /></div><br><br><br> |
|3. Edit the slot information for this node<br><br>   1. Custom name: clearly identify the slot position / parameter;；<br><br>   2. Use default value for component；<br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131012-1705895512955.png" width="1002px" /></div><br><br><br> |
|4. Click the Upload icon in the top‑left corner to view all slot information<br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131011-502058023115.png" width="1034px" /></div><br><br><br>&nbsp;<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131012-756183251497.png" width="2404px" /></div><br><br><br> |



* Tips：For common img2img workflows, **be sure to create input image and output image slots**. Otherwise, the input image may not take effect, service deployment may fail, or the output will be empty.

* The same applies to txt2img: create an output image slot.



&nbsp;

3. ## Start One\-click Deployment <span id="HHqtloCb"></span>



<columns>
<columnsItem zoneid="uIL03X927D">

<div style="text-align: center">
One\-click Deployment<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930083824-28542681834.png" /></div>




</columnsItem>
<columnsItem zoneid="lsm8qUdJGf">

1. Click the **Simple Deployment** button at the bottom.

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="W0KNmah1J2">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930084004-836087756314.png" /></div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416132658-1493355137883.png) </span>Name Your Capability

</columnsItem>
<columnsItem zoneid="evwC8rXHDN">

2. After loading completes, name the **Capability Name**:

   1. ⚠️This name will be the final algorithm **req_key**.It should clearly reflect business, scenario, and function.Subsequent access requests, resources, and call volume will all be bound to this req_key.

   * Only letters, numbers, and underscores _ are allowed; max 40 characters.

   * Cannot end with _ or _ + digit (e.g., i2v_test_ or i2v_test_1).

   * One deployed capability corresponds to one req_key. Avoid creating multiple req_keys for the same capability.

   2.  Select One\-click deployment, the resource will be exclusive. Otherwise ther resource will be shared. 

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="UClCHrcWA2">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416132807-1524076389084.png" /><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416132812-1360345117035.png" />Verify Information</div>


</columnsItem>
<columnsItem zoneid="YK635BbTXB">

3. Check slotting information:

   1. Double‑confirm that the parameter keys (keys in request req_json), corresponding workflow node IDs (node_id), class types (class_type), and attributes (input_key) are as expected.If any parameters are missing, return to the workspace to adjust.

</columnsItem>
</columns>



4. ## Deployment completed.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131013-19984493402.png) </span> <span id="UrD1VD8m"></span>

5. ## Customer Access <span id="eW2HKbUt"></span>


<span id="qzU7WBVk"></span>
### 5.1 Capability & Resource Access

Access can be performed for published capabilities.


<columns>
<columnsItem zoneid="DCCO3rCagm">

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131012-579280815602.png) </span>

</columnsItem>
<columnsItem zoneid="HHAoa74dFH">

1. Click "Access capabilities and resources"

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="OotmzjqRP4">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131015-830111292476.png" width="2648px" /></div>


</columnsItem>
<columnsItem zoneid="I2aJYcxoFE">

2. Select the capability to access. If the capability has multiple versions, you can select the desired one.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131012-293480526677.png) </span>

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="u7HEwiqVQz">

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131014-772011404175.png) </span>

</columnsItem>
<columnsItem zoneid="gShx7WJd7B">

3. Enter the **Resource Name**. This parameter is also required for subsequent OpenAPI access.

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="do197Bb7tt">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131013-1341296030964.png" width="2632px" /></div>


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416143328-1595619180404.png" width="2698px" /></div>


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140343-78795840826.png" width="2288px" /></div>


</columnsItem>
<columnsItem zoneid="J2bxzC26DY">

4. Use the **Resource Calendar** to apply for concurrency for capability invocation by date.

5. If the available concurrency quota is insufficient, contact technical support to allocate more resources.

6. The applied resources require some time to deploy.You can check the deployment status in the instance information on the service details page.Instances in the **healthy** status are ready for invocation.


  Service name format:{capability_name}\-dedicated\-{resource_name}

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="rLnvx4fskr">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131012-342922159311.png" width="2516px" /></div>


</columnsItem>
<columnsItem zoneid="rusYeAdmtB">

7. You can preview the effects with the applied resources.

</columnsItem>
</columns>


<span id="J206GPj1"></span>
### 5.2 OpenAPI Capability Integration

The one\-click deployed capability supports both synchronous invocation and asynchronous invocation.

Synchronous invocation: LumiProcess

Asynchronous invocation: LumiSync2AsyncSubmitTask + LumiSync2AsyncBatchGetResults

[LumiProxyApi Integration Document](https://docs.byteplus.com/en/docs/seedream/LumiProxyApi-Integration-Document)

<span id="SmkJtNTG"></span>
### 5.3 Resource Modification and Release


<columns>
<columnsItem zoneid="BuyZyEKE3v">

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131013-1341291647409.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260511114243-517118238795.png) </span>

</columnsItem>
<columnsItem zoneid="MpdIjYYN3H">

1. Deployed resources will be **automatically released** upon expiration.You may modify the **Resource Calendar** before expiration to extend the resource usage period.

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="wmblqJbmZc">

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131015-1187458599623.png) </span>

</columnsItem>
<columnsItem zoneid="ceHw3K7EQI">

2. Click **Delete Resource** to release the resource and stop further consumption.**Please ensure that online traffic has been completely stopped before releasing the resource.** 

</columnsItem>
</columns>



&nbsp;

6. ## Service Upgrade <span id="DowX9wFR"></span>


<div data-tips="true" data-tips-type="warning">Service upgrade can be implemented in two ways:</div>



1. <div data-tips="true" data-tips-type="warning">Based on the existing capability, perform <strong>one\-click deployment again</strong> using the <strong>same capability name</strong>.Customers do not need to replace the req_key in OpenAPI requests.</div>


2. <div data-tips="true" data-tips-type="warning">【Recommended】Use a <strong>new capability name</strong> to redeploy and reconnect.Customers can complete the upgrade by replacing the req_key in OpenAPI requests.</div>



This section mainly introduces the **first method**.After completing the automatic deployment of the existing version, you can modify the original workflow.Once modified, repeat steps 2–5 and select the **same capability name**.


<columns>
<columnsItem zoneid="Wj8QMGpIOb">

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131015-347182380394.png) </span>

</columnsItem>
<columnsItem zoneid="vv1titV94N">

1. After submitting One\-click deployment, new deployment information will appear.

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="ILaLUfutl7">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131013-382826151202.png" width="2448px" /></div>


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260511114258-357193148955.png" width="318px" /></div>




</columnsItem>
<columnsItem zoneid="SRd1thte2i">

2. In the instance information, you can **switch the template ** of the applied resource to the new template.




</columnsItem>
</columns>


<span id="80tqjLZm"></span>
# FAQ


1. ## What should I do if the available quota in the Resource Calendar is 0 when applying for resource access? <span id="l8PkUIIo"></span>


The Resource Calendar requires pre\-application. Quota is obtained by consuming computing points.Currently, you can only contact technical support offline for configuration.

&nbsp;

&nbsp;

<span id="om0nj60e"></span>
# 一键部署详细操作步骤

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">仅限特定套餐用户可使用</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416134807-1582162846550.png) </span>


1. ## Lumina创建工作流 <span id="xHtQrlmO"></span>


[https://ai.byteplus.com/lumina/workflow-as-room/modal](https://ai.byteplus.com/lumina/workflow-as-room/modal)

可以选取以下方式创建工作流

Option a. 新建画布专业版搭建工作流<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930083341-559921273372.png) </span>

&nbsp;

Option b. 通过工作流模版导入工作流

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930083444-511233236311.png) </span>

&nbsp;

Option c. 导入已有的工作流文件

在空白的智能画布中，拖拽导入保存的工作流文件

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930084434-653530938058.png) </span>


&nbsp;

2. ## workflow 参数定义（开槽） <span id="wl7AreCm"></span>


参数定义也就是常说的「开槽」，这里是明确 workflow 中的哪些节点被开放，将工作流中的参数暴露为算法服务 API 中的参数信息，未被「开槽」的节点参数将统一封装。


|<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416135010-1772695491393.png" width="2362px" /><strong>Example</strong></div><br> |常见开槽参数：<br><br><br>1. loadimage+saveimage：上传图、输出结果图<br><br>2. ksample：<br><br>   1. denoise<br><br>   2. seed<br><br>3. prompt: 跟设计师确认具体开槽节点<br><br><br><div data-tips="true" data-tips-type="warning">这意味着在后续的 API 接入中：</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>以上参数会显示默认值，并可以被调整</strong></div><br><br><br><div data-tips="true" data-tips-type="warning">实际部署中仅需根据业务需求开放对应参数即可，「一键部署」功能提供自动开槽的能力，但目前<strong>只支持img2img场景</strong>，输入、输出及seed 自动开槽，推荐用户手动完成开槽。</div><br> |
|---|---|


**开槽流程：** 


|<div style="text-align: center"><br>步骤</div><br> |<div style="text-align: center"><br>示意图</div><br> |
|---|---|
|1. 在节点上**右键**<br><br>2. 选择**槽位标记**<br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416135324-190028215319.png" width="858px" /></div><br> |
|3. 编辑该节点的槽位信息<br><br>   1. 名称自定义：能明确开槽位置/参数等信息；<br><br>   2. 组件**默认**即可；<br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416135421-1131269648036.png" width="1014px" /></div><br> |
|4. 点击左上角「保存」图标，查看全部槽位信息<br><br><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416135456-1531607735096.png" width="832px" /></div><br><br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131012-756183251497.png" width="2404px" /></div><br> |



* Tips：对于常见图生图工作流，切记要创建输入图片和输出图片槽位，否则会出现输入图片不生效或服务部署失败/输出为空。文生图同理创建输出图片；



&nbsp;

3. ## 开启自动部署 <span id="RaOuUfqH"></span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">请务必在工作流跑通后再进行一键部署</div>



<columns>
<columnsItem zoneid="cqfWtgdy">

<div style="text-align: center">
一键部署</div>


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930083824-28542681834.png" /></div>




</columnsItem>
<columnsItem zoneid="oOMx5I4X">

1. 点击下方简易部署按钮

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="rU8WwNcH">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260930084004-836087756314.png" /></div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416135831-1702661175086.png) </span>能力命名

</columnsItem>
<columnsItem zoneid="qon9tnNY">

2. 加载完成后，对「能力名称」进行命名

   1. ⚠️该命名也即最终的算法「req_key」，命名需要有明确的业务、场景、名称等信息，后续接入请求和资源、调用量等信息均会绑定该req_key。

      1. 只支持字母、数字以及_符号，且不超过 40字符；

      2. 不支持以_ 或 _数字结尾；（如i2v_test_ 或 i2v_test_1）

      3. 一个部署能力一个 req_key，避免相同能力创建多个 req_key

   2. 选择一键部署，则资源为独占模式；否则资源为共享模式。

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="wFewhLim">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416135923-1274845185045.png" width="2418px" /><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416135928-568224574593.png" width="2324px" />检查信息</div>


</columnsItem>
<columnsItem zoneid="vKV5fbwb">

3. **检查**开槽信息

   1. 再次确认参数标识(请求 req_json 中的 key )及其对应的工作流节点ID(node_id)、类型(class_type)、属性(input_key)是否符合预期，如果有遗漏参数，需返回房间中重新调整。

</columnsItem>
</columns>



4. ## 部署完成 <span id="pmDMynnH"></span>


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140031-1130889613581.png" width="2354px" /></div>



5. ## 客户接入 <span id="7jzxGSdJ"></span>

1. ### 能力与资源接入 <span id="N7rmp145"></span>


已经发布的能力即可进行接入。


<columns>
<columnsItem zoneid="A2FLC7cn">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140101-1029198495531.png" width="2516px" /></div>


</columnsItem>
<columnsItem zoneid="PFnOQVGF">

1. 点击接入能力与资源

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="bM3U05Av">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140207-219122453666.png" width="2662px" /></div>


</columnsItem>
<columnsItem zoneid="fzINUud7">

2. 选择要接入的能力。能力如果包含多个版本可以点击选择。


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140126-1683660975832.png) </span>

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="n2noyL5H">

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416131014-772011404175.png) </span>

</columnsItem>
<columnsItem zoneid="LCL4NpuF">

3. 输入资源名称，后续接入 Openapi 时也需要传递这个参数。

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="dudzY13G">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140334-279997485114.png" width="2644px" /><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140338-192335764202.png" width="2708px" /><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140343-78795840826.png" width="2288px" /></div>


</columnsItem>
<columnsItem zoneid="AwIc1toV">

4. 资源日历按照日期申请能力调用的并发

5. 如果可申请并发不足，请联系技术支持同学开通更多资源。

6. 申请的资源需要一定时间去部署，在服务详情的实例信息可以看到部署状态，达到 healthy 状态的实例即可调用。服务名称的命名为 {能力名称}\-dedicated\-{资源名称}.

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="DBqAJelR">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140318-864555211460.png" width="2516px" /></div>


</columnsItem>
<columnsItem zoneid="NRgrYV3U">

7. 已申请的资源可以进行效果预览

</columnsItem>
</columns>


<span id="Zv8Vvq3f"></span>
### 5.2 Openapi 能力对接

一键部署的能力支持同步调用(**LumiProcess**) 和异步调用(**LumiSync2AsyncSubmitTask + LumiSync2AsyncBatchGetResults**)

[LumiProxyApi接入文档](https://docs.byteplus.com/en/docs/seedream/LumiProxyApi-Integration-Document)

<span id="Dg7OoJTo"></span>
### 5.3 资源修改与释放


<columns>
<columnsItem zoneid="iL7r2v8j">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140504-125167007558.png" width="2516px" /><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140511-870891230709.png" width="2640px" /></div>


</columnsItem>
<columnsItem zoneid="hKag00U6">

1. 已经部署的资源，在到期后会自动释放，可以在到期前修改资源日历，延长资源使用时间。

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="GsyzGOOT">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140529-475588357584.png" width="2622px" /></div>


</columnsItem>
<columnsItem zoneid="r8x57VUX">

2. 点击删除资源即可释放资源，不再消耗资源，请务必在线上流量已经结束的情况下再释放资源。

</columnsItem>
</columns>



&nbsp;

6. ## 服务升级 <span id="CAa1HA3v"></span>


<div data-tips="true" data-tips-type="warning">服务升级可以通过两种方式来实现：</div>



1. <div data-tips="true" data-tips-type="warning">在现有能力基础上，使用同样的能力名称再次进行一键部署，客户侧无需替换请求 Openapi 的 req_key；</div>


2. <div data-tips="true" data-tips-type="warning">【推荐】使用新的能力名称，重新进行部署、接入，客户侧可以通过替换请求 Openapi 的 req_key 实现升级。</div>



这里主要介绍第一种方式。在完成已有版本的自动部署后，可以在此前 workflow 基础上进行改动，改动完之后可以重新走 2\-5 步，选择**同样的能力名称**。


<columns>
<columnsItem zoneid="pxVPUpeM">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140612-1528072735558.png" width="2350px" /></div>


</columnsItem>
<columnsItem zoneid="oSaQETuk">

1. 提交完成一键部署后，会出现新的部署信息。

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="mVfED7MV">

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140629-1549920699449.png" width="2448px" /><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416140633-86762547055.png" width="1094px" /></div>




</columnsItem>
<columnsItem zoneid="412u30R8">

2. 可以在实例信息将已申请资源的模板切换成新的模板。




</columnsItem>
</columns>


<span id="kJdQooXD"></span>
# FAQ


1. ## 申请资源接入时，资源日历可用为 0，该怎么办？ <span id="P5GTvXSY"></span>


资源日历需要预先申请，消耗算点置换资源日历可用额度。目前只能通过线下联系技术支持同学添加配置
