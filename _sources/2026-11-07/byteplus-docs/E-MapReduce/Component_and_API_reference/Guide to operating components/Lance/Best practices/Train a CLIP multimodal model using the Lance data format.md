---
title: "Train a CLIP multimodal model using the Lance data format"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Train_a_CLIP_multimodal_model_using_the_Lance_data_format"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document is based on the official Lance example and demonstrates an example of Lance ON TOS. For local examples, refer to the official documentation: <a href="https://lancedb.github.io/lance/examples/flickr8k_dataset_creation.html">数据准备</a>, <a href="https://lancedb.github.io/lance/examples/clip_training.html">模型训练</a>.</div>


<span id="ada0e7b4"></span>
## Prepare the Lance dataset

<span id="cfa58427"></span>
### Download the data and extract the dataset

```Bash
wget https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_Dataset.zip
wget https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_text.zip
unzip Flickr8k_text.zip
unzip Flickr8k_Dataset.zip
```


<span id="dcf113fc"></span>
### Python operations

```Python
import os
import cv2
import random

import lance
import pyarrow as pa

import matplotlib.pyplot as plt

from tqdm.auto import tqdm

captions = "Flickr8k.token.txt"
image_folder = "Flicker8k_Dataset/"

with open(captions, "r") as fl:
    annotations = fl.readlines()

# Converts the annotations where each element of this list is a tuple consisting of image file name, caption number and caption itself
annotations = list(map(lambda x: tuple([*x.split('\t')[0].split('#'), x.split('\t')[1]]), annotations))

captions = []
image_ids = set(ann[0] for ann in annotations)
for img_id in tqdm(image_ids):
    current_img_captions = []
    for ann_img_id, num, caption in annotations:
        if img_id == ann_img_id:
            current_img_captions.append((num, caption))

    # Sort by the annotation number
    current_img_captions.sort(key=lambda x: x[0])
    captions.append((img_id, tuple([x[1] for x in current_img_captions])))

def process(captions):
    for img_id, img_captions in tqdm(captions):
        try:
            with open(os.path.join(image_folder, img_id), 'rb') as im:
                binary_im = im.read()

        except FileNotFoundError:
            print(f"img_id '{img_id}' not found in the folder, skipping.")
            continue

        img_id = pa.array([img_id], type=pa.string())
        img = pa.array([binary_im], type=pa.binary())
        capt = pa.array([img_captions], pa.list_(pa.string(), -1))

        yield pa.RecordBatch.from_arrays(
            [img_id, img, capt],
            ["image_id", "image", "captions"]
        )

schema = pa.schema([
    pa.field("image_id", pa.string()),
    pa.field("image", pa.binary()),
    pa.field("captions", pa.list_(pa.string(), -1)),
])


reader = pa.RecordBatchReader.from_batches(schema, process(captions))
lance.write_dataset(reader, "flickr8k.lance", schema)
```


To store the data on TOS, modify `lance.write_dataset(reader, "flickr8k.lance", schema)` to the following code.

```Python
storage_options={
        "access_key_id": "<用户实际的AK>",
        "secret_access_key": "<用户实际的SK>",
        "aws_endpoint": "https://bucket1.tos-s3-cn-shanghai.ivolces.com",
        "virtual_hosted_style_request": "true"
    }

lance.write_dataset(reader, "s3://{PATH}/flickr8k.lance", schema, storage_options=storage_options)
```


For parameter descriptions of object storage, refer to [使用Lance Python SDK访问TOS上的Lance数据](https://www.volcengine.com/docs/6491/1359395).

<span id="bb1f0f9c"></span>
## Train the CLIP model

```Python
import cv2
import lance

import numpy as np

import torch
import torch.nn as nn
import torch.nn.functional as F
from torch.utils.data import Dataset, DataLoader
from torchvision import transforms

import timm
from transformers import AutoModel, AutoTokenizer

import itertools
from tqdm import tqdm

import warnings
warnings.simplefilter('ignore')

class Config:
    img_size = (128, 128)
    bs = 32
    head_lr = 1e-3
    img_enc_lr = 1e-4
    text_enc_lr = 1e-5
    max_len = 18
    img_embed_dim = 2048
    text_embed_dim = 768
    projection_dim = 256
    temperature = 1.0
    num_epochs = 2
    img_encoder_model = 'resnet50'
    text_encoder_model = 'bert-base-cased'



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

train_augments = transforms.Compose(
    [
        transforms.ToTensor(),
        transforms.Resize(Config.img_size),
        transforms.Normalize([0.5], [0.5]),
    ]
)


class ImageEncoder(nn.Module):
    """Encodes the Image"""
    def __init__(self, model_name, pretrained = True):
        super().__init__()
        self.backbone = timm.create_model(
            model_name,
            pretrained=pretrained,
            num_classes=0,
            global_pool="avg"
        )

        for param in self.backbone.parameters():
            param.requires_grad = True

    def forward(self, img):
        return self.backbone(img)

class TextEncoder(nn.Module):
    """Encodes the Caption"""
    def __init__(self, model_name):
        super().__init__()

        self.backbone = AutoModel.from_pretrained(model_name)

        for param in self.backbone.parameters():
            param.requires_grad = True

    def forward(self, captions):
        output = self.backbone(**captions)
        return output.last_hidden_state[:, 0, :]

class Head(nn.Module):
    """Projects both into Embedding space"""
    def __init__(self, embedding_dim, projection_dim):
        super().__init__()
        self.projection = nn.Linear(embedding_dim, projection_dim)
        self.gelu = nn.GELU()
        self.fc = nn.Linear(projection_dim, projection_dim)

        self.dropout = nn.Dropout(0.3)
        self.layer_norm = nn.LayerNorm(projection_dim)

    def forward(self, x):
        projected = self.projection(x)
        x = self.gelu(projected)
        x = self.fc(x)
        x = self.dropout(x)
        x += projected

        return self.layer_norm(x)

def loss_fn(img_embed, text_embed, temperature=0.2):
    """
    https://arxiv.org/abs/2103.00020/
    """
    # Calculate logits, image similarity and text similarity
    logits = (text_embed @ img_embed.T) / temperature
    img_sim = img_embed @ img_embed.T
    text_sim = text_embed @ text_embed.T
    # Calculate targets by taking the softmax of the similarities
    targets = F.softmax(
        (img_sim + text_sim) / 2 * temperature, dim=-1
    )
    img_loss = (-targets.T * nn.LogSoftmax(dim=-1)(logits.T)).sum(1)
    text_loss = (-targets * nn.LogSoftmax(dim=-1)(logits)).sum(1)
    return (img_loss + text_loss) / 2.0

def forward(img, caption):
    # Transfer to device
    img = img.to('cuda')
    for k, v in caption.items():
        caption[k] = v.to('cuda')

    # Get embeddings for both img and caption
    img_embed = img_head(img_encoder(img))
    text_embed = text_head(text_encoder(caption))

    return img_embed, text_embed


# Define image encoder, image head, text encoder, text head and a tokenizer for tokenizing the caption
img_encoder = ImageEncoder(model_name=Config.img_encoder_model).to('cuda')
img_head = Head(Config.img_embed_dim, Config.projection_dim).to('cuda')

tokenizer = AutoTokenizer.from_pretrained(Config.text_encoder_model)
text_encoder = TextEncoder(model_name=Config.text_encoder_model).to('cuda')
text_head = Head(Config.text_embed_dim, Config.projection_dim).to('cuda')

# Since we our optimizing two different models together, we will define parameters manually
parameters = [
    {"params": img_encoder.parameters(), "lr": Config.img_enc_lr},
    {"params": text_encoder.parameters(), "lr": Config.text_enc_lr},
    {
        "params": itertools.chain(
            img_head.parameters(),
            text_head.parameters(),
        ),
        "lr": Config.head_lr,
    },
]

optimizer = torch.optim.Adam(parameters)


# We assume the flickr8k.lance dataset is in the same directory
dataset = CLIPLanceDataset(
    lance_path="flickr8k.lance",
    max_len=Config.max_len,
    tokenizer=tokenizer,
    transforms=train_augments,
)

dataloader = DataLoader(
    dataset,
    shuffle=False,
    batch_size=Config.bs,
    pin_memory=True
)

img_encoder.train()
img_head.train()
text_encoder.train()
text_head.train()

for epoch in range(Config.num_epochs):
    print(f"{'='*20} Epoch: {epoch+1} / {Config.num_epochs} {'='*20}")

    prog_bar = tqdm(dataloader)
    for img, caption in prog_bar:
        optimizer.zero_grad(set_to_none=True)

        img_embed, text_embed = forward(img, caption)
        loss = loss_fn(img_embed, text_embed, temperature=Config.temperature).mean()

        loss.backward()
        optimizer.step()

        prog_bar.set_description(f"loss: {loss.item():.4f}")
    print()
```


For tasks accessing object storage, replace `dataset = CLIPLanceDataset( lance_path="flickr8k.lance", max_len=Config.max_len, tokenizer=tokenizer, transforms=train_augments, )` with the following code.

```Python
storage_options={
    "access_key_id": "<用户实际的AK>",
    "secret_access_key": "<用户实际的SK>",
    "aws_endpoint": "https://bucket1.tos-s3-cn-shanghai.ivolces.com",
    "virtual_hosted_style_request": "true"
}

dataset = CLIPLanceDataset(
    lance_path="s3://{PATH}/flickr8k.lance",
    max_len=Config.max_len,
    tokenizer=tokenizer,
    transforms=train_augments,
    storage_options=storage_options,
)
```
