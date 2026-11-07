---
title: "Inter-instance synchronization"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions"
---

CR provides the registry replication feature for Standard Edition instances. You can create custom registry replication rules to synchronize images and Helm charts from the specified source instance to a specific location in the target instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This operation applies only to standard instances and does not apply to proxy repositories.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Application scenario

This article covers the following two registry replication scenarios:


|**Synchronization scenario** |**Description** |
|---|---|
|**Synchronization within or across regions** |Under the same BytePlus root user, synchronize images from the Standard Edition instance to other Standard Edition instances in the same region or across regions. Applicable to scenarios such as multi\-region deployment, disaster recovery backup, and pulling images from the nearest location. |
|**Synchronize to custom repository** |Synchronize images in the Standard Edition instance to external repositories outside BytePlus, such as Self\-built Harbor, Alibaba Cloud ACR, Huawei Cloud SWR, Tencent Cloud TCR, and more. Applicable to scenarios such as hybrid cloud deployment, cross\-cloud distribution, and multi\-cloud disaster recovery. |


<span id="13XYlJUV"></span>
## Prerequisites


|**Application scenario** |**Condition** |
|---|---|
|**Synchronization within or across regions** |Both the source instance and the target instance are **Standard Edition**, and their state is **Running**. For details on how to create an instance, see [Create a Standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance). |
||The source instance and target instance belong to the same BytePlus root user. |
||The target Standard Edition instance has been purchased and the namespace has been created. For details on creating a namespace, see [Create namespace ](https://docs.byteplus.com/en/docs/cr/create-a-namespace) **.**  |
||In cross\-region scenarios, the Source instance and Target instance must each enable **Public network access**. For details on enabling public network access, see  ** ** [Enable public network access](https://docs.byteplus.com/en/docs/cr/enable-public-network-access?lang=en). |
|**Synchronize to custom repository** |The source instance is **Standard Edition**, and its state is **Running**. For details on how to create an instance, see [Create a Standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance). |
||Supported external Target repository types for synchronization: Self\-built Harbor, Alibaba Cloud ACR, Huawei Cloud SWR, Tencent Cloud TCR. |
||The custom repository supports connection via public network. |
||The service address, username, and password for the external target repository have been obtained. |
||Confirm that the corresponding namespace exists in the external target repository (if a namespace with the same name does not exist, synchronization will fail). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5ZCM5q2l6KeE5YiZ"></span>
### Step 1: Configure a registry replication rule


1. Log in to the [CR console](https://console.byteplus.com/cr).

2. In the left navigation pane, select **Registry replication**, and click **Create registry replication rule**.

3. On the **Create registry replication rule** page, configure the parameters based on your needs.

   * Registry replication type

      
      |**Parameter** |**Description** |
      |---|---|
      |Synchronization type |Select **Inter\-instance synchronization** to synchronize the Standard Edition instance to other Standard Edition instances within this account, or to an external custom repository. |
      

   * Basic information

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |The custom name of the registry replication rule. The name must be unique within the same account. |
      |Description |Enter a description for the rule. The description can be empty and cannot exceed 200 characters. |
      

   * Source instance

      
      |**Parameter** |**Description** |
      |---|---|
      |Instance |Select the source Standard Edition instance to synchronize. |
      |Namespace |Select the name of the namespace to be synchronized in the source instance. |
      |Repository |The names of the OCI artifact repositories to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact repositories in the specified namespace.<br><br>* **Regex matching**: Match the OCI artifact repositories to be synchronized using regular expression rules. For common regex matching examples, see [Regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
      |Tag |The OCI artifact tags to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact tags in the specified repository.<br><br>* **regex matching**: Match OCI artifact versions to synchronize using regular expression rules. For common regex matching examples, see [regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
      

   * Target instance

      
      <Tabs>
      <Tab zoneid="Lm8so0uceO" title="Within the main account (synchronization within or across regions)">
      <TabTitle>Within the main account (synchronization within or across regions)</TabTitle>
      
      Synchronize the image to other Standard Edition instances within this account, either in the same region or across regions.
      
      
      |**Parameter** |**Description** |
      |---|---|
      |Synchronization type |Select **Within the main account**. |
      |Region |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In cross\-region scenarios, both the source instance and target instance must turn on <strong>Public network access</strong>. For details on turning on public network, see <strong> </strong><a href="https://docs.byteplus.com/en/docs/cr/enable-public-network-access?lang=en">Enable public network access</a>.</div><br><br><br>Select the region where the target Standard Edition instance is located. |
      |Instance name |Select the target Standard Edition instance. |
      |Namespace |Select the namespace in the target instance. If not specified, synchronization defaults to the namespace with the same name as the source instance; if the namespace does not exist, it will be automatically created. |
      
      
      <span id="MA0iTxnn"></span>
      #### 
      
      
      </Tab>
      <Tab zoneid="tVrqLwKVty" title="Custom (synchronize to custom repository)">
      <TabTitle>Custom (synchronize to custom repository)</TabTitle>
      
      Synchronize the image to an external custom repository outside BytePlus. Currently supported: Self\-built Harbor, Alibaba Cloud, Huawei Cloud, Tencent Cloud.
      
      
      |**Parameter** |**Description** |
      |---|---|
      |Synchronization type |Select **Custom**. |
      |Service address |The external custom repository address starting with `http(s)://`. For example, `http(s)://index.dockerhub.io`. |
      |Ignore certificate validity |Whether to ignore certificate validity.<br><br><br>* **Yes**: Ignore the validity of the external repository certificate and synchronize directly.<br><br>* **No**: Do not ignore certificate validity. Synchronization will fail if the certificate is not within the valid period. The external repository certificate must be issued by an authoritative institution. |
      |Username |The username for logging in to the external custom repository. |
      |Password |The password for logging in to the external custom repository. |
      |Namespace |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the external Custom repository is Alibaba Cloud ACR, do not include the <code>/</code> character in the repository (repo) name under the namespace, otherwise synchronization will fail.</div><br><br><br>Enter the target namespace name in the external custom repository. If not filled in, synchronization will Default to the namespace with the same name as the Source instance; if a namespace with the same name does not exist, synchronization will fail. |
      
      
      
      
      
      </Tab>
      </Tabs>
      

   * Synchronization rules

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Synchronization rules triggered by event\-driven triggering and timed trigger both support manual trigger.      </div>
      

      
      |**Parameter** |**Description** |
      |---|---|
      |Image overwriting |You can select "Enable" to enable this feature. After enabling, if the target instance contains an image with the same name as the source instance, the image from the source instance will overwrite the existing image with the same name in the target instance. |
      |Rule state |After selecting, enable this rule and set the following trigger conditions:<br><br><br>* **Event\-driven triggering**: Synchronization is automatically triggered when a rule\-compliant event occurs. That is, if you push a rule\-compliant artifact to the OCI artifact repository that complies with the registry replication rule in the source instance, synchronization will be automatically triggered once, and only the newly pushed artifact will be synchronized.<br><br>   You can also set **Trigger immediately** to **Yes** to specify that rule matching is triggered immediately after the registry replication rule is created to perform a synchronization operation.<br><br>* **Timed trigger**: Synchronization is triggered at the configured fixed intervals, with the first synchronization time set by the user.<br><br>   * **First trigger time**: Take note that this parameter can only be set to any time starting from the current time.<br><br>   * **Trigger frequency**: Specify the synchronization interval. By default, synchronization is triggered every 24 hours. The valid interval ranges from 1 to 720 hours.<br><br>* **Manual trigger**: If this option is selected, the rule will not be triggered automatically and synchronization must be executed manually. |
      


<span id=".5q2l6aqk5LqM77ya5omn6KGM5ZCM5q2l6KeE5YiZ"></span>
### Step 2: Execute the registry replication rule

The following three trigger methods are supported:


* If you select **Event\-driven triggering** when you configure the registry replication rule, the system automatically triggers synchronization when a rule\-compliant event occurs. If you select **Event\-driven triggering** and set **Trigger immediately** to **Yes**, rule matching will be triggered immediately after the registry replication rule is created.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also manually trigger an event\-driven registry replication rule.   </div>
   

* If you select **Timed trigger** when you configure the registry replication rule, the system will automatically trigger synchronization at scheduled intervals.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also manually trigger a timed trigger registry replication rule.   </div>
   

* If **Manual trigger** is selected, you can manually trigger the rule by referring to the following steps:

   1. In the navigation bar on the left of [CR Console ](https://console.byteplus.com/cr), select **registry replication**.

   2. On the **Registry replication** page, locate the rule to be triggered, and click **Trigger** in the **Actions** column.

   3. In the system pop\-up dialog box, verify the rule information, and click **Confirm** to trigger the synchronization operation.


<span id=".5q2l6aqk5LiJ77ya5p-l55yL5ZCM5q2l5pel5b-X"></span>
### Step 3: View synchronization logs


1. In the left navigation bar of the [CR Console ](https://console.byteplus.com/cr), select **registry replication**.

2. On the **Registry replication** page, locate the target rule and click the rule name.

3. On the rule details page, click the **Synchronization log** tab to view all synchronization logs of the rule.

   
   |Parameter |Description |
   |---|---|
   |Task ID |The synchronization task ID (unique within the instance). |
   |Synchronization state |The task state, which can be Running, Succeed, and Failed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the synchronization state is <strong>Succeed</strong>, the synchronization task is triggered as expected and at least one image tag is synchronized.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the synchronization state is <strong>Failed</strong>, the task fails to be triggered. Possible causes:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The state of the source Standard Edition instance is not <strong>running</strong>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The state of the target Standard Edition instance is not <strong>running</strong>.</div><br> |
   |Task duration |The time consumed to complete all synchronization tasks. |
   |Success rate |(Number of  synchronized tags/Total number of tags to be synchronized) × 100% |
   |Number of synchronization repositories |The number of OCI artifact repositories to be synchronized by the current task. |
   |Trigger time |The trigger time of the synchronization task. |
   

4. Click the task ID to view the details of the synchronization task. The following information is displayed: `[namespace]/[repo]:tag` of the source instance, `[namespace]/[repo]:tag` of the target instance, and synchronization state of the synchronization task.

   If the synchronization state is **Succeed**, the artifacts have been successfully synchronized from the source instance to the target instance. If the synchronization state is **Failed**, the artifacts fail to be synchronized from the source instance to the target instance.
