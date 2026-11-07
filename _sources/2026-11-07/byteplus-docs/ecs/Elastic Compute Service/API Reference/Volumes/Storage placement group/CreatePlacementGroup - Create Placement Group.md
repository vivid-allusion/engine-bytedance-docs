---
title: "CreatePlacementGroup - Create Placement Group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Createplacementgroup"
---

Call CreatePlacementGroup to create a storage placement group.

<span id=".5L2_55So6K-05piO"></span>
## Usage Instructions

The storage placement group specifies the availability zone and the number of storage subgroups in that group. You can bind a storage placement group when creating a volume and specify the number of the storage subgroup. The system will deploy volumes with different subgroup numbers in separate clusters based on indicators such as cluster health and water level, enabling data isolation and protection.


* Storage Placement Group (PlacementGroup): Used to set the number of storage subgroups. A storage placement group can contain multiple subgroups, with up to 10 subgroups allowed.

* Storage Subgroup (SubGroup): Each storage subgroup maps to one or more clusters. When creating a volume, the system will create it in the corresponding cluster based on the specified placement group and subgroup number (if provided). If the number of storage subgroups is less than the number of clusters, and a certain cluster is over capacity, the volume will be scheduled to another cluster for creation; that is, one storage subgroup can map to multiple clusters.


<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions

The number of clusters in the availability zone for storage placement groups will decrease when downsizing online resources or performing machine maintenance If the number of storage sub\-placement groups specified by the user exceeds the number of clusters, ECS will prioritize ensuring volume creation succeeds when resources are insufficient. This may result in the volume being created successfully, but anti\-affinity not being applied

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreatePlacementGroup&groupName=%E5%AD%98%E5%82%A8%E6%94%BE%E7%BD%AE%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the request parameters unique to this API and some common parameters are listed below For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters)



**Action ** <span data-label="purple">string </span><span data-api-tag="require|BE5oZK">必选</span> `Example: CreatePlacementGroup`

Operation to perform: CreatePlacementGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|PvVwUX">必选</span> `Sample value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**Name ** <span data-label="purple">string </span><span data-api-tag="require|OpyVcg">必选</span> `Example: test-pg`

Placement group name details:


* The first character can only be a Chinese character, letter, or underscore (_).

* Can contain Chinese characters, letters, digits, underscores (_), hyphens (\-), or periods (.).

* Length must be between 1 and 128 characters.



**Description ** <span data-label="purple">string </span>`Optional` `Example: testDescription`

Description of the storage placement group. By default, this field is empty. Details are as follows:


* The first character can only be a Chinese character, letter, or underscore (_).

* Can contain Chinese characters, letters, digits, underscores (_), hyphens (\-), or periods (.).

* The length limit is 1 to 128 characters.



**ZoneId ** <span data-label="purple">string </span><span data-api-tag="require|3dLmGo">必选</span>`Optional` `Example: ap-southeast-1-a`

The availability zone where the storage placement group is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The storage placement group's availability zone must be within the requested region.</div>




**SubgroupCount ** <span data-label="purple">integer </span><span data-api-tag="require|FeAvG5">必选</span>`Example value: 2`

Specifies the number of storage sub\-placement groups. The minimum value is 2, and the maximum value is min {number of zone clusters, 10}.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the number of clusters in a zone is less than the value of <code>SubgroupCount</code>, an <code>SubGroupCountExceedClusters</code> error will be reported, and the current number of available clusters will be returned.</div>


* <div data-tips="true" data-tips-type="tip">After you set storage sub\-placement groups, the system automatically assigns numbers to each group in numerical order. The numbering starts at 1, with the maximum number equal to the total number of storage sub\-placement groups.</div>




**AutoAssign ** <span data-label="purple">boolean </span>`Optional` `Example value: true`

Enable automatic assignment of storage sub\-placement groups for volumes. When creating a volume, binding it to a placement group and enabling auto\-assignment will automatically assign a storage sub\-placement group for the volume. Values:


* true: Enable the auto\-assignment feature.

* false: Do not enable the auto\-assignment feature.

   The default value is false.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you enable the automatic allocation feature and set the <code>SubgroupNumber</code> parameter when creating the volume, the system will automatically assign a storage subplacement group to the volume, and the <code>SubgroupNumber</code> parameter will become invalid.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

Only the parameters unique to this API are listed below For more information, see [Return Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)



**Id ** <span data-label="purple">string </span>`Sample value: pg-d5ard493uxd44up7****`

Storage placement group ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=CreatePlacementGroup&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20250724T100233Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250724/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Name": "test-pg",
  "ZoneId": "ap-southeast-1-a",
  "SubgroupCount": 2
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "20250724180311221168252213EA****",
    "Action": "CreatePlacementGroup",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "pg-d5ard493uxd44up7****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists the error codes related to this interface and business logic. For public error codes, see the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |SubGroupCountExceedClusters |The subgroup count exceeds the cluster count for the placement group, with a maximum of {{param}}. |The number of anti\-affinity groups exceeds the cluster total, with a maximum of {{param}}. |
