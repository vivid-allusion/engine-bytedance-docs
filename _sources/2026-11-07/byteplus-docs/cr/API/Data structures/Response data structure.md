---
title: "Response data structure"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/data-structures-of-responses"
---

This document primarily describes the general response data structure for the OpenAPI of the Container Registry.

<span id="registry"></span>
## Registry


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |test\-registry |The name of the Container Registry instance. |
|Type |String |Basic |The type of the Container Registry instance. The parameter values are as follows:<br><br><br>* **Basic Edition**: The Basic Edition instance. Only some users of historical versions are supported to use, and it can not be viewed in the console.<br><br>* **Trial Edition**: The Trial Edition instance.<br><br>* **Standard Edition**: The Standard Edition instance.<br><br>* **Micro**: The Micro Edition instance. |
|ChargeType |String |PostCharge |The payment type of the Container Registry instance. Currently, only the **PostCharge** Pay\-as\-you\-go mode is supported. |
|Status |Object<[RegistryStatus](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#registrystatus)\> |{<br><br>"Phase": "Running",<br><br>"Conditions": ["Ok"]<br><br>} |The status of the Container Registry instance, composed of **Phase** and **Conditions**. The valid combinations of **Phase** and **Conditions** are as follows:<br><br><br>* `{Creating, [Progressing]}`: The instance is being created.<br><br>* `{Running, [Ok]}`: The instance is running normally.<br><br>* `{Running, [Degraded]}`: The instance is running but in a degraded status.<br><br>* `{Stopped, [Balance]}`: The instance has been shut down due to arrears.<br><br>* `{Stopped, [Released]}`: The instance is pending reclamation.<br><br>* `{Stopped, [Released, Balance]}`: The instance has been shut down due to arrears.<br><br>* `{Starting, [Progressing]}`: The instance is being started.<br><br>* `{Deleting, [Progressing]}`: The instance is being deleted.<br><br>* `{Failed, [Unknown]}`: The instance is in an abnormal status. |
|Project |String |default |The project to which the instance needs to be associated. Each instance supports association with only one project. |
|ResourceTags |List<[ResourceTag](https://docs.byteplus.com/en/docs/cr/data-structures-of-requests#resourcetag)\> |Refer to the general data structure |Allow customizing instance labels using key\-value pairs. Supported viewing billing information based on instance labels in the **splitting bills**. For details, please refer to [Splitting bills](https://docs.byteplus.com/en/docs/6269/177196). |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the Container Registry instance was created. The [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) formatted UTC+0 time. |


<span id="registrystatus"></span>
## RegistryStatus

For the description of the combinations of **Phase** and **Condition**, please refer to the description of parameter **Status** in [Registry](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#registry) above in this document.


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Phase |String |Deleting |The status of the Container Registry instance. The parameter values are as follows:<br><br><br>* **Creating**<br><br>* **Running**<br><br>* **Stopped**<br><br>* **Starting**<br><br>* **Deleting**<br><br>* **Failed** |
|Conditions |List |["Progressing"] |The conditions under which the Container Registry instance enters the current status, i.e., the reasons for entering this status. There can be multiple reasons. The parameter values are as follows:<br><br><br>* **Ok**<br><br>* **Progressing**<br><br>* **Degraded**<br><br>* **Balance**<br><br>* **Released**<br><br>* **Unknown** |


<span id="namespace"></span>
## Namespace


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |ns1 |The name of the namespace. |
|Project |String |projecta |The name of the project to which the namespace belongs. If this parameter is left blank, it indicates that the created Namespace does not belong to any project. |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the namespace was created. The [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) formatted UTC+0 time. |


<span id="repository"></span>
## Repository


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Namespace |String |ns1 |The name of the namespace. |
|Name |String |repo1 |The name of the OCI artifact repository. |
|AccessLevel |String |Private |The access level of the OCI artifact repository:<br><br><br>* **Private**: A private type OCI artifact repository that requires an access key for access.<br><br>* **Public**: A public OCI artifact repository that can be accessed directly via its URL. |
|Description |String |This is a description |The description of the Container Registry, with a length of 0 to 300 UTF\-8 characters. |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the OCI artifact repository was created. The [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) formatted UTC+0 time. |
|UpdateTime |String |2022\-05\-20T13:00:55Z |The last time the OCI artifact repository was updated. The [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) formatted UTC+0 time. |


<span id="tag"></span>
## Tag


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |v2 |The name of the OCI artifact version (Tag). |
|Type |String |Image |The type of the OCI artifact Tag:<br><br><br>* **Image**: The Tag corresponds to a container image.<br><br>* **Chart**: The Tag corresponds to a Helm Chart. |
|Digest |String |sha256:dd97a3eb42\*\*\*\*\*\*\*\* |The digest of the OCI artifact, represented as a SHA256 value. |
|PushTime |String |2022\-05\-03T12:08:01Z |The time of the last push of the OCI artifact. The [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) formatted UTC+0 time. |
|Size |Long |10061844 |The size of the OCI artifact, in bytes. |
|ImageAttributes |List<[ImageAttribute](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#imageattribute)\> | |The relevant attributes when the Tag type is **Image**. For details, please refer to [ImageAttribute](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#imageattribute). |
|ChartAttribute |[ChartAttribute](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#chartattribute) | |The relevant attributes when the Tag type is **Chart**. For details, please refer to [ChartAttribute](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#chartattribute). |


<span id="imageattribute"></span>
## ImageAttribute


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Author |String |user@test.com |The creator of the image, i.e., the BytePlus root user that uploads the image to the Container Registry. |
|Architecture |String |amd64 |The architecture of the image. |
|Os |String |linux |The operating system supported by the image. |
|Digest |String |sha256:dd97a3eb42\*\*\*\*\*\*\*\* |The digest of the image, represented as a SHA256 value. |


<span id="chartattribute"></span>
## ChartAttribute


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ApiVersion |String |v2 |The Helm version. |
|Name |String |mysql |The name of the Helm Chart. |
|Version |String |8.6.1 |The version of the Helm Chart. |


<span id="domain"></span>
## Domain


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Domain |String |helm\-cr\-cn\-beijing.cr.volces.com |The domain names of the Container Registry:<br><br><br>* Trial Edition instances:<br><br>   * For existing instances: `cr-cn-beijing.volces.com`<br><br>   * For new or upgraded instances: `[Instance Name]-[Region].cr.volces.com`<br><br>* Standard Edition instances: `[Instance Name]-[Region].cr.volces.com` |
|Type |String |System |The type of the domain name:<br><br><br>* System: A domain name provided by the system.<br><br>* Volcengine: A BytePlus domain name.<br><br>* ThirdParty: A third\-party domain name. |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the domain name was created, in RFC 3339 format. |
|Default |Bool |true |Whether the domain name is the system domain name of the Container Registry.<br><br><br>* true: It is the default domain name.<br><br>* false: It is not the default domain name. |


<span id="success"></span>
## Success


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |v1 |The name of the Tag. |


<span id="failure"></span>
## Failure


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |v1 |The name of the Tag. |
|Reason |String |tag v1 not exist |The reason for the deletion failure. |


<span id="vpcinfo"></span>
## VpcInfo


|**Parameter Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|VpcId |String |vpc\-luebclsohfwnljn\*\*\*\* |VPC ID. |
|SubnetId |String |subnet\-nlohebas\*\*\*\* |The ID of the subnet. |
|Region Code |String |cn\-beijing |The region where the VPC is located. |
|AccountId |Integer |140000\*\*\*\* |The ID of the root user to which the VPC belongs. |
|Ip |String |192.168.12.33 |The IP address of the Container Registry within the VPC. |
|Status |String |Enabled |The status of the access endpoint:<br><br><br>* Enabling: turning on<br><br>* Enabled: turned on<br><br>* Disabling: turning off<br><br>* Failed: failed |
|CreateTime |String |2022\-05\-20T13:00:55Z |The creation time. |
