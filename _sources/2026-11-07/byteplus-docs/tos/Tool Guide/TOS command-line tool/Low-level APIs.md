---
title: "Low-level APIs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Low-level_APIs"
---

Low\-level APIs or commands map one\-to\-one with TOS server\-side APIs. Designed for fine\-grained control and advanced feature invocation, they cover atomic operations such as bucket management, object operations, multipart uploads, and transfer acceleration. This topic explains how to use the low\-level APIs.

<span id="6c8fbd87"></span>
## Overview


|Command |Description |Example link |
|---|---|---|
|Core commands |Basic commands for creating and managing buckets and objects. |[Core commands](https://docs.byteplus.com/docs/tos/Low-level_APIs#b1d04bc4) |
|Bucket configuration commands |Commands for bucket configuration. Each command group typically supports the sub\-actions of `get`, `put`, and `delete`. |[Bucket configuration commands](https://docs.byteplus.com/docs/tos/Low-level_APIs#10495699) |
|Advanced feature commands |Commands for TOS's extended features such as image styles and content moderation. |[Advanced feature commands](https://docs.byteplus.com/docs/tos/Low-level_APIs#b343a2c3) |


<span id="b1d04bc4"></span>
### Core commands


|Command group |Sub\-command |
|---|---|
|bucket |`create`/`head`/`delete`/`list`/`stat`/`info`/`location` |
|object |`upload`/`download`/`form-upload`/`copy`/`delete`/`batch-delete`/`list`/`list-versions`/`head`/`stat`/`set-meta`/`set-time`/`set-expires`/`append`/`seal-append`/`modify`/`rename`/`restore`/`status`/`get-acl`/`set-acl`/`get-tagging`/`set-tagging`/`delete-tagging`/`link`/`get-symlink`/`create-symlink`/`get-fetch-task`/`create-fetch-task`/`fetch`/`set-retention`/`get-retention` |
|multipart |`create`/`upload`/`complete`/`abort`/`copy`/`list-parts`/`list` |
|turbo |`open`/`append`/`list`/`close` |


<span id="10495699"></span>
### Bucket configuration commands

Bucket configuration command groups manage various TOS bucket settings. Each command group typically supports the sub\-actions of `get`, `put`, and `delete`. Use the `--describe` option to view the available sub\-actions.


* Supported command groups:

   `quota`, `policy`, `lifecycle`, `storageclass` (formerly `storgeclass`), `cors`, `versioning`, `replication`, `encryption`, `custom-domain`, `notification`, `website`, `mirror`, `inventory`, `tagging`, `acl`, `rename`, `real-time-log`, `access-monitor`, `worm`, `trash`, `payment`, `logging`, `intelligent-tiering`, `transfer-acceleration`, `cdn-notification`, `https-config`, `pay-by-traffic`, `max-age`, and `redundancy-transition`.

* To view available sub‑actions for a specific command group:

   ```Bash
   ve-tos-cli lifecycle --describe --output json
   ve-tos-cli versioning --describe --output json
   ve-tos-cli cors --describe --output json
   ```
   


<span id="b343a2c3"></span>
### Advanced feature commands

The advanced feature commands manage the extended features of TOS. Supported command groups:

`data-process` (image styles, workflows, and content moderation), `object-set`, `accelerator`, `mrap` (multi\-region access points), `ap` (access points), `cap` (converged access points), `dataset` (intelligent retrieval and datasets), and `control` (control plane operations).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Recommended usage:</div>



1. <div data-tips="true" data-tips-type="default">Run <code>ve-tos-cli <group> --describe --output json</code> to view the command contract.</div>


2. <div data-tips="true" data-tips-type="default">Preview the operation with <code><group> <action> --dry-run</code>. After confirming, execute the actual command.</div>
