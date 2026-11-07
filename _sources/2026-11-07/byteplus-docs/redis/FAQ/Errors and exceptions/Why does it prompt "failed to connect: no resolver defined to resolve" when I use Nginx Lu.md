---
title: "Why does it prompt \"failed to connect: no resolver defined to resolve\" when I use Nginx Lua to connect to Redis?"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/no-resolver-defind-to-resolve"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Problem phenomenon

When accessing an instance through Nginx + Lua by using the address domain name of Redis, some error messages appear, such as `failed to connect: no resolver defind to resolve`. They prompt that the address cannot be resolved properly.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you use other clients or ECS to access Redis instances through addresses, similar error messages related to failed domain name resolution may appear (For example, <code>Temporary failure in name resolution</code> or <code>Could not connect to Redis: No address associated with hostname</code>). If they prompt that the address cannot be resolved properly, refer to the solutions in this article to deal with the problem.</div>


<span id=".5Y-v6IO95Y6f5Zug"></span>
## Possible cause

The cause of the above errors may be that the DNS settings in the Nginx profile are incorrect, which results in failed address resolution. Check the Redis address domain name. Check whether the DNS settings in the Nginx profile are correct.

For Nginx 0.6.18 and later versions, when using variables to construct server addresses, use the `resolver` command to specify the DNS server address.

<span id=".5aSE55CG5pa55rOV"></span>
## Solution

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This article takes the Linux environment as an example to introduce relevant solutions.</div>



1. Check whether the Redis address set in the business code is correct.

   Log on to the Redis console to view the address and port number of the target Redis instance. For specific procedures, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/redis/view-address).

2. Confirm the DNS server settings in the profile `nginx.conf` of Nginx. Add the DNS server information of the BytePlus to the profile with the following command.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Nginx is used as an example in this article. You can modify the DNS server settings of the client or ECS in use based on your actual business.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>100.96.0.2</code> and <code>100.96.0.3</code> are DNS servers used by BytePlus.   </div>
   

   ```Bash
   resolver 100.96.0.2，100.96.0.3;
   ```
