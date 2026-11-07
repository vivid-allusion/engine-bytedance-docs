---
title: "DescribeHpcClusters - Queries detailed list of HPC clusters"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeHpcClusters"
---

Call the DescribeHpcClusters operation to query the list of HPC clusters that meet the specified conditions with detailed information.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeHpcClusters&groupName=%E9%AB%98%E6%80%A7%E8%83%BD%E8%AE%A1%E7%AE%97%E9%9B%86%E7%BE%A4&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|aYUamK">必选</span> `Sample value: DescribeHpcClusters`

The action that you want to perform. Value: DescribeHpcClusters.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|W1XJcc">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**HpcClusterIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: HpcClusterIds.1=hpcCluster-ybo1y364wkf80o0m****&HpcClusterIds.2=hpcCluster-ybn3a2zyiib1wzr2****`

The HPC cluster ID.


* Argument \- N: specifies the serial number of the HPC cluster.

* Separate multiple IDs with ampersands (&).



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 100

* Default value: 10



**Name** <span data-label="purple">string</span> `Optional` `Sample value: hpcCluster-01`

Query by filtering the HPC cluster name.



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with ampersands (&).

* Tag keys must be unique.



**TagFilters.N.Values.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The specified tag value when querying resources based on tags.


* The first N: specifies the serial number of the tag key. Value range: 1–10.

* The second N: specifies the serial number of the tag value. Value range: 1–3. You can query up to three tag values of the same tag key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone where the HPC cluster is deployed.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**HpcClusters** <span data-label="purple">object[]</span> `Sample value: --`

Information about HPC clusters that meet the conditions.


**ProjectName** <span data-label="purple">string</span> `Sample value: project_a`

The name of the project to which the resource belongs.



**Tags** <span data-label="purple">object[]</span> `Sample value: --`

The information of tags associated with resources.


**Key** <span data-label="purple">string</span> `Sample value: k1`

The tag key of the resource.



**Value** <span data-label="purple">string</span> `Sample value: v1`

The tag value of the resource.




**CreatedAt** <span data-label="purple">string</span> `Sample value: 2024-07-26T21:55:12+08:00`

The creation time. Format: RFC3339.



**Description** <span data-label="purple">string</span> `Sample value: HPC cluster for testing.`

The description of the HPC cluster.



**HpcClusterId** <span data-label="purple">string</span> `Sample value: hpcCluster-ybo1y364wkf80o0m****`

The HPC cluster ID.



**Name** <span data-label="purple">string</span> `Sample value: hpcCluster-01`

The name of the HPC cluster.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2024-07-26T21:55:12+08:00`

The update time. Format: RFC3339.



**VpcId** <span data-label="purple">string</span> `Sample value: vpc-3qd85471bl7nk7prml024****`

VPC ID.



**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The ID of the availability zone where the HPC cluster is deployed.




**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeHpcClusters&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20220518171951010211173098094C****",
    "Action": "DescribeHpcClusters",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "NextToken": "",
    "HpcClusters": [
      {
        "HpcClusterId": "hpcCluster-ybo1y364wkf80o0m****",
        "Name": "hpcCluster-01",
        "VpcId": "vpc-3qd85471bl7nk7prml024****",
        "Description": "HPC cluster for testing.",
        "ZoneId": "cn-beijing-a",
        "CreatedAt": "2022-05-07T00:42:43+08:00",
        "UpdatedAt": "2022-05-07T15:17:21+08:00",
        "Tags": [
          {
            "Key": "sys:tag:createdBy",
            "Value": "IAMUser:3723****:****"
          }
        ],
        "ProjectName": "default"
      },
      {
        "HpcClusterId": "hpcCluster-ybmta3h9gwkrkfjr****",
        "Name": "hpcCluster-02",
        "VpcId": "",
        "Description": "",
        "ZoneId": "cn-beijing-a",
        "CreatedAt": "2022-04-19T20:36:04+08:00",
        "UpdatedAt": "2022-04-24T16:09:55+08:00",
        "Tags": [
          {
            "Key": "sys:tag:createdBy",
            "Value": "IAMUser:3723****:****"
          }
        ],
        "ProjectName": "default"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).
