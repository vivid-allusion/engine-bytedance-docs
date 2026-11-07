---
title: "Ray architectural practices in multimodal image processing"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_architectural_practices_in_multimodal_image_processing"
---

In today's digital era, multimodal data processing—especially image processing—has become a focal point across many fields. From intelligent image recommendations on social media platforms to precise analysis of medical imaging, multimodal image processing technologies are playing an increasingly important role. Ray, as a powerful distributed computing framework, demonstrates outstanding performance and flexibility in architectural practices for multimodal image processing.

<span id="e6247214"></span>
## Background

This article uses fine\-tuning model training for image editing as an example to describe the significant benefits brought by upgrading to the Ray+Lance architecture in this scenario.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35dbfc2930e44ae9a130a13580af1959~tplv-goo7wpa0wc-image.image) </span>

The fine\-tuning process for image editing models generally includes the following four steps:


* **Data crawling:** 

   * Open image datasets are selectively collected based on the training objectives.

* **Data filtering:** 

   * Aspect ratio information

   * URL data source

   * Lighting and shadow

   * Aesthetic score threshold

* **Model inference processing:** 

   * Aesthetic score evaluation

   * Caption

   * Clip

* **Model training fine\-tuning**

   * Stable Duffsion

   * FLUX.1\-dev


<span id="80a09911"></span>
## Historical architecture

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54a58ec336774962917d32bb410d3108~tplv-goo7wpa0wc-image.image) </span>

For the user's historical architecture, attention should be paid to the following five points.


1. **Data storage**: The collected data is organized in the form of webdataset.

   1. Using webdataset can solve the problem of excessively high QPS in object storage caused by small files.

   2. Drawback: If files are accessed randomly or filtered based on certain conditions, webdataset performs poorly. The json files in the tar package need to be extracted, resulting in significant IO amplification.

2. **Data sharding**: When distributed preprocessing of data is required, directories are manually split, and each machine processes only a portion of the data.

   1. Drawback: Manually splitting the dataset is a complex task, requiring evaluation of whether the data assigned to each task is evenly distributed.

   2. Drawback: If there is shuffling or aggregation during data processing, manual distribution results in different tasks, making it impossible to process different data within the same task.

3. **Heterogeneous data processing**: Both CPU and GPU operators are on the same node, and the CPU directly utilizes resources from the host machine where the GPU resides.

   1. Disadvantage: When there is a significant difference in concurrency between CPU operators and GPU operators, backpressure may occur for individual operators.

4. **Training data preparation**: In the last mile of training, simple conditions are typically used to filter datasets. Therefore, the solution chosen by the customer is to store image data labels in a database and store images as columns in Parquet format. Since Parquet contains only a single column for image content, the issue of IO amplification is somewhat alleviated.

   1. Disadvantage: It is necessary to associate two types of data sources, and association logic is also required.

   2. Disadvantage: The Dataloader loads the entire column, including the image_content column, so shuffling during the loading process uses a large amount of memory, resulting in slower loader performance.

5. **Model training**: Distributed training on a single machine with multiple GPUs is implemented using Pytorch DDP.


<span id="cfc00676"></span>
## Architecture after volcano upgrade

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65827ff381134dc4802d63c2d2c18d6e~tplv-goo7wpa0wc-image.image) </span>


1. **Data storage**: Data storage has transitioned from the original webdataset format to the Lance format. Lance offers significant advantages in multimodal storage scenarios. Lance expands the original metadata stored in JSON into specific columns and persists image content as binary type. For a detailed introduction to Lance, see [Training CLIP multimodal models using the Lance data format](https://www.volcengine.com/docs/6491/1359401).

   1. Advantage: Metadata and data can be stored simultaneously in the form of a Lance table.

   2. Advantage: Random reads and QPS pressure on image files are reduced.

   3. Advantage: For scenarios involving adding columns or labels, Lance's merge_columns capability can be used.

2. **Data sharding**: Data is directly sharded using Ray Data.

   1. Advantage: Ray Data has automatic sharding capability; you only need to set the concurrency and num_cpus to control concurrency and resource consumption.

   2. Advantage: Ray Data itself has backpressure capability, allowing control of task execution rate and preventing OOM occurrences.

   3. Advantage: Volcano's Ray Data enhances elastic scaling capability, the expanded webdataset JSON feature, and adds scenarios for backpressure strategies.

3. **Heterogeneous data processing**: Data filtering uses the CPU, while the inference process uses the GPU. Ray can simultaneously schedule heterogeneous resource types within a single pipeline.

   1. Advantage: Data transmission between heterogeneous resources is performed in memory, eliminating the need for persistence, resulting in better performance and supporting more frequent iterations.

   2. Advantage: Operators can be triggered on different resource pools, which allows for optimal support of varying workloads for different operators. For example, if the filter has a high selection rate and requires more CPU resources, the CPU resource pool can be provisioned with more resources.

   3. Advantage: The inference process can use either online inference or offline inference. Online inference enables resource pre\-allocation and model preloading. If the inference parameters are small and can be passed via Fastapi, online inference can be used. If resource pre\-allocation is not required, offline inference can be used.

4. **Training data preparation**: After processing, Lance is used to store the data. In the Dataloader, Lance can use the rowid primary key as shuffle information, which greatly reduces the amount loaded into memory and significantly decreases load time.


```Python
def load_image(ds, idx):
    # Utility function to load an image at an index and convert it from bytes format to img format
    raw_img = ds.take([idx], columns=['image']).to_pydict()
    raw_img = np.frombuffer(b''.join(raw_img['image']), dtype=np.uint8)
    img = cv2.imdecode(raw_img, cv2.IMREAD_COLOR)
    img = cv2.cvtColor(img, cv2.COLOR_RGB2BGR)
    return img

def load_caption(ds, idx):
    # Utility function to load an image's caption. Currently we return the longest caption of all
    captions = ds.take([idx], columns=['captions']).to_pydict()['captions'][0]
    return max(captions, key=len)

class CLIPLanceDataset(Dataset):
    """Custom Dataset to load images and their corresponding captions"""
    def __init__(self, lance_path, max_len=18, tokenizer=None, transforms=None, storage_options=None):
        self.ds = lance.dataset(lance_path, storage_options=storage_options)
        self.max_len = max_len
        # Init a new tokenizer if not specified already
        self.tokenizer = AutoTokenizer.from_pretrained('bert-base-cased') if not tokenizer else tokenizer
        self.transforms = transforms

    def __len__(self):
        return self.ds.count_rows()

    def __getitem__(self, idx):
        # Load the image and caption
        img = load_image(self.ds, idx)
        caption = load_caption(self.ds, idx)

        # Apply transformations to the images
        if self.transforms:
            img = self.transforms(img)

        # Tokenize the caption
        caption = self.tokenizer(
            caption,
            truncation=True,
            padding='max_length',
            max_length=self.max_len,
            return_tensors='pt'
        )
        # Flatten each component of tokenized caption otherwise they will cause size mismatch errors during training
        caption = {k: v.flatten() for k, v in caption.items()}

        return img, caption 
```



5. **Model training**: Ray DDP is used in Ray to transform the original single\-machine multi\-GPU DDP. The code changes are compatible and do not require awareness of the rank.

   1. Advantage: The following can be omitted:

      * Environment initialization

      * DDP model setup

      * Data sharding logic setup

      * Data migration to GPU

   2. Advantage: Ray Data can be used for data loading. This reduces the need for persisting simple data conversions in the last mile.


**Pytorch DDP VS Ray Pytorch DDP example**:

```Python
def train_func(config):
    # Setup distributed env
    dist.init_process_group('nccl')
    rank = os.environ["LOCAL_RANK"]
    device = torch.device("cuda:" + rank)
    
    # Setup DDP model
    model = MyTorchModel(...)
    model = model.to(device)
    model = DDP(model, device_ids=[device])
    
    # Setup distributed sampler
    sampler = DistributedSampler(
        dataset,
        rank=os.environ["RANK"],     num_replicas=os.environ["WORLD_SIZE"],
        shuffle=True,
    )
    dataloader = DataLoader(
       ...,
        sampler=sampler
    )
    
    # Training
    for epoch in range(num_epochs):
        for inputs, labels in dataloader:
            # train batch
            inputs = inputs.to(device)
            labels = labels.to(device)
```


```Python
from ray.train.torch import prepare_model, prepare_data_loader, TorchTrainer

def train_func(config):
    model = MyTorchModel(...)
    model = prepare_model(model)
    dataloader = DataLoader(...)
    dataloader =  prepare_data_loader(dataloader)
    # Training
    for epoch in range(num_epochs):
        for inputs, labels in dataloader:
           ...

from ray.train.torch import TorchTrainer
from ray.train import ScalingConfig
trainer = TorchTrainer(
    train_func,
    scaling_config=ScalingConfig(num_workers=16, use_gpu=True)
)
trainer.fit()
```


**Ray Train + Ray Data example**:

```Python
import ray.data
import ray.train

# Run On GPU
def train_func():
    dataset_shard = ray.train.get_dataset_shard("train")
    dataloader = dataset_shard.iter_torch_batches(...)
   ...
   
scaling_config = ray.train.ScalingConfig(num_workers=4, use_gpu=True)
# Run on CPU Nodes
dataset = ray.data.read_parquet(...).map_batches(...)
trainer = TorchTrainer(
        train_func,
        scaling_config = scaling_config,
        datasets = {"train": dataset},
    )
trainer.fit()
```


<span id="0eadb966"></span>
## Benefits of the new architecture

<span id="98faf0e2"></span>
### Webdataset2Lance

4TB/300CU converted to Lance format, filtering out abnormal images and URLs. Time cost: 1 hour.

<span id="d1f12d27"></span>
### CPU MergeColumns

Add a label using width and height attributes. big_pic(boolean), 4TB/300CU, time cost: 1.5 minutes.

<span id="0a9df0fb"></span>
### Offline inference aesthetics score

Using Ray's distributed architecture for offline inference scoring, transitioning from the original 300CU CPU to a 4\-GPU distributed setup, resulting in a significant performance improvement.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/996ba204c86b485b8fd8c153c5311a17~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3b9d17b3210436383f31a5325e36263~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4923249b9c149feb26349f5e7c4ad9f~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89ab59640ecb4f0b8ea4fa35c9730d23~tplv-goo7wpa0wc-image.image) </span>

<span id="179b9deb"></span>
### Model training


1. DataLoader: Loading 4TB of data in Parquet format takes one hour, whereas Lance requires only a few minutes, and it also allows for adding simple conditional filters.

2. Distributed Train: The single\-machine multiprocessing scenario has been upgraded to multi\-machine concurrent processing. The resource allocation has shifted from an offline fixed resource pool to online pay\-as\-you\-go billing. Training time has been optimized from the original 48 hours to 6 hours.
