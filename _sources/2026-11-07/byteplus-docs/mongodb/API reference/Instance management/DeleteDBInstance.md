---
title: "DeleteDBInstance"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/deletedbinstance"
---

Call the DeleteDBInstance API to delete the target MongoDB instance.

## Request type

Asynchronous request.

## Precautions

* Currently, only the MongoDB instances with pay\-as\-you\-go billing (i.e., the value of the instance billing type `ChargeType` is `PostPaid`) support calling the DeleteDBInstance interface to delete the instance. When deleting, the system will initiate a backup to save all data before deletion. You can view the backup details of the deleted instance on the **Backups of deleted instance** page.

* You can unsubscribe (i.e., delete) the annual and monthly subscribed MongoDB instances through the console or the cost center. For specific operation steps, refer to [Unsubscribing from a yearly or monthly subscription instance](https://docs.byteplus.com/en/docs/mongodb/unsubscribe-instance). When unsubscribing the annual and monthly subscribed instances, the instance backup retention policy is not supported for selection. The system will initiate a backup to save all data before deletion. You can view the backup details of the deleted instance on the **Backups of deleted instance** page.

* The retention period of the deleted instance backup is 7 days by default. If necessary, it is recommended that you restore the data to a new instance in a timely manner through the deleted instance backup. For specific operation steps, please refer to [Recovery from a deleted instance](https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance). Otherwise, after the instance is deleted and the backup of the deleted instance exceeds the retention period, all nodes and all data will be completely cleared and cannot be recovered.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DeleteDBInstance&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-e405f8e2****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202202211539050101742350380678****",
        "Action": "DeleteDBInstance",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
