---
title: "TOS PyTorch Connector data types"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/TOS_PyTorch_Connector_data_types"
---

This topic introduces the data types in TOS PyTorch Connector.

<span id="24478e08"></span>
## TosMapDataset


|Attribute/Method |Type/Return type |Description |
|---|---|---|
|__getitem__ |int |Returns a single sample based on the index. |
|__len__ |int |Returns the total number of samples in the dataset. |
|close |None |Releases and closes a resource. |
|__enter__ |None |Enters the context manager. |
|__exit__ |None |Exits the context manager to release resources or perform cleanup operations. |


<span id="39f3332b"></span>
## TosIterableDataset


|Attribute/Method |Type/Return type |Description |
|---|---|---|
|__iter__ |Any |Returns an iterator to sequentially traverse the samples. |
|__len__ |int |Returns the total number of samples in the dataset. |
|close |None |Releases and closes a resource. |
|__enter__ |None |Enters the context manager. |
|__exit__ |None |Exits the context manager to release resources or perform cleanup operations. |


<span id="e8fb2db3"></span>
## TosObjectWriter


|Method |Type |Description |
|---|---|---|
|bucket |str |Specifies the name of the bucket in which the object is stored. |
|key |str |Specifies the name of the object. |
|closed |bool |Indicates whether the stream is closed. |
|write |int |Writes data to the object stream and returns the number of bytes written. |
|close |None |Closes the write stream, which triggers an upload to TOS. |
|tell |int |Returns the current position of the write pointer within the object. |
|writable |bool |Indicates whether the stream is writable. |
|__enter__ |None |Enters the context manager. |
|__exit__ |None |Exits the context manager to release resources or perform cleanup operations. |


<span id="bd20f7a4"></span>
## TosObjectReader


|Method |Type |Description |
|---|---|---|
|bucket |str |Specifies the name of the bucket in which the object is stored. |
|key |str |Specifies the name of the object. |
|size |int |Specifies the object size. |
|etag |str |Specifies the ETag of the object. |
|crc64 |int |Specifies the CRC64 checksum of the object. |
|closed |bool |Indicates whether the stream is closed. |
|read |bytes |Reads data from the object stream and returns the bytes read. |
|readinto |int |Reads data into a pre\-allocated buffer and returns the number of bytes read. |
|seek |int |Moves the pointer to a specific position inside an object. |
|close |None |Closes the read stream. |
|tell |int |Returns the current position of the read pointer within the object. |
|readable |bool |Indicates whether the stream can be read from. |
|seekable |bool |Indicates whether the stream is seekable. |
|__enter__ |None |Enters the context manager. |
|__exit__ |None |Exits the context manager to release resources or perform cleanup operations. |
