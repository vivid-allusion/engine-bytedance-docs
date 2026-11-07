---
title: "TOS PyTorch Connector Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/TOS_PyTorch_Connector_Overview"
---

TOS PyTorch Connector is a high\-performance data read\-write tool provided by BytePlus TOS for AI training scenarios. With TOS PyTorch Connector, you can efficiently read large model training data from TOS, significantly speeding up data loading for large\-scale machine learning or deep learning projects under the PyTorch framework.

<span id="10899b3e"></span>
## Benefits


|Item |Use TOS PyTorch Connector |Not using TOS PyTorch Connector<br><br>(such as Python SDK, FSX) |
|---|---|---|
|Performance |High, with special optimizations for reading and writing dataset loading and checkpoint data. |Low, lacking targeted optimizations. |
|Data Loading Methods |Supports stream loading to effectively reduce costs and management burden. |Requires pre\-downloading (warming up) data, adding extra costs and management overhead. |
|Data Access |Read and write to TOS directly via HTTP protocol for the shortest access path. |Scenarios like FSX involve an additional FUSE protocol conversion, increasing complexity.<br><br> |
|Usability |Provides dataset and checkpoint model support for the Torch framework with simple configuration and ready\-to\-use features. |Requires writing custom code to wrap datasets and checkpoint models, increasing development complexity. |


<span id="d838ee9f"></span>
## Features

TOS PyTorch Connector offers the following three key features for the PyTorch framework:


|Function |Protocol characteristics |Related classes |Methods |
|---|---|---|---|
|Mapped dataset |Suitable for random access, allowing quick retrieval of specific data during training. |TosMapDataset |TosMapDataset and TosIterableDataset provide the same methods:<br><br><br>* from_prefix()<br><br>   Construct a dataset using the TOS_URI prefix, suitable for scenarios where TOS storage paths follow a consistent pattern.<br><br>* from_urls()<br><br>   Create a dataset from a list of TOS_URIs, suitable for scenarios where TOS storage paths are specific but scattered.<br><br><br> |
|Iterable dataset |Suitable for streaming sequential access, efficiently handling large continuous data streams. |TosIterableDataset ||
|Checkpoint interface |Loads checkpoints from TOS during model training and saves checkpoints directly to TOS after periodic training. |TosCheckpoint |* TosCheckpoint()<br><br>   Initialize a TosCheckpoint object to load checkpoints from TOS during model training and save checkpoints directly to TOS after periodic training cycles.<br><br>* TosObjectReader()<br><br>   TosCheckpoint object method to read checkpoints from TOS.<br><br>* TosObjectWriter()<br><br>   TosCheckpoint object method to write checkpoints to TOS. |


<span id="b40e351a"></span>
## Working principles

The workflow for using TOS PyTorch Connector to train with data from TOS in PyTorch is shown in the diagram below:<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cc5f84a919d8be6a9fde2fc7d57ea461.png) </span>

<span id="a8bdad9c"></span>
## Next steps


1. [Install TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Install_TOS_PyTorch_Connector).

2. [Configure TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Configure_TOS_PyTorch_Connector).

3. Use TOS PyTorch Connector.

   * Use [TosMapDataset](https://docs.byteplus.com/docs/6349/2201575) to build a map\-style dataset suitable for random access.

   * Use [TosIterableDataset](https://docs.byteplus.com/docs/6349/2201568) to build an iterable dataset suitable for sequential streamed access.

   * Use [TosCheckpoint](https://docs.byteplus.com/docs/6349/2201574) to store and access checkpoints.


<span id="1dcb84b4"></span>
## Related documentation

[Performance](https://docs.byteplus.com/docs/tos/Performance)

[Topic](https://docs.byteplus.com/docs/tos/Topic)
