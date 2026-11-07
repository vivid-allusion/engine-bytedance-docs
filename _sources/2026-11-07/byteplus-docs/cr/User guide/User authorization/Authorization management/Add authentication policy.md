---
title: "Add authentication policy"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/authentication"
---

This topic describes how to authorize IAM users to access Container Registry (CR) resources and the relevant authentication policies.

<span id=".6LWE5rqQ5o-P6L-w"></span>
## Resource description

For IAM\-based authorization, resources are described in the following format:


|Resource type |Resource description in authentication policy |
|---|---|
|repository |trn:cr:$regionid:$accountid:repository/$instance/$namespace/$repository |


Parameter descriptions are as follows:


|Parameter |Description |
|---|---|
|$regionid |Region ID. Use` * `to match all regions. |
|$accountid |BytePlus account ID. Use` * `to match any account. |
|$instance |Name of the CR Standard Edition instance. |
|$namespace |Name of the namespace. |
|$repository |Name of the OCI artifact repository. |


<span id=".6Ym05p2D6KeE5YiZ"></span>
## Authentication rules

When an IAM user calls the CR API, the service requests an authentication check from IAM. The permissions required for an API call are dynamically determined based on the resources involved and the semantics of the API. The authentication rules for each API are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can use the <a href="https://console.byteplus.com/iam/policymanage/policy/new">visual editor for custom policies </a> to create custom policies.</div>


* <div data-tips="true" data-tips-type="tip">Currently, the <strong>PushRepository (push image)</strong> and <strong>PullRepository (pull image)</strong> actions cannot be added via the visual editor. To grant these permissions, refer to the API\-based method described below.</div>




|API |Authentication action |Authentication resource |
|---|---|---|
|Creates a CR instance |cr:CreateRegistry |trn:cr:\*:\*:instance/\* |
|Deletes a CR instance |cr:DeleteRegistry |trn:cr:\*:\*:instance/$instance |
|Starts a CR instance |cr:StartRegistry |trn:cr:\*:\*:instance/$instance |
|Queries CR instances |cr:ListRegistries |\* |
|Updates CR public network endpoint |cr:UpdatePublicEndpoint |trn:cr:\*:\*:instance/$instance |
|Obtains CR public network endpoint information |cr:GetPublicEndpoint |trn:cr:\*:\*:instance/$instance |
|Updating VPC access portals |cr:UpdateVpcEndpoint |trn:cr:\*:\*:instance/$instance |
|Obtains VPC access endpoint |cr:GetVpcEndpoint |trn:cr:\*:\*:instance/$instance |
|Queries CR domain name |cr:ListDomains |trn:cr:\*:\*:instance/$instance |
|Create a namespace |cr:CreateNamespace |trn:cr:\*:\*:repository/\* |
|Deleting a namespace |cr:DeleteNamespace |trn:cr:\*:\*:repository/$instance/$namespace |
|Queries namespaces |cr:ListNamespaces |\* |
|Creating OCI artifact repositories |cr:CreateRepository |trn:cr:\*:\*:repository/\* |
|Deleting OCI artifact repositories |cr:DeleteRepository |trn:cr:\*:\*:repository/$instance/$namespace/$repository |
|Pushing Images |cr:PushRepository |trn:cr:\*:\*:repository/$instance/$namespace/$repository |
|Pulling Images |cr:PullRepository |trn:cr:\*:\*:repository/$instance/$namespace/$repository |
|Queries OCI artifact repositories |cr:ListRepositories |\* |
|Queries OCI artifact version |cr:ListTags |trn:cr:\*:\*:repository/$instance/$namespace/$repository |
|Updates CR user information |cr:SetUser |trn:cr:\*:\*:instance/$instance |
|Obtains CR user information |cr:GetUser |trn:cr:\*:\*:instance/$instance |
|Obtains a temporary access key for logging in to CR |cr:GetAuthorizationToken |trn:cr:\*:\*:instance/$instance |


<span id=".6Ym05p2D56S65L6L"></span>
## Authentication examples

The following are examples of how to use authentication rules in different CR scenarios.

<span id=".5Zy65pmv5LiA77ya5o6o6YCB6ZWc5YOP"></span>
### Scenario 1: Push images

Grant an IAM user the permission to push images to a specific namespace associated with a Standard Edition instance (for example: Standard Edition instance "instance\-a" and namespace "library"). After logging in to the CR console as the IAM user, you can push all image instances under the specified namespace. You can also obtain information about the namespace and all image instances under it via OpenAPI.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cr:List*",
        "cr:Get*",
        "cr:Pull*",
        "cr:Push*"
      ],
      "Resource": [
        "trn:cr:*:*:instance/instance-a", 
        "trn:cr:*:*:repository/instance-a/library", 
        "trn:cr:*:*:repository/instance-a/library/*"
      ]
    }
  ]
}

```


<span id=".5Zy65pmv5LqM77ya5ouJ5Y-W6ZWc5YOP"></span>
### Scenario 2: Pull images

Grant an IAM user the read permission for a namespace associated with a Standard Edition instance (for example: Standard Edition instance "instance\-a" and namespace "library"). After logging in to the CR console as the IAM user, you can pull all image instances under the specified namespace. You can also obtain information about the namespace and all image instances under it via OpenAPI.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cr:List*",
        "cr:Get*",
        "cr:Pull*"
      ],
      "Resource": [
        "trn:cr:*:*:instance/instance-a", 
        "trn:cr:*:*:repository/instance-a/library", 
        "trn:cr:*:*:repository/instance-a/library/*"
      ]
    }
  ]
}

```
