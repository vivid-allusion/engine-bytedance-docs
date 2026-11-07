---
title: "Migration Issues"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Migration-issues"
---

This article summarizes common questions you may have when using the Storage Migration Service.

<span id=".5Li65LuA5LmI6L-B56e75pWw5o2u5YiwLXRvcy3lkI7vvIx0b3Mt5o6n5Yi25Y-w5bGV56S655qE5paH5Lu25L-u5pS55pe26Ze05piv6L-B56e75pWw5o2u55qE5pe26Ze077yf"></span>
### Why is the file modification time displayed on the TOS console the time of data migration after migrating data to TOS?

Starting from July 18, 2023, when migrating data, the last modified time of the source files will no longer be preserved. After migrating to TOS, the file modification time displayed on the TOS console will change from inheriting the last modified time of the source files to being consistent with the migration time.

<span id=".5Lu75Yqh5Ye6546w6L-B56e75aSx6LSl5pe277yM5aaC5L2V5aSE55CG77yf"></span>
### How to handle migration failure when a task occurs?

You can click **Download the migration report** in the **operation** column of the target task in the task list to view detailed error reasons in the migration report and then proceed with the corresponding handling.

<span id=".5aaC5L2V5p-l55yL6L-B56e76L-b5bqm77yf"></span>
### How to check migration progress?

You can click on the task name that you want to check the progress of in the task list, and enter the task details page to view the migration progress.

<span id=".5aaC5L2V6aKE5Lyw6L-B56e75pe26Ze077yf"></span>
### How to estimate migration time?

When creating a migration task, you can set the maximum migration speed. However, the actual migration speed during the migration process is closely related to the network conditions at that time, and it is difficult to make a precise prediction before the migration.

During the migration process, the storage migration service will calculate the estimated completion time based on the actual speed and the total size of the files to be migrated, for your reference.

**What is the difference between classic mode and cross\-service authorization model?** 

The functionalities achieved by the classic mode and the cross\-service authorization model are the same. By using the cross\-service authorization model to migrate the object storage buckets under the current account, detailed information such as AccessKey ID and AccessKey Secret does not need to be set. With your authorization, the data migration service can directly access the list of storage buckets, read files and write files.

<span id=".5L2_55So5a2Q6LSm5Y-35Yib5bu66L-B56e75Lu75Yqh5pe277yM6Leo5pyN5Yqh5o6I5p2D5aSx6LSl5oCO5LmI5Yqe77yf"></span>
### What should I do if cross\-service authorization fails when using a sub\-account to create a migration task?

When you use a sub\-account to create a migration task, cross\-service authorization requires the sub\-account to have the permission to create IAM policies. For more information, please refer to [About policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).

The strategy content is as follows:

```json
{
  "Statement":[
    {
      "Effect":"Allow",
      "Action":[
        "iam:CreateRole",
        "iam:CreatePolicy",
        "iam:AttachRolePolicy",
        "iam:DetachRolePolicy",
        "iam:ListEntitiesForPolicy",
        "iam:DeletePolicy",
        "iam:ListRoles"
        ],
        "Resource":[
          "*"
        ]
    }
  ]
}
```
