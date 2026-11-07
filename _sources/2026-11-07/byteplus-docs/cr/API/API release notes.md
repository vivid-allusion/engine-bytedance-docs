---
title: "API release notes"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/API_release_history"
---

<span id=".XzIwMjYt5bm0LTA4LeaciA=="></span>
## August 2026


|API |Release date |Change log |Associated features |
|---|---|---|---|
|<span data-api-tag="update\|TLBahM">更新</span> [GetAuthorizationToken](https://docs.byteplus.com/en/docs/cr/getauthorizationtoken) |2026\-08\-01 |Adds the request parameter `ExpiresAt`. |Custom expiration times are supported for temporary access credentials. |


<span id=".XzIwMjYt5bm0LTA2LeaciA=="></span>
## June 2026


|API |Release date |Change log |Associated features |
|---|---|---|---|
|<span data-api-tag="add\|7U7ewo">新增</span> [UpdateTagDescription](https://docs.byteplus.com/en/docs/cr/UpdateTagDescription) |2026\-06\-30 |Updates image tag description. |New API added. |


<span id=".XzIwMjUt5bm0LTA2LeaciA=="></span>
## June 2025


|API |Release date |Change log |Associated features |
|---|---|---|---|
|<span data-api-tag="add\|ozVoFT">新增</span> [CreateRobotAccount](https://docs.byteplus.com/en/docs/cr/CreateRobotAccount) |2025\-06\-10 |Added API to create robot accounts. Robot accounts are only associated with the instance status and are not affected by changes to IAM users. |New API added. |
|<span data-api-tag="add\|45tmGP">新增</span> [ListRobotAccounts](https://docs.byteplus.com/en/docs/cr/ListRobotAccounts) ||Lists the robot accounts. ||
|<span data-api-tag="add\|uGv7my">新增</span> [UpdateRobotAccount](https://docs.byteplus.com/en/docs/cr/UpdateRobotAccount) ||Updates a robot account. ||
|<span data-api-tag="add\|m4m05q">新增</span> [UpdateRobotAccountPassword](https://docs.byteplus.com/en/docs/cr/UpdateRobotAccountPassword) ||Updates the password of a robot account. ||
|<span data-api-tag="add\|YTQ8Vi">新增</span> [DeleteRobotAccount](https://docs.byteplus.com/en/docs/cr/DeleteRobotAccount) ||Deletes a robot account. ||


<span id=".XzIwMjQt5bm0LTA3LeaciA=="></span>
## July 2024


|**API** |Release date |**Change log** |**Associated features** |
|---|---|---|---|
|[CreateRegistry](https://docs.byteplus.com/en/docs/cr/createregistry) |2024\-07\-24 |Added support for customizing instance labels using key\-value pairs. Supported viewing billing information based on instance labels in the **splitting bills**. For details, please refer to [Splitting bills](https://docs.byteplus.com/en/docs/byteplus-platform/SplitBills). |API modified. |
|[ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) |2024\-07\-24 |Added support for filtering instances by instance labels. |API modified. |
|[Registryfilter](https://docs.byteplus.com/en/docs/cr/data-structures-of-requests#registryfilter) |2024\-07\-24 |Released the Micro Edition Container Registry (GA). Added the Micro Edition instance to the instance types. |API modified. |
|[Registry](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#registry) |2024\-07\-24 |Released the Micro Edition Container Registry (GA). Added the Micro Edition instance to the instance types. |API modified. |


<span id=".XzIwMjQt5bm0LTA2LeaciA=="></span>
## June 2024


|**API** |Release date |**Change log** |**Associated features** |
|---|---|---|---|
|[CreateRegistry](https://docs.byteplus.com/en/docs/cr/createregistry) |2024\-06\-30 |Added support for associating instances with projects. After association, members of the project will obtain corresponding permissions for the Container Registry based on project authorization. |API modified. |
|[ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) |2024\-06\-30 |Added support for filtering instances by project name. |API modified. |


<span id=".XzIwMjQt5bm0LTAzLeaciA=="></span>
## March 2024


|**API** |Release date |**Change log** |**Associated features** |
|---|---|---|---|
|[UpdateRepository](https://docs.byteplus.com/en/docs/cr/updaterepository) |2024\-03\-29 |Officially released the UpdateRepository API, which supports updating OCI artifact repository information under a specified namespace. |New API added. |
|[CreateEndpointAclPolicies](https://docs.byteplus.com/en/docs/cr/createendpointaclpolicies) |2024\-03\-29 |Added the CreateEndpointAclPolicies API to support creating the allowlist endpoint for Elastic IP addresses. |New API added. |
|[DeleteEndpointAclPolicies](https://docs.byteplus.com/en/docs/cr/deleteendpointaclpolicies) |2024\-03\-29 |Added the DeleteEndpointAclPolicies API to support deleting the allowlist endpoint for Elastic IP addresses. |New API added. |


<span id=".XzIwMjMt5bm0LTA3LeaciA=="></span>
## July 2023


|**API** |Release date |**Change log** |**Associated features** |
|---|---|---|---|
|[Request data structure](https://docs.byteplus.com/en/docs/cr/data-structures-of-requests) |2023\-07\-13 |Added the Trial Edition type "Trial" to the Types field in the request parameter RegistryFilter. |Trial instances are available. |
|[Response data structure](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses) |2023\-07\-13 |Added the Trial Edition type "Trial" to the Types field in the response parameter Registry. |Trial instances are available. |


<span id=".XzIwMjMt5bm0LTA0LeaciA=="></span>
## April 2023


|**API** |Release date |**Change log** |**Associated features** |
|---|---|---|---|
|[ListNamespaces](https://docs.byteplus.com/en/docs/cr/listnamespaces) |2023\-04\-21 |Added the Project field to the Namespace result in the response parameters. |The project associated with the namespace displayed. |
|[CreateNamespace](https://docs.byteplus.com/en/docs/cr/createnamespace) |2023\-04\-21 |Added an optional Project field to the request parameters. |Supported associating a namespace with a specified project. If this parameter is left blank, it means the created namespace does not belong to any project. |
