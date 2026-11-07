---
title: "tosfsspec troubleshooting"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_troubleshooting"
---

This article mainly introduces some common issues encountered when using tosfsspec and how to locate them.

<span id="7fd5c095"></span>
## Issue location

When you encounter problems, enable debug logs for `fsspec` and `tosfsspec` to help identify the issue. The following is a sample that can be used independently in your code:

```Python
import logging
logging.basicConfig(level=logging.DEBUG)
logging.getLogger('fsspec').setLevel(logging.DEBUG)
logging.getLogger('tosfsspec').setLevel(logging.DEBUG)
```


This code prints detailed information on low\-level operations and network requests to help you analyze the problem.

<span id="e8782755"></span>
## Troubleshooting

<span id="27f2c4e5"></span>
### `ValueError: The part_size must be >= 4194304`


* Symptoms:

   ValueError occurs when initializing `TosFileSystem` or calling `fs.open()`, indicating that `part_size` or `block_size` must be at least 4MB.

* What it means:

   TOS sets a minimum part size limit for multipart uploads. In write modes (`'wb'`, `'ab'`), the `block_size` parameter determines the size of each part; if it is less than 4MB, this error occurs.

* How to fix it:

   * When using write mode with `fs.open(..., mode='wb')` or `fs.open(..., mode='ab')`, ensure the `block_size` parameter is at least `4 * 1024 * 1024`.

   * When initializing `TosFileSystem(part_size=...)`, make sure the `part_size` parameter is at least `4 * 1024 * 1024`.

   * If unsure about the suitable value, do not explicitly set `block_size`; `tosfsspec` will use the default value of 8MB.


<span id="2ec87671"></span>
### Permission error (for example, `TosException: status=403`)


* Symptoms:

   Receiving `tos.exceptions.TosException` with status code 403 (Forbidden) during operations like `ls`, `open`, or `put`.

* What it means:

   * AK/SK error: the provided `key` (Access Key ID) or `secret` (Secret Access Key) is incorrect or expired.

   * IAM policy restriction: the IAM policy attached to your account does not grant permission for the operation. For example, you may only have read permission (`tos:GetObject`) but lack write permission (`tos:PutObject`) or list permission (`tos:ListObjects`).

   * IP whitelist restriction: the Bucket or account has an IP whitelist, and your access IP is not allowed.

* How to fix it:

   * Verify AK/SK: ensure there are no leading or trailing spaces, the credentials are active, and they match the account used.

   * Check IAM policy: ensure it includes the required permissions, commonly read `tos:GetObject`, write `tos:PutObject`, and list `tos:ListObjects`.

   * Confirm outbound IP: check if it is allowed by the Bucket’s access control policy.


<span id="d8910090"></span>
### Directory operation does not match expectations


* Symptoms:

   * There are files under the path, but when you use `fs.isdir('tos://my-bucket/some/path/')` to check, it returns `False`.

   * The directory is empty, and you want to delete it using `fs.rmdir()`, but the deletion fails.

* What it means:

   TOS’s FNS (flat namespace) Bucket does not have a real directory concept. Directories are simulated by zero\-byte objects ending with `/`.

   * `isdir` checks whether an object named `some/path/` exists. If this object does not exist (even if `some/path/file.txt` exists), `isdir` returns `False`.

   * `rmdir` can only delete zero\-byte objects representing directories, and it requires that no other objects exist under that object (no objects with the `prefix` of that directory).

* How to fix it:

   * Use `fs.makedirs(path, exist_ok=True)` to explicitly create directories, ensuring the directory object is created.

   * A more reliable way to check if a path is a directory is to verify if its name ends with `/` or use `fs.info(path)['type'] == 'directory'`.

   * To delete a non\-empty directory, use `fs.rm(path, recursive=True)`.


<span id="b02bee68"></span>
### `ValueError: The maxdepth is not supported for hns bucket`


* Symptoms:

   When performing recursive operations like `walk()`, `glob()`, and `rm(recursive=True)`, passing the `maxdepth` parameter to a Bucket triggers a `ValueError`.

* What it means:

   The `maxdepth` parameter limits the depth of recursive traversal, supported only in FNS (flat namespace) Buckets. HNS (hierarchical namespace) Buckets use native directory structures, and their underlying traversal API does not support depth limits.

* How to fix it:

   * Please confirm your Bucket type.

   * If it is an HNS Bucket, remove the `maxdepth` parameter. Handle depth limitations in your business code, for example, by adding a counter in the `walk` loop.

   * If you must use `maxdepth`, consider migrating data to an FNS type Bucket.


<span id="b2f222ed"></span>
### `FileNotFoundError`


* **Issue Description**:

   When accessing a path you expect to exist, a `FileNotFoundError` is returned.

* What it means:

   * The path does not exist: the Bucket name or Object Key is misspelled.

   * Insufficient permissions: lacking `tos:GetObject` or `tos:ListObjects` permissions for the object may also cause it to appear as not found in some cases.

   * missing directory marker: for `fs.info()`, when the path is a directory but lacks a corresponding directory marker object (a 0\-byte object ending with `/`), it may also return `FileNotFoundError`.

* How to fix it:

   * use `fs.ls()` to list parent paths step by step, confirming each level of the path (bucket, prefix, object name) is correct.

   * check and complete IAM permissions.

   * for directory scenarios, use `fs.ls(path)` to check contents first instead of relying only on `fs.info(path)`.
