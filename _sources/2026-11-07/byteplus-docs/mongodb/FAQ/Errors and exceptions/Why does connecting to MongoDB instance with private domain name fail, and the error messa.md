---
title: "Why does connecting to MongoDB instance with private domain name fail, and the error message contains public domain name information?"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Why_does_connecting_to_MongoDB_instance_with_private_domain_name_fail_and_error_message_contains_pub"
---

<span id="E7S9ANKq"></span>
## Problem

Connecting to MongoDB instance with private domain name (that is, domain name ending with `ibytepluses.com`) fails, and the returned error message displays public domain name (that is, domain name ending with `bytepluses.com`) or `fail to satisfy horizon { horizonName:[ "public" ] }`.

<span id="L6lsIqY8"></span>
## Possible causes

Document Database for MongoDB uses the following private network segments by default:


* `10.0.0.0-10.255.255.255`

* `172.16.0.0-172.31.255.255`

* `192.168.0.0-192.168.255.255`

* `33.0.0.0-33.255.255.255`


If the Virtual Private Cloud(VPC) you selected when creating a MongoDB instance is not within the default network segments mentioned above, MongoDB might incorrectly resolve the private IP address used by your client as a public IP address when you connect to MongoDB instance using private domain name. This leads to connection failure and public domain name information being displayed in the returned error message.

<span id="gwcg1NPZ"></span>
## Solution


1. Obtain the IP address range information of the VPC currently used by the MongoDB instance and confirm whether this range is within the default private network segments.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view the VPC information currently used by the instance in the <strong>Basic information</strong> section under the MongoDB <strong>Summary</strong> tab. Click the VPC name to navigate to its details page and view its IP address information. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/view-instance">Viewing instance information</a> and <a href="https://docs.byteplus.com/en/docs/vpc/Viewing-details-of-a-VPC">Viewing VPC details</a>.   </div>
   

2. Add the IP address range of the VPC currently used by the MongoDB instance to the `splitClientPrivateAddress` parameter value. For specific procedure of parameter modification, refer to [Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The parameter <code>splitClientPrivateAddress</code> is currently in gray release, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to apply for usage.   </div>
