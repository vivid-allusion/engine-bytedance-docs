---
title: "NFS protocol"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/NFS_protocol"
---

EFS uses the NFS protocol for network access and storage resource sharing. This topic covers the basic concepts, versions, and data and metadata consistency mechanisms of the NFS protocol.

<span id="fSedpRl7"></span>
## Basic concepts

Network File System (NFS) is a distributed file system that allows users on client computers to access files over a computer network as if the files were local.

<span id="yikn4fz4"></span>
## Protocol versions

Today, most systems use either NFS version 3 (NFSv3) or NFS version 4 (NFSv4). NFSv4 has three variants: 4.0, 4.1, and 4.2. EFS supports both NFSv4.1 and NFSv3. The difference between NFSv3 and NFSv4 is as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">For more information on the NFSv3 and NFSv4 protocols, see <a href="https://datatracker.ietf.org/doc/html/rfc1813">NFS Version 3 Protocol Specification</a> and <a href="https://datatracker.ietf.org/doc/html/rfc3530">Network File System (NFS) version 4 Protocol</a>.</div>



|**Differences** |**NFSv3** |**NFSv4** |
|---|---|---|
|Protocol characteristics |NFSv3 operates over TCP with a stateless nfsd server. It relies on supplementary services, such as rpc.mountd, rpc.statd, and lockd, for mounting file systems and locking files. |NFSv4 is a stateful protocol that does not rely on NLM or MOUNT. Instead, it natively implements file locking and file system root access. |
|Request handling |NFSv3 supports asynchronous writes and sends ACCESS requests to check permissions. |NFSv4 only provides two requests: NULL and COMPOUND. All operations are integrated into the COMPOUND request, which allows multiple operations to be bundled into a single request. |
|Security |NFSv3 does not natively support encryption or Kerberos authentication. However, it can use RPC AUTH_SYS to verify a mounted client's permissions for specific files. |NFSv4 supports Kerberos\-based authentication (RPCSEC_GSS), which provides granular, improved security. |
|Compatibility |NFSv3 is compatible with a variety of operating systems and hardware platforms. |NFSv4 requires newer kernel versions, and may not work on legacy systems or hardware. |


<span id="RvCokUG8"></span>
## Data and metadata consistency

To ensure data consistency across clients, NFS provides weak cache consistency guarantees for file sharing.

<span id="UiwGoT6L"></span>
### Eventual consistency based on kernel cache timeout

The NFS client caches both data and metadata obtained from the server, and considers this cached information valid for a specified duration. When the client subsequently accesses the same file, it directly reads the cached information, including file attributes, content, and directory listings, if the cache is valid. If the cache expires, the client fetches updated file information from the server to maintain consistency. For more information, see [NFS](https://linux.die.net/man/5/nfs).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">NFS cache entry timeout value: Adaptive, with a default range of 1 to 60 seconds.</div>


* <div data-tips="true" data-tips-type="tip">Cached information in NFS includes file attributes, file content, and directory entries. Details are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">File attributes: Cache metadata such as GIDs, UIDs, modes, and access/modify/change time (a/m/ctime).</div>


   * <div data-tips="true" data-tips-type="tip">File content: Caches the actual data of the file.</div>


   * <div data-tips="true" data-tips-type="tip">Directory entries: Cache the list of files present or absent within a directory.</div>



<span id="hXTIJAJm"></span>
### Close\-to\-open (CTO) cache consistency

With the cache timeout mechanism, changes made by Client A to a shared file may not be immediately visible to Client B if multiple clients are accessing the file at the same time. To enhance data consistency, NFS offers a cache consistency mechanism that checks and flushes files when they are opened and closed. This ensures that the latest data and metadata are available when the file is reopened. The CTO consistency model guarantees that subsequent clients reopening the same file after a client has opened, modified, and closed it will access the most recently written data.
