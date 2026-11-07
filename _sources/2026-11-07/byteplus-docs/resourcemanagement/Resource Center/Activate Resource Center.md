---
title: "Activate Resource Center"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Activate_Resource_Center"
---

The resource center is a free service available for regular use upon activation and does not incur additional charges.

<span id="procedure"></span>
## Procedure


1. Log in to [Resource center](https://console.byteplus.com/resourcemanager/resource_center/my_resource).

2. Select the check box and click the button to enable the resource center.

> Note: The first data build of the resource center usually takes a few minutes, and it may take longer when the resource volume is large.


3. Complete the activation process.


<span id="impacts"></span>
## Impacts


1. When you activate the resource center, you need to authorize the system to create a service\-linked role named ServiceRoleForResourceCenter. The resource center will use this role to call the resource list or query APIs of cloud services to obtain cloud resource data.

2. After the resource center is activated, you can view resource data in the resource center, and the resource search module on the homepage will also support global searches for resources.

3. Every time the resource center retrieves a cloud resource, a log is recorded and can be queried through operation audits.
