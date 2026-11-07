---
title: "Access control overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/access-control-overview"
---

BytePlus MediaLive provides three features for managing client\-side access: URL authentication, IP allowlist and blocklist, and Referer allowlist and blocklist. Only users who comply with the rules can push or pull streams.


* [Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication): Validate whether a request is valid by adding authentication information to the URL, which is a highly secure mechanism.

* [IP restrictions](https://docs.byteplus.com/docs/byteplus-media-live/docs-ip-blocklist-and-allowlist): Control access by allowing or denying specific IP addresses.

* [Referer](https://docs.byteplus.com/docs/byteplus-media-live/docs-referer): Control access by allowing or denying specific sources.


Because the Referer and IP address can be spoofed, unauthorized users can still be able to push or pull streams. Therefore, if you have high security requirements for live stream content, we recommend that you use URL authentication.
