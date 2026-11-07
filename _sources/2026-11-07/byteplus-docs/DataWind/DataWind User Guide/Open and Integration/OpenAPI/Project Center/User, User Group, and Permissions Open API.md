---
title: "User, User Group, and Permissions Open API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/User_User_Group_and_Permissions_Open_API"
---

This document introduces Open APIs related to users, user groups, and permissions.

<span id="0e6c7725"></span>
# Function overview


|API |Note |
|---|---|
|Create user group |Create a new user group. Only project administrators can perform this action. Supports setting public attributes, an administrator list, and description information |
|Query the list of user groups in the project |Get all user group information in the specified project. Returns fields including group ID, name, description, public status, and more |
|Query user group members |Get the list of members in the user group. Supports pagination and keyword search. Can distinguish member types (user / subgroup) |
|Delete user group member |Remove a specified member from the user group. Supports operations by user ID, user group ID, or username list |
|Add user group member |Add members to the user group. Supports batch addition of users, subgroups, or matching by username |
|Delete user from project |Remove users from the project. Supports batch deletion of multiple users |
|Add user to project |Add users to a project and assign permissions; repeated additions will overwrite existing advanced permissions |
|Associate system\-level user groups with a project | |
|Get the project list | |
|Get the project user list |Get the list of users in a project, supporting keyword filtering and pagination |
|Authorization API |Grant permissions to resources (datasets, dashboards, and more), supporting batch authorization for multiple users and multiple permissions |
|Get resource authorization details |Query resource authorization details, including direct permissions for users or groups and permissions inherited through roles |
|User attribute modification API |Modify a user's custom attribute value; you must specify the attribute ID and the new value |
|User attribute deletion API |Delete a specified custom attribute of a user |
|Get data permission members API |Query the list of members associated with a data permission rule, supporting pagination and sorting |
|Add data permission members API |Add associated members to a data permission rule, supporting users or user groups |
|Delete data permission members API |Remove associated members from a data permission rule |
|Get the list of row and column permission rules on a dataset |Query row\-level and column\-level permission rules for a dataset, supporting permission filtering for specified users |
|Create new row and column permissions on a dataset |Create row\-level or column\-level permission rules for a dataset, supporting fixed value and dynamic value configuration |
|Delete row and column permissions on a dataset |Delete specified row and column permission rules for a dataset |
|Modify row and column permissions on a dataset |Update the configuration content of row and column permission rules for a dataset |
|Authorize specified data permission rules to specified users on a dataset |Apply existing permission rules to specified users or groups |
|Remove specified data permission rule permissions from specified users on a dataset |Disassociate users or groups from specified permission rules |
|Get all fields with row and column permissions set on a chart |Query the list of fields with permission control configured in the dataset associated with the chart |


<span id="233aa52f"></span>
# Precautions

Before using the interfaces described in this document, familiarize yourself with the invocation methods. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="7945f44e"></span>
# Create a user group

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only project administrators can perform this operation.</div>


<span id="e8c0bf46"></span>
## Request description


* Request method: POST

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/group`


<span id="5e9d9490"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. For how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |
|name |string |Yes |“zhangsan” |User group name |
|description |string |Yes |"description_info", |User group description |
|isPublic |int |Yes |1 |1: Public user group, 0: Private user group |
|ownerList |string array |Yes |["admin1","admin2"] |Administrator list. Each element is a string. |


<span id="d5baaaaa"></span>
## Request example

```JSON
{
    "appId": 1, 
    "name": "zhangsan",
    "description": "description_info",  
    "isPublic": 1,
    "ownerList": ["admin1","admin2"]
}
```


<span id="ebe8c2f2"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |Status code, indicates the result of request processing |
|data |object | |User group information |
|msg |string |"Success" |Status message, textual description of the request result |


<span id="10c4adcf"></span>
## Response example

```JSON
{
  "code": "aeolus/ok", 
  "data": {
     用户组信息
  }, 
  "msg": "成功"
}
```


<span id="5e9a5349"></span>
# Query the list of user groups in a project

<span id="7e0a77a3"></span>
## Request description


* Request method: GET

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/groupList`


<span id="e93f10a7"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. For how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |


<span id="8e7f5c9b"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|data.groups |array |See the description below |User group list array |
|data.groups.description |string |"description" |User group description information |
|data.groups.id |int |1 |User group ID |
|data.groups.isPublic |int |0 |Whether it is a public user group. 1: Public user group, 0: Private user group |
|data.groups.name |string |"name" |User group name |
|data.groups.originId |string |"" |Original ID (may be empty) |
|data.groups.ownerList |array |["demo\-creator@2100\*\*\*\*\*\*"] |Administrator list |
|data.groups.source |int |4 |User group type (0: Department group; 1: Global user group; 2: Project user group; 3: Feishu group) |


<span id="64a39154"></span>
## Response example

```JSON
{
  "code": "aeolus/ok", 
  "msg": "成功",
  "data": {
    "groups": [
      {
        "description": "description",
        "id": 1,
        "isPublic": 0,
        "name": "name",
        "originId": "",
        "ownerList": [
            "demo-creator@2100******"
        ],
        "source": 4
      }
    ]
  }
}
```


<span id="2a4236ae"></span>
# Query user group members

<span id="2a1d6710"></span>
## Request description


* Request method: GET

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/groupMember`


<span id="ad2b8634"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. For how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |
|subjectId |number |Yes |1 |User group ID. For how to obtain it, see **Query the list of user groups under the project** |
|kw |string |No |"keywords" |Search keyword parameter. Default is empty, which means query all |
|perPage |int |No |20 |Pagination parameter, specifies the number per page, default is 20 |
|page |int |No |1 |Pagination parameter, specifies the page number, default is 1 |


<span id="993e2e03"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|data.members |array |*  |Member list |
|data.members.description |string |“description” |Member description |
|data.members.id |int |1 |Member ID |
|data.members.name |string |"Group name"/"Name" |Member name |
|data.members.originId |string |"Group id"/"Username" |Original member ID |
|data.members.source |int |0 |Source identifier (when type is 1, 0 means department, 1 means system\-level group, 2 means project\-level group; when type is 0, this field is not used) |
|data.members.type |int |1 |Member type (1 means group, 0 means user) |
|data.members.avatar |string |"Avatar link" |User avatar link (only present when type is 0) |
|data.members.departmentName |string |"Department name" |Department name (only present when type is 0) |
|data.members.emailPrefix |string |"Username" |User email prefix (only present when type is 0) |
|data.total |int |2 |Total number of members |
|msg |string |"Success" |Return message |


<span id="d91cdb67"></span>
## Response example

```Perl
{
    "code":"aeolus/ok",
    "data":{
        "members":[
            {
                "description":null,
                "id":1,
                "name":"组名称",
                "originId":"组id",
                "source":0, # When type is 1, source 0 means department, 1 means system-level group, 2 means project-level group
                "type":1 # type 1 means group
            },
            {
                "avatar":"头像链接",
                "departmentName":"部门名称",
                "emailPrefix":"用户名",
                "id":2,
                "name":"姓名",
                "originId":"用户名",
                "source":0, # When type is 0, the source field is not used
                "type":0 # type 0 means user
            }
        ],
        "total":2
    },
    "msg":"成功"
}
```


<span id="f4a5da8e"></span>
# Delete user group members

<span id="973ace5a"></span>
## Request description


* Request method: DELETE

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/groupMember`


<span id="f42f4955"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for instructions on obtaining it. |
|subjectId |number |Yes |12 |User group ID. See **Query the user group list under the project** for instructions. |
|groups |array[number] |No |[12,13] |User group ID list |
|users |array[number] |No |[1,2] |User ID list |
|originUsers |array[string] |No |["admin"] |Username list, union with users |


<span id="1a6fb6ad"></span>
## Request example

```JSON
{
    "appId": 1,  项目ID  类型int  必须参数
    "subjectId": 12,  用户组Id   类型number  必须参数
    "groups": [12,13],   用户组id列表(元素的类型为number)   可选参数
    "users": [1,2],   用户id列表(元素的类型为number)   可选参数
    "originUsers": ["admin"], 用户名列表，可选参数，与users取并集
}
```


<span id="1017e4dd"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |Status code returned by the API, indicating the result of the request |
|msg |string |"Success" |Status description returned by the API |


<span id="93d8b482"></span>
## Response example

```Perl
{
  "code": "aeolus/ok", 
  "msg": "成功"
}
```


<span id="696fcfcf"></span>
# Add user group members

<span id="cd2306d8"></span>
## Request description


* Request method: PUT

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/groupMember`


<span id="afa340f1"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for instructions on obtaining it. |
|subjectId |number |Yes |6 |User group ID |
|groups |array[number] |No |[12,13] |User group ID list |
|users |array[number] |No |[1,2] |User ID list |
|originUsers |array[string] |No |["admin"] |Username list, union with users |


<span id="53118da1"></span>
## Request example

```JSON
{
    "appId": 1,   项目ID  类型int  必须参数
    "subjectId": 6,   用户组Id   类型number  必须参数
    "groups": [12,13],   用户组id列表(元素的类型为number)   可选参数
    "users": [1,2],  用户id列表(元素的类型为number)   可选参数
    "originUsers": ["admin"],  用户名列表，可选参数，与users取并集
}
```


<span id="64091d68"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |Status code returned by the API, indicating the result of the request |
|msg |string |"Success" |Status description returned by the API |


<span id="55b06d69"></span>
## Response example

```Perl
{
  "code": "aeolus/ok", 
  "msg": "成功"
}
```


<span id="6c13ab58"></span>
# Remove users from a project

<span id="b25c40bb"></span>
## Request description


* Request method: DELETE

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/user`


<span id="98ccbe5f"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for instructions on obtaining it. |
|subjectIdList |array[number] |Yes |[12,13] |User group ID list |


<span id="4ecea54d"></span>
## Request example

```Perl
{
    "appId": 1,    项目ID  类型int  必须参数
    "subjectIdList": [12,13]    用户组Id列表(元素的类型为number) 必须参数
}
```


<span id="5629ca43"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |Status code returned by the API, indicating the result of the request |
|data |object |{} |Contains the specific data content returned by the request |
|msg |string |"Success" |Status description returned by the API |


<span id="bec9b15d"></span>
## Response example

```Perl
{
  "code": "aeolus/ok", 
  "data": {
  }, 
  "msg": "成功"
}
```


<span id="4b55565d"></span>
# Add users to a project

<span id="cf3234c9"></span>
## Request description


* Request method: DELETE

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/user`


<span id="4e2561e9"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for instructions on obtaining it. |
|originIdList |array[string] |Yes |["xiajinfu.xjf"] |List of users to be processed; elements are usernames. |
|action |string |Yes |"read_role" |Project permissions owned by the user. Enumeration values: read_role (read permission), write_role (write permission), read_all_role (read all permission), admin (administrator permission). When adding a user repeatedly, their existing higher\-level permissions will be revoked |


<span id="e7c4df35"></span>
## Request example

```JSON
{
     目标项目的id
    "appId": 1, 
     被操作的用户列表
    "originIdList": ["xiajinfu.xjf"], 
     用户拥有的项目权限，枚举值，read_role, write_role, read_all_role, admin
     重复添加用户会取消已有的更高级权限
     比如用户原有项目编辑权限，重复添加了用户，且参数是read_role，用户会被取消编辑权限，只有读权限
    "action": "read_role"  
}
```


<span id="68cc35e1"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |Status code returned by the API, indicating the result of the request |
|data |object |{} |Contains the specific data of the operation result |
|data.fails |array[string] |[] |List of users failed to be added |
|data.users |array[string] |[] |List of users added successfully |
|msg |string |"Success" |Status description returned by the API |


<span id="9e488683"></span>
## Response example

```Plain
{
  "code": "aeolus/ok", 
  "data": {
     添加失败的用户列表
    "fails": []
     添加成功的用户列表
    "users": []
  }, 
  "msg": "成功"
}
```


<span id="bc8884fa"></span>
# Associate a system\-level user group with a project

<span id="bf841f90"></span>
## Request description


* Request method: POST

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/relateGroup`


<span id="0de78e26"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for instructions on obtaining it. |
|originIdList |array[number] |Yes |[122345] |Primary key ID list of user groups; elements are numbers. |


<span id="d1db7b27"></span>
## Request example

```JSON
{
    # 目标项目的id
    "appId": 1, 
    # Kani 用户组的主键 id
    "originIdList": [122345],
}
```


<span id="f5dcb47b"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |Status code returned by the API, indicating the result of the request |
|data |object |{} |Contains the specific data of the association result |
|data.fails |array[number] |[] |List of user group IDs failed to be associated |
|data.groups |array[number] |[] |List of user group IDs associated successfully |
|msg |string |"Success" |Status description returned by the API |


<span id="be6669c9"></span>
## Response example

```JSON
{
  "code": "aeolus/ok", 
  "data": {
    # 关联失败的用户列表
    "fails": []
    # 关联成功的用户列表
    "groups": []
  }, 
  "msg": "成功"
}
```


<span id="2c0ec0db"></span>
# Get project list

<span id="19cf38b5"></span>
## Request description


* Request method: GET

* Request URL: `{{domain}}/aeolus/api/v3/open/queryEngine/apps`


<span id="3b5ce9a2"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID (see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for acquisition method) |


<span id="f2d6020d"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |Status code returned by the API, indicating the result of the request processing |
|data |array |*  |Project information list. Each element is a project object |
|data.appSettings |object |{} |Project settings |
|data.ctime |string |"2023\-07\-11 21:17:19" |Project creation time. Format: "YYYY\-MM\-DD HH:MM:SS" |
|data.id |int |1 |Project ID |
|data.isAdmin |int |1 |Whether it is an administrator project (1 = Yes, 0 = No) |
|data.isFavored |int |0 |Whether it is favorited (1 = Yes, 0 = No) |
|data.isPermitted |int |1 |Whether access is permitted (1 = Yes, 0 = No) |
|data.name |string |"Test project 1" |Project name |
|data.org |object |*  |Information about the organization the project belongs to |
|data.org.id |int |1 |Organization ID |
|data.org.name |string |"Default group" |Organization name |
|msg |string |"Success" |Status description returned by the API |


<span id="422b0fe7"></span>
## Response example

```SQL
{
  "code": "aeolus/ok", 
  "data": [
    {
      "appSettings": {},
      "ctime": "2023-07-11 21:17:19",
      "id": 1,
      "isAdmin": 1,
      "isFavored": 0,
      "isPermitted": 1,
      "name": "测试项目1",
      "org": {
        "id": 1,
        "name": "默认集团"
      }
    }
  ], 
  "msg": "成功"
}
```


<span id="8006acc3"></span>
# Get project user list

<span id="db2bd207"></span>
## Request description


* Request method: GET

* Request URL: `{{domain}}/aeolus/api/v3/open/userManagement/userList`


<span id="9620a146"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID (see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for acquisition method) |
|kw |string |No |"keywords" |Search keyword parameter. If empty, queries all records |
|perPage |int |No |20 |Pagination parameter. Specifies the number of items per page. Default is 20 |
|page |int |No |1 |Pagination parameter. Specifies the page number. Default is 1 |


<span id="331549bd"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|code |string |“aeolus/ok” |Status code returned |
|data.total |int |1 |User count |
|data.users |array |See return example |User list |
|data.users.id |long |100000000 |User ID |
|data.users.originId |string |“admin” |Original ID |
|data.users.name |string |“admin” |Username |
|data.users.email |string |"" |User email |
|data.users.phoneNumber |string |"" |User phone number |
|data.users.enable |boolean |true |Whether the user is enabled |
|msg |string |Success |Return message |


<span id="9e9d59fb"></span>
## Response example

```Plain
{
  "code": "aeolus/ok", 
  "data": {
      "total": 1,  用户数量
      "users": [{
        "id": 100000000,
        "originId": "admin",
        "name": "admin", 
        "email": "", 
        "phoneNumber": "",
        "enable": true
      }]
  }, 
  "msg": "成功"
}
```


<span id="9ac061a4"></span>
# Authorization API

<span id="a244012d"></span>
## Request description


* Request method: PUT

* Request URL: `{{domain}}/aeolus/api/v3/open/authManagement/resourceAuth`


<span id="6c8dc873"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|appId |int |Yes |123 |Project ID (see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for acquisition method) |
|resId |int |Yes |456 |Authorized resource ID |
|resType |string |Yes |data_set |Resource type (data_set: dataset, dashboard: dashboard, data_connection: data connection) |
|actions |array |Yes |["read_role"] |Permission list (read: read_role, write: write_role, manage: admin) |
|subjectList |array |Yes |[{"originId":"user_1", "type":0}] |Authorized subject list. Each object contains originId (username / group name) and type (0 \-\> person, 1 \-\> group) |


<span id="90fdb598"></span>
## Request example

```JSON
{
    // Project ID, type: integer
    "appId": {app_id},
    // Authorized resource ID, type: integer
    "resId": {res_id},
    // Resource type, type: string. data_set: dataset, dashboard: dashboard, data_connection: data connection
    "resType": {res_type},
    // Permission. read: read_role, write: write_role, manage: admin
    "actions":["read_role"],
    // originId: username, type: 0 -> person, 1 -> group. Multiple users can be added at once
    "subjectList":[{"originId":"user_1", "type":0}]
}
```


<span id="c8f5531f"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|code |string |aeolus/ok |Status code returned |
|data.fails |array |[{"originId":"user_1","subjectType":0,"reason":"xxx"}] |List of subjects for which authorization failed. If there are failures, fails is not empty. Each object contains originId (username / group name), subjectType (0 \-\> person, 1 \-\> group), and the reason for failure |
|msg |string |Success |Return message |


<span id="04cf0f65"></span>
## Response example

```Bash
{
  "code": "aeolus/ok",
  "data": {
    // 如果有失败则fails不为空
    // originId：用户名，subjectType：0->人，1->组，reason：失败原因
    "fails": [{"originId": "user_1", "subjectType": 0, "reason": "xxx"}]
  },
  "msg": "成功"
}
```


<span id="a3b284fc"></span>
# Get resource authorization details

<span id="5457a052"></span>
## Request description


* Request method: GET

* Request URL: `{{domain}}/aeolus/api/v3/open/authManagement/resourceAuth`


<span id="90576e61"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|appId |int |Yes |123 |Project ID (see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for acquisition method) |
|resId |int |Yes |456 |Resource ID |
|resType |string |Yes |data_set |Resource type (data_set: dataset, dashboard: dashboard) |
|detailed |int |No |1 |Permission acquisition mode (0: only acquire the user's own permissions on the resource, 1: consider permissions inherited by the user through roles and groups, default is 0) |


<span id="b00090b5"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|code |string |aeolus/ok |Return status code |
|data.roleList |array |*  |Role permission details list |
|data.roleList.actions |object | |Permission list (admin: admin, edit: write_role, view: read_role, view only: view_only_role) |
|data.roleList.actions.[Permission type] |array |[{"name":"role 1","subjectType":2}] |Role list corresponding to specific permissions |
|data.roleList.admins |array |[{"avatar":"","originId":"user_1"}] |Role administrator list |
|data.roleList.name |string |“role 1” |Role name |
|data.roleList.originId |string |“role_1” |Role id |
|data.roleList.roleKey |string |“role_key_1” |Role key |
|data.roleList.type |int |2 |Authorization entity type flag (0 \-\> user, 1 \-\> group, 2 \-\> role) |
|data.subjects |array |*  |User and group permission details list |
|data.subjects.actions |object | |Permission list |
|data.subjects.avatar |string |“” |Avatar URL |
|data.subjects.department |string |“department_1” |Department |
|data.subjects.emailPrefix |string |“” |Username (same as originId) |
|data.subjects.independentAuth |boolean |false |Whether to enable group authorization blocking |
|data.subjects.name |string |"User 1" |User name |
|data.subjects.originId |string |“user_1” |Username |
|data.subjects.source |int |0 |Authorization entity source (for groups: 0 \-\> department, 1 \-\> system\-level, 2 \-\> project\-level) |
|data.subjects.subjectId |int |1 |Authorization entity internal id |
|data.subjects.type |int |0 |Authorization entity type flag (0 \-\> user, 1 \-\> group, 2 \-\> role) |
|msg |string |"Success" |Return message |


<span id="56b0bb57"></span>
## Response example

```JSON
{
  "code": "aeolus/ok",
  "data": {
    // Role permission details list (if any)
    "roleList": [
      {
        // Permission list: admin: admin, edit: write_role, view: read_role, view only: view_only_role
        "actions": {
          "readRole": [
            {
              // Role name
              "name": "role 1",
              // Authorization entity type flag, 0 -> user, 1 -> group, 2 -> role
              "subjectType": 2
            }
          ],
          "viewOnlyRole": [
            {
              "name": "role 1",
              "subjectType": 2
            }
          ]
        },
        // Role administrator
        "admins": [
          {
            // Administrator avatar URL
            "avatar": "",
            // Administrator username
            "originId": "user_1"
          }
        ],
        // Role name
        "name": "role 1",
        // Role id
        "originId": "role_1",
        // Role key
        "roleKey": "role_key_1",
        // Authorization entity type flag, 0 -> user, 1 -> group, 2 -> role
        "type": 2
      }
    ],
    // User and group permission details list
    "subjects": [
      {
        // Permission list: admin: admin, edit: write_role, view: read_role, view only: view_only_role
        "actions": {
          "admin": [
            {
              // Authorization entity name
              "name": "用户1",
              // Authorization entity type flag, 0 -> user, 1 -> group, 2 -> role
              "subjectType": 0
            }
          ],
          "readRole": [],
          "viewOnlyRole": [],
          "writeRole": []
        },
        // Avatar URL
        "avatar": "",
        // Department
        "department": "department_1",
        // Username (same as originId)
        "emailPrefix": "",
        // Whether to enable group authorization blocking
        "independentAuth": false,
        // User name
        "name": "用户1",
        // Username
        "originId": "user_1",
        // Authorization entity source (for groups) 0 -> department, 1 -> system-level, 2 -> project-level
        "source": 0,
        // Authorization entity internal id
        "subjectId": 1,
        // Authorization entity type flag, 0 -> user, 1 -> group, 2 -> role
        "type": 0
      }
    ]
  },
  "msg": "成功"
}
```


<span id="d8a4efc2"></span>
# Update user attribute API

```Bash
请求说明
请求地址：PUT http://{domain}/aeolus/api/v3/open/userManagement/subjectAttributeValue
请求参数
参数为json格式，originId表示的用户需要在系统中存在，如下：
{
    // 项目id
    "appId": {app_id},
    // 用户名
    "originId": {origin_id},
    // 属性id
    "attributeId": {attribute_id},
    // 属性值
    "valueList": ["test"]
}

返回示例
{
  "code": "aeolus/ok",
  "data": {attribute_value_id},
  "msg": "成功"
}
```


The user attribute ID can be viewed in the console on the user attribute page, for example:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b4a22247de89dc508eef9fca247ed3e.png) </span>

The attribute ID in the delete user attribute API can be viewed in the same way.

<span id="9c58b464"></span>
# Delete user attribute API

```Apache
请求说明
请求地址：DELETE http://{domain}/aeolus/api/v3/open/userManagement/subjectAttribute
Authorization: Bearer jwt_token
请求参数
入参：json格式
{
     项目id
    "appId":{appId},
     属性id
    "attributeId":65
}
返回示例
{
  "code": "aeolus/ok", 
  "data": 65, 
  "msg": "成功"
}
```


<span id="fb9d3114"></span>
# Get data permission member API

```Bash
请求说明
请求地址：GET http://{domain}/aeolus/api/v3/open/authManagement/filterRuleMember
请求参数
参数：query string
appId: 必选参数，项目id
filterRuleId: 必选参数，规则id
perPage: 可选参数
page: 可选参数
kw: 可选参数，过滤关键词，不传则不过滤
orderBy: 可选参数，默认成员时间addTime排序
order: 可选参数，默认降序
needAll: 可选参数，1为返回全量；0为分页返回，默认为0

返回示例
{
  "code": "aeolus/ok", 
  "data": {
    "subjectList": [
      {
        // 添加时间
        "addTime": "2022-01-01 00:00", 
        "department": "", 
        // 用户姓名
        "name": "用户1", 
        // 用户名
        "originId": "user_1", 
        // 0->人，1->组
        "type": 0
        "subjectId": 1, 
      }
    ], 
    // 总记录数
    "total": 1
  }, 
  "msg": "成功"
}
```


<span id="9e8d80ad"></span>
# Add data permission member API

```Bash
请求地址
POST http://{domain}/aeolus/api/v3/open/authManagement/filterRuleMember
请求参数
参数为json格式，originId表示的用户需要在系统中存在，如下：
{
    // 项目id
    "appId": {app_id},
    // 数据权限id
    "filterRuleId": {filter_rule_id},
    // originId：用户名，type：0->人，1->组
    "originList":[{"originId":"user_1", "type":0}]
}

返回示例
{
  "code": "aeolus/ok",
  "data": {
    // 如果有失败则fails不为空
    // originId：用户名，subjectType：0->人，1->组，reason：失败原因
    "fails": [{"originId": "user_1", "subjectType": 0, "reason": "xxx"}]
  },
  "msg": "成功"
}
```


<span id="fedb7797"></span>
# Delete data permission member API

```Bash
请求说明
请求地址 ：DELETE http://{domain}/aeolus/api/v3/open/authManagement/filterRuleMember
请求参数
参数为json格式，originId表示的用户需要在系统中存在，如下：
{
    // 项目id
    "appId": {app_id},
    // 数据权限id
    "filterRuleId": {filter_rule_id},
    // originId：用户名，type：0->人，1->组
    "originList":[{"originId":"user_1", "type":0}]
}

返回示例
{
  "code": "aeolus/ok",
  "data": {
    // 如果有失败则fails不为空
    // originId：用户名，subjectType：0->人，1->组，reason：失败原因
    "fails": [{"originId": "user_1", "type": 0, "reason": "xxx"}]
  },
  "msg": "成功"
}
```


<span id="de993a83"></span>
# Get the list of row and column permission rules on the dataset

```Plain
请求说明
请求地址：GET http://{domain}/aeolus/api/v3/open/authManagement/dataPermissions
请求参数
参数：query string
appId: 必选参数，项目id
dataSetId: 必选参数，资源id
page: 必选参数，第几页，1
perPage: 必选参数，每页多少，20
authOriginId: 可选参数，被授权人originId，zhangsan.1

返回示例
{
    "code": "aeolus/ok",
    "data": {
        // 是否开启黑白名单
        "blackEnabled": false,
        // 规则列表
        "filterRuleList": [
            {
                // 项目ID
                "appId": 1,
                // 创建时间，默认按照创建时间排序
                "ctime": "2022-08-02 15:40",
                // 数据集ID
                "dataSetId": ******,
                // 子规则列表
                "filterRowList": [
                    {
                        // 子规则ID
                        "rowId": ****,
                        // 子规则内容
                        "rowNode": {
                            // 列权限受限数据集字段
                            "dimMetList": [
                                {
                                    // 数据集字段ID
                                    "id": 158*********190,
                                    // 数据集字段名
                                    "name": "特殊字段"
                                },
                                {
                                    "id": 158*********176,
                                    "name": "产品 ID"
                                }
                            ],
                            // 列权限受限底表字段
                            "fieldList": [
                                {
                                    // 底表字段名
                                    "fieldName": "国家/地区",
                                    // 底表字段关联的数据集字段
                                    "relatedDimMetList": [
                                        {
                                            // 数据集字段类型
                                            "dataTypeName": "string",
                                            // 数据集字段关联的底表字段
                                            "fieldList": "[\"国家/地区\"]",
                                            // 数据集字段ID
                                            "id": 158*********175,
                                            // 数据集字段名
                                            "name": "国家/地区",
                                            "persisted": true
                                        }
                                    ]
                                },
                                {
                                    "fieldName": "细分",
                                    "relatedDimMetList": [
                                        {
                                            "dataTypeName": "string",
                                            "fieldList": "[\"细分\"]",
                                            "id": 158*********188,
                                            "name": "细分",
                                            "persisted": true
                                        }
                                    ]
                                }
                            ],
                            // 子规则内关联关系，仅行权限有效，'and'->且，'or'->或
                            "linkType": "and"
                        },
                        // 固定值还是动态值，仅行权限有效，0->固定值，1->动态值
                        "rowTmplType": 0,
                        // 行权限还是列权限，0->行权限，1->列权限
                        "rowType": 1
                    }
                ],
                // 规则名字
                "name": "测试2",
                // 规则创建者
                "owner": {
                    // 创建者头像
                    "avatar": "url",
                    // 创建者名字
                    "name": "xxx",
                    // 创建者origin_id
                    "originId": "xxx",
                    // 创建者类型，一般为0
                    "subjectType": 0
                },
                // 行权限还是列权限，0->行权限，1->列权限
                "rowType": 1,
                // 规则ID
                "ruleId": 1447,
                // 规则适用对象列表
                "subjectList": [
                    {
                        // 用户origin_id，在用户中唯一标识
                        "originId": "xxx"
                        // 邮箱前缀
                        "emailPrefix": null,
                        // subject表ID
                        "id": xxx,
                        // 名字
                        "name": "xxx",
                        // 和type一起判断组类型，0->部门组，1->系统组，2->项目组
                        "source": 0,
                        // 个人还是用户组，1->组，0->个人
                        "type": 1
                    },
                    {
                        "emailPrefix": "xxx",
                        "id": xxx,
                        "name": "xxx",
                        "source": 0,
                        // 个人
                        "type": 0
                    }
                ],
                // 规则类型，0->个人，1->审批流，一般TOB只有0
                "type": 0
            },
            {
                "appId": 1,
                "ctime": "2022-08-02 15:39",
                "dataSetId": 183454,
                "filterRowList": [
                    {
                        "rowId": 6248,
                        "rowNode": {
                            "dimMetList": [],
                            "fieldList": [
                                {
                                    // 数据集字段ID
                                    "fieldId": 158*********180,
                                    // 数据集字段名
                                    "fieldName": "城市",
                                    // 操作符，in->在列表内
                                    "op": "in",
                                    // 用户属性ID,-1用户名,-2姓名,-3邮箱,-4部门,-5城市
                                    "value": -5
                                },
                                {
                                    "fieldId": 158*********179,
                                    "fieldName": "子类别",
                                    "op": "in",
                                    // 用户自己设置的动态值属性
                                    "value": 316
                                }
                            ],
                            // 子规则内关联关系，且
                            "linkType": "and"
                        },
                        // 动态值
                        "rowTmplType": 1,
                        // 行权限
                        "rowType": 0
                    },
                    {
                        "rowId": 6249,
                        "rowNode": {
                            "dimMetList": [],
                            "fieldList": [
                                {
                                    "fieldId": 158*********176,
                                    "fieldName": "产品 ID",
                                    // op与valOption组合为操作符
                                    "op": "in",
                                    "valOption": {},
                                    // 固定值
                                    "value": [
                                        "办公用-信封-10000017"
                                    ]
                                },
                                {
                                    "fieldId": 158*********178,
                                    "fieldName": "地区",
                                    "op": "in",
                                    "valOption": {},
                                    "value": [
                                        "中南"
                                    ]
                                }
                            ],
                            // 子规则内关联关系，或
                            "linkType": "or"
                        },
                        // 固定值
                        "rowTmplType": 0,
                        // 行权限
                        "rowType": 0
                    }
                ],
                "name": "ceshi121",
                "owner": {
                    "avatar": "xxx",
                    "name": "xxx",
                    "originId": "xxx",
                    "subjectType": 0
                },
                "rowType": 0,
                "ruleId": 1446,
                "subjectList": [
                    {
                        "emailPrefix": "xxx",
                        "id": xxx,
                        "name": "xxx",
                        "source": 0,
                        "type": 0
                    },
                    {
                        "emailPrefix": null,
                        "id": xxx,
                        "name": "xxx",
                        "source": 0,
                        "type": 1
                    }
                ],
                "type": 0
            }
        ],
        // 合计，不受分页影响
        "total": 9
    },
    "msg": "成功"
}
```


<span id="c493f8c4"></span>
# Create row and column permissions on the dataset

Create row permissions

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_927592fb760389bfcbce0c4311b65d78.png) </span>

```Plain
请求说明
请求地址：POST http://{domain}/aeolus/api/v3/open/authManagement/filterRule
请求参数
参数为json格式，originId表示的用户需要在系统中存在，如下：
{
    // 项目ID
    "appId": 1,
    // 数据集ID
    "dataSetId": ******,
    // 规则名字，同一数据集下不能重名
    "name": "ceshi6",
    // 适用对象
    "originList": [
        {
            //subject表的origin_id
            "originId": "xxxx",
            // 个人还是组，0->个人，1->组
            "type": 0
        },
        {
            "originId": "*****",
            "type": 1
        }
    ],
    // 规则内容
    "rowNodeList": [
        {
            // 行权限还是列权限，0->行，1->列
            "rowType": 0,
            // 动态值还是固定值，0->固定值，1->动态值
            "rowTmplType": 0,
            // 子规则内容
            "rowNode": {
                // 子规则内关联关系,'and'->且，'or'->或
                "linkType": "or",
                "fieldList": [
                    {
                        // 数据集ID
                        "fieldId": ****,
                        // 操作符，一般op和valOption结合确认操作符
                        "op": "in",
                        // 辅助操作符
                        "valOption": {},
                        // 固定值
                        "value": [
                            "办公020"
                        ]
                    },
                    {
                        "fieldId": {fieldId},
                        "op": "in",
                        "valOption": {},
                        "value": [
                            "CN-20062"
                        ]
                    }
                ]
            }
        },
        {
            "rowType": 0,
            // 动态值
            "rowTmplType": 1,
            "rowNode": {
                // 子规则内，取'且'的逻辑判断
                "linkType": "and",
                "fieldList": [
                    {
                        "fieldId": {fieldId},
                        "op": "in",
                        // 用户属性ID,-1用户名,-2姓名,-3邮箱,-4部门,-5城市
                        "value": -5
                    },
                    {
                        "fieldId": {fieldId},
                        "op": "in",
                        // 用户属性ID，大于0的是自建属性ID
                        "value": 352
                    }
                ]
            }
        }
    ]
}

返回示例
{
    "code": "aeolus/ok",
    "data": {
        // 规则ID
        "filterRuleId": 1450
    },
    "msg": "成功"
}
```


Create column permissions

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35eeb5054296ca91e3e66c398f4dda36.png) </span>

```Plain
请求说明
请求地址：POST http://{domain}/aeolus/api/v3/open/authManagement/filterRule
请求参数
参数为json格式，originId表示的用户需要在系统中存在，如下：
{
    "appId": 1,
    "dataSetId": ******,
    "name": "ceshi8",
    "originList": [
        {
            "originId": "xxx",
            "type": 0
        }
    ],
    "rowNodeList": [
        {
            //固定为1，列权限
            "rowType": 1,
            // 固定为0
            "rowTmplType": 0,
            "rowNode": {
                // 固定为'and'
                "linkType": "and",
                // 受限底表字段列表
                "fieldList": [
                    {
                        // 底表字段名
                        "fieldName": "地区"
                    },
                    {
                        "fieldName": "子类别"
                    }
                ],
                // 受限数据集字段列表
                "dimMetList": [
                    {
                        // 数据集字段ID
                        "id": {id},
                        // 数据集字段名
                        "name": "订单 ID"
                    },
                    {
                        "id": {id},
                        "name": "行 ID"
                    }
                ]
            }
        }
    ]
}
```


<span id="feef82e5"></span>
# Delete row and column permissions on the dataset

```Plain
请求说明
请求地址：DELETE /aeolus/api/v3/open/authManagement/filterRule
Authorization: Bearer jwt_token
请求参数
入参：json格式
{
    // 项目ID
    "appId": 1,
    // 行列权限规则ID
    "filterRuleId": ****
}
返回示例
{
    "code": "aeolus/ok",
    "data": {
        "affectedRows": 1
    },
    "msg": "成功"
}
```


<span id="17ac3649"></span>
# Edit row and column permissions on the dataset

```Plain
请求说明
请求地址：PUT http://{domain}/aeolus/api/v3/open/authManagement/filterRule
请求参数
修改传参与新建传参基本一致，新增filterRuleId字段，指定更新哪个规则
参数为json格式，originId表示的用户需要在系统中存在，如下：
{
    "appId": 1,
    "dataSetId":******,
    "name": "ceshi6",
    // 行列权限规则ID
    "filterRuleId": "****",
    "originList": [
        {
            "originId": "*****",
            "type": 1
        },
        {
            "originId": "xielinjiang",
            "type": 0
        }
    ],
    "rowNodeList": [
        {
            "rowType": 0,
            "rowTmplType": 0,
            "rowNode": {
                "linkType": "or",
                "fieldList": [
                    {
                        "fieldId": {fieldId},
                        "op": "in",
                        "valOption": {},
                        "value": [
                            "办公用-信封-10000020"
                        ]
                    },
                    {
                        "fieldId": {fieldId},
                        "op": "in",
                        "valOption": {},
                        "value": [
                            "CN-2016-1******"
                        ]
                    }
                ]
            }
        },
        {
            "rowType": 0,
            "rowTmplType": 1,
            "rowNode": {
                "linkType": "and",
                "fieldList": [
                    {
                        "fieldId": {fieldId},
                        "op": "in",
                        "value": -5
                    },
                    {
                        "fieldId":{fieldId},
                        "op": "in",
                        "value": 352
                    }
                ]
            }
        }
    ]
}

返回示例
{
    "code": "aeolus/ok",
    "data": {
        "filterRuleId": ****
    },
    "msg": "成功"
}
```


<span id="af51628b"></span>
# Get the list of row and column permission rules for a specified person on the dataset

Refer to `Get the list of row and column permission rules on the dataset`

Use the field authOriginId

<span id="4f8416b6"></span>
# Authorize a specified user with a specified data permission rule on the dataset

Not for creating new data permissions; to create, use the `Create row and column permissions on the dataset` API

```Plain
请求地址
POST http://{domain}/aeolus/api/v3/open/authManagement/filterRuleMember
请求参数
参数为json格式，originId表示的用户需要在系统中存在，如下：

{
    // 项目ID
    "appId": 1,
    // 规则ID
    "filterRuleId": ****,
    // 需要授予权限的对象列表
    "originList": [
        {
            // 对象origin_id
            "originId": "xxx",
            // 指定0
            "type": 0
        }
    ]
}

返回示例
{
    "code": "aeolus/ok",
    "data": {
        // 操作失败的用户会在这里
        "fails": [
            {
                "originId": "xxx",
                "reason": "subject未找到",
                "type": 0
            }
        ]
    },
    "msg": "成功"
}
```


<span id="a7926253"></span>
# Remove a specified data permission rule from a specified user on the dataset

Not for deleting data permissions; to delete, use the `Delete row and column permissions on the dataset` API

```Plain
请求地址
DELETE http://{domain}/aeolus/api/v3/open/authManagement/filterRuleMember
请求参数
参数为 json 格式，originId 表示的用户需要在系统中存在，与授予权限一致，如下：

{
    // 项目ID
    "appId": 1,
    // 规则ID
    "filterRuleId": ****,
    // 需要移除权限的对象列表
    "originList": [
        {
            // 对象origin_id
            "originId": "xxx",
            // 指定0
            "type": 0
        }
    ]
}

返回示例
{
    "code": "aeolus/ok",
    "data": {
        // 操作失败的用户会在这里
        "fails": [
            {
                "originId": "xxx",
                "reason": "subject未找到",
                "type": 0
            }
        ]
    },
    "msg": "成功"
}
```


<span id="f5d5616e"></span>
# Get all fields with row and column permissions set on the chart

```Plain
请求地址
GET http://{domain}/aeolus/api/v3/open/authManagement/sensitiveDimMet
请求参数
参数：query string
appId: 必选参数，项目id
resType: 必选参数，资源类型，目前仅支持图表，report
resId: 必选参数，资源ID

返回示例
{
    "code": "aeolus/ok",
    "data": {
        // 数据集ID
        "183454": {
            // 行权限
            "0": {
                // 字段ID：字段名
                "158*********176": "产品 ID",
                "158*********177": "订单 ID",
                "158*********178": "地区",
                "158*********179": "子类别",
                "158*********180": "城市",
                "158*********184": "订单日期",
                "158*********185": "发货日期",
                "158*********188": "细分",
                "158*********192": "折扣"
            },
            // 列权限
            "1": {
                // 字段ID：字段名
                "158*********175": "国家/地区",
                "158*********176": "产品 ID",
                "158*********177": "订单 ID",
                "158*********178": "地区",
                "158*********179": "子类别",
                "158*********188": "细分",
                "158*********190": "特殊字段",
                "158*********193": "行 ID"
            }
        }
    },
    "msg": "成功"
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on the wildcard for data row and column permissions, see <a href="https://docs.byteplus.com/docs/DataWind/Data_Row_and_Column_Permission_Operators">Data Row and Column Permission Operators</a>.</div>
