---
title: "High-level APIs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/High-level_APIs"
---

High\-level APIs or commands are designed for file transfers and routine object and bucket management. Semantically aligned with user habits, they can be used directly in scripts and automation workflows. This topic explains how to use the high\-level APIs.

<span id="c015367b"></span>
## Overview


|Command |Description |Example link |
|---|---|---|
|`cp` |Copies local files/TOS objects/objects with the same prefix. |[cp (copy/upload/download)](https://docs.byteplus.com/docs/tos/High-level_APIs#ce6fb06d) |
|`mv` |Moves an object by copying the object to the specified destination and deleting the source object. |[mv (move)](https://docs.byteplus.com/docs/tos/High-level_APIs#8fed96d0) |
|`sync` |Incremental synchronization. |[sync (incremental synchronization)](https://docs.byteplus.com/docs/tos/High-level_APIs#922c68ec) |
|`mb` |Creates a bucket. |[mb (create bucket)](https://docs.byteplus.com/docs/tos/High-level_APIs#567b815f) |
|`rb` |Deletes a bucket. |[rb (delete bucket)](https://docs.byteplus.com/docs/tos/High-level_APIs#0d4376be) |
|`rm` |Deletes an object/objects with the same prefix. |[rm (delete object)](https://docs.byteplus.com/docs/tos/High-level_APIs#3ab8bcfd) |
|`ls` |Lists buckets or objects. |[ls (list buckets)](https://docs.byteplus.com/docs/tos/High-level_APIs#70bea5f2) |
|`stat` |Queries bucket/object metadata. |[stat (query bucket metadata)](https://docs.byteplus.com/docs/tos/High-level_APIs#421be46e) |
|`du` |Calculates the size of objects with the same prefix. |[du (prefix statistics)](https://docs.byteplus.com/docs/tos/High-level_APIs#b37cac32) |
|`find` |Search by name/size/time/storage type. |[find (search by storage type)](https://docs.byteplus.com/docs/tos/High-level_APIs#6b37e2a2) |
|`cat` |Streaming read. |[cat (streaming read)](https://docs.byteplus.com/docs/tos/High-level_APIs#5699a836) |
|`put` |Uploads data from stdin. |[put (upload)](https://docs.byteplus.com/docs/tos/High-level_APIs#2974caf0) |
|`presign` |Pre\-signed URLs |[presign (pre-signed URL)](https://docs.byteplus.com/docs/tos/High-level_APIs#4a79c9a7) |
|`restore` |Restores archived objects. |[restore (restore archived objects)](https://docs.byteplus.com/docs/tos/High-level_APIs#53daa377) |


<span id="4a27860a"></span>
## High\-level commands

<span id="ce6fb06d"></span>
### cp (copy/upload/download)

The common parameters are as follows:


|Parameter |Description |
|---|---|
|\-\-storage\-class <STANDARD\|IA\|ARCHIVE_FR\|INTELLIGENT_TIERING\|COLD_ARCHIVE\|ARCHIVE\|DEEP_COLD_ARCHIVE\> |Specifies the storage type for uploaded or copied objects. |
|\-\-acl <private\|public\-read\|...\> |Sets the access control list (ACL) permissions for an object. |
|\-\-recursive/\-\-include\-parent/\-\-include/\-\-exclude |Sets the scope of recursive listing and the rules for filtering objects. |
|\-\-checkpoint/\-\-checkpoint\-dir/\-\-checkpoint\-threshold <20MB\> |Enables resumable uploads and configures the checkpoint directory and threshold. |
|\-\-batch\-concurrency (default: 16)/\-\-list\-concurrency (default: 4)/\-\-multipart\-concurrency |Sets concurrency for batch operations, listing, and multipart uploads. |
|\-\-recursive\-list\-mode <auto\|flat\|hierarchical\> |Sets the recursive listing mode. The default mode is `auto`, meaning FNS buckets use flat listing and HNS buckets use hierarchical listing. To enable prefix\-level concurrency in FNS buckets, set the `hierarchical` option explicitly. |
|\-\-bandwidth\-limit <100MB\> |Sets the maximum bandwidth for transfers. |
|\-\-overwrite\-strategy <force\|no\-clobber\|newer\>/\-\-no\-clobber |Sets the file overwrite policy. |
|\-\-content\-type/\-\-meta key=v#key2=v2 |Sets the `Content-Type` and user\-defined metadata for objects. |
|\-\-report\-path/\-\-report\-failures\-only/\-\-manifest\-path/\-\-no\-manifest |Configures the output path of operation logs, the filtering rules, and the manifest files. |
|\-\-progress/\-\-no\-progress<br><br>\-\-progress\-granularity <part\|byte\> |Enables or disables progress display and sets the progress granularity to either `part` or `byte`. |
|A remote path ending with "/" |"/" is treated as a directory marker. |


Code example:

```JSON
ve-tos-cli cp ./file.txt tos://mybucket/path/file.txt
ve-tos-cli cp tos://mybucket/path/ ./local_dir/ --recursive
ve-tos-cli cp ./dir/ tos://mybucket/prefix/ --recursive --include "*.log"
ve-tos-cli cp large.bin tos://mybucket/large.bin --checkpoint
ve-tos-cli cp ./a.txt tos://mybucket/a.txt --storage-class IA --acl public-read
```


<span id="567b815f"></span>
### mb (create bucket)

The common parameters are as follows:

`--region`, `--storage-class` (default: STANDARD), `--acl`, `--az-redundancy <single-az|multi-az>`, `--bucket-type <fns|hns>`, and `--bucket-object-lock-enabled`.

Code example:

```Bash
ve-tos-cli mb tos://new-bucket
ve-tos-cli mb tos://new-bucket --storage-class IA
ve-tos-cli mb tos://new-bucket --bucket-type hns
ve-tos-cli mb tos://new-bucket --region cn-beijing --acl private --az-redundancy multi-az --bucket-object-lock-enabled
```


<span id="8fed96d0"></span>
### mv (move)

Code example:

```JSON
ve-tos-cli mv tos://b/old.txt tos://b/new.txt --force --confirm tos://b/old.txt
```


<span id="922c68ec"></span>
### sync (incremental synchronization)

Code example:

```JSON
ve-tos-cli sync ./local-dir/ tos://b/backup/ --delete --force --confirm tos://b/backup/
```


<span id="0d4376be"></span>
### rb (delete bucket)

Code example:

```JSON
ve-tos-cli rb tos://mybucket --force --confirm tos://mybucket
```


<span id="3ab8bcfd"></span>
### rm (delete object)

Code example:

```Bash
ve-tos-cli rm tos://b/prefix/ --recursive --all-versions --force --confirm tos://b/prefix/
```


<span id="70bea5f2"></span>
### ls (list buckets)

Code example:

```Shell
ve-tos-cli ls tos://b/prefix/ --max-keys 100 --human-readable --sort size --columns key,size,last_modified
```


<span id="421be46e"></span>
### stat (query bucket metadata)

Code example:

```Shell
ve-tos-cli stat tos://b/file.txt --version-id v1 --output json
```


<span id="b37cac32"></span>
### du (prefix statistics)

Code example:

```Shell
ve-tos-cli du tos://b/prefix/ --human-readable --max-depth 2 --cost --storage-price STANDARD=0.12
```


<span id="6b37e2a2"></span>
### find (search by storage type)

Code example:

```Shell
ve-tos-cli find tos://b/ --name "*.log" --size +100MB --mtime -7d --storage-class STANDARD
```


<span id="5699a836"></span>
### cat (streaming read)

Code example:

```Shell
ve-tos-cli cat tos://b/file.txt --range bytes=0-1023
```


<span id="2974caf0"></span>
### put (upload)

Code example:

```Shell
ve-tos-cli put tos://b/path/file.gz --content-type application/gzip --storage-class IA --no-clobber
```


<span id="4a79c9a7"></span>
### presign (pre\-signed URL)

Code example:

```Shell
ve-tos-cli presign tos://b/file.txt --expires 7200 --method PUT
```


<span id="53daa377"></span>
### restore (restore archived objects)

Code example:

```Shell
ve-tos-cli restore tos://b/archived.txt --days 7 --force
ve-tos-cli restore tos://b/prefix/ --recursive --tier Standard --force
ve-tos-cli restore tos://b/prefix/ --manifest list.txt --force
```
