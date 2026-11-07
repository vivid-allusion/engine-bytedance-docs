---
title: "Creating tag immutability rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/create-a-version-immutable-rule"
---

CR offers tag immutability rules. This prevents pushed image tags from being overwritten by subsequent pushes, thereby mitigating the risk of accidental image tag overwrites.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This action is only applicable to Standard instances and is not supported for proxy repositories.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* Image tags that match a tag immutability rule cannot be deleted manually or by [tag retention rules](https://docs.byteplus.com/en/docs/cr/create-a-tag-retention-rule?lang=en). If you need to delete a corresponding tag, modify or delete the tag immutability rule so that it no longer applies to the target image tag.

* You can enable a maximum of 15 tag immutability rules. Once the limit is reached, no new rules can be created.


<span id="XoQHgpwp"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar of the instance page, click **tag immutability**.

3. On the **Tag immutability** page, click **Create tag immutability rule**.

4. Fill in the rule configuration information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default configuration is that all image tags in the repository except for the <code>latest</code> tag are immutable.   </div>
   

   
   |Configuration item |Description |
   |---|---|
   |Name |A custom name of the tag immutability rule. |
   |Description |A custom description of the tag immutability rule. |
   |Effective namespace |Select the namespace to which the rule applies. You can only select one namespace per rule. |
   |OCI artifact repository |Filter the target OCI artifact repository and artifact repository tag. Both **Match **  and **Exclude **  modes are supported. Multiple expressions are separated by a comma (`,`). The following matching methods are supported:<br><br><br>* Exact matching: Precisely match the specified name, for example, `myrepo`.<br><br>* Full matching: Match all repositories or tags by entering `**`.<br><br>* Prefix matching: Match names that start with the specified characters, for example, `repo*`.<br><br>* Suffix match: Match names ending with specified characters, for example `*repo`.<br><br>* Part match: Match names with specified characters at the beginning and end, and any characters in between, for example `r*po`. |
   |Tier ||
   |Enable now |Specifies whether to enable the rule upon creation. |
   

5. Click **confirm** to complete the operation.
