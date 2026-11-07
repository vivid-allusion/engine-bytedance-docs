---
title: "CreateDiagnosisInstance - Creating an instance diagnosis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/CreateDiagnosisInstance"
---

Call the CreateDiagnosisInstance API to create an instance diagnosis.

## Request parameters

**Action ** String必选 `Example: CreateDiagnosisInstance`

The interface name. The current API name is `CreateDiagnosisInstance`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.

**ResourceType ** String必选`Example: EIP`

The resource type. Valid values:

* EIP

* NAT: NAT gateway.

* CLB: Classic Load Balancer.

* VPN: VPN gateway.

* TR: Transit Router.

* PL: PrivateLink.

* DC: Direct Connect.

**ResourceRegion ** String必选 `Example: cn-beijing`

The region where the resource resides.

**ResourceInstanceId ** String必选 `Example: eip-2ziwb7ujxscd****`

Resource instance ID.

## Response parameters

**DiagnosisInstanceId ** String`Example: di-12b8n3mdsl4hs****`

Instance diagnosis ID.

## Request example

```json
GET /?Action=CreateDiagnosisInstance&Version=2020-04-01&ResourceType=EIP&ResourceRegion=cn-beijing&ResourceInstanceId=eip-2ziwb7ujxscd****
Host: na.byteplusapi.com
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/na/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDiagnosisInstance",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "DiagnosisInstanceId": "di-12b8n3mdsl4hs****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidDiagResourceRegion.NotSupported |The specified resource region is not supported. |The specified resource region is not supported. |
|400 |InvalidDiagResourceType.NotSupported |The specified resource type is not supported. |The specified resource type is not supported. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidResourceInstance.Limit |The specified resource instance has been diagnosed recently, please try again later. |The specified resource instance has been diagnosed recently. Please try again later. |
|400 |InvalidResourceInstance.NotFound |The specified resource instance is not found. |The specified resource instance is not found. |
|500 |ErrDiagEntryNotFound |Can't get diagnosis entries for the specified resource type |Diagnostic items cannot be retrieved for the specified resource type. |
