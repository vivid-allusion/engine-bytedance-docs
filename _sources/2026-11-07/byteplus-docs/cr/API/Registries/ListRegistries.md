---
title: "ListRegistries"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/listregistries"
---

Query one or more Container Registry instances.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

When querying Container Registry Instances, use the **Filter** parameter to control the filtering criteria for Container Registry Instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For more details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=ListRegistries&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListRegistries |The API name. The current API's name is `ListRegistries`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [RegistryFilter](https://docs.byteplus.com/en/docs/65/22269#registryfilter) |no | |The filtering conditions for the Container Registry instances to be queried. |
|ResourceTagFilters |Array of [ResourceTagFilter](https://docs.byteplus.com/en/docs/65/22269#resourcetagfilter) |no | |The filtering conditions for querying the labels of Container Registry instances. |
|PageSize |Long |no |10 |The number of Container Registry instances displayed per page. With a default value of 10, it takes integer values within the range [1,100]. |
|PageNumber |Long |no |1 |The page number from which to start displaying the returned results. It starts from 1, with a default value of 1, and takes integer values within the range [1, 2147483647]. |


<span id="registryfilter"></span>
### RegistryFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Names |Array of String |no |["registrya", "registryb"] |The names of the specified Container Registry instances or proxy cache registries. In the [Container Registry console](https://console.byteplus.com/cr), go to the **Instance List** page or the **Proxy Cache** page to obtain the name of the instance or proxy cache registry. Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 instance names or proxy cache registry names can be specified in a single request. |
|Types |Array of String |no |["Micro","Enterprise"] |The type of the Container Registry instance. The possible values are as follows:<br><br><br>* Basic: basic instance.<br><br>* Trial: trial instance.<br><br>* Enterprise: standard instance.<br><br>* **Micro**: The Micro Edition instance. You can fill in one or more instance types. |
|Projects |Array of String |no |["default","projecta"] |The names of the associated projects. |
|Statuses |Array of [StatusFilter](https://docs.byteplus.com/en/docs/65/22269#statusfilter) |no | |The status of Container Registry Instances. You can specify up to 10 **StatusFilter** combinations in a single call. |


<span id="resourcetagfilter"></span>
### ResourceTagFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key1 |The Key value of the label. |
|Values |Array of String |Yes |["value1","value2"] |Label value. |


<span id="statusfilter"></span>
### StatusFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Phase |String |no |Running |The instance status (**Status**) is composed of Phase and Conditions.<br><br><br>* **Creating**, [ **Progressing** ]: The instance is being created.<br><br>* **Running**, [ **Ok** ]: The instance is running normally.<br><br>* **Running**, [ **Degraded** ]: Running.<br><br>* **Stopped**, [ **Balance** ]: Suspended for non\-payment.<br><br>* **Stopped**, [ **Released** ]: Pending reclamation.<br><br>* **Stopped**, [ **Released**, **Balance** ]: Suspended for non\-payment.<br><br>* **Starting**, [ **Progressing** ]: Starting up.<br><br>* **Deleting**, [ **Progressing** ]: Destroying.<br><br>* **Failed**, [ **Unknown**]: Exception. |
|Condition |String |no |Ok |The instance status (Status) is composed of Phase and Conditions. Creating, [ Progressing ]: Creating in progress. Running, [ Ok ]: In progress. Running, [ Degraded ]: The instance is running but in a degraded state. Stopped, [ Balance ]: The instance has been shut down due to arrears. Stopped, [ Released ]: The instance is suspended and waiting for reclamation. Stopped, [ Released, Balance ]: The instance has been shut down due to arrears. Starting, [ Progressing ]: the instance is being started. Deleting, [ Progressing ]: the instance is being deleted. Failed, [ Unknown ]: The instance is in an abnormal status. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=ListRegistries&Version=2022-05-12
{
    "Filter": {
        "Names": [
            "example"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TotalCount |Long |1 |The number of Container Registry instances queried. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |The number of Container Registry instance information items displayed per page. |
|Items |Array of [Registry](https://docs.byteplus.com/en/docs/65/22269#registry) | |The list of Container Registry instances. |


<span id="registry"></span>
### Registry


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |test\-registry |The name of the Container Registry instance. |
|Type |String |Basic |The type of the Container Registry instance. The parameter values are as follows:<br><br><br>* Basic: basic instance. Only some users of historical versions are supported to use, and it can not be viewed in the console.<br><br>* Trial: trial instance.<br><br>* Enterprise: standard instance.<br><br>* **Micro**: The Micro Edition instance. |
|ChargeType |String |PostCharge |Currently, only the **PostCharge** pay\-as\-you\-go model is supported for Container Registry Instances. |
|Status |Object of [RegistryStatus](https://docs.byteplus.com/en/docs/65/22269#registrystatus) |{<br><br>"Phase": "Running",<br><br>"Conditions": ["Ok"]<br><br>} |The status of the Container Registry instance, composed of **Phase** and **Conditions**. The valid combinations of **Phase** and **Conditions** are as follows:<br><br><br>* `{Creating, [Progressing]}`: The instance is being created.<br><br>* `{Running, [Ok]}`: The instance is running normally.<br><br>* `{Running, [Degraded]}`: The instance is running but in a degraded status.<br><br>* `{Stopped, [Balance]}`: The instance has been shut down due to arrears.<br><br>* `{Stopped, [Released]}`: The instance is pending reclamation.<br><br>* `{Stopped, [Released, Balance]}`: The instance has been shut down due to arrears.<br><br>* `{Starting, [Progressing]}`: The instance is being started.<br><br>* `{Deleting, [Progressing]}`: The instance is being deleted.<br><br>* `{Failed, [Unknown]}`: The instance is in an abnormal status. |
|Project |String |projecta |The project to which the instance needs to be associated. Each instance supports association with only one project. |
|ResourceTags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/65/22269#resourcetag) | |Allow customizing instance labels using key\-value pairs.  |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the Container Registry instance was created. UTC+0 time in [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) format. |
|ExpireTime |String |2022\-05\-20T13:00:55Z |The expiration time of the instance or proxy cache registry. A return value exists only when the billing type is HybridCharge (mixed billing). |
|RenewType |String |Manual |The expiration time of the instance or proxy cache registry. A return value exists only when the billing type is HybridCharge (mixed billing). |
|ProxyCache |Object of [ProxyCache](https://docs.byteplus.com/en/docs/65/22269#proxycache) |{<br><br>"Type": "Dockerhub"<br><br>} |The configuration description of the proxy cache registry. |
|ProxyCacheEnabled |Boolean |true |Indicates whether it is a proxy cache registry. |


<span id="registrystatus"></span>
### RegistryStatus


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Phase |String |Running |The status of the Container Registry instance. The parameter values are as follows:<br><br><br>* **Creating**<br><br>* **Running**<br><br>* **Stopped**<br><br>* **Starting**<br><br>* **Deleting**<br><br>* **Failed** |
|Conditions |Array of String |["ok"] |The conditions under which the Container Registry instance enters the current status, i.e., the reasons for entering this status. There can be multiple reasons. The parameter values are as follows:<br><br><br>* **Ok**<br><br>* **Progressing**<br><br>* **Degraded**<br><br>* **Balance**<br><br>* **Released**<br><br>* **Unknown** |


<span id="resourcetag"></span>
### ResourceTag


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |key1 |The Key value of the label. |
|Value |String |val1 |The list of values for the label. |


<span id="proxycache"></span>
### ProxyCache


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |DockerHub |The type supported by the proxy cache registry.<br><br><br>* DockerHub: A proxy cache registry of the Docker Hub type, which supports pulling images from Docker Hub in the mainland region.<br><br>* DockerRegistry: A general\-purpose proxy cache registry, which supports the requirements for primary and secondary registries in multi\-cloud scenarios. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "ListRegistries",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1,
        "Items": [
            {
                "Name": "example",
                "Type": "Enterprise",
                "Status": {
                    "Phase": "Running",
                    "Conditions": [
                        "ok"
                    ]
                },
                "CreateTime": "2022-05-20T13:00:55Z"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
