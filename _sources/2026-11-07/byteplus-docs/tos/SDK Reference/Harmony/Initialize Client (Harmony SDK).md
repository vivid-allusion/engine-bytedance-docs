---
title: "Initialize Client (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initialize-the-client-harmony-sdk"
---

You can send HTTP/HTTPS requests to the TOS service only after initializing the TOSClient instance. This article introduces the initialization methods of Harmony SDK.

The TOS Harmony client provides a series of interfaces for interacting with TOS services, enabling the management of buckets, objects, and other TOS resources. When initializing the client, you need to configure the AccessKey ID, AccessKey Secret, Region, and other relevant information.

<span id="00458664"></span>
## Create TosClient

STS (Security Token Service) is a service that authorizes temporary access for third\-party users. With STS, you can provide token access credentials with customizable expiration times to third\-party applications or sub\-users.

Harmony SDK provides corresponding access interfaces and supports temporary authorization to access TOS via STS. It is recommended to use STS to access TOS in Harmony SDK. During configuration, you need to set the authorized Token in the SDK.

The following code demonstrates how to initialize TosClient using STS.

```TypeScript
const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region",
  endpoint: "Provide your endpoint",
});
```


<span id="536b6cad"></span>
## Initialization Parameter List


|**Parameter** |**Parameter Type** |**Required or Optional** |**Example Value** |**Description** |
|---|---|---|---|---|
|accessKeyId |String |Required |AKTPYmI1Z\*\*\*\* |Access Key ID。 For detailed steps on viewing AK and SK information, see [Viewing AK/SK Information](https://docs.byteplus.com/en/docs/6291/65568). |
|accessKeySecret |String |Required |T1dJM01UU\*\*\*\*== |AccessKey Secret, a private access key. |
|region |String |Required |cn\-beijing |The region where the TOS server is located. For information on the regions and access domain names supported by TOS, please refer to [Region and Access Domain Name (Endpoint)](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint). |
|endpoint |String |Optional |tos\-ap\-southeast\-1.bytepluses.com |Access domain name: If left empty, use the access domain name of the region where `region` is located. |
|securityToken |String |Optional |STSkeyJBY2NvdW50SW\*\*\*\*\*\*\*\*\*\*\*\* |Security token in the temporary access credential. For a detailed introduction to creating temporary access credentials, please refer to [Using STS temporary AK/SK+Token to access BytePlus TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service). |
|secure |Boolean |Optional |true |Indicates whether to use HTTPS requests. The value descriptions are as follows:<br><br><br>* `true`: Use HTTPS requests.<br><br>* `false`: Do not use HTTPS requests.<br><br><br>The default is `true`. |
|isCustomDomain |Boolean |Optional |false |Whether to prepend the bucket name to the Endpoint and access TOS using a virtual host domain name. The value options are explained as follows:<br><br><br>* `true`: Do not concatenate.<br><br>* `false`: Concatenation.<br><br><br>The default is `false`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS via a custom domain, you need to set <code>isCustomDomain</code> to <code>true</code>.</div><br> |
