---
title: "AddHostGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/AddHostGroup"
---

A domain group is a collection of domains that can be used to associate the corresponding blocklist or allowlist in bulk, improving the efficiency of configuring and maintaining access control policies. You can use the AddHostGroup API to add domains that have already been integrated into WAF to the created domain group, enabling centralized creation of access control policies.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important notes

Before creating a domain group, ensure that the protected domains to be added have already been integrated into the WAF instance.

<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=AddHostGroup&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|-2VhMQ">必选</span> `Sample value: AddHostGroup`

API name. The current API name is `AddHostGroup`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|3Wj_79">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name. The default is "default". The current resource is associated with the corresponding project and can only be associated with projects for which the current identity has permission.


* For information on how to obtain the project name, refer to ListProjectResources.

* You can also call CreateProject to create a new project.



**Description ** <span data-label="purple"> String  </span>`Optional` `Sample value: Used for bulk association with blocklist.`

Domain group description, used to specify the purpose or use of the domain group.



**HostList ** <span data-label="purple"> String[]  </span><span data-api-tag="require|qPhxlK">必选</span> `Sample value: ["volcwaf.com","www.testwaf.com"]`

Domains to be added to this domain group. The domains to be added must already be integrated into the WAF protection instance; otherwise, they cannot be added.



**Name ** <span data-label="purple"> String  </span><span data-api-tag="require|WSEoxe">必选</span> `Sample value: Keydomainnames`

Domain group name, used to identify this domain group.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The name must begin with a Chinese character, a letter, or a digit.</div>


* <div data-tips="true" data-tips-type="default">The name can contain letters, digits, Chinese characters, periods (.), underscores (_), and hyphens (\-).</div>


* <div data-tips="true" data-tips-type="default">The name must be between 1 and 128 characters long.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**HostGroupId ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 7515`

Domain group ID, which can be used to query, edit, and delete the domain group.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
