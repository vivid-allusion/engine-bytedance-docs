---
title: "GetAnalysisPathReport - Getting a path analysis report"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/GetAnalysisPathReport"
---

Call the GetAnalysisPathReport API to obtain the path analysis report.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=GetAnalysisPathReport&groupName=%E8%B7%AF%E5%BE%84%E5%88%86%E6%9E%90&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: GetAnalysisPathReport`

Action to execute. Set the value to GetAnalysisPathReport.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**PathReportId ** string必选 `Example: par-ak3v00jduk1s3r****`

Path analysis report ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**CreateTime ** string`Example: 2025-04-18 15:02:37`

Creation time.

**PathDetails ** string`Example: { "SourceId":"i-ye8klde7swh9l3bn****", "SourceType":"ECS", "SourceIp":"192.168.1.1", "TargetId":"i-abcdefgh12345678", "TargetType":"ECS", "TargetIP":"10.0.0.1", "TargetPort":3306, "Protocol":"TCP" }`

Network path details, containing information about the source and destination, such as ID, type, IP address, port, and protocol.

* SourceId: Source node resource ID.

* SourceType: Source node type.

* SourceIp: Source node IP address.

* TargetId: Target node resource ID.

* TargetType: Target node type.

* TargetIP: Target node IP address.

* TargetPort: Target node port.

* Protocol: Path analysis protocol.

**PathId ** string`Example: pa-3ogfsspk3cf0g6****`

Network path ID.

**PathReportId ** string`Example: par-ak3v00jduk1s3r****`

Path analysis report ID.

**Reachability ** string`Example: Reachable`

Path reachability analysis result.

* Reachable

* Unreachable

* Unknown

**ReportDetails ** string`Example: [ { "Id": "i-ye5jsoketcv****", "ResourceType": "ECS", "Level": "Normal", "AbnormalResults": null, "Data": { "EcsId": "i-ye5jsok****", "EcsName": "i-ye5jsok****", "Region": "cn-beijing", "Status": "RUNNING", "VpcId": "vpc-2ff1***", "VpcName": "vpc-2ff1***", "Zone": "cn-beijing-a" } }, ... { "Id": "i-ye5jswu****", "ResourceType": "ECS", "Level": "Normal", "AbnormalResults": null, "Data": { "EcsId": "i-ye5jswu77****", "EcsName": "i-ye5jswu77****", "Region": "cn-beijing", "Status": "RUNNING", "VpcId": "vpc-2ff1f3fr***", "VpcName": "vpc-2ff1f3fr***", "Zone": "cn-beijing-a" } } ]`

Path analysis report details, containing detailed results and diagnostic information from the path analysis.

* ID: Resource node ID.

* ResourceType: The resource type of the node.

* Level: Node status.

* AbnormalResults: Abnormal results.

* Data: Presents information unique to the node.

**Status ** string`Example: Finish`

Status of the path analysis task.

* Init: Initialize.

* Running: Analyzing.

* Finish: Completed.

## Request example

```text
GET /?Action=GetAnalysisPathReport&Version=2020-04-01&PathReportId=par-ak3v00jduk1s3r****
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetAnalysisPathReport",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreateTime": "2025-04-18 15:02:37",
        "PathDetails": "{\"SourceId\":\"i-ye5jsok****\",\"SourceType\":\"ECS\",\"SourceIp\":\"192.168.0.106\",\"TargetId\":\"i-ye5jswu****\",\"TargetType\":\"ECS\",\"TargetIP\":\"192.168.0.105\",\"TargetPort\":22,\"Protocol\":\"TCP\"}",
        "PathId": "pa-3ogfsspk3cf0g6****",
        "PathReportId": "par-ak3v00jduk1s3r****",
        "Reachability": "Reachable",
        "ReportDetails": "[{\"Id\":\"i-ye5jsok****0\",\"ResourceType\":\"ECS\",\"Level\":\"Normal\",\"AbnormalResults\":null,\"Data\":{\"EcsId\":\"i-ye5jsok****\",\"EcsName\":\"i-ye5jsok****\",\"Region\":\"cn-beijing\",\"Status\":\"RUNNING\",\"VpcId\":\"vpc-2ff1f3f****\",\"VpcName\":\"vpc-2ff1f3f****\",\"Zone\":\"cn-beijing-a\"}},{\"Id\":\"eni-2ff1f7n****1\",\"ResourceType\":\"ENI\",\"Level\":\"Normal\",\"AbnormalResults\":null,\"Data\":{\"EniId\":\"eni-2ff1f7n****\",\"EniName\":\"eni-2ff1f7n****\",\"MAC\":\"00:16:3e:22:e9:d1\",\"PrimaryIPAddress\":\"192.168.0.106\",\"Region\":\"cn-beijing\",\"SecurityGroupMatched\":[{\"CIDR\":\"0.0.0.0/0\",\"Description\":\"****\",\"Direction\":\"egress\",\"Policy\":\"accept\",\"PortRange\":\"ALL\",\"Priority\":100,\"Protocol\":\"all\",\"SecurityGroupId\":\"sg-2ff1f3lo****\",\"SecurityGroupName\":\"\",\"SecurityGroupRuleId\":\"2ff1f3nn****\"}],\"Status\":\"InUse\",\"SubnetId\":\"subnet-12bjoep****\",\"SubnetName\":\"subnet-12bjoep****\",\"VpcId\":\"vpc-2ff1f3f****\",\"VpcName\":\"vpc-2ff1f3f****\",\"Zone\":\"cn-beijing-a\"}},{\"Id\":\"subnet-12bjoep****2\",\"ResourceType\":\"Subnet\",\"Level\":\"Normal\",\"AbnormalResults\":null,\"Data\":{\"IPv4CIDR\":\"192.168.0.0/24\",\"NACLMatched\":null,\"Region\":\"cn-beijing\",\"SubnetId\":\"subnet-12bjoep****\",\"SubnetName\":\"subnet-12bjoep****\",\"VpcId\":\"vpc-2ff1f3f****\",\"VpcName\":\"vpc-2ff1f3f****\",\"Zone\":\"cn-beijing-a\"}},{\"Id\":\"eni-12bjoil****3\",\"ResourceType\":\"ENI\",\"Level\":\"Normal\",\"AbnormalResults\":null,\"Data\":{\"EniId\":\"eni-12bjoil****\",\"EniName\":\"eni-12bjoil****\",\"MAC\":\"00:16:3e:77:79:ba\",\"PrimaryIPAddress\":\"192.168.0.105\",\"Region\":\"cn-beijing\",\"SecurityGroupMatched\":[{\"CIDR\":\"192.168.0.0/24\",\"Description\":\"\",\"Direction\":\"ingress\",\"Policy\":\"accept\",\"PortRange\":\"ALL\",\"Priority\":1,\"Protocol\":\"all\",\"SecurityGroupId\":\"sg-2ff1f3lo****\",\"SecurityGroupName\":\"\",\"SecurityGroupRuleId\":\"2ff1fp74****\"}],\"Status\":\"InUse\",\"SubnetId\":\"subnet-12bjoep****\",\"SubnetName\":\"subnet-12bjoep****\",\"VpcId\":\"vpc-2ff1f3f****\",\"VpcName\":\"vpc-2ff1f3f****\",\"Zone\":\"cn-beijing-a\"}},{\"Id\":\"i-ye5jswu****4\",\"ResourceType\":\"ECS\",\"Level\":\"Normal\",\"AbnormalResults\":null,\"Data\":{\"EcsId\":\"i-ye5jswu****\",\"EcsName\":\"cc-ser-勿删\",\"Region\":\"cn-beijing\",\"Status\":\"RUNNING\",\"VpcId\":\"vpc-2ff1f3f****\",\"VpcName\":\"vpc-2ff1f3f****\",\"Zone\":\"cn-beijing-a\"}}]",
        "Status": "Finish"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAnalysisPathReport.NotFound |The specified analysis path report is not found. |The specified path analysis report is not found. |
