---
title: "Code source branching model"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Code_source_branching_model"
---

With the pipeline branch model, Code Pipeline automates the creation and merging of integration branches for you. You only need to focus on the feature branches that are ready for integration and release, allowing you to efficiently manage your code branches.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

The branch model is a core method for managing code changes in version control systems. By defining the roles of different branches and establishing merging rules, it enables team collaboration, feature development, integration testing, and release management.


|Type |Descriptions |
|---|---|
|Basic branches |Typically, `master` or `main` is used as the base branch. Because `master` or `main` usually represents the newest and most complete code in various branch models. |
|Feature branches |A feature branch is created from the base branch `master` or `main`, and is used to implement a requirement or fix a bug. Developers typically perform complete development and testing on feature branches. Integration and release of multiple feature branches should only proceed when the quality of the feature branches has been assessed as relatively good. |
|Integration branches |Before releasing a branch, you need to create an integration branch from the latest code of the base branch `master` or `main`. Then, merge the feature branches one by one, and perform integration testing and deployment. After the release, it is recommended to merge the integration branch into the base branch.<br><br>Integration groups support the following features:<br><br><br>* During the integration process, new feature branches can continually be added for integration and verification.<br><br>* When issues arise during integration, developers can continue to fix them in their own feature branches. After the issue is resolved, redeploy and retest.<br><br>* If an issue with a feature branch for a particular feature cannot be resolved, you can remove the corresponding feature branch from the integration branch set. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The main branch and sub\-branches have been created in the code repository.

* A code source has been created in Code Pipeline. For details on actions, see [Connect code source](https://docs.byteplus.com/en/docs/cp/Create_a_code_source).

* The pipeline has been created. For details about the operations, see [Create pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">On first run, by default, an integration branch is created based on the base branch configured in the branch manager.</div>


* <div data-tips="true" data-tips-type="tip">The pipeline will lock the commits of the corresponding integration branch after branch management has been executed. During pipeline task execution, if the <strong>download code</strong> feature is configured, the code from the commit record locked by the branch manager will be used for execution.</div>



<span id=".56ys5LiA5q2l77ya5byA5ZCv5YiG5pSv5qih5byP"></span>
### Step 1: Turn on branch mode


1. In the code source configuration of the pipeline, turn on **branch mode**.

2. At the **branch integration** node, select the **base branch** under branch management.


<span id=".56ys5LqM5q2l77ya6L-Q6KGM5rWB5rC057q_"></span>
### Step 2: Run the pipeline

After you turn on branch mode, you can select different branches for integration.


1. On the pipeline details page, click **Run now**.

2. On the **pipeline run** configuration page, select the branch to be integrated.

3. Run succeeded. View branch integration status.

4. (Optional) Resolving issues by following the prompts is supported when execution fails due to a conflict. After the issue is resolved, click **Mark as resolved** to automatically retry and complete branch integration.
