---
title: "Access control based on IAM for the VKE console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Access_control_based_on_IAM_for_VKE_console"
---

This topic mainly describes how to use BytePlus IAM in the VKE console to manage access permissions for Kubernetes clusters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in the <strong>public beta</strong> stage.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

In modern cloud\-native applications, Kubernetes has become a standard platform for building and managing containerized applications. However, protecting Kubernetes clusters from the risk of unauthorized access is critical. This topic mainly describes how to effectively manage and protect access to your Kubernetes clusters in the VKE console by using the IAM service provided by BytePlus.

IAM functions as an access control service provided by BytePlus, which is used to manage access permissions on cloud resources. By configuring IAM policies, you can manage the access methods and permissions of users, roles, or entities on specific resources in a fine\-grained manner.   For more information, see [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

<span id=".5L2_55So6K-05piO"></span>
## Notes

The solution described in this topic applies only to permissions for accessing Kubernetes clusters in the VKE console. It does not apply to permissions for accessing APIs of Kubernetes clusters via tools such as kubectl. When you access a cluster by using an API, you can directly access the cluster by using the API server of Kubernetes, which is not controlled by IAM of BytePlus.

<span id=".5Z-65LqOLWlhbS3nmoTorr_pl67mjqfliLbnrZbnlaU="></span>
## IAM\-based access control policies

VKE allows you to operate pods, similar to running the `kubectl exec -it {your_container_name} -- /bin/bash` command in the cluster. This feature lets you interact directly with containers to simplify operations. 

However, users with strict security needs require both ease of use and stricter access controls. To restrict VKE console access to specific IP addresses, use the solutions in this topic to configure access policies. This enhances cluster security, prevents unauthorized access, and ensures system stability and data security.

&nbsp;

The sample policy code is as follows:

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "vke:GetTerminal"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "NotIpAddressIfExists": {
                    "volc:SourceIp": [
                        "192.168.xx.xx"
                    ]
                }
            }
        }
    ]
}
```


The preceding sample policy indicates that access to the VKE console will be denied unless the request originates from the IP address `192.168.xx.xx`. When used with common cluster policies where **Effect** is set to **Allow**, such as VKEReadOnlyAccess, this sample policy can effectively prevent insecure network access to pods in the VKE console. The following table describes the policy code parameters.


|Parameters |Description |
|---|---|
|Effect |The result of the access policy in this example is set to **Deny**, which indicates the **deny** operation.  For more syntax details, see [Policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax). |
|Action |The specific operation that is denied. In this example, the value is set to **vke:GetTerminal**, which rejects (prohibits) obtaining terminal access for the Kubernetes cluster.  For more syntax details, see [Policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax). |
|Resource |Specify the resource on which the specified operation is performed based on your business requirements. You can also specify a specific cluster ID to prohibit obtaining terminal access for the cluster.  For more syntax details, see [Policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax).<br><br><br>* `*`: Indicates all resources, meaning that obtaining terminal access for all Kubernetes clusters is prohibited.<br><br>* `trn:vke:{your_region}:*:cluster/{your_clusterid}`: Prohibits obtaining terminal access for the specified cluster.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In actual business scenarios, replace <code>{your_region}</code> with the actual business region and <code>{your_clusterid}</code> with the specified cluster ID, such as <code>trn:vke:cn-shanghai:*:cluster/ccuu2o48q8******.</code>   </div><br>    |
|Condition |Specify the condition under which the policy takes effect. In this example, NotIpAddressIfExists is used, which indicates that if the request contains the `volc:SourceIp` field and its value is `192.168.xx.xx`, access is allowed. Otherwise, access is denied.  |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>Deny</strong> IAM access control policy prevails over other policies. As a result, if multiple policies are used, of which a <strong>Deny</strong> policy is included, the final effect will be <strong>Deny</strong>. Therefore, you can combine the preceding policy with any cluster allow policy.</div>


<span id=".5bqU55SoLWlhbS3orr_pl67mjqfliLbnrZbnlaU="></span>
## Applying IAM policies

You can apply IAM policies by performing the following steps to protect the access permissions on your Kubernetes cluster:


1. Create an IAM policy.

   Create the preceding policy in the [IAM console](https://console.byteplus.com/iam/).  For detailed operations, see [Creating user-defined policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

2. Associate the policy.

   * Associate the created policy with the IAM user or IAM role for which you want to restrict access.  For detailed instructions, see [Managing users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

   * In addition to the preceding IAM permission control for accessing the VKE console, Kubernetes also has its own RBAC permission control. Make sure that the IAM user or IAM role has the other RBAC permissions required to manage the cluster. For RBAC\-related descriptions, see [Configuring user RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In this example, make sure that the IAM user or IAM role to which the policy is attached has exec permissions on pods. Otherwise, the result of permission control cannot be tested.      </div>
      

3. Test the policy.

   Verify whether the policy works as expected by using both authorized and unauthorized IP addresses. The pod console will directly display **disconnect** for blocked requests, which is shown in the following figure.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d496063a09bd7d7ed55177167fb830bf.png) </span>

4. Monitor and optimize the policy.

   * Regularly review and optimize IAM policies to ensure that they are secure and efficient.

   * Monitor the logs and audit information of policies to promptly identify and address security risks.
