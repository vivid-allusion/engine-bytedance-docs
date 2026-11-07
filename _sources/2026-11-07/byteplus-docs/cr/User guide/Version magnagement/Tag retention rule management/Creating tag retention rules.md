---
title: "Creating tag retention rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/create-a-tag-retention-rule"
---

Tag management enables you to manage image tags automatically within an instance, namespace, or OCI artifact repository. Tags not covered by a retention policy are cleared automatically. This topic describes how to create a tag retention rule.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This action applies only to Standard instance and does not apply to proxy repository.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created a CR instance. For details, see [Create Standard Edition instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The first pushed image version has a two\-hour version protection period during which it will not be cleaned up.</div>


* <div data-tips="true" data-tips-type="warning">After a tag retention rule is executed, all image tags (both existing and new) that are excluded by the rule are cleared automatically.</div>


* <div data-tips="true" data-tips-type="warning">The storage space of cleared image tags is released within 1 to 5 hours after the task is completed.</div>


* <div data-tips="true" data-tips-type="warning">A maximum of 10 retention rules can be enabled. Any new rules created beyond this limit will be in a disabled state. To enable a new rule, first disable or delete an existing one.</div>


1. Log in to the [CR console](https://console.byteplus.com/cr).

2. In the left navigation bar, click **Tag retention**.

3. On the **Tag retention rule** page, click **Create tag retention rules**.

4. Fill in the tag retention rules configuration information.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |Name |The custom name of the tag retention rule. |
      |Description |Enter the description of the tag retention rule. |
      

   * **Effective scope**

      
      |Parameter |Description |
      |---|---|
      |Effective level |The level at which the image retention rule is applied. Options: Instance, Namespace, and OCI artifact repository.<br><br><br>* Instance: Defines the image tag retention rule based on the instance dimension, and clears existing and new image tags not covered by the rule.<br><br>* Namespace: Defines the image tag retention rule based on the namespace dimension, and clears existing and new image tags not covered by the rule.<br><br>* OCI artifact repository: Defines the image tag retention rule based on the OCI artifact repository dimension, and clears existing and new image tags not covered by the rule. |
      |Instance |Select the instance to which the retention rule applies. |
      |Namespace |Select the namespace to which the retention rule applies. |
      |OCI artifact repository |Select the OCI artifact repository where the retention rule takes effect. This option is only supported when **Effective scope** is set to **OCI artifact repository**. |
      

   * **Rule settings**

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The retention rule is applied independently to each OCI artifact repository. For example, if you set the rule to retain the 30 most recently pushed tags, up to 30 tags are retained in each selected OCI artifact repository.      </div>
      

      
      |Parameter |Description |
      |---|---|
      |Retention rule |You can combine the condition\-based rule and the regex matching\-based rule using **OR** or **AND** logic.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">An image is considered <strong>Pull</strong> if a <code>get manifest</code> request exists. This includes scenarios where pipeline build uses a local cache, or where <code>kubectl</code> image pulls involves local cache. A <code>head manifest </code>request alone is not counted as a pull. Whether an image was recently pulled is determined by the pull time of the image tag.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Not retained images cannot be recovered after cleanup. Do not configure <strong>pull</strong>\-based retention policies if you are unsure about client behavior (such as whether local image caches are being used), as cleanup might cause service impact.</div><br><br><br>* By version count or days:<br><br>   * By version count: Retains a specified number of the most recently pushed or pulled tags.<br><br>   * By days: Retains tags that have been pushed or pulled within a specified number of days.<br><br>* Regular expression matching: Retains image tags that match the specified regular expression. The matching object of the regex pattern is the image tag name, such as `latest `or `v1`. For common regex matching examples, see [Regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en).<br><br>* Automatically delete empty OCI artifact repositories: When this feature is enabled, the system automatically deletes an OCI artifact repository when all its image tags are cleaned up based on retention rules. |
      |Rule state |Specifies whether the tag retention rule is enabled or disabled. |
      |Trigger rule |Select how the tag retention rule is triggered: manually or automatically on a schedule.<br><br><br>* Manual trigger: To clear specified image tags, you need to trigger the rule manually for execution.<br><br>* Timed trigger: Supports both manual and timed triggers. For a timed trigger, configure the following:<br><br>   * First trigger time: Select the time for the first automatic cleanup of the images not covered by the rule.<br><br>   * Trigger frequency: Select the trigger cycle for cleaning images. |
      

5. After the configuration is complete, click **Confirm**.
