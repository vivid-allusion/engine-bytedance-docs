---
title: "What is the policy syntax"
product: "BytePlus IAM"
product_code: "IAM"
source: "https://docs.byteplus.com/en/docs/IAM/what-is-the-policy-syntax"
---

Policies are described through PolicyDocument in JSON format. A policy syntax includes the following elements:


|**Element** |**Description** |
|---|---|
|Statement |The `Statement` element is the main and required element of a policy. It can contain an individual statement only or an array of individual statements.<br><br>Each individual statement block must be placed in curly brackets ({ }). For multiple statements, the array must be placed in square brackets ([ ]). |
|Effect |The `Effect` element is required. It indicates the result of the statement. Its valid values are `Allow` or `Deny`. |
|Action |The `Action` element describes the specific action. It has the same meaning as the `Action` element in cloud service API. Therefore, when describing the `Action`, element, it is necessary to describe the specific cloud service in the prefix `{service}:{action}`. `*` and `?` are supported when describing the `Action` element. |
|Resource |The `Resource` element specifies the resource that the `Action` element covers. It is described in TRN format: `trn: {service}:{region}:{account}: {resourceType}/{id}`.<br><br>***Note***: For resource\-based policies, the `Resource` element has been specified in the relationship between the policy and resource, so this element will be excluded.<br><br>The format descriptions are as follows:<br><br><br>* `trn`: The required prefix.<br><br>* `{service}`: The abbreviation of the cloud service's name. Refer to the product documentation for this field.<br><br>* `{region}`: The region where the cloud service is deployed.<br><br>* `{account}`: The account that the cloud resource belongs to.<br><br>* `{resourceType}`: The type of cloud resource. Refer to the product documentation for this field.<br><br>* `{id}`: The ID of cloud resource.<br><br>   For example: If the ID of an account is `3000000001` and the account creates an IAM user named `Bob`, the `Resource` element would be `trn:iam::3000000001:username/Bob`.<br><br>   ***Note***: IAM is a global service instead of a region\- specific service, so the `{region}` element is empty here. |
|Principal |The `Principle` element specified the identity that is given or denied the access to a cloud resource. It is also described in TRN format.<br><br>***Note***: For identity\-based policies, the `Principal` element has been specified in the relationship between the policy and identity, so this field will be excluded. |


In the following syntax sample, the permission to get the details of a user named Bob is defined.

```text
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iam:GetUser"
      ],
      "Resource": [
        "trn:iam::3000000001:user/Bob"
      ]
    }
  ]
}
```
