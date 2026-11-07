---
title: "DescribeAvailabilityZones"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeavailabilityzones"
---

Call the DescribeAvailabilityZones API to view the list of availability zones.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The DescribeAvailabilityZones API forwards requests based on the Region parameter in the header. It only queries availability zone information for the region specified in the header and will not return information for other regions.

* Call the [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeregions) API to query region information.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAvailabilityZones&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

None.


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|SpecFamily |String |No |General |Instance specification type. Values:<br><br><br>* `General`, a general\-type specification.<br><br>* `Shared`: a shared\-type specification. |
|StorageType |String |No |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|RegionId |String |cn\-beijing |Region ID |
|Zones |Array of [Zone](https://docs.byteplus.com/en/docs/40/15456#zone) |{<br><br>"Description": "North China 2 (Beijing) \- availability zone A",<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"ZoneName": "cn\-beijing\-a"<br><br>} |Availability zone list. |


<span id="zone"></span>
### Zone


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ZoneId |String |cn\-beijing\-a |The ID of the availability zone. |
|ZoneName |String |cn\-beijing\-a |The Name of the availability zone. |
|Description |String |North China 1 (Beijing) \- Availability zone A |Description of the availability zone. |
|status |String |Normal |Availability zone state. Values are as follows:<br><br><br>* `Normal`: available.<br><br>* `Disable`: Unavailable.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is returned only when <code>SpecFamily</code> or <code>StorageType</code> is passed in the request parameters; otherwise, it is not returned.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeAvailabilityZones&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202301092220460BDD841A0E0BF2B51B42",
        "Action": "DescribeAvailabilityZones",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "RegionId": "cn-beijing",
        "Zones": [
            {
                "Description": "华北2（北京）-可用区A",
                "ZoneId": "cn-beijing-a",
                "ZoneName": "cn-beijing-a"
            },
            {
                "Description": "华北2（北京）-可用区B",
                "ZoneId": "cn-beijing-b",
                "ZoneName": "cn-beijing-b"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
