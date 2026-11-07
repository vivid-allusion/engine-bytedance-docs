---
title: "CreateTrafficMirrorFilter - Creating a filter instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorFilter"
---

Call the CreateTrafficMirrorFilter API to create a Traffic Mirror Filter.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

CreateTrafficMirrorFilter is an asynchronous API; when a request ID is returned, the system is still creating in the background. You can call [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to check the status of a Traffic Mirror Filter. Creating indicates the filter is being created, and Available indicates the creation is complete.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTrafficMirrorFilter&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|xSalOE">必选</span> `Example value: CreateTrafficMirrorFilter`

The interface name. The current API name is `CreateTrafficMirrorFilter`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|ZBL5va">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TrafficMirrorFilterName ** <span data-label="purple"> String  </span>`optional` `Example value: TM_Filter_1`

Name of the traffic mirror filter.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the Traffic Mirror Filter ID.



**Description ** <span data-label="purple"> String </span>`optional` `Example value: TM_Filter_1_Description`

Description of the Traffic Mirror Filter.


* Must be 0 to 255 characters.

* If left blank, this parameter defaults to an empty string.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



**ProjectName ** <span data-label="purple"> String  </span>`optional` `Example value: default`

The name of the project to which the Traffic Mirror Filter belongs. If left blank, it defaults to the default project.



**Tags.N.Key ** <span data-label="purple"> String </span>`optional` `Example value: key1`

The tag key of the user tag.


* N specifies the serial number of a tag key. Valid values: 1–50.

* Separate multiple tag keys with ampersands (&).

* Cannot start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple"> String  </span>`optional` `Example: value1`

The tag value of the user tag.


* N specifies the serial number of a tag value. Valid values: 1–50.

* Separate multiple tag values with ampersands (&).

* The length ranges from 0 to 256 characters. If left blank, it defaults to an empty value.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




**ClientToken ** <span data-label="purple"> String  </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`Example value: 2021062415303301022514515207C4****`

Request ID.



**TrafficMirrorFilterId ** <span data-label="purple"> String  </span>`Example value: tmf-bp1opxu1zkhn00123****`

ID of the Traffic Mirror Filter.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateTrafficMirrorFilter&Version=2020-04-01&TrafficMirrorFilterName=TM_Filter_1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateTrafficMirrorFilter",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TrafficMirrorFilterId": "tmf-bp1opxu1zkhn00123****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |QuotaExceeded.TrafficMirrorFilter |You've reached the limit on the number of traffic mirror filters that you can create. |The maximum number of mirror traffic filters that can be created has been reached. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
