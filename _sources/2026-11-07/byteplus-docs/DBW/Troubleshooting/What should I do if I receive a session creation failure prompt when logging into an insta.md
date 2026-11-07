---
title: "What should I do if I receive a session creation failure prompt when logging into an instance on the Data Interaction Platform?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/session_creation_failure"
---

<span id=".5Y-v6IO95Y6f5Zug5LiA"></span>
## Possible Cause 1

During the first login to the Data Interaction Platform, the system automatically binds a whitelist to the instance by default. If you performed any of the following actions, it may result in session creation failure:


* Unbinding the instance from the system's automatically bound whitelist.

* Modifying or deleting the IP address in the whitelist.


**Solution**


* Rebind the whitelist to the instance.

* If you modified the IP address in the whitelist, you need to re\-add the IP address to the whitelist.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are logging into a Redis or MongoDB instance, you need to add the <code>100.64.0.0/10</code> address to the whitelist.   </div>
   

<span id=".5Y-v6IO95Y6f5Zug5LqM"></span>
## Possible Cause 2

The database connection has exceeded the default maximum number of connections for the instance specification. If you encounter such issues, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.
