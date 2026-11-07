---
title: "Using FSSpec in the PyTorch training framework"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Using_FSSpec_in_the_PyTorch_training_framework"
---

PyTorch is one of the mainstream training frameworks and is widely used in the field of deep learning. Many researchers and developers choose PyTorch to build and train their deep learning models. The advantages of PyTorch include:


* Simplicity and ease of use: PyTorch's API is designed to be concise and intuitive, making it easy to learn and use.

* Dynamic computation graph: PyTorch adopts a dynamic computation graph mechanism, allowing computation graphs to be constructed dynamically at runtime, which facilitates debugging and flexible model adjustments.

* Rich features: PyTorch provides a wide range of features, including tensor operations, automatic differentiation, neural network modules, and more, making it convenient to build and train deep learning models.

* Strong community support: PyTorch has a large community, with extensive documentation, tutorials, and open\-source projects available for reference and learning.


PyTorch supports loading datasets through the fsspec interface, and TOSFS is the standard implementation of the fsspec interface. This article introduces demos for combining PyTorch and TOSFS to implement **dataset loading/iteration**, **save/load checkpoint**, and **training** in these three scenarios.

Install the latest version of TOSFS and PyTorch\-related dependencies using the following command:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to use Python version 3.9 or above.</div>


```Shell
pip install tosfs
pip install torch
pip install torchdata
pip install torchvision
pip install lightning
```


<span id="6d1d8de2"></span>
## Dataset loading and iteration

```Python
import os

import fsspec
from torchdata.datapipes.iter import FSSpecFileLister, FSSpecFileOpener
from tos import EnvCredentialsProvider

fsspec.register_implementation("tos", "tosfs.TosFileSystem", )

if __name__ == '__main__':

    kwargs = {
        'endpoint_url': os.environ.get("TOS_ENDPOINT"),
        'credentials_provider' : EnvCredentialsProvider(),
        'region': 'cn-beijing'
    }

    # iterable-style datasets
    file_lister = FSSpecFileLister(root='tos://{your-bucket}/{your-dataset}/', **kwargs)
    iterable_dataset = FSSpecFileOpener(file_lister, mode="rb", **kwargs)

    for _, item in iterable_dataset:
        data = item.read()
```


<span id="aba3708c"></span>
## Save and load checkpoint

```Python
import os

import torch
import torchvision
from tos import EnvCredentialsProvider

from tosfs.core import TosFileSystem

if __name__ == '__main__':
    tosfs = TosFileSystem(
        endpoint_url=os.environ.get("TOS_ENDPOINT"),
        region=os.environ.get("TOS_REGION"),
        credentials_provider=EnvCredentialsProvider(),
    )

    model = torchvision.models.resnet18()

    # save
    with tosfs.open('{bucket}/checkpoint/epoch1.ckpt', 'wb') as writer:
        torch.save(model.state_dict(), writer)

    # load
    with tosfs.open('{bucket}/checkpoint/epoch1.ckpt', 'rb') as reader:
        stat_dict = torch.load(reader)

    model.load_state_dict(stat_dict)
```


<span id="b6b52835"></span>
## Training

```Python
import os
import time

import fsspec
import lightning as L
import torch
import torchvision
from PIL import Image
from torchdata.datapipes.iter import FSSpecFileLister, FSSpecFileOpener
from tos import EnvCredentialsProvider

fsspec.register_implementation("tos", "tosfs.TosFileSystem")

class VisionModel(L.LightningModule):
    def __init__(
            self,
            dataset: torch.utils.data.Dataset,
            model_name: str,
            batch_size: int,
            num_workers: int,
    ):
        super().__init__()

        ctor = getattr(torchvision.models, model_name)
        self.model = ctor(weights=None)
        self.dataset = dataset
        self.batch_size = batch_size
        self.num_workers = num_workers
        self.epoch_start_time = None
        self.epoch_images = 0

        self.loss_fn = torch.nn.CrossEntropyLoss()

    def configure_optimizers(self):
        return torch.optim.AdamW(self.parameters(), lr=1e-3)

    def train_dataloader(self) -> torch.utils.data.DataLoader:
        if self.epoch_start_time is None:
            self.epoch_start_time = time.perf_counter()
        return torch.utils.data.DataLoader(
            self.dataset, batch_size=self.batch_size, num_workers=self.num_workers, shuffle=False,
        )

    def forward(self, imgs):
        return self.model(imgs)

    def training_step(self, batch, batch_idx):
        imgs, labels = batch
        self.epoch_images += len(imgs)
        preds = self.forward(imgs)
        loss = self.loss_fn(preds, labels)
        self.log('train_loss', loss)
        return loss

    def on_train_epoch_end(self):
        t = time.perf_counter() - self.epoch_start_time
        self.log('throughput', self.epoch_images / t)
        print(f'{self.epoch_images} images in {t:.2f}s = {self.epoch_images / t:.2f} images/sec')
        self.epoch_start_time = time.perf_counter()
        self.epoch_images = 0


def load_image(sample):
    to_tensor = torchvision.transforms.ToTensor()
    return (to_tensor(Image.open(sample['.jpg'])), int(sample['.cls'].read()))


if __name__ == '__main__':

    kwargs = {
        'endpoint_url': os.environ.get("TOS_ENDPOINT"),
        'credentials_provider' : EnvCredentialsProvider(),
        'region': 'cn-beijing'
    }

    dataset_uri = 'tos://{your-bucket}/{your-dataset}/'

    file_lister = FSSpecFileLister(root=dataset_uri, **kwargs)
    file_lister = file_lister.sharding_filter()
    iterable_dataset = FSSpecFileOpener(file_lister, mode='rb', **kwargs)
    iterable_dataset = iterable_dataset.load_from_tar().webdataset().map(load_image)

    L.seed_everything(21, True)
    trainer = L.Trainer(
        max_epochs=3, precision='16-mixed',
        enable_checkpointing=False,
    )

    model = VisionModel(
        iterable_dataset, model_name='resnet50', batch_size=64, num_workers=1)

    start = time.perf_counter()
    trainer.fit(model)
    end = time.perf_counter()
    print(end - start)
```
