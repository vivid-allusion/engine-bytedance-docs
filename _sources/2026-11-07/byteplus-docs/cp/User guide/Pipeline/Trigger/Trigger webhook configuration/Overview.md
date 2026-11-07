---
title: "Overview"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Trigger_events_and_trigger_conditions"
---

This article introduces the trigger events supported by code source triggers, what each trigger event means, and the rules for matching trigger conditions.


* **Trigger event**

   By configuring trigger events, you can filter Webhook events of the code source. The trigger events supported by each code source are as follows.

   
   | |GitLab |GitHub |BitbucketCloud |
   |---|---|---|---|
   |Push code |✔️ |✔️ |✔️ |
   |Create a tag |✔️ |✔️ |✔️ |
   |After the merge request is completed |✔️ |✔️ |✔️ |
   |Create or update merge requests |✔️ |✔️ |✔️ |
   |Create patch sets |❌ |❌ |❌ |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">General Git and Perforce code sources do not directly support the code source trigger function. To enable code source event triggers, configure <a href="https://docs.byteplus.com/en/docs/cp/General_webhook_trigger">standard Webhook trigger</a>, and additionally specify which events to send in your code repository settings.   </div>
   

* **Trigger conditions**

   Each trigger event can be configured with its corresponding conditions. Trigger conditions are usually branch names or TAG keywords. By setting trigger conditions, you can further filter the Webhook events of the code source.


<span id=".5Luj56CBLXB1c2g="></span>
## Code push


* Code push: Any push event in the repository will trigger the pipeline to run. For example: pushing a local branch to the corresponding remote branch, modifying files on the code management platform, and more. The pipeline runs on the target branch of the push.

* When the target branch of the push successfully matches the trigger condition, the pipeline is triggered.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Codeup code source supports adding <strong>file path</strong> as a filter condition for code push events. After adding a file path, only Push events in specific code paths can trigger the pipeline.</div>



* <div data-tips="true" data-tips-type="tip">The file path defaults to a path under the root directory, so there is no need to start with<code>/</code>Beginning.</div>


* <div data-tips="true" data-tips-type="tip">Multiple file paths can be specified, and regular expressions are supported. The matching rules are the same as those for trigger conditions described below in <strong>Trigger condition matching rules</strong>.</div>


* <div data-tips="true" data-tips-type="tip">When both the trigger condition for code Push and the file path are added, the filter applies an AND relationship. For example, the trigger condition for a code push is a push to the Master branch, with the file paths set to demo/a.txt and demo/b.txt. The pipeline is triggered only when a Push event occurs for demo/a.txt or demo/b.txt under the Master branch.</div>



<span id=".dGFnLeWIm-W7ug=="></span>
## Create a tag


* TAG creation: Creating or updating a TAG in the repository triggers pipeline execution, and the target TAG is used as the code version for the pipeline run.

* TAG creation + trigger condition: When the name of a TAG that is created or updated matches the trigger condition, the pipeline is triggered to run.


<span id=".5ZCI5bm26K-35rGC5a6M5oiQ5ZCO"></span>
## After the merge request is completed


* After a merge request is completed, a merge request event created in the code source will trigger the pipeline to run. For example, initiate a merge request from the remote Dev branch (source branch) to the Master branch (target branch). Code Pipeline matches the target branch of the merge request with the Filter. If the match is successful, it triggers the pipeline and uses the **Master branch (target branch)**  as the branch for pipeline execution.

* After the merge request is completed – Trigger condition: When the target branch into which the merge is made matches the trigger condition, the pipeline runs.


<span id=".5ZCI5bm26K-35rGC5paw5bu6LeabtOaWsA=="></span>
## Create or update merge requests


* Merge request creation/update: Creating a merge request event in the code source will trigger the pipeline to run. For example, initiate a merge request from the remote Dev branch (source branch) to the Master branch (target branch). Code Pipeline matches the target branch of the merge request against the filter criteria. If the match is successful, the pipeline is triggered, and the **Dev branch (source branch)**  is used as the branch during pipeline execution.

* Merge request creation or update and trigger condition: When the source branch matches the trigger condition, the pipeline runs.


<span id=".6KGl5LiB6ZuG5Yib5bu6"></span>
## Create a patch set


* Patch set creation: After a new patch set is created in the repository, the pipeline is triggered to run. The branch on which the pipeline runs is the branch used to create the patch set.

* Patch set creation and trigger conditions: When the branch used to create a patch set matches the trigger conditions, the pipeline is triggered.


<span id=".6Kem5Y-R5p2h5Lu255qE5Yy56YWN6KeE5YiZ"></span>
## Matching rules for trigger conditions


* The matching rules for each trigger condition are as follows:

   * If the trigger condition expression does not contain special metacharacters, it is considered an **exact match**.

   * If the following special metacharacters are present, it is considered **a Golang regular expression match**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The metacharacters in Golang regular expressions are:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Basic metacharacters:<code>.</code>,<code>\</code>,<code>*</code>,<code>+</code>,<code>?</code>,<code>^</code>,<code>$</code>, <code>[]</code>,<code>{}</code>,<code>|</code>, <code>()</code>   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Complex metacharacters: <code>[^]</code>, <code>[-]</code>, <code>(?:)</code>, <code>(?!)</code>, <code>(?=)</code>, <code>(?<=)</code>, <code>(?<!)</code>   </div>
   

   For example:

   
   |Trigger event |Trigger conditions ||Meaning |
   |---|---|---|---|
   |Code push |`feature` ||**Exact match**: Only code submitted to the `feature` branch will trigger the pipeline to run. |
   |Code push |`^feature$` ||**Regular expression matching**: Only code submitted to the `feature` branch will trigger pipeline execution. |
   |Code push |`feature\|dev\|sit` ||**Regex match**: Any code submission to a branch whose name contains `feature`, `dev`, or `sit` will trigger the pipeline. |
   |Create a tag |`v1.0` ||**Regular expression matching**:`.`Matches any single character except for the newline character. Therefore, creating a TAG such as `v1.0`, `v1a0`, or `v110` will trigger the pipeline to run. |
   |Create a tag |`^v1\.0$` ||**Regex matching**: The pipeline is triggered only by the creation of a TAG for `v1.0`. |
   |Create a TAG |`^SNAPSHOT-V.*` ||**Regular expression match**: The creation of any TAG with the `SNAPSHOT-V` prefix will trigger pipeline execution. |
   

* Allows you to add multiple trigger conditions, which are connected by an "or" relationship.

   For example:

   
   |Trigger event |Trigger condition 1 |Trigger condition 2 |Meaning ||
   |---|---|---|---|---|
   |Push code |`feature` |`dev` |Submitting code to the `feature` branch or the `dev` branch will trigger the pipeline to run. ||
   |Push code |`^feature.*` |`^dev.*` |Submitting code to any branch whose name starts with `feature` or `dev` will trigger the pipeline. ||
