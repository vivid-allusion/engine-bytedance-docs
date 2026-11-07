---
title: "RestoreObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-restoreobject"
---

Call the RestoreObject interface to restore objects in Archive, Cold Archive, and Deep Cold Archive.

<span id="7daf43f3"></span>
## Precautions


* Symbolic links do not support recovery. When the storage type of a symbolic link is Archive, Cold Archive, or Deep Cold Archive, you can directly access the object without needing to recover it first. When accessing the target object via a symbolic link, if the storage type of the target object is Archive, Cold Archive, or Deep Cold Archive, you need to recover it first.

* Objects in Archive, Cold Archive, or Deep Cold Archive cannot be directly read; you need to recover the object first to perform the read operation. Before restoring an object, you need to have RestoreObject permissions.

* After restoring objects in Archive, Cold Archive, or Deep Cold Archive, TOS will generate a temporary copy of Standard Storage type for you to read. The copy will be automatically deleted after the expiration period you set.

* After restoring objects from Archive, Cold Archive, or Deep Cold Archive, you can also use the RestoreObject interface to extend the copy's expiration period.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, only extending the validity period of replicas is supported, not shortening it.   </div>
   

* The recovery time for objects in Archive, Cold Archive, and Deep Cold Archive varies as follows:

   * The recovery time for Archive objects is within 1 minute.

   * The recovery time for Cold Archive objects depends on the recovery mode you choose. Different recovery modes have varying retrieval times and unit prices; the shorter the time, the higher the price. The recovery modes are explained as follows:

      * **Quick retrieval**: Generally completed within 1 to 5 minutes. Suitable for scenarios where urgent access is needed.

      * **Standard retrieval**: Generally completed within 2 to 5 hours.

      * **Batch retrieval**: Generally completed within 5 to 12 hours.

   * The recovery time for Deep Cold Archive objects depends on the recovery mode you choose. The retrieval time and unit price vary with different recovery modes; the shorter the time, the higher the price. The recovery modes are described as follows:

      * **Standard retrieval**: Generally completed within 12 hours.

      * **Batch retrieval**: Generally completed within 48 hours.

* Deep Cold Archive is currently in beta testing. If you need to use this feature, please contact your account manager.


<span id="d3d07314"></span>
## **Request syntax**

```JSON
POST /objectname?restore
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue
```


<span id="5af21b68"></span>
## **Request parameters and headers**

This request uses the common request header, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|restore |Query |String |Yes |\- |Represents the special identifier for RestoreObject requests. |
|versionId |Query |String |No |570773C5A7847849299D |The version number of the object. Specify the version to restore the object. |


<span id="95120c80"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Days |Integer |Yes |10 |The number of days for object recovery. The value range is 1 to 365.<br><br>The parent node is RestoreRequest. |
|RestoreJobParameters |Object |No |\- |Restore priority information. |
|Tier |String |No |Standard |Restore priority. The parent node is RestoreJobParameters.<br><br><br>* The recovery priority for Archive objects can only be `Standard`, indicating that the objects are restored within 1 minute.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>Standard</code> has different implications for the recovery priority of Archive, Cold Archive, and Deep Cold Archive objects, as explained below:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you restore Archive objects and set <code>Tier</code> to <code>Standard</code>, the objects will be restored within 1 minute.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you restore Cold Archive objects and set <code>Tier</code> to <code>Standard</code>, the objects will be restored within 2 to 5 hours.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you restore Deep Cold Archive objects and set <code>Tier</code> to <code>Standard</code>, the objects will be restored within 12 hours.   </div><br>   <br><br>* The recovery priority for Cold Archive objects is as follows:<br><br>   * `Expedited`: Quick retrieval, recovery completed within 1 to 5 minutes.<br><br>   * `Standard`: Standard retrieval, recovery completed within 2 to 5 hours.<br><br>   * `Bulk`: Batch retrieval, recovery completed within 5 to 12 hours.<br><br>* The recovery priority for Deep Cold Archive objects is as follows:<br><br>   * `Standard`: Standard retrieval, recovery completed within 12 hours.<br><br>   * `Bulk`: Batch retrieval, recovery completed within 48 hours.<br><br><br>If RestoreJobParameters information is not set, the `Standard` mode is used by default for retrieval. |


<span id="aa20130f"></span>
## **Response headers**

This request returns the common response message headers, please see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="5f272623"></span>
## **Response body elements**

There is no message element in this request response.

<span id="93f35824"></span>
## **Sample request**

<span id="7e59d000"></span>
### **Sample request 1**

Restore the objects from Archive, Cold Archive, or Deep Cold Archive.

```JSON
POST /objectname?restore
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue

{
  "Days": 10
}
```


<span id="53c09bcd"></span>
### **Sample request** **2**

Restore specified version of Archive, Cold Archive, or Deep Cold Archive.

```JSON
POST /objectname?restore&versionId=***
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue

{
    "Days": 10,
    "RestoreJobParameters": {
        "Tier": "Standard"
    }
}
```


<span id="c78382db"></span>
### **Sample request** **3**

Extend the validity period of copies for Archive, Cold Archive, or Deep Cold Archive.

```JSON
POST /objectname?restore
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue

{
  "Days": 12
}
```


<span id="5714ac5f"></span>
## **Sample response**

<span id="33a0ddbb"></span>
### **Sample response** **1**

Restore objects in Archive, Cold Archive, or Deep Cold Archive.

```JSON
HTTP/1.1 202 Accepted
x-tos-id-2: 5726ce090a2d002d-a444ed0
x-tos-request-id: 5726ce090a2d002d-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 0
```


<span id="ab2d9b96"></span>
### **Sample response** **2**

Restore again for Archive, Cold Archive, or Deep Cold Archive objects currently in recovery.

```JSON
HTTP/1.1 409 Conflict
x-tos-id-2: 5726ce090a2d002d-a444ed0
x-tos-request-id: 5726ce090a2d002d-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 0

{
    "Code": "RestoreAlreadyInProgress",
    "RequestId": "23480125cb6573606625cb65-ac1a6118-1ryjQL-RO-cb-1AZ-F-LFRZ-B-K2-1",
    "HostId": "jONFHoplLHsdsOxAENiZdsWlVlti****",
    "Message": "Object restore is already in progress",
    "EC": "0017-00000507"
}
```


<span id="5c694ce2"></span>
### **Sample response** **3**

Extend the validity period of replicas for Archive, Cold Archive, or Deep Cold Archive objects that have completed recovery.

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 5726ce090a2d002d-a444ed0
x-tos-request-id: 5726ce090a2d002d-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 0
```
