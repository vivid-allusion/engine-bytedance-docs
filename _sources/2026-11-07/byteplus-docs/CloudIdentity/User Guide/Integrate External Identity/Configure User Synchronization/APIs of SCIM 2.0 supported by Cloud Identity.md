---
title: "APIs of SCIM 2.0 supported by Cloud Identity"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/APIs-of-SCIM-supported-by-Cloud-Identity"
---

<span id="usage-notes"></span>
## **Usage notes**

The implementation of the APIs of SCIM 2.0 complies with RFC 7644. For details, refer to [RFC 7644](https://datatracker.ietf.org/doc/html/rfc7644).

<span id="endpoint-and-region"></span>
## Endpoint and region

Endpoint of the SCIM service: [https://cloudidentity-scim.${region}.bytepluses.com/scim/v2/](https://cloudidentity-scim.$%7Bregion%7D.bytepluses.com/scim/v2/)

<span id="apis-of-scim-2-0"></span>
## APIs of SCIM 2.0


|Category |API |Supported |Description |
|---|---|---|---|
|/Me |N/A |No |N/A |
|/Bulk |N/A |No |N/A |
|Discovery Endpoint |/ServiceProviderConfig |Yes |Describes the SCIM features supported by the service provider (SP). |
||/ResourceTypes |Yes |Discovers the resource types supported by the SCIM SP, such as users and groups. |
||/Schemas |Yes |Obtains the information of the schemas supported by the SCIM SP. |
|/Users |GET /Users |Yes |Queries user information by condition or queries the list of all users.<br><br>If you do not specify a filter, all users are returned. |
||GET /Users/ |Yes |Queries the user with the specified ID. |
||POST /Users |Yes |Creates users. |
||PUT /Users/ |Yes |Replaces the information of the user with the specified ID. |
||DELETE /Users/ |Yes |Deletes the user with the specified ID. |
||PATCH /Users/ |Yes |Updates the information of the user with the specified ID. The following three options are supported: add, remove, and replace. |
|/Groups |GET /Groups |Yes |Queries user group information by condition or queries the list of all user groups.<br><br>If you do not specify a filter, all user groups are returned. |
||GET /Groups/ |Yes |Queries the user group with the specified ID. |
||POST /Groups |Yes |Creates user groups. |
||PUT /Groups/ |Yes |Replaces the information of the user group with the specified ID. |
||DELETE /Groups/ |Yes |Deletes the user group with the specified ID. |
||PATCH /Groups/ |Yes |Updates the information of the user group with the specified ID. |


<span id="discovery-endpoint"></span>
## Discovery Endpoint

<span id="serviceproviderconfig"></span>
### /ServiceProviderConfig

<span id="feature-description"></span>
#### Feature description

Obtains the SP configuration.

<span id="sample-request"></span>
#### Sample request

```sql
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/ServiceProviderConfig'  
--header 'Authorization: Bearer ••••••'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "authenticationSchemes": [ 
        { 
            "description": "Authentication using OAuth Bearer Token", 
            "documentationUri": "https://docs.byteplus.com/en/docs/CloudIdentity/Overview-of-SCIM-based-user-synchronization", 
            "name": "OAuth Bearer Token", 
            "primary": true, 
            "specUri": "https://tools.ietf.org/html/rfc6750", 
            "type": "oauth2" 
        } 
    ], 
    "bulk": { 
        "maxOperations": 0, 
        "maxPayloadSize": 0, 
        "supported": false 
    }, 
    "changePassword": { 
        "supported": false 
    }, 
    "documentationUri": "https://docs.byteplus.com/en/docs/CloudIdentity/Overview-of-SCIM-based-user-synchronization", 
    "etag": { 
        "supported": false 
    }, 
    "filter": { 
        "maxResults": 100, 
        "supported": true 
    }, 
    "patch": { 
        "supported": true 
    }, 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:ServiceProviderConfig" 
    ], 
    "sort": { 
        "supported": false 
    } 
}
```


<span id="resourcetypes"></span>
### /ResourceTypes

<span id="feature-description"></span>
#### Feature description

Discovers the resource types supported by the SCIM SP, such as users and groups.

<span id="sample-request"></span>
#### Sample request

```bash
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/ResourceTypes'  
--header 'Authorization: Bearer ••••••'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "itemsPerPage": 2, 
    "resources": [ 
        { 
            "description": "Work-Force User", 
            "endpoint": "/Users", 
            "id": "User", 
            "meta": { 
                "location": "/ResourceTypes/User", 
                "resourceType": "ResourceType" 
            }, 
            "name": "User", 
            "schema": "urn:ietf:params:scim:schemas:core:2.0:User", 
            "schemas": [ 
                "urn:ietf:params:scim:schemas:core:2.0:ResourceType" 
            ] 
        }, 
        { 
            "description": "Work-Force User Group", 
            "endpoint": "/Groups", 
            "id": "Group", 
            "meta": { 
                "location": "/ResourceTypes/Group", 
                "resourceType": "ResourceType" 
            }, 
            "name": "Group", 
            "schema": "urn:ietf:params:scim:schemas:core:2.0:Group", 
            "schemas": [ 
                "urn:ietf:params:scim:schemas:core:2.0:ResourceType" 
            ] 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:ListResponse" 
    ], 
    "startIndex": 1, 
    "totalResults": 2 
}
```


<span id="schemas"></span>
### /Schemas

<span id="feature-description"></span>
#### Feature description

Obtains the information of the schemas supported by the SCIM SP.

<span id="sample-request"></span>
#### Sample request

```bash
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Schemas'  
--header 'Authorization: Bearer ••••••'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "itemsPerPage": 2, 
    "resources": [ 
        { 
            "attributes": [ 
                { 
                    "caseExact": false, 
                    "description": "Human-Readable User Unique Identifier", 
                    "multiValued": false, 
                    "mutability": "readWrite", 
                    "name": "userName", 
                    "required": true, 
                    "returned": "always", 
                    "type": "string", 
                    "uniqueness": "server" 
                }, 
                { 
                    "caseExact": false, 
                    "description": "Display Name for Assisting in User Identity Identification, Non-Unique", 
                    "multiValued": false, 
                    "mutability": "readWrite", 
                    "name": "displayName", 
                    "required": false, 
                    "returned": "default", 
                    "type": "string", 
                    "uniqueness": "none" 
                }, 
                { 
                    "caseExact": false, 
                    "description": "Contact Email of User", 
                    "multiValued": true, 
                    "mutability": "readWrite", 
                    "name": "emails", 
                    "required": false, 
                    "returned": "default", 
                    "subAttributes": [ 
                        { 
                            "caseExact": false, 
                            "multiValued": false, 
                            "mutability": "readWrite", 
                            "name": "value", 
                            "required": true, 
                            "returned": "default", 
                            "type": "string", 
                            "uniqueness": "none" 
                        } 
                    ], 
                    "type": "complex", 
                    "uniqueness": "none" 
                }, 
                { 
                    "caseExact": false, 
                    "description": "Contact mobile number of User", 
                    "multiValued": true, 
                    "mutability": "readWrite", 
                    "name": "phoneNumbers", 
                    "required": false, 
                    "returned": "default", 
                    "subAttributes": [ 
                        { 
                            "caseExact": false, 
                            "multiValued": false, 
                            "mutability": "readWrite", 
                            "name": "value", 
                            "required": true, 
                            "returned": "default", 
                            "type": "string", 
                            "uniqueness": "none" 
                        } 
                    ], 
                    "type": "complex", 
                    "uniqueness": "none" 
                } 
            ], 
            "description": "Work-Force User", 
            "id": "urn:ietf:params:scim:schemas:core:2.0:User", 
            "meta": { 
                "location": "/Schemas/urn:ietf:params:scim:schemas:core:2.0:User", 
                "resourceType": "Schema" 
            }, 
            "name": "User", 
            "schemas": [ 
                "urn:ietf:params:scim:schemas:core:2.0:Schema" 
            ] 
        }, 
        { 
            "attributes": [ 
                { 
                    "caseExact": false, 
                    "description": "Human-Readable User Group Unique Identifier", 
                    "multiValued": false, 
                    "mutability": "readWrite", 
                    "name": "displayName", 
                    "required": true, 
                    "returned": "always", 
                    "type": "string", 
                    "uniqueness": "none" 
                }, 
                { 
                    "caseExact": false, 
                    "description": "Display Name for User Group, Non-Unique", 
                    "multiValued": true, 
                    "mutability": "readWrite", 
                    "name": "members", 
                    "required": false, 
                    "returned": "default", 
                    "subAttributes": [ 
                        { 
                            "caseExact": false, 
                            "multiValued": false, 
                            "mutability": "readWrite", 
                            "name": "value", 
                            "required": true, 
                            "returned": "default", 
                            "type": "string", 
                            "uniqueness": "none" 
                        } 
                    ], 
                    "type": "complex", 
                    "uniqueness": "none" 
                } 
            ], 
            "description": "Work-Force User Group", 
            "id": "urn:ietf:params:scim:schemas:core:2.0:Group", 
            "meta": { 
                "location": "/Schemas/urn:ietf:params:scim:schemas:core:2.0:Group", 
                "resourceType": "Schema" 
            }, 
            "name": "Group", 
            "schemas": [ 
                "urn:ietf:params:scim:schemas:core:2.0:Schema" 
            ] 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:ListResponse" 
    ], 
    "startIndex": 1, 
    "totalResults": 2 
}
```


<span id="users"></span>
## /Users

<span id="get-users"></span>
### GET /Users

<span id="feature-description"></span>
#### Feature description

Queries user information by condition or queries the list of all users.

<span id="limits"></span>
#### Limits


* You can only specify the externalId, userName, or id field as a filter, and can only use the EQ and AND operators.

* You can use the pagination method of SCIM, which can return up to 100 records each page. If you specify a count value greater than 100, 100 is used as the actual count value.

* You can only query users synchronized by the SCIM service.



|Parameter |Description |Example |
|---|---|---|
|filter |Supports only the EQ and AND expressions of the userName, externalId, or id field. |* filter=Id eq 3001234662656<br><br>* filter=externalId eq exid\-sfji2ni3ti3<br><br>* filter=userName eq test\-user |
|startIndex |Specifies the index. It can be left empty and the default value is 1. |\- startIndex=1 |
|count |Specifies the number of users on each page. It can be left empty and the default value is 10.。 |\- count=100 |


<span id="sample-request"></span>
#### Sample request

```bash
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Users?filter=id+eq+%223001234662656%22'  
--header 'Authorization: Bearer ••••••'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "itemsPerPage": 100, 
    "resources": [ 
        { 
            "displayName": "test-user", 
            "emails": [], 
            "id": "3001234662656", 
            "meta": { 
                "created": "2025-04-15T08:17:13Z", 
                "lastModified": "2025-04-15T08:17:13Z", 
                "location": "/Users/3001234662656", 
                "resourceType": "User" 
            }, 
            "phoneNumbers": [], 
            "schemas": [ 
                "urn:ietf:params:scim:schemas:core:2.0:User" 
            ], 
            "userName": "test" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:ListResponse" 
    ], 
    "startIndex": 1, 
    "totalResults": 1 
}
```


<span id="get-users"></span>
### GET /Users/

<span id="feature-description"></span>
#### Feature description

Queries the user with the specified ID.

<span id="limits"></span>
#### Limits


* If the user with the specified ID does not exist, access is denied.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Users/3001234662656'  
--header 'Authorization: Bearer ••••••'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "displayName": "test-user", 
    "emails": [], 
    "id": "3001234662656", 
    "meta": { 
        "created": "2025-04-15T08:17:13Z", 
        "lastModified": "2025-04-15T08:17:13Z", 
        "location": "/Users/3001234662656", 
        "resourceType": "User" 
    }, 
    "phoneNumbers": [], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:User" 
    ], 
    "userName": "test" 
}
```


<span id="post-users"></span>
### POST /Users

<span id="feature-description"></span>
#### Feature description

Creates users.

<span id="limits"></span>
#### Limits


* If users with the same name exist in the Cloud Identity instance, the creation request is denied.

* If users with the same externalId exist in the Cloud Identity instance, the creation request is denied.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location --request POST  'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Users'  
--header 'Content-Type: application/json'  
--header 'Authorization: Bearer ••••••'  
--data-raw '{ 
    "displayName": "test-user", 
    "emails": [ 
        { 
            "value":"<your email>" 
        } 
    ], 
    "phoneNumbers": [ 
        { 
            "value":"<your phone>" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:User" 
    ], 
    "userName": "test-user" 
}'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "displayName": "test-user", 
    "emails": [ 
        { 
            "primary": true, 
            "type": "work", 
            "value": "<your email>" 
        } 
    ], 
    "id": "3158367515904", 
    "meta": { 
        "created": "2025-05-08T10:52:32Z", 
        "lastModified": "2025-05-08T10:52:32Z", 
        "location": "/Users/3158367515904", 
        "resourceType": "User" 
    }, 
    "phoneNumbers": [ 
        { 
            "primary": true, 
            "value": "<your phone>", 
            "type": "work" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:User" 
    ], 
    "userName": "test-user" 
}
```


<span id="put-users"></span>
### PUT /Users

<span id="feature-description"></span>
#### Feature description

Replaces the information of the user with the specified ID.

<span id="limits"></span>
#### Limits


* An ID is required, and fields defined in the schema are modified.

* If the user with the specified ID does not exist, access is denied.

* As the PUT method is used, the original attributes are overwritten.

* As the PUT method is used, fields that are not specified remain unchanged, while fields explicitly set to an empty value are overwritten with that empty value.

* Only the information of users synchronized by the SCIM service can be modified.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location --request PUT 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Users/3158367515904'  
--header 'Content-Type: application/json'  
--header 'Authorization: Bearer ••••••'  
--data '{ 
    "externalId": "test-exid", 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:User" 
    ], 
    "userName": "test-user" 
}'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "displayName": "test-user", 
    "emails": [ 
        { 
            "primary": true, 
            "type": "work", 
            "value": "<your email>" 
        } 
    ], 
    "externalId": "test-exid", 
    "id": "3158367515904", 
    "meta": { 
        "created": "2025-05-08T10:52:32Z", 
        "lastModified": "2025-05-08T10:59:08Z", 
        "location": "/Users/3158367515904", 
        "resourceType": "User" 
    }, 
    "phoneNumbers": [ 
        { 
            "primary": true, 
            "value": "<your phone>", 
            "type": "work" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:User" 
    ], 
    "userName": "test-user" 
}
```


<span id="delete-users"></span>
### DELETE /Users

<span id="feature-description"></span>
#### Feature description

Deletes the user with the specified ID.

<span id="limits"></span>
#### Limits


* An ID is required.

* If the user with the specified ID does not exist, access is denied.

* Only users synchronized by the SCIM service can be deleted.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location --request DELETE 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Users/3158367515904'  
--header 'Authorization: Bearer ••••••'
```


<span id="patch-users"></span>
### PATCH /Users

<span id="feature-description"></span>
#### Feature description

Updates the information of the user with the specified ID.

<span id="limits"></span>
#### Limits


* An ID is required.

* If the user with the specified ID does not exist, access is denied.

* Only the information of users synchronized by the SCIM service can be modified.

* The maximum operation length is 10.

* The PATCH method supports three options: add, replace, and remove.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location --request PATCH 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Users/3158367515904'  
--header 'Content-Type: application/json'  
--header 'Authorization: Bearer ••••••'  
--data '{ 
    "Operations": [ 
        { 
            "op": "remove", 
            "path": "displayName" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
}'
```


<span id="example-operations"></span>
#### Example operations

```json
// Remove displayName. 
{ 
    "Operations": [ 
        { 
            "op": "remove", 
            "path": "displayName" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
} 


// Replace emails, displayName, and userName. 
{ 
    "Operations": [ 
        { 
            "op": "replace", 
            "value": { 
                "emails": [ 
                    { 
                        "primary": true, 
                        "type": "work", 
                        "value": "youremail2@test.com" 
                    } 
                ], 
                "displayName": "test-displayName", 
                "userName": "test-userName" 
            } 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
} 


// Add emails. 
{ 
    "Operations": [ 
        { 
            "op": "add", 
            "path": "emails[type eq "work"]", 
            "value": { 
                "value": "<your email>" 
            } 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
}
```


<span id="groups"></span>
## /Groups

<span id="get-groups"></span>
### GET /Groups

<span id="feature-description"></span>
#### Feature description

Queries user group information by condition or queries the list of all user groups.

<span id="limits"></span>
#### Limits


* You can only specify the externalId, displayName, or id field as a filter, and can only use the EQ and AND operators.

* You can use the pagination method of SCIM, which can return up to 100 records each page. If you specify a count value greater than 100, 100 is used as the actual count value.

* You can only query user groups synchronized by the SCIM service.



|Parameter |Description |Example |
|---|---|---|
|filter |Supports only the EQ and AND expressions of the displayName, externalId, or id field. |* filter=Id eq 30012346621521<br><br>* filter=externalId eq exid\-g\-sfji2ni3ti3<br><br>* filter=displayName eq test\-group |
|startIndex |Specifies the index. It can be left empty and the default value is 1. |startIndex=1 |
|count |Specifies the number of user groups on each page. It can be left empty and the default value is 10. |count=100 |


<span id="sample-request"></span>
#### Sample request

```bash
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Groups?filter=id%20eq%20%223000927463168%22'  
--header 'Authorization: Bearer ••••••'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "itemsPerPage": 100, 
    "resources": [ 
        { 
            "displayName": "test-group", 
            "id": "3000927463168", 
            "members": [], 
            "meta": { 
                "created": "2025-04-15T10:02:08Z", 
                "lastModified": "2025-04-21T03:17:53Z", 
                "location": "/Groups/3000927463168", 
                "resourceType": "Group" 
            }, 
            "schemas": [ 
                "urn:ietf:params:scim:schemas:core:2.0:Group" 
            ] 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:ListResponse" 
    ], 
    "startIndex": 1, 
    "totalResults": 1 
}
```


<span id="get-groups"></span>
### GET /Groups/

<span id="feature-description"></span>
#### Feature description

Queries the user group with the specified ID.

<span id="limits"></span>
#### Limits


* If the user group with the specified ID does not exist, access is denied.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Groups/3000927463168'  
--header 'Authorization: Bearer ••••••'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "displayName": "displayName", 
    "id": "3000927463168", 
    "members": [], 
    "meta": { 
        "created": "2025-04-15T10:02:08Z", 
        "lastModified": "2025-04-21T03:17:53Z", 
        "location": "/Groups/3000927463168", 
        "resourceType": "Group" 
    }, 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:Group" 
    ] 
}
```


<span id="post-groups"></span>
### POST /Groups

<span id="feature-description"></span>
#### Feature description

Creates user groups.

<span id="limits"></span>
#### Limits


* If user groups with the same name exist in the Cloud Identity instance, the creation request is denied.

* If user groups with the same externalId exist in the Cloud Identity instance, the creation request is denied.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Groups'  
--header 'Content-Type: application/json'  
--header 'Authorization: Bearer ••••••'  
--data '{ 
    "displayName": "test-group-12519512", 
    "externalId": "ex-g-2139251251", 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:Group" 
    ] 
}'
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "displayName": "test-group-12519512", 
    "externalId": "ex-g-2139251251", 
    "id": "3162821984768", 
    "members": [], 
    "meta": { 
        "created": "2025-05-08T12:05:50Z", 
        "lastModified": "2025-05-08T12:05:50Z", 
        "location": "/Groups/3162821984768", 
        "resourceType": "Group" 
    }, 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:Group" 
    ] 
}
```


<span id="put-groups"></span>
### PUT /Groups

<span id="feature-description"></span>
#### Feature description

Replaces the information of the user group with the specified ID.

<span id="limits"></span>
#### Limits


* An ID is required, and fields defined in the schema are modified.

* If the user group with the specified ID does not exist, access is denied.

* As the PUT method is used, the original attributes are overwritten.

* As the PUT method is used, fields that are not specified remain unchanged, while fields explicitly set to an empty value are overwritten with that empty value.

* Only the information of user groups synchronized by the SCIM service can be modified.

* Only users synchronized by the SCIM service can be added to user groups.

* The list of members in a user group is not returned.

* When you initiate a PUT request to overwrite the members of a user group, only up to 100 users can be overwritten in the request.


<span id="sample-request"></span>
#### Sample request

```json
{ 
    "displayName": "test-group", 
    "externalId": "ex-g-124924", 
    "members": [ 
        { 
            "value": "3001234662656" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:Group" 
    ] 
}
```


<span id="sample-response"></span>
#### Sample response

```json
{ 
    "displayName": "test-group", 
    "externalId": "ex-g-124924", 
    "id": "3162821984768", 
    "members": [], 
    "meta": { 
        "created": "2025-05-08T12:05:50Z", 
        "lastModified": "2025-05-08T12:08:02Z", 
        "location": "/Groups/3162821984768", 
        "resourceType": "Group" 
    }, 
    "schemas": [ 
        "urn:ietf:params:scim:schemas:core:2.0:Group" 
    ] 
}
```


<span id="delete-groups"></span>
### DELETE /Groups

<span id="feature-description"></span>
#### Feature description

Deletes the user group with the specified ID.

<span id="limits"></span>
#### Limits


* An ID is required.

* If the user group with the specified ID does not exist, access is denied.

* Only user groups synchronized by the SCIM service can be deleted.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location --request DELETE 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Groups/3162821984768'  
--header 'Authorization: Bearer ••••••'
```


<span id="patch-groups"></span>
### PATCH /Groups

<span id="feature-description"></span>
#### Feature description

Updates the information of the user group with the specified ID.

<span id="limits"></span>
#### Limits


* An ID is required.

* If the user group with the specified ID does not exist, access is denied.

* Only the information of user groups synchronized by the SCIM service can be modified.

* The maximum operation length is 10.

* The PATCH method supports three options: add, replace, and remove.

* One operation can include up to 100 members.


<span id="sample-request"></span>
#### Sample request

```bash
curl --location --request PATCH 'https://cloudidentity-scim.ap-southeast-1.bytepluses.com/scim/v2/Groups/3000927463168'  
--header 'Content-Type: application/json'  
--header 'Authorization: ••••••'  
--data ' 
{ 
    "Operations": [ 
        { 
            "op": "remove", 
            "path": "members[value eq "21425125124312"]" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
} 
'
```


<span id="example-operations"></span>
#### Example operations

```json
// Remove externalId. 
{ 
    "Operations": [ 
        { 
            "op": "remove", 
            "path": "externalId" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
} 

// Remove externalId. 
{ 
    "Operations": [ 
        { 
            "op": "remove", 
            "path": "members[value eq "21425125124312"]" 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
} 

// Replace displayName and members. 
{ 
    "Operations": [ 
        { 
            "op": "replace", 
            "value": { 
                "displayName": "test-displayName", 
                "members": [ 
                    { 
                        "value": "<member-user-id>" 
                    } 
                ] 
            } 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
} 

// Add members. 
{ 
    "Operations": [ 
        { 
            "op": "add", 
            "path": "members", 
            "value": { 
                "value": "<member-user-id>" 
            } 
        } 
    ], 
    "schemas": [ 
        "urn:ietf:params:scim:api:messages:2.0:PatchOp" 
    ] 
}
```


&nbsp;
