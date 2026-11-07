---
title: "API overview"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/api-overview"
---

The following API actions are available for Container Registry (CR).


|**Category** |**API Action** |**Description** |
|---|---|---|
|Instance management |[CreateRegistry](https://docs.byteplus.com/en/docs/cr/createregistry) |Creates a CR Enterprise Edition instance. |
||[ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) |Queries one or more CR instances. |
||[DeleteRegistry](https://docs.byteplus.com/en/docs/cr/deleteregistry) |Deletes a CR Enterprise Edition instance. |
||[StartRegistry](https://docs.byteplus.com/en/docs/cr/startregistry) |Starts a CR Enterprise Edition instance. |
|User management |[SetUser](https://docs.byteplus.com/en/docs/cr/setuser) |Sets a CR user. |
||[GetUser](https://docs.byteplus.com/en/docs/cr/getuser) |Queries information about a CR user. |
|Namespace management |[CreateNamespace](https://docs.byteplus.com/en/docs/cr/createnamespace) |Creates a namespace under a specified CR instance. |
||[DeleteNamespace](https://docs.byteplus.com/en/docs/cr/deletenamespace) |Deletes a namespace from a specified CR instance. |
||[ListNamespaces](https://docs.byteplus.com/en/docs/cr/listnamespaces) |Queries one or more namespaces under a specified CR instance. |
|OCI artifact repository management |[CreateRepository](https://docs.byteplus.com/en/docs/cr/createrepository) |Creates an OCI artifact repository under a specified namespace. |
||[UpdateRepository](https://docs.byteplus.com/en/docs/cr/updaterepository) |Update an OCI artifact repository in a specified namespace. |
||[DeleteRepository](https://docs.byteplus.com/en/docs/cr/deleterepository) |Deletes an OCI artifact repository from a specified namespace. |
||[ListRepositories](https://docs.byteplus.com/en/docs/cr/listrepositories) |Queries one or more OCI artifact repositories under a specified CR instance. |
|OCI artifact version management |[ListTags](https://docs.byteplus.com/en/docs/cr/listtags) |Queries the OCI artifact tag under a specified OCI artifact repository. |
||[DeleteTags](https://docs.byteplus.com/en/docs/cr/deletetags) |Deletes OCI artifact (image and Helm chart) tags in a batch. |
|Endpoint management |[UpdatePublicEndpoint](https://docs.byteplus.com/en/docs/cr/updatepublicendpoint) |Updates the internet endpoint of a specified CR instance. |
||[GetPublicEndpoint](https://docs.byteplus.com/en/docs/cr/getpublicendpoint) |Obtains the internet endpoint of a specified CR instance. |
||[UpdateVpcEndpoint](https://docs.byteplus.com/en/docs/cr/updatevpcendpoint) |Updates a VPC endpoint. |
||[GetVpcEndpoint](https://docs.byteplus.com/en/docs/cr/getvpcendpoint) |Queries a VPC endpoint. |
||[CreateEndpointAclPolicies](https://docs.byteplus.com/en/docs/cr/createendpointaclpolicies) |Create an entrance for public IP whitelist. |
||[DeleteEndpointAclPolicies](https://docs.byteplus.com/en/docs/cr/deleteendpointaclpolicies) |Queries a VPC endpoint. |
|Access credential |[GetAuthorizationToken](https://docs.byteplus.com/en/docs/cr/getauthorizationtoken) |Obtains the temporary token for logging on to a specified CR instance. |
|Robot Account Management |[CreateRobotAccount](https://docs.byteplus.com/en/docs/cr/CreateRobotAccount) |Create a robot account. |
||[ListRobotAccounts](https://docs.byteplus.com/en/docs/cr/ListRobotAccounts) |List the robot accounts. |
||[UpdateRobotAccount](https://docs.byteplus.com/en/docs/cr/UpdateRobotAccount) |Update the robot accounts. |
||[UpdateRobotAccountPassword](https://docs.byteplus.com/en/docs/cr/UpdateRobotAccountPassword) |Update the password of the robot account. |
||[DeleteRobotAccount](https://docs.byteplus.com/en/docs/cr/DeleteRobotAccount) |Delete the robot account. |
