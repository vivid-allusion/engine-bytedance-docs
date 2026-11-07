---
title: "Limiting the instance scope of IAM user management by tags"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Limiting_the_instance_scope_of_IAM_user_management_by_tags"
---

You can bind tags to different PostgreSQL instances, then authorize different IAM users by tags through custom IAM permission policies. This restricts IAM users from viewing or managing only PostgreSQL instances with specified tags.

<span id="FAFRU9KE"></span>
## Precautions


* IAM users with configured tag permission restrictions: the instance list is empty by default when they first enter the instances page. Manual tag filtering is required, after which the instance list with corresponding permissions is displayed.

* IAM users without configured tag permission restrictions: all instances are displayed by default when first entering the instances page, but they can only access the details pages of authorized instances and cannot view instances without permissions. After manual tag filtering, only instances bound with the corresponding tags are displayed.


<span id="vLWxNoeX"></span>
## Procedure

Take IAM user `Account-user` as an example, allowing management only of PostgreSQL instances tagged with `Department:RD`, with no permissions to view or manage other PostgreSQL instances.


1. Log in to the console using the root account.

2. [Create an IAM user](https://docs.byteplus.com/en/docs/6257/64977?lang=en#%E6%96%B0%E5%BB%BA%E7%94%A8%E6%88%B7). The IAM user in this topic is `Account-user`.

3. [Authorize the IAM user](https://docs.byteplus.com/en/docs/6257/64977?lang=en#%E7%AE%A1%E7%90%86%E7%94%A8%E6%88%B7). This topic grants view and management permissions for PostgreSQL instances.

   1. Create a custom permission policy. The policy names in this topic are `TagPermissionPolicy` and `PostgresqlPolicy`.

      * `TagPermissionPolicy`: grants the IAM user permissions for the tag service to ensure normal use of the tag service. Otherwise, the user cannot filter tags.


```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tag:GetTags",
        "tag:GetTagKeys",
        "tag:GetTagValues",
        "tag:Resources"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```



      * `PostgresqlPolicy`: grants the IAM user instance management permissions with the tag `Department:RD`.


```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "rds_postgresql:*"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "volc:RequestTag/Department": "RD"
                }
            }
        }
    ]
}
```



   2. Grant the IAM user the custom policies `TagPermissionPolicy` and `PostgresqlPolicy`.


<span id="0CkSWoZV"></span>
## Result verification


1. Log in to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg) using IAM `Account-user`.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. On the **Instances** page, click the filter icon on the right of the **Tag** column.

4. In the pop\-up text box, set the tag key and tag value for filtering.

   * When first entering the instances, it is empty by default with a prompt indicating no permission.

   * Manually filter PostgreSQL instances with the tag `Department:RD`, and the filtered list shows instances you have permission for.


&nbsp;

&nbsp;
