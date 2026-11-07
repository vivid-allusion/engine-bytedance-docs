---
title: "FSX compatibility priority mode"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/FSX_compatibility_priority_mode"
---

This article mainly introduces the usage and compatibility boundaries of FSX compatibility priority mode, as well as differences in common tools/workflows under this mode.

<span id="d061dff9"></span>
## Background and objectives

FSX defaults to performance priority mode, which focuses on enhancing object storage semantics and data read/write performance (such as sequential large file read/write and cache optimization). However, its underlying behavior may differ from standard local file systems in supporting certain POSIX semantics. To address this, FSX offers a **compatibility priority mode** (`compatible_mode`).

The core goal of this mode is to align POSIX access behavior of common ecosystem tools as much as possible, reducing execution failures or exceptions caused by differences in underlying tool calls; it also ensures seamless migration of existing business from traditional file system clients to FSX without changing original behavior and logic.

<span id="1f0867c1"></span>
## Core features

After enabling compatibility priority mode, FSX mainly supports the following features:


* File operations: supports random file writes and file truncation (both extension and reduction).

* Attribute simulation: deeply simulate file permissions, owner/group (UID/GID), and timestamps.

* Interface completion: complete system\-level interfaces such as symlink and device node (mknod).

* Directory and error code mechanism: optimize directory recognition and rename logic, and align error codes of some standard system call interfaces.


<span id="0a13b8b0"></span>
## Configuration method

Enable this mode if your business strongly depends on POSIX semantics. Enable it by specifying the `compatible_mode=true` parameter when mounting FSX.

<span id="2ca18f5e"></span>
### Mount command example

```Shell
mount -t fsx /tos/<bucket> <mount_point> \
  -o region="<region>",endpoint="<endpoint>",access_key_id=<ak>,secret_access_key=<sk>,\
no_writeback_cache,tos_allow_delete=true,compatible_mode=true
```


<span id="71215490"></span>
### Key parameter description


* `compatible_mode`: compatibility priority mode switch. Enable it by setting `true`.

* `no_writeback_cache`: disable write\-back cache. Recommended for tool calls, code compilation, and small file\-intensive scenarios; if the business heavily relies on cache to improve write performance, separate evaluation is required.

* `tos_allow_delete`: enable file deletion permission. Compatible priority mode does not strictly depend on this, but it affects many tool behaviors.


<span id="a6ec4a98"></span>
## Scenario\-based support differences (common tools/workflows)

The following shows support status and configuration recommendations for common tools and workflows under compatible priority mode:

✅ Supported, ❇️ Partially supported, ❌ Not supported


|Tools/scenarios |Support level |Description |
|---|---|---|
|cat/echo |✅ |Supports read\-write redirection and append write operations. |
|vim |❇️ |Supports file editing. Due to the vim mechanism, `.swp` temporary files may remain (related to deletion/overwrite policies); it is recommended to use parameters that allow deletion/overwrite or adjust the editor's temporary file strategy. |
|cp/mv |❇️ |Supports basic copy and move operations.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Creating hard links using the <code> cp -l </code> command is not supported.</div><br> |
|rsync |❇️ |Supports data synchronization and preserves file `mode`, `uid`, and `gid` attributes. |
|git |❇️ |Supports core actions such as `clone`, `init`, `pull`, `push`, and `checkout`. Executing `stash/stash pop` operations may generate warning logs but does not affect the main process.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Avoid frequent branch switching and massive small file writes in this mode to prevent performance bottlenecks.</div><br> |
|scp/sftp |✅ |Supports basic file transfer functions **.**  |
|tar/zip/gzip |✅ |Supports standard compression and decompression operations. If you need to strictly preserve timestamps and permission information, verify in the production environment first. |
|tosutil |❇️ |Supports file uploading. Due to differences in underlying mechanisms, large file download performance has some limitations; it is not recommended for regular large file download scenarios. |
|Language compilation (C++/Go/Java/Python/Nodejs) |❇️ |Supports normal compilation but takes longer overall. It is recommended to store source code or compilation archives only on FSX mount points, with compilation performed on local drives. |
|openclaw/sqlite |❇️ |Supports basic operation but has average read and write performance. |
|Rust compilation |❌ |Known compilation failures occur in compatibility\-first mode with hard links; use is not recommended. |
