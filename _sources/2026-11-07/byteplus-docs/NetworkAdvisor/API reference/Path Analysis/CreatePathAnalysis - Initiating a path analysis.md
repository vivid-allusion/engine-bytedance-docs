---
title: "CreatePathAnalysis - Initiating a path analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/CreatePathAnalysis"
---

Call the CreatePathAnalysis API to initiate path analysis.

## Request parameters

**Action ** String必选 `Example: CreatePathAnalysis`

The interface name. The current API name is `CreatePathAnalysis`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.

**SourceType ** String必选 `Example: ECS`

Source resource type. Valid values:

* ECS: Elastic Compute Service.

* PublicIP: EIP.

* DCG: Direct Connect Gateway.

* TRIPSec: TR\-type IPsec\-VPN connection.

* VGW: VPN gateway.

**SourceId ** String必选 `Example: i-ye8klde7swh9l3bn****`

Source resource ID.

**SourceIP ** String`optional` `Example: 192.168.1.64`

Source IP address.

If SourceType is set to ECS, it is only used to specify the primary private IP address of the primary or secondary network interface.

**TargetType ** String必选 `Example: ECS`

Destination resource type. Valid values:

* ECS: Elastic Compute Service.

* CLB: Classic Load Balancer.

* PublicIP: EIP.

* DCG: Direct Connect Gateway.

* TRIPSec: TR type IPsec connection.

* VGW: VPN gateway.

* PrivateIP: Private IP address.

**TargetId ** String必选 `Example: i-ye8klde7swh9l3b****`

Destination resource ID.

**TargetIP ** String`optional` `Example: 192.168.0.120`

Destination IP address.

**Protocol ** String必选 `Example: TCP`

Protocol type. Valid values:

* TCP

* UDP

* ICMP

**TargetPort ** Integer`optional` `Example: 80`

The destination port.

**Save ** Boolean`optional` `Example: true`

Whether to save the network path analysis results. Valid values:

* true: Save.

* false (default): Do not save.

**PathName ** String必选 `Example: PublicIP_ECS_TCP_80_19250`

Path name.

* Must be 1 to 128 characters in length.

* Must start with a letter, Chinese character, or digit. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example: PublicIP_ECS_TCP_80_19250`

Network path description information.

* Must be 0 to 255 characters.

* If left blank, this parameter defaults to an empty string.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**PrivateIP ** String`optional` `Example: 192.168.1.64`

Custom source private IP address. If not specified, SourceIP is used by default.

> **tip**

> It is only used in container network path analysis scenarios as the actual source IP address.

## Response parameters

**PathId ** String`Example: pa-3ogfsspk3cf0g6****`

Network path ID.

**PathReportId ** String`Example: par-ak3v00jduk1s3r****`

Path analysis report ID.

## Request example

```json
GET /?Action=CreatePathAnalysis&Version=2020-04-01&SourceType=ECS&SourceId=i-ye8klde7swh9l3bn****&SourceIP=192.168.1.64&TargetType=ECS&TargetId=i-ye8klde7swh9l3b****&TargetIP=192.168.0.120&Protocol=TCP&TargetPort=80&Save=true&PathName=PublicIP_ECS_TCP_80_19250&Description=PublicIP_ECS_TCP_80_19250
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePathAnalysis",
        "Version": "2020-04-01",
        "Service": "",
        "Region": "cn-beijing"
    },
    "Result": {
        "PathId": "pa-3ogfsspk3cf0g6****",
        "PathReportId": "par-ak3v00jduk1s3r****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAllPublicIP |The specified source ip and target ip are public ip. |When the source is public IPs, the destination must be an EIP. |
|400 |InvalidIPv4 |The specified ipv4 is not invalid. |The specified IPv4 is invalid. |
|400 |InvalidPathAnalysisEndType |The specified end type is invalid. |The specified end type is invalid. |
|400 |InvalidPort |The specified port is invalid. |The specified port number is invalid. |
|400 |InvalidProtocol |The specified protocol is invalid. |The specified protocol type is invalid. |
|400 |InvalidSourceTarget |The specified source and target should not be same. |The specified source and destination cannot be the same. |
