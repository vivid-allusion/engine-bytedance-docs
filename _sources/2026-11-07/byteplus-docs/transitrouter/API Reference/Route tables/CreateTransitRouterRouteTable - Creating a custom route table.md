---
title: "CreateTransitRouterRouteTable - Creating a custom route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteTable"
---

Call CreateTransitRouterRouteTable to create a custom route table for a Transit Router (TR).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterRouteTable&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|LTi-9V">必选</span> `Example: CreateTransitRouterRouteTable`

The interface name. The current API name is `CreateTransitRouterRouteTable`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|F7hw8W">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple"> String  </span><span data-api-tag="require|BP2vHY">必选</span> `Example value: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**Description ** <span data-label="purple"> String  </span>`Optional` `Example value: This route table is used for test.`

Description of the route in the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**TransitRouterRouteTableName ** <span data-label="purple"> String  </span>`Optional` `Example: routetable-02`

Name of the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, it defaults to the ID of the TR route table.



**Tags.N.Key ** <span data-label="purple"> String </span>`optional` `Example: k1`

The tag key of the TR route table.


* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Tag keys of the same resource must be unique.</div>


* <div data-tips="true" data-tips-type="default">If you do not provide this parameter or leave it unset, it defaults to empty.</div>




**Tags.N.Value ** <span data-label="purple"> String </span>`optional` `example value: v1`

The tag value of the TR route table.


* Must be 0 to 255 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To provide this parameter, provide Tags.N.Key first.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterRouteTableId ** <span data-label="purple">String </span>`Example: tr-rtb-hy13n2l4c6c0v****`

ID of the TR route table.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateTransitRouterRouteTable&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T035221Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250804115225065077224154DCCF5F",
    "Action": "CreateTransitRouterRouteTable",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "TransitRouterRouteTableId": "tr-rtb-hy13n2l4c6c0v****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified Transit Router (TR) is suspended due to overdue payments. Action unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |QuotaExceeded.TransitRouterRouteTable |You've reached the maximum number of route tables that can be created on one Transit Router. |You have reached the maximum number of route tables that you can create for a single TR. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
