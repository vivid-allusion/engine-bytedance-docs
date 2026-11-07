---
title: "Set predefined access policy for bucket or object (set-acl)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-a-predefined-access-policy-for-a-bucket-or-object-set-acl"
---

You can use the `set-acl` command to set the predefined access policy for a bucket or an object within a bucket.

<span id="29b3bba4"></span>
## Set bucket ACL

<span id="dbb3f00d"></span>
### Command format


<Tabs>
<Tab zoneid="fyYFiLCa" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil set-acl tos://bucket acl [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="FKZoNqq7" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil set-acl tos://bucket acl [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="6cc9f632"></span>
### Parameters

For descriptions of common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. |
|acl |Enum |Specify the predefined access policy of the bucket. Valid values:<br><br><br>* `private`: private, default value.<br><br>* `public-read`: public read.<br><br>* `public-read-write`: public read and write.<br><br>* `authenticated-read`: authenticated user read.<br><br>* `bucket-owner-read`: bucket owner read.<br><br>* `bucket-owner-full-control`: bucket owner full control. |


<span id="b09ddce4"></span>
### Example usage

The following command sets the predefined access policy of the `bucketname` bucket to `public-read`.


* Command


```Plain
./tosutil set-acl tos://bucketname public-read
```



* Return


```Plain
Start at 2024-01-22 10:42:49.230198 +0000 UTC
 
Set acl for bucket [bucketname] successfully!
```


<span id="27e3c653"></span>
## Set object ACL

<span id="81b4e242"></span>
### Command format


<Tabs>
<Tab zoneid="Xh2JNXF2RL" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Set a predefined access policy for a single object


```Bash
./tosutil set-acl tos://bucket/key acl [-versionId=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Set predefined access policies for multiple objects in bulk


```Bash
./tosutil set-acl tos://bucket/[prefix] acl -r [-j=1] [-v] [-include=*.xxx] [-exclude=*.xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="ywErsJIu8a" title=" Windows">
<TabTitle> Windows</TabTitle>

* Set a predefined access policy for a single object


```Bash
tosutil set-acl tos://bucket/key acl [-versionId=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Set predefined access policies for multiple objects in bulk


```Bash
tosutil set-acl tos://bucket/[prefix] acl -r [-j=1] [-v] [-include=*.xxx] [-exclude=*.xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



</Tab>
</Tabs>


<span id="3f138f18"></span>
### Parameters

For the description of general optional parameters, please refer to [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |bucket name. |
|key |String |Object name. |
|prefix |String |Prefix for object names in batch operations. |
|acl |Enum |predefined access policies for designated objects. supported values are as follows:<br><br><br>* `private`<br><br>* `public-read`<br><br>* `public-read-write`<br><br>* `authenticated-read`<br><br>* `bucket-owner-read`<br><br>* `bucket-owner-full-control`<br><br>* `bucket-owner-entrusted` |
|\-r |Bool |Execute batch operations to set predefined access policies for objects. |
|\-j |Integer |The maximum concurrent number for batch setting of object predefined access policies, defaulting to `defaultJobs` in the configuration file. |
|\-v |Bool |Batch set predefined access policies for multiple versions of objects by specified object name prefix. |
|\-versionId |String |The version number of a single object pending predefined access policy setup. |
|\-include |String |When batch setting predefined access policies for objects, the name matching pattern for included objects supports the following characters:<br><br><br>* `?`: matches any single character.<br><br>* `*`: matches any sequence of characters.<br><br>* `#`: serves as a delimiter.<br><br><br>For example, `-include=*.png#*.txt` matches all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing errors caused by operating system escaping special characters, it is recommended to use quotation marks when setting the name matching pattern.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name matching pattern only applies when uploading folders or file lists.</div><br> |
|\-exclude |String |When batch setting predefined access policies for objects, the following characters are supported in name matching patterns that do not include objects:<br><br><br>* `?`: matches a single arbitrary character.<br><br>* `*`: matches multiple arbitrary characters.<br><br>* `#`: serves as a delimiter.<br><br><br>For example, `-exclude=*.png#*.txt` matches all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing failures caused by operating system escape of special characters, it is recommended to use quotation marks to set the name matching pattern.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name matching pattern only takes effect when uploading folders or file lists.</div><br> |
|\-fr |Bool |Generate a result list file when setting a predefined access policy for a single object. |
|\-o |String |The folder for generating the result list file defaults to `defaultOutputDir` in the configuration file. |
|\-bt |String |Type of the bucket. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the bucket type is not specified, the bucket type is retrieved from the bucket metadata by default. |


<span id="8afd7819"></span>
### Example

<span id="6086e841"></span>
#### Set predefined access policy for a single object

The following command sets the predefined access policy for the **object.png** object in the **bucketname** bucket to **public\-read**.


* Command

   ```Plain
   ./tosutil set-acl tos://bucketname/object.png public-read
   ```
   

* Return

   ```Plain
   Start at 2024-01-22 14:22:15.66498 +0000 UTC
   
   Set acl for object [object.png] in the bucket [bucketname] successfully, cost [179], request id [f06701ae7a17971865ae7a17-b293fe0-1rRvBn-POA-cb-tos-front-azc-1]
   ```
   


<span id="5680eb82"></span>
#### Predefined access policies for multiple objects

The following command sets the predefined access policy of objects with the prefix **object** in the **bucketname** bucket to **public\-read**.


* Command

   ```Plain
   ./tosutil set-acl tos://bucketname/object public-read -r
   ```
   

* Return

   ```Plain
   Start at 2024-01-22 14:23:36.625134 +0000 UTC
   
   [--------------------------------------------------------------------------------------------] 100.00% tps:0.00 1/1 90ms
   Succeed count is:   1         Failed count is:    0
   Metrics [max cost:46 ms, min cost:46 ms, average cost:46.00 ms, average tps:10.99]
   
   Task id is: d4b331fc-b931-11ee-8422-b645e1163e55
   ```
   


&nbsp;
