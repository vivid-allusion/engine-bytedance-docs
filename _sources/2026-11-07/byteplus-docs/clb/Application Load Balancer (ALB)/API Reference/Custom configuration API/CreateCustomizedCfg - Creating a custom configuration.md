---
title: "CreateCustomizedCfg - Creating a custom configuration"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateCustomizedCfg"
---

Call the CreateCustomizedCfg API to create a custom configuration.

## Instructions

An account can create up to 50 custom configurations per region.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateCustomizedCfg&groupName=%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: CreateCustomizedCfg`

Action to execute. Set the value to CreateCustomizedCfg.

**Version ** string必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**CustomizedCfgName ** string必选 `Example: myCustomizedCfg`

The name of a custom configuration follows these rules:

* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

**CustomizedCfgContent ** string必选 `Example: client_max_body_size 60M keepalive_timeout 75s`

The content of custom configuration items follows these rules:

* Length must not exceed 4096 characters.

* Spaces and semicolons must be escaped.

* Different configuration items are separated by ";\r\n", and configuration items cannot be duplicated.

* Currently supported configuration items include ssl_protocols, ssl_ciphers, client_max_body_size, keepalive_timeout, proxy_request_buffering, proxy_connect_timeout, add_header, client_header_timeout, proxy_read_timeout, proxy_send_timeout, client_body_timeout, send_timeout, and ssl_verify_depth. For details, see **Custom configuration items** at the end.

**Description ** string`optional` `Example: This is a CustomizedCfg`

Description of the custom configuration. The specific rules are as follows:

* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。)

* Must be 1 to 255 characters.

* If left blank, this parameter defaults to an empty string.

**Tags.N.Value ** string[]`optional` `Example: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the custom tag.

* To provide this parameter, provide Tags.N.Key first.

* The specific rules are as follows:

   * The length limit is 0 to 256 characters.

   * Case\-sensitive.

   * Must not start or end with a space.

   * May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

**Tags.N.Key ** string[]`optional` `Example: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the custom tag. The specific rules are as follows:

* Must be 1 to 128 characters.

* Case\-sensitive.

* Cannot start with any case‑insensitive combination of volc: or sys:.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

* Tag keys of the same resource must be unique.​

**ProjectName ** string`optional` `Example: default`

The name of the project to which the custom configuration belongs.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

**CustomizedCfgId ** string`Example: ccfg-3cj44nv0jhhxc6c6rrtet****`

ID of the custom configuration.

## Request example

```text
GET /?Action=CreateCustomizedCfg&CustomizedCfgName=test-1&Description=test&CustomizedCfgContent=client_max_body_size+60M;keepalive_timeout+75s;&ProjectName=default&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "0cd0297c-9a88-48cb-9ba2-82c3dcbc****",
        "Action": "CreateCustomizedCfg",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "0cd0297c-9a88-48cb-9ba2-82c3dcbc****",
        "CustomizedCfgId": "ccfg-3lk5o0tulupdswet340b****"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidCustomizedCfgName.Malformed |The specified CustomizedCfgName is malformed. |The specified CustomizedCfgName parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'CustomizedCfgContent'. |This request does not contain the required parameter. Ensure that your request includes all required parameters, such as CustomizedCfgContent. |
|400 |OperationFailed.QueryProject |The request on the specified resource failed due to the query on project failed. |The request to operate on this resource failed because the project query failed. |
|400 |QuotaExceed.CustomizedCfgPerRegion |You've reached the limit on the number of CustomizedCfgs the current region you can create in, usage xx/xx. |The maximum number of custom configurations that can be created in the current region has been reached. Used: xxx. Quota: xxx |
|400 |OperationFailed.AddIntoProjectFailed |The request on the specified resource failed due to adding it into the project failed. |The request to operate on this resource failed because adding the resource to the project failed. |
|400 |InvalidTags.Key.Malformed |The specified Tags.Key is malformed. |The specified Tags.Key parameter format is invalid. |
|400 |InvalidTags.Value.Malformed |The specified Tags.Value is malformed. |The specified Tags.Value parameter format is invalid. |
|400 |InvalidTags.Key.Duplicated |The specified Tags.Key is duplicated. |The specified Tags.Key is duplicated. |
|400 |CustomizedCfgOnlyTLSv13WithCipher.Malformed |ssl_ciphers is not allowed when ssl_protocols only contains TLSv1.3 |When ssl_protocols is configured with only TLSv1.3, ssl_ciphers cannot be configured |
|400 |InvalidCustomizedCfgContent.Malformed |The specified CustomizedCfgContent is malformed. ssl_ciphers is not allowed when ssl_protocols only contains TLSv1.3. |The specified CustomizedCfgContent parameter format is invalid. When ssl_protocols is configured with only TLSv1.3, ssl_ciphers cannot be configured. |
|400 |InvalidCustomizedCfgContent.Malformed |The specified CustomizedCfgContent is malformed. max_headers config in CustomizedCfgContent is invalid. |The specified CustomizedCfgContent parameter format is invalid. The max_headers configuration is invalid. |
|400 |InvalidCustomizedCfgContent.Malformed |The specified CustomizedCfgContent is malformed. ssl_session_timeout config in CustomizedCfgContent is invalid. |The specified CustomizedCfgContent parameter format is invalid. The ssl_session_timeout configuration is invalid. |
|400 |InvalidCustomizedCfgContent.Duplicated |The specified CustomizedCfgContent is duplicated. ssl_session_timeout config in CustomizedCfgContent is duplicated. |The specified CustomizedCfgContent is duplicated. The ssl_session_timeout configuration item is duplicated. |
|400 |InvalidCustomizedCfgContent.Duplicated |The specified CustomizedCfgContent is duplicated. max_headers config in CustomizedCfgContent is duplicated. |The specified CustomizedCfgContent is duplicated. The max_headers configuration item is duplicated. |
|403 |Forbidden |You are not authorized to configure TLSv1.3\-only. |No permission to configure ssl_protocols TLSv1.3;. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
