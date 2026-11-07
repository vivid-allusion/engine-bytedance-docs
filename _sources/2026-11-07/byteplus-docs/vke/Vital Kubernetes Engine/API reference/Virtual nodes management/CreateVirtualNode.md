---
title: "CreateVirtualNode"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateVirtualNode"
---

Create a virtual node.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for Trial</strong></a>]: APIs related to virtual nodes are in the <strong>beta</strong> phase. To use these APIs, submit an application.</div>


<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This is an asynchronous API. When this API returns a success message, it will return the ID of the virtual node, and the virtual node will enter the `{Creating, [Progressing]}` state. After the node is created, it will enter the `{Running, [Ok]}` state. You can call the [ListVirtualNodes](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes) API to obtain the current status of the virtual node and check whether the virtual node has been created.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateVirtualNode&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateVirtualNode |The API name. The name of the current API is `CreateVirtualNode`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClientToken |String |no |BC028527\-33B9\-4990\-A633\-84E9F9xxxx |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|Name |String |no |vci\-vnode\-cn\-beijing\-1 |The name of the virtual node.<br><br><br>* The name must be unique within the same VPC.<br><br>* It can contain uppercase and lowercase letters, digits, and hyphens (\-) and is 2 to 64 characters in length.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This name is only the display name of the virtual node and is not the same as <code>node.name</code> in Kubernetes.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not specify a name, the system will name the virtual node by using the format <code>vci-vnode-<Availability Zone ID></code>.</div><br> |
|Kubeconfig |String |Yes |YXBpVmVyc2lvbjogdjEKY2x1c3RlcnM6\*\*\*\*\*\*\* |The KubeConfig of the target Kubernetes cluster to which the virtual node will connect.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to Base64\-encode KubeConfig before passing it in. For more information about Base64 encoding, see <a href="https://docs.byteplus.com/en/docs/vke/FAQs-about-using-the-command-line-for-base64-encoding">FAQ</a>.</div><br> |
|VirtualNodeConfig |Object of [VirtualNodeConfig](https://docs.byteplus.com/en/docs/vke/CreateVirtualNode#virtualnodeconfig) |Yes |\- |The configuration information of the virtual node. |
|KubernetesConfig |Object of [VirtualNodeKubernetesConfigRequest](https://docs.byteplus.com/en/docs/vke/CreateVirtualNode#virtualnodekubernetesconfigrequest) |no |\- |The Kubernetes configuration information of the virtual node. |


<span id="virtualnodeconfig"></span>
### VirtualNodeConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|VpcId |String |Yes |vpc\-2d73mgm\*\*\*\*\*\*\*\* |The ID of the VPC where the virtual node network is located.<br><br>You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API of VPC to obtain the VPC ID. |
|SubnetIds |Array of String |Yes |["subnet\-2d73mhao7vj0g58ozf\*\*\*\*"] |The IDs of subnets where the virtual node network is located.<br><br>You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API of VPC to obtain the subnet ID.<br><br><br>* You can enter only subnets within the same VPC and the same availability zone.<br><br>* You can enter up to five subnet IDs. |
|SecurityGroupIds |Array of String |Yes |["sg\-3re8ffwjclybk5zsk\*\*\*\*"] |The IDs of security groups where the virtual node network is located.<br><br>You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API of VPC to obtain the security group IDs.<br><br><br>* The ENI and VCI pod of the virtual node will be added to the security group by default.<br><br>* You can enter up to five security group IDs. |


<span id="virtualnodekubernetesconfigrequest"></span>
### VirtualNodeKubernetesConfigRequest


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/vke/CreateVirtualNode#label) |no |\- |The Kubernetes label information of the virtual node. |
|Taints |Array of [Taint](https://docs.byteplus.com/en/docs/vke/CreateVirtualNode#taint) |no |\- |The Kubernetes taint information of the virtual node. |


<span id="label"></span>
### Label


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |label\-key |The label key. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#syntax-and-character-set).<br><br>A valid label key consists of <prefix\> and <Name\>, which are separated by a slash (`/`).<br><br><br>* <Name\> is required, which can contain uppercase or lowercase letters, digits, hyphens (`-`), underscores (`_`), and periods (`.`). It must start and end with a letter or digit and can be up to 63 characters in length.<br><br>* <prefix\> is optional. If <prefix\> is specified, it must be a DNS subdomain, which is a series of DNS labels separated by periods (`.`), with a length not exceeding 253 characters.<br><br>* The total length of <prefix\> and <Name\> must not exceed 82 characters. |
|Value |String |no |label\-value |The label value. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br><br>* The value cannot exceed 63 characters in length and can be left empty.<br><br>* The value can start and end with an uppercase or lowercase letter, or a digit.<br><br>* The value can contain the following special characters: hyphens (`-`), underscores (`_`), and periods (`.`). |


<span id="taint"></span>
### Taint


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Effect |String |no |NoSchedule |The taint effect. Valid values:<br><br><br>* **NoSchedule**: (Default) No scheduling is performed.<br><br>* **NoExecute**: Pods that do not tolerate the taint are evicted.<br><br>* **PreferNoSchedule**: Avoid scheduling if possible. |
|Key |String |Yes |taint\-key |The taint key. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#syntax-and-character-set).<br><br>A valid taint key consists of <prefix\> and <Name\>, which are separated by a slash (`/`).<br><br><br>* <Name\> is required, which can contain uppercase or lowercase letters, digits, hyphens (`-`), underscores (`_`), and periods (`.`). It must start and end with a letter or digit and can be up to 63 characters in length.<br><br>* <prefix\> is optional. If <prefix\> is specified, it must be a DNS subdomain, which is a series of DNS labels separated by periods (`.`), with a length not exceeding 253 characters.<br><br>* The total length of <prefix\> and <Name\> must not exceed 82 characters. |
|Value |String |no |taint\-value |The taint value. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#syntax-and-character-set).<br><br><br>* The value cannot exceed 63 characters in length and can be left empty.<br><br>* The value can start and end with an uppercase or lowercase letter, or a digit.<br><br>* The value can contain the following special characters: hyphens (`-`), underscores (`_`), and periods (`.`). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=CreateVirtualNode&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "Name": "virtualnode-1",
    "VirtualNodeConfig": {
        "VpcId": "vpc-3reuafbrw1********",
        "SubnetIds": ["subnet-3rfcnoazj4cu85zsk2j******"],
        "SecurityGroupIDs": ["sg-3reuafhozdwjk5zsk2i******"]
    },
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9******",
    "KubernetesConfig": {
        "Labels": [
            {"Key": "nodetype", "Value": "vci"}
        ],
        "Taints": [
            {
                "Key": "t1",
                "Value": "tv1",
                "Effect": "NoSchedule"
            }
        ]
    },
    "Kubeconfig": "YXBpVmVyc2lvbjogdjEKY2x1c3RlcnM6*******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|id |String |v73mhao7vj0g\*\*\*\*\*\*\*\* |The ID of the virtual node. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "021635*******",
        "Action": "CreateVirtualNode",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "id": "vck4gdidle********"
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic for details.


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |VpcMismatch.{{parameter}} |The specified {{resourceType}} {{resourceId}} is not in the same VPC. |The specified subnet IDs do not belong to the same VPC. Specify the parameter and try again. |
|400 |OperationDenied.Subnet |The specified Subnet {{subnetId}} is not in the VCI zones. |The availability zone of the specified subnet is not within the availability zone range where VCI is available. |
|409 |Conflict.Name |The specified name conflicts with existing {{resourceType}}. |A resource with the same name exists in the specified region. Update the resource name and try again later. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified parameter is not supported, such as **SecurityGroupIds**. Verify the parameters and try again. |


&nbsp;
