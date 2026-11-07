---
title: "Request data structure"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/data-structures-of-requests"
---

This document primarily describes the general request data structure for the OpenAPI of the Container Registry.

<span id="resourcetagfilters"></span>
## ResourceTagFilters


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key1 |The Key value of the label. |
|Values |List |Yes |["value1","value2"] |The list of values for the label. |


<span id="resourcetag"></span>
## ResourceTag


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key1 |The Key value of the label. |
|Value |String |Yes |value1 |The values of the label. |


<span id="registryfilter"></span>
## RegistryFilter


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Names |List<String\> |no |["test1","jt\*tt","\*test","li\*"] |The name of the specified Container Registry instance. You can obtain the instance name from the **Instances** page in the [Container Registry Console](https://console.byteplus.com/cr). Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 instance names can be specified in a single request. |
|Types |List<String\> |no |["Basic"] |The type of the Container Registry instance. The possible values are as follows:<br><br><br>* **Basic Edition**: The Basic Edition instance.<br><br>* **Trial Edition**: The Trial Edition instance.<br><br>* **Standard Edition**: The Standard Edition instance.<br><br>* **Micro**: The Micro Edition instance. You can fill in one or more instance types. |
|Statuses |List<[StatusFilter](https://docs.byteplus.com/en/docs/cr/data-structures-of-requests#statusfilter)\> |no | |The statuses of the Container Registry instances. For details, please refer to [StatusFilter](https://docs.byteplus.com/en/docs/cr/data-structures-of-requests#statusfilter). A maximum of 10 **StatusFilter** combinations can be filled in a single call. |


<span id="statusfilter"></span>
## StatusFilter

For the valid combinations of **Phase** and **Condition**, please refer to the description of parameter **Status** in [Registry](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#registry).


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Phase |String |no |Running |The instance status (**Status**) is composed of Phase and Conditions.<br><br><br>* **Creating**, [ **Progressing** ]: The instance is being created.<br><br>* **Running**, [ **Ok** ]: The instance is running normally.<br><br>* **Running**, [ **Degraded** ]: The instance is running but in a degraded status.<br><br>* **Stopped**, [ **Balance** ]: The instance has been shut down due to arrears.<br><br>* **Stopped**, [ **Released** ]: The instance is pending reclamation.<br><br>* **Stopped**, [ **Released**, **Balance** ]: The instance has been shut down due to arrears.<br><br>* **Starting**, [ **Progressing** ]: The instance is being started.<br><br>* **Deleting**, [ **Progressing** ]: The instance is being deleted.<br><br>* **Failed**, [ **Unknown** ]: The instance is in an abnormal status. |
|Condition |String |no |Ok ||


<span id="namespacefilter"></span>
## NamespaceFilter


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Names |List<String\> |no |["test", "\*st", "t\*st","tes\*"] |The name of the specified namespace. You can obtain the namespace name from the **Namespace** page of the target instance in the [Container Registry Console](https://console.byteplus.com/cr). Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 namespace names can be filled in at once. |


<span id="repositoryfilter"></span>
## RepositoryFilter


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Namespaces |List<String\> |no |["testns"] |The namespaces to which the specified OCI artifact repositories belong. You can obtain the namespace name from the **Namespace** page of the target instance in the [Container Registry Console](https://console.byteplus.com/cr). Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 namespace names can be filled in at once. |
|Names |List<String\> |no |["test", "\*st", "t\*st","tes\*"] |The names of the specified OCI artifact repositories. You can obtain the OCI artifact repository name from the **OCI artifact repository** page of the target instance in the [Container Registry Console](https://console.byteplus.com/cr). Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 OCI artifact repository names can be specified in a single request. |
|AccessLevels |List<String\> |no |["Private"] |The access levels of the OCI artifact repositories, with the following values:<br><br><br>* **Private**: A private OCI artifact repository that can only be accessed by authorized users.<br><br>* **Public**: A public OCI artifact repository that can be accessed by all users. You can fill in one or more access levels at a time. |


<span id="tagfilter"></span>
## TagFilter


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Names |List<String\> |no |["tag"] |Specifies the Tags to filter by, supporting both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard, with a maximum of 20. |
|Types |List<String\> |no |["Chart"] |The types of OCI artifact Tags, with values as follows:<br><br><br>* **Image**: The Tag corresponds to a container image.<br><br>* **Chart**: The Tag corresponds to a Helm Chart. You can fill in one or more Tag types at a time. |


<span id="vpcmeta"></span>
## VpcMeta


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|VpcId |String |Yes |vpc\-3rfawyc34g0sg5zsk2idd\*\*\*\* |The VPC ID. The Container Registry instance will configure the access endpoint within this VPC. |
|SubnetId |String |no |subnet\-jhhsrhjjdfssi\*\*\*\* |The subnet ID under the VPC. If not specified, the subnet with the most remaining IP addresses in the VPC will be automatically selected, and it cannot be changed afterwards. |
|AccountId |Integer |no |140000\*\*\*\* |The ID of the root user to which the VPC belongs. This ID needs to be specified when exposing a Standard Edition instance to a VPC under another root user. |


<span id="vpcendpointfilter"></span>
## VpcEndpointFilter


|**Parameter Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Statuses |List |no |["Enabling", "Enabled"] |An array of VPC access endpoint statuses, used to filter out VPC access entries that are in the specified statuses.<br><br><br>* **Enabling**: turning on<br><br>* **Enabled**: turned on<br><br>* **Disabling**: turning off<br><br>* **Failed**: failed |
