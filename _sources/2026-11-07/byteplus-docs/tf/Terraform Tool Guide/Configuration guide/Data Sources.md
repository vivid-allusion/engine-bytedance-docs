---
title: "Data Sources"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Data-Sources"
---

A data source is a special resource for querying the attributes and information of existing resources. You can declare a data source using the keyword "data."

<span id=".5p-l6K-i6LWE5rqQ5L-h5oGv"></span>
## Querying resource information

The following example demonstrates how to query the ID and other information of an elastic IP address (EIP) named "test\-eip1."

```Plain Text
data "byteplus_eip_addresses" "default"{
  name = "test-eip1"
}
```


<span id=".5byV55So6LWE5rqQ5L-h5oGv"></span>
## Referencing resource information

When you reference resource information, the format is data.DATA_TYPE.NAME.ATTRIBUTE. For example:

```Plain Text
resource "byteplus_eip_associate" "foo" {
  allocation_id = data.byteplus_eip_addresses.default.id
  ...
}
```
