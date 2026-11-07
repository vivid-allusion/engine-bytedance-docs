---
title: "API list"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/API_list"
---

The Container Registry (CR) provides the following lists of APIs.

<span id=".5a6e5L6L566h55CG"></span>
## Instance management


|API |Description |
|---|---|
|[CreateRegistry](https://docs.byteplus.com/en/docs/cr/createregistry) |Create CR instance. |
|[ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) |Query one or more Container Registry instances. |
|[DeleteRegistry](https://docs.byteplus.com/en/docs/cr/deleteregistry) |Delete a Standard Edition instance of the Container Registry. |
|[StartRegistry](https://docs.byteplus.com/en/docs/cr/startregistry) |Start a Standard Edition instance of the Container Registry. |


<span id=".55So5oi3566h55CG"></span>
## User management


|API |Description |
|---|---|
|[SetUser](https://docs.byteplus.com/en/docs/cr/getuser) |Sets a user for the Container Registry, which refers to the user logging into the Container Registry instance. |
|[GetUser](https://docs.byteplus.com/en/docs/cr/setuser) |Query the user information of the Container Registry. |


<span id=".5ZG95ZCN56m66Ze0566h55CG"></span>
## Namespace management


|API |Description |
|---|---|
|[CreateNamespace](https://docs.byteplus.com/en/docs/cr/createnamespace) |Creates a namespace under a specified Container Registry instance. |
|[ListNamespaces](https://docs.byteplus.com/en/docs/cr/listnamespaces) |Query one or more namespaces under a specified Container Registry instance. |
|[DeleteNamespace](https://docs.byteplus.com/en/docs/cr/deletenamespace) |Deletes a namespace under a specified Container Registry instance. |


<span id=".b2NpLeWItuWTgeS7k-W6k-euoeeQhg=="></span>
## OCI artifact repository management


|API |Description |
|---|---|
|[CreateRepository](https://docs.byteplus.com/en/docs/cr/createrepository) |Create an OCI artifact repository under a specified namespace. |
|[UpdateRepository](https://docs.byteplus.com/en/docs/cr/updaterepository) |Update the information of an OCI artifact repository under a specified namespace. |
|[ListRepositories](https://docs.byteplus.com/en/docs/cr/listrepositories) |Queries one or more OCI artifact repositories under a specified Container Registry instance. |
|[DeleteRepository](https://docs.byteplus.com/en/docs/cr/deleterepository) |Deletes an OCI artifact repository from a specified namespace. |


<span id=".b2NpLeWItuWTgeeJiOacrOeuoeeQhg=="></span>
## OCI artifact version management


|API |Description |
|---|---|
|[ListTags](https://docs.byteplus.com/en/docs/cr/listtags) |Queries one or more OCI artifact (image, Helm Chart) versions within a specified OCI artifact repository. |
|[DeleteTags](https://docs.byteplus.com/en/docs/cr/deletetags) |Deletes the OCI artifact (image, Helm Chart) versions, with support for batch deletion. |
|[UpdateTagDescription](https://docs.byteplus.com/en/docs/cr/UpdateTagDescription) |Update image tag description. |


<span id=".5Z-f5ZCN566h55CG"></span>
## Domain management


|API |Description |
|---|---|
|[ListDomains](https://docs.byteplus.com/en/docs/cr/ListDomains) |Queries the domain names of a Container Registry instance. |


<span id=".6K6_6Zeu5YWl5Y-j566h55CG"></span>
## Access endpoint management


|API |Description |
|---|---|
|[UpdatePublicEndpoint](https://docs.byteplus.com/en/docs/cr/updatepublicendpoint) |Update the public network access information of the Container Registry instance. |
|[GetPublicEndpoint](https://docs.byteplus.com/en/docs/cr/getpublicendpoint) |Obtain the public network access information of the Container Registry instance. |
|[UpdateVpcEndpoint](https://docs.byteplus.com/en/docs/cr/updatevpcendpoint) |Update the VPC access endpoint. |
|[GetVpcEndpoint](https://docs.byteplus.com/en/docs/cr/getvpcendpoint) |Query the VPC access endpoint information. |
|[CreateEndpointAclPolicies](https://docs.byteplus.com/en/docs/cr/createendpointaclpolicies) |Create an Elastic IP Address allowlist endpoint. |
|[DeleteEndpointAclPolicies](https://docs.byteplus.com/en/docs/cr/deleteendpointaclpolicies) |Delete an Elastic IP Address allowlist endpoint. |


<span id=".5Li05pe26K6_6Zeu5a-G6ZKl"></span>
## Temporary access key


|API |Description |
|---|---|
|[GetAuthorizationToken](https://docs.byteplus.com/en/docs/cr/getauthorizationtoken) |Obtains a temporary access key for logging into a Container Registry instance. |


<span id=".5py65Zmo5Lq66LSm5oi3566h55CG"></span>
## Robot account management


|API |Description |
|---|---|
|[CreateRobotAccount](https://docs.byteplus.com/en/docs/cr/CreateRobotAccount) |Creates a robot account. |
|[ListRobotAccounts](https://docs.byteplus.com/en/docs/cr/ListRobotAccounts) |Lists the robot accounts. |
|[UpdateRobotAccount](https://docs.byteplus.com/en/docs/cr/UpdateRobotAccount) |Updates a robot account. |
|[UpdateRobotAccountPassword](https://docs.byteplus.com/en/docs/cr/UpdateRobotAccountPassword) |Updates the password of a robot account. |
|[DeleteRobotAccount](https://docs.byteplus.com/en/docs/cr/DeleteRobotAccount) |Delete robot account. |
