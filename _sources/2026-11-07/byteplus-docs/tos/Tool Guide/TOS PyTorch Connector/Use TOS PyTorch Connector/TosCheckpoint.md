---
title: "TosCheckpoint"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/TosCheckpoint"
---

This article introduces how to read and write checkpoints directly from TOS using TosCheckpoint.

<span id="80406b4e"></span>
## Prerequisites

TOS PyTorch Connector is installed and configured. For detailed steps, see [Install TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Install_TOS_PyTorch_Connector) and [Configure TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Configure_TOS_PyTorch_Connector).

<span id="cfa670b8"></span>
## TosObjectWriter

The TosObjectWriter() method of TosCheckpoint writes data to checkpoints.

<span id="3fe6c497"></span>
### Parameter description

Using TosCheckpoint requires proper configuration. For details, see [Pass credentials](https://docs.byteplus.com/docs/tos/Configure_TOS_PyTorch_Connector#bbfc758a).

<span id="787f3ad9"></span>
### Code example

The following example demonstrates how to use PyTorch to write checkpoints through TosCheckpoint. Replace region, endpoint, ak/sk, and other parameters with the values you need.

```Python
import torch
import torchvision
from tostorchconnector import TosCheckpoint, CredentialProvider

checkpoint_uri = 'tos://bucket/key'
region = 'cn-beijing'
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'

with TosCheckpoint(region, endpoint, cred=CredentialProvider(ak, sk)) as checkpoint:
    model = torchvision.models.resnet18()
    with checkpoint.writer(checkpoint_uri) as writer:
        torch.save(model, writer)
```


<span id="73e8968b"></span>
## TosObjectReader

The TosObjectReader() method of TosCheckpoint can read checkpoints from TOS.

<span id="430e0245"></span>
### Parameter description

When using TosCheckpoint, configure it accordingly. For detailed configuration instructions, see [Passing Credentials](https://docs.byteplus.com/docs/tos/Configure_TOS_PyTorch_Connector#bbfc758a).

<span id="2842eb35"></span>
### Code example

The following example demonstrates how to use PyTorch to read checkpoints from TOS through TosCheckpoint. Replace region, endpoint, ak/sk, and other parameters with the values you need.

```Python
import torch
from tostorchconnector import TosCheckpoint, CredentialProvider

checkpoint_uri = 'tos://bucket/key'
region = 'cn-beijing'
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'

with TosCheckpoint(region, endpoint, cred=CredentialProvider(ak, sk)) as checkpoint:
    with checkpoint.reader(checkpoint_uri) as reader:
        model = torch.load(reader)
        print(model)
```
