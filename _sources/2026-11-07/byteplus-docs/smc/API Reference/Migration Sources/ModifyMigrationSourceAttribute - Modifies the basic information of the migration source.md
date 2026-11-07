---
title: "ModifyMigrationSourceAttribute - Modifies the basic information of the migration source"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/ModifyMigrationSourceAttribute"
---

Call the ModifyMigrationSourceAttribute operation to modify the basic information of the migration source.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyMigrationSourceAttribute&groupName=%E8%BF%81%E7%A7%BB%E6%BA%90&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|9jB2RL">必选</span> `Sample value: ModifyMigrationSourceAttribute`

The operation that you want to perform. Valid value: ModifyMigrationSourceAttribute.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Csrqod">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**SourceId ** <span data-label="purple">string </span><span data-api-tag="require|WvehKo">必选</span> `Sample value: s-3tiegs1y963****`

The migration source ID. You can call the [DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) operation to query and obtain the migration source ID.



**MigrationSourceDescription ** <span data-label="purple">string </span>`Optional` `Sample value: Local virtual machine`

The description of the migration source.


* Start with a letter or a Chinese character only.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is left blank, the original configuration is retained.</div>


* <div data-tips="true" data-tips-type="tip">If an empty string is passed in, the original description information will be cleared.</div>




**SourceName ** <span data-label="purple">string </span>`Optional` `Sample value: LocalVM_New`

The migration source name.


* Can not start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is not specified or an empty string is passed in, the original name will be retained.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SourceId ** <span data-label="purple">string </span>`Sample value: s-3tiegs1y963****`

The migration source ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyMigrationSourceAttribute&Version=2020-04-01&SourceId=s-3tiegs1y963****&SourceName=LocalVM_New HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202306021637410F150D*****",
    "Action": "ModifyMigrationSourceAttribute",
    "Version": "2020-04-01",
    "Service": "smc",
    "Region": "cn-beijing"
  },
  "Result": {
    "SourceId": "s-3tiegs1y963****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidMigrationSourceDescription.Malformed |The specified MigrationSourceDescription is malformed. |The specified MigrationSourceDescription value is invalid. |
|400 |InvalidMigrationSourceName.Malformed |The specified migration source name is malformed. |The migration source name is invalid. |
|400 |InvalidSourceName.Malformed |The specified SourceName is malformed. |The specified SourceName value is invalid. |
|400 |MissingParameter.SourceId |The required parameter SourceId is not supplied. |The SourceId parameter cannot be empty. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API does not exist. |
|404 |InvalidMigrationSource.NotFound |The specified migration source does not exist. |The specified migration source does not exist. |
