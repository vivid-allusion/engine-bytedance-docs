---
title: "Synchronizing external repositories to CR"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/replicate-images-from-a-third-party-registry-to-the-container-registry"
---

This topic describes how to use the registry replication feature to migrate an external repository to a BytePlus CR Standard Edition instance.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## **Usage limits**


* Currently, the following external repositories can be migrated: Tencent Cloud TCR Enterprise Edition, Alibaba Cloud ACR, AWS ECR **private** repositories, Harbor instances, Docker Hub, Google Artifact Registry (GAR), and Docker Registry instances.

* Make sure that images can be pulled from and pushed to the external repositories as expected over the **public network**. Currently, only synchronization over the public network is supported for external images.

* The migration success rate is not guaranteed when external image repositories from regions outside of China are migrated to CR instances in the Chinese mainland regions.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* The source instance and the target instance are in **Running** state.

* The address, username, password, and other relevant information for the external repository are prepared.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5ZCM5q2l6KeE5YiZ"></span>
### Step 1: Configure a registry replication rule


1. Log in to the [CR console](https://console.byteplus.com/cr).

2. In the left navigation pane, select **Registry replication**, and click **Create registry replication rule**.

3. On the **Create registry replication rule** page, configure the parameters based on your needs.

   * **Registry replication type**

      
      |**Parameter** |**Description** |
      |---|---|
      |Synchronization type |Select **External migration** to migrate external repositories to BytePlus CR Standard Edition instances. |
      

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |The custom name of the registry replication rule. The name must be unique within the same account. |
      

   * **Source/Target instance configuration**

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Currently, the following external repositories can be the migration source: Tencent Cloud TCR <strong>Enterprise Edition</strong>, Alibaba Cloud ACR, AWS ECR <strong>private</strong> repositories, Harbor instances, Docker Hub, GAR, and Docker Registry instances.      </div>
      

      * Source instance

         
         <Tabs>
         <Tab zoneid="lihAlzgwDr" title="Tencent Cloud - Enterprise Edition">
         <TabTitle>Tencent Cloud - Enterprise Edition</TabTitle>
         
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
         
         
         <div data-tips="true" data-tips-type="default">Only <strong>Tencent Cloud TCR Enterprise Edition</strong> can be migrated to BytePlus CR.</div>
         
         
         
         |**Parameter** |**Description** |
         |---|---|
         |Service address |The external source repository service address starting with `http(s)://`. For example, `https://test-sync.tencentcloudcr.com`. |
         |Access Key ID |Enter the SecretId from [Access Management > API Key Management](https://console.cloud.tencent.com/cam/capi) in the Tencent Cloud console. |
         |Secret Access Key |Enter the SecretKey from [Access Management > API Key Management](https://console.cloud.tencent.com/cam/capi) in the Tencent Cloud console. |
         |Repository type |Synchronization is only supported for artifacts in **image** repositories, not for those in Chart repositories. |
         |Namespace |The name of the namespace to be synchronized from Tencent Cloud TCR. Click Enter to confirm the namespace. |
         |Repository |The OCI artifact repository in the namespace of the external source repository to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact repositories in the specified namespace.<br><br>* **Regular expression matching**: Match the OCI artifact repositories to be synchronized by entering a regular expression rule. For configuration details, see [regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         |Tag |The OCI artifact tags to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact tags in the specified repository.<br><br>* **Regular expression matching**: Match the OCI artifact tags to be synchronized by entering a regular expression rule. For configuration details, see [regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         
         
         
         
         
         </Tab>
         <Tab zoneid="i1fhRJPuOC" title="Alibaba Cloud">
         <TabTitle>Alibaba Cloud</TabTitle>
         
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
         
         
         
         * <div data-tips="true" data-tips-type="warning">When you migrate image resources from Alibaba Cloud ACR to BytePlus CR, to prevent rate limiting on the source instance, the number of images synchronized in a single synchronization task must not exceed 20. We recommend that this number be kept within 15.</div>
         
         
         * <div data-tips="true" data-tips-type="warning">The Access Key ID must have at least the read\-only access permissions for Alibaba Cloud ACR (such as <a href="https://ram.console.aliyun.com/policies/AliyunContainerRegistryReadOnlyAccess/System/content">AliyunContainerRegistryReadOnlyAccess</a>), to prevent synchronization failures caused by insufficient permissions.</div>
         
         
         
         
         |**Parameter** |**Description** |
         |---|---|
         |API call address |The API service access address starting with `http(s)://`. For example, `https://cr.cn-beijing.aliyuncs.com`. |
         |Instance ID |The ID of the Alibaba Cloud ACR instance to be synchronized. |
         |Access Key ID |The account for accessing Alibaba Cloud OpenAPI. |
         |Secret Access Key |The key corresponding to the account for accessing Alibaba Cloud OpenAPI. |
         |Repository type |Synchronization is only supported for artifacts in **image** repositories, not for those in Chart repositories. |
         |Namespace |The name of the namespace to be synchronized from Alibaba Cloud ACR. Click Enter to confirm the namespace. |
         |Repository |The OCI artifact repository in the namespace of the external source repository to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact repositories in the specified namespace.<br><br>* **Regular expression matching**: Match the OCI artifact repositories to be synchronized by entering a regular expression rule. For configuration details, see [regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         |Tag |The OCI artifact tags to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact tags in the specified repository.<br><br>* **Regular expression matching**: Match the OCI artifact tags to be synchronized by entering a regular expression rule. Configuration details, see [regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         
         
         
         
         
         </Tab>
         <Tab zoneid="l2yenErDfQ" title="Harbor">
         <TabTitle>Harbor</TabTitle>
         
         
         |**Parameter** |**Description** |
         |---|---|
         |Service address |The external source repository service address starting with `http(s)://`. For example, `http://180.**.**.**`. |
         |Ignore certificate validity |Whether to ignore the validity of the certificate for the source repository.<br><br><br>* **Yes**: Ignore the validity of the external source repository certificate and synchronize the external repository to CR.<br><br>* **No**: Do not ignore the validity of the external source repository certificate. Synchronization cannot be executed if the certificate is outside its validity period. Select **No** for service addresses starting with `https`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The external source repository certificate must be issued by an authoritative institution. Otherwise, if <strong>No</strong> is selected for this parameter, synchronization will fail.</div><br> |
         |Username |The username for logging in to the Harbor repository. |
         |Password |The password for logging in to the Harbor repository. |
         |Namespace |The name of the project to be synchronized from the Harbor repository. |
         |Repository |The OCI artifact repository in the namespace of the external source repository to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact repositories in the specified namespace.<br><br>* **Regular expression matching**: Match the OCI artifact repositories to be synchronized by entering a regular expression rule. For configuration details, see [Regex Matching Examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         |Tag |The OCI artifact tags to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact tags in the specified repository.<br><br>* **Regular expression matching**: Match the OCI artifact tags to be synchronized by entering a regular expression rule. For configuration details, see [regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         
         
         
         
         
         </Tab>
         <Tab zoneid="sFjS1zEQ9P" title="AWS">
         <TabTitle>AWS</TabTitle>
         
         
         |**Parameter** |**Description** |
         |---|---|
         |Service address |The external source repository service address starting with `http(s)://`. For example, `http(s)://index.dockrhub.io`. |
         |Ignore certificate validity |Whether to ignore the validity of the certificate for the source repository.<br><br><br>* **Yes**: Ignore the validity of the external source repository certificate and synchronize the external repository to CR.<br><br>* **No**: Do not ignore the validity of the external source repository certificate. Synchronization cannot be executed if the certificate is outside its validity period.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The external source repository certificate must be issued by an authoritative institution. Otherwise, if <strong>No</strong> is selected for this parameter, synchronization will fail.</div><br> |
         |Access Key ID |The Access Key ID of the AWS account. |
         |Secret Access Key |The Secret Access Key of the AWS account. |
         |Repository |The OCI artifact repository in the namespace of the external source repository to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact repositories in the specified namespace.<br><br>* **Regular expression matching**: Match the OCI artifact repositories to be synchronized by entering a regular expression rule. For configuration details, see [Regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         |Tag |The OCI artifact tags to be synchronized.<br><br><br>* **All**: Synchronize all OCI artifact tags in the specified repository.<br><br>* **Regular expression matching**: Match the OCI artifact tags to be synchronized by entering a regular expression rule. For configuration details, see [Regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         
         
         
         
         
         </Tab>
         <Tab zoneid="Episnp8Joy" title="Docker">
         <TabTitle>Docker</TabTitle>
         
         &nbsp;
         
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
         
         
         <div data-tips="true" data-tips-type="warning">Docker Hub imposes image pull rate limits on free users. Exceeding such limits may result in synchronization failures. The recommended configuration methods are as follows:</div>
         
         
         
         * <div data-tips="true" data-tips-type="warning">Use exact <strong>regular expression matching</strong> instead of fuzzy matching to avoid pulling unnecessary images. For example, enter <code>nginx</code> in the <strong>Repository</strong> field. In the <strong>Tag</strong> field, select "Regular expression matching" and enter <code>^v1.0.0$</code> .</div>
         
         
         * <div data-tips="true" data-tips-type="warning">Set the synchronization interval to longer than 6 hours to prevent rate limiting caused by frequent image pulls.</div>
         
         
         * <div data-tips="true" data-tips-type="warning"></div>
         
         
               
               |**Parameter** |**Description** |
               |---|---|
               |Access address |This parameter is fixed as `https://hub.docker.com`. |
               |Username |The username for logging in to the Docker Hub repository.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to use the registered username of the Docker Hub repository to log in. Logging in with an email address is not supported.</div><br> |
               |Password |The password for logging in to the Docker Hub repository. |
               |Type |Public repositories and personal repositories can be synchronized:<br><br><br>* **library**: Synchronize public Docker Hub repositories to obtain base images such as `nginx` and `ubuntu`.<br><br>* **Personal repository**: Synchronize Docker Hub repositories in your personal account. |
               |Namespace |The name of the namespace to be synchronized from the Docker repository.<br><br><br>* **library (public repository)** : Fixed as **library**.<br><br>* **Personal repository**: Corresponds to **an account and its associated organization** in Docker Hub. |
               |Repository |The OCI artifact repository in the namespace of the external source repository to be synchronized.<br><br><br>* **library (public repository):** <br><br><br>Only exact repository name matching is supported. You must correctly enter the name of the public repository, such as `nginx`, `ubuntu`, `python`, `redis`, and more.<br><br><br>* **Personal repository:** <br><br>   * All: Synchronize all OCI artifact repositories in the specified namespace.<br><br>   * Regular expression matching: Match the OCI artifact repositories to be synchronized by entering a regular expression rule. For configuration details, see [regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
               |Tag |The OCI artifact tags to be synchronized.<br><br><br>* **library (public repository):** <br><br>   * latest: The latest tag of the OCI artifact. By default, the `latest` tag is synchronized.<br><br>   * Regular expression matching: Match the OCI artifact tags to be synchronized by entering a regular expression rule. You can enter `.*` to synchronize all tags. For configuration details, see [regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en).<br><br>* **Personal repository:** <br><br>   * All: Synchronize all OCI artifact tags in the specified repository.<br><br>   * Regular expression matching: Match the OCI artifact tags to be synchronized by entering a regular expression rule. For configuration details, see [regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
               
         
         
         
         
         </Tab>
         <Tab zoneid="C9kPJHZTXP" title="Docker Registry">
         <TabTitle>Docker Registry</TabTitle>
         
         
         |**Parameter** |**Description** |
         |---|---|
         |Service address |Enter the service address of the source instance. |
         |Ignore certificate validity |Whether to skip the validation of SSL/TLS certificate validity to avoid errors. |
         |Image pull authentication |Whether to enable authentication for image pulling. To pull private images, you need to enable authentication and enter the username and password. |
         |Username |Enter the username for logging in to the repository. |
         |Password |Enter the password for logging in to the repository. |
         |Namespace |Enter the name of the namespace to be synchronized from the repository.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can enter only one namespace for each rule.</div><br> |
         |Repository |Enter the OCI artifact repository in the namespace of the external source repository to be synchronized. You can enter multiple OCI artifact repositories. |
         |Tag |Enter the OCI artifact tags to be synchronized.<br><br><br>* All: Synchronize all OCI artifact tags in the specified repository.<br><br>* Regular expression matching: Match the OCI artifact tags to be synchronized by entering a regular expression rule. Configuration details, see [regex matching example](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         
         
         
         
         
         </Tab>
         <Tab zoneid="AuPV5QFCkF" title="Google Cloud">
         <TabTitle>Google Cloud</TabTitle>
         
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
         
         
         
         * <div data-tips="true" data-tips-type="warning">Only the China (Hong Kong), Asia Pacific (Johor), and Asia Pacific (Jakarta) regions support the registry replication feature for GAR.</div>
         
         
         * <div data-tips="true" data-tips-type="warning">To migrate Google Cloud public images, select <strong>Source instance</strong> \> <strong>Source</strong> and then select <strong>Docker Registry</strong>.</div>
         
         
         
         
         |**Parameter** |**Description** |
         |---|---|
         |Service address |The external source repository service address starting with `http(s)://`. For example, `https://southamerica-west1-docker.pkg.dev`. |
         |Username |It is automatically obtained. You do not need to enter it. |
         |Access key |The Google Cloud Platform (GCP) access key. Create a service account and generate a key on the [GCP Service Accounts page](https://console.cloud.google.com/projectselector2/iam-admin/serviceaccounts/create). You must obtain at least the Artifact Registry Reader role and add the `resourcemanager.projects.get` permission. |
         |Repository type |This parameter is fixed as **Image**. |
         |Namespace |The namespace in the GAR project, corresponding to the code `repository` in GAR. |
         |Project name |Enter the project name in GCP. |
         |Repository |The images to be synchronized.<br><br><br>* **All**: Synchronize all images in the specified namespace.<br><br>* **Regular expression matching**: Match the images to be synchronized by entering a regular expression rule. Configuration details, see [regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         |Tag |The image tags to be synchronized.<br><br><br>* **All**: Synchronize all image tags in the specified repository.<br><br>* **Regular expression matching**: Match the image tags to be synchronized by entering a regular expression rule. For configuration details, see [Regex Matching Examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
         
         
         
         
         
         </Tab>
         </Tabs>
         

      * Target instance

         
         |**Parameter** |**Description** |
         |---|---|
         |Instance name |Select the target Standard Edition instance in CR. The external repository will be synchronized to this Standard Edition instance. |
         |Namespace |Select the target namespace in the Standard Edition instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not configure this parameter, synchronization will default to the namespace that has the same name as the namespace in the source repository.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not configure this parameter and a namespace with the same name does not exist, a namespace with the same name will be created by default in the target instance.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the source instance is of Docker type and library is selected, synchronization defaults to the library namespace. If the library namespace does not exist, it will be created by default.</div><br> |
         

* **Synchronization rules**

   
   |**Parameter** |**Description** |
   |---|---|
   |Image overwriting |You can select "Enable" to enable this feature. When this feature is enabled, if an image with the same name as an image in the external repository exists in the target Standard Edition instance, the image from the external repository will overwrite the existing image with the same name in the target instance. |
   |Rule state |You can select "Enable" to enable the rule and configure the following trigger conditions based on your needs:<br><br><br>* **Timed trigger**: Synchronization is triggered at the configured fixed intervals, with the first synchronization time set by the user.<br><br>   * **First trigger time**: Take note that this parameter can only be set to any time starting from the current time.<br><br>   * **Trigger frequency**: Specify the synchronization interval. By default, synchronization is triggered every 24 hours. The valid interval ranges from 1 to 720 hours.<br><br>* **Manual trigger**: If this option is selected, the rule will not be triggered automatically and synchronization must be executed manually. |
   


<span id=".5q2l6aqk5LqM77ya5omn6KGM5ZCM5q2l6KeE5YiZ"></span>
### Step 2: Execute the registry replication rule

The following two trigger methods are supported:


* If you select **Timed trigger** when you configure the registry replication rule, the system will automatically trigger synchronization at scheduled intervals.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also manually trigger a timed trigger registry replication rule.   </div>
   

* If **Manual trigger** is selected, you can manually trigger the rule by referring to the following steps:

   1. In the left navigation pane of the [CR console](https://console.byteplus.com/cr), select **Registry replication**.

   2. On the **Registry replication** page, locate the rule to be triggered, and click **Trigger** in the **Actions** column.

   3. In the system pop\-up dialog box, verify the rule information, and click **Confirm** to trigger the synchronization operation.


<span id=".5q2l6aqk5LiJ77ya5p-l55yL5ZCM5q2l5pel5b-X"></span>
### Step 3: View synchronization logs


1. In the left navigation pane of the [CR console](https://console.byteplus.com/cr), select **Registry replication**.

2. On the **Registry replication** page, locate the target rule and click the rule name.

3. On the rule details page, click the **Synchronization log** tab to view all synchronization logs of the rule.

   
   |Parameter |Description |
   |---|---|
   |Task ID |The synchronization task ID (unique within the instance). |
   |Synchronization state |The task state, which can be Running, Succeed, and Failed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the synchronization state is <strong>Succeed</strong>, the synchronization task is triggered as expected and at least one OCI artifact tag is synchronized.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the synchronization state is <strong>Failed</strong>, the task fails to be triggered. Possible causes:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The network between CR and the external source repository is unreachable.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The address of the external source repository does not exist.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The username or password for the external source repository is incorrect.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The password for the external source repository has expired.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The namespace in the target Standard Edition instance does not exist.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The target Standard Edition instance is not in <strong>Running</strong> state.</div><br> |
   |Task duration |The time consumed to complete all synchronization tasks. |
   |Success rate |(Number of  synchronized tags/Total number of tags to be synchronized) × 100% |
   |Number of synchronization repositories |The number of OCI artifact repositories to be synchronized by the current task. |
   |Trigger time |The trigger time of the synchronization task. |
   

4. Click the task ID to view the details of the synchronization task. The following information is displayed: `[namespace]/[repo]:tag` of the source instance, `[namespace]/[repo]:tag` of the target instance, and synchronization state of the synchronization task.

   If the synchronization state is **Succeed**, the artifacts have been successfully synchronized from the source instance to the target instance. If the synchronization state is **Failed**, the artifacts fail to be synchronized from the source instance to the target instance.
