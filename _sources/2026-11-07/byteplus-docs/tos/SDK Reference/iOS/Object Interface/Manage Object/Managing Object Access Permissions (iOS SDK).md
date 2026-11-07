---
title: "Managing Object Access Permissions (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-access-to-objects-ios-sdk"
---

This article describes how to obtain and configure access permissions for objects. The access permissions of an object take precedence over those of the bucket. If no access permissions are set for the object, the bucket's access permissions will apply.

<span id=".5a-56LGh5p2D6ZmQ6K-05piO"></span>
## Description of Object Permissions


|**Access Permission Value** |**Description** |
|---|---|
|private |Private. The owner of the object possesses all permissions, while other users are not authorized to operate the object. |
|public\-read |Public reading. The owner of the object has all permissions, while other users have only read permission for that object. |
|public\-read\-write |Public read/write. All users have read and write permissions for the object file. |
|authenticated\-read |The owner of the object possesses all permissions, while authenticated users are granted read access to the object. |
|bucket\-owner\-read |The object owner has all permissions, while the bucket owner has read permission for the object. |
|bucket\-owner\-full\-control |Both the bucket owner and the object owner have full operation permissions on the object. |


<span id=".6K6-572u5a-56LGh55qE6K6_6Zeu5p2D6ZmQ"></span>
## **Configuring Object Access Permissions**

The following code demonstrates how to configure access permissions for an object.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSPutObjectACLInput *putAcl = [TOSPutObjectACLInput new];
putAcl.tosBucket = @"bucket-name";
putAcl.tosKey = @"object-name";

TOSGrantee *grantee = [TOSGrantee new];
grantee.tosType = TOSGranteeType;
grantee.tosID = @"id";

TOSGrant *grant = [TOSGrant new];
grant.tosGrantee = grantee;
grant.tosPermission = TOSPermissionType;

NSMutableArray *grants = [NSMutableArray array];
[grants addObject:grant];
putAcl.tosGrants = grants;

TOSOwner *owner = [[TOSOwner alloc] init];
owner.tosID = @"test-cid";
putAcl.tosOwner = owner;

TOSTask *task = [client putObjectAcl:putAcl];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Put object acl success.");
        TOSPutObjectACLOutput *output = task.result;
    } else {
        NSLog(@"Put object acl failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".6I635Y-W5a-56LGh55qE6K6_6Zeu5p2D6ZmQ"></span>
## **Obtaining Access Permissions for Objects**

The following code demonstrates how to obtain access permissions for an object.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectACLInput *getAcl = [TOSGetObjectACLInput new];
getAcl.tosBucket = @"bucket-name";
getAcl.tosKey = @"object-name";

TOSTask *task = [client getObjectAcl:getAcl];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Get object acl success.");
        TOSGetObjectACLOutput *output = task.result;
    } else {
        NSLog(@"Get object acl failed, error: %@" , task.error);
    }
    return nil;
}];
```
