---
title: "Purge and prefetch"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/purge-prefetch-faq_en-us"
---

<span id="purging-prefetching-blocking-and-unblocking-under-a-wildcard-domain"></span>
## Purging, prefetching, blocking, and unblocking under a wildcard domain

You cannot purge, prefetch, block, or unblock files or directories directly using a wildcard domain. You must specify the exact subdomain.

For example, suppose your accelerated domains include `www.example.com`, `img.example.com`, and `doc.example.com`, and you also have a wildcard domain `*.example.com`. If you want to purge the file `/file/1.txt` under these domains, you cannot use `*.example.com/file/1.txt` as the purge URL. Instead, you must specify the purge URL for each exact accelerated domain:

> www.example.com/file/1.txt

> img.example.com/file/1.txt

> doc.example.com/file/1.txt
