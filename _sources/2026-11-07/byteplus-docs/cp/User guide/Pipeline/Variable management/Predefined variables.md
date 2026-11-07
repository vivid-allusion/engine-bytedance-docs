---
title: "Predefined variables"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Predefined_variables"
---

System\-defined variables are built\-in variables that help customize pipeline workflows. Preset variables do not need to be created in advance and cannot be modified or deleted. Code Pipeline currently provides the following commonly used predefined variables.


|Variable name |Description |
|---|---|
|CP_WORKSPACE |Pipeline task workspace path. |
|WORKSPACE_ID |Workspace ID. |
|DATETIME |The variable uses the current time in the UTC time zone. For example, 20220223110105 indicates that the current UTC time is 11:01:05 on February 23, 2022. |
|PIPELINERUN_ID |Pipeline run record ID. |
|PIPELINE_ID |Pipeline ID. |
|PIPELINE_NAME |Pipeline name. |
|SCM_BRANCH |The run branch name. |
|SCM_TAG |Tag that triggers pipeline execution.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">SCM_TAG only has a value when the pipeline is triggered by the code source and the trigger event is tag creation.</div><br> |
|SCM_COMMIT_ID |The revision version number for the running branch is the complete commit ID. For example: 1e872b59013425b7c404a91d16119e8452b983f2. |
|SCM_COMMIT_ID_SHORT |The revision number of the running branch is the first seven characters of the commit ID. For example: 1e872b5. |
|P4_SHELVE_ID |Applicable only to Perforce code sources; identifies shelved file identifiers. |
|ACCOUNT_ID |BytePlus account (main account) ID. |
|USER_ID |Sub\-user (IAM user) ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Manually run the pipeline and display the actual trigger user ID. If the operator is the main account, USER_ID is 0; if the operator is an IAM user, USER_ID is the current IAM user ID.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The trigger activates the pipeline. The trigger creator ID is displayed. If the creator is the main account, USER_ID is 0; if the creator is an IAM user, USER_ID is the current IAM user ID.</div><br> |
