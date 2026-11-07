---
title: "Tag Overview"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview"
---

Resource tags are key\-value pairs. You can use resource tags to categorize and manage cloud resources from different dimensions, as well as for scenarios such as tag\-based authorization and bill management.

<span id="benefits"></span>
## **Benefits**

As a commonly used cloud resource management tool, resource tags offer the following benefits:


* **Convenience**: Provides unified, visualized console pages for querying and managing all cloud resources associated with tags.

* **Flexibility**: Supports single or batch operations for creating, deleting, modifying, and querying tags by using consoles or calling APIs.

* **Visibility**: Enables bill management based on resource tags across different dimensions, making departmental and product\-related expenses more transparent.


<span id="concepts"></span>
## **Concepts**


|**Term** |**Description** |
|---|---|
|Tag key\-value pair |A tag consists of a key and a value. A key can have multiple values, and both key and value are case\-sensitive. Multiple tags can be attached to a single resource, but each key can have only one value. |
|System tag |System tags are predefined tags attached to cloud resources by the system, typically prefixed with `volc:` or `sys:`. These tags are read\-only and cannot be modified, deleted, or manually attached by users. |
|Custom tag |Custom tags are user\-defined tags that can be attached to or detached from resources. Users can attach custom tags directly via cloud consoles or predefine them during resource planning for future use. |
|Createdby tag |Createdby tag are system\-generated tags automatically attached to resources, identifying their creators. These tags are often used for resource tracking and bill management based on resource ownership. |
