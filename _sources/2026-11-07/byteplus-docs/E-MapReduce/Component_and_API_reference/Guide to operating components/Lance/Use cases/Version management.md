---
title: "Version management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Version_management"
---

<span id="239da94d"></span>
## Scenario description

During model training, it is often necessary to adjust the data content to optimize model performance, such as applying different cropping methods to images in the field of computer vision.

Each data processing operation generates a data version. Since data transformations may not always improve performance, historical versions are retained; at the same time, model training often requires reviewing previous results, so all data versions need to be preserved throughout the data processing steps.

<span id="f0630b0c"></span>
## Current solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68ee930c1eac43288e399f7796099e4a~tplv-goo7wpa0wc-image.image) </span>

The current solution typically uses dataset copies to record different changes. For example, in the scenario above:


1. First, the preprocessed training data is placed into dataset 1, and then training is started based on dataset 1, and the model is trained.

2. If the model does not perform well, some data in dataset 1 is corrected and saved as dataset 2, and model 2 is trained on dataset 2.

3. By comparing the results of model 1 and model 2, if model 2 performs worse, dataset 2 and model 2 are discarded. Then, other correction methods are retried on dataset 1, and model 3 is trained again.

4. After comparing the results, if model 3 performs better, dataset 3 is retained. To preserve the record of data operations, the data in dataset 1 is also retained.


<span id="f5ef20a2"></span>
## Lance solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/143abedbf853494b9ec6315e84e55f10~tplv-goo7wpa0wc-image.image) </span>

Lance is a data lake architecture that manages data using versioning:


1. After data is imported, this becomes the initial version in Lance, and this version is used to train the model.

2. After certain changes, version 2 is created. If the training results are not satisfactory, Lance can directly roll back to version 1.

3. Then, further data changes can be made on version 1 to create version 3.

4. Lance will always retain all versions, including not only version 1 and version 3, but also version 2.


<span id="ff18148f"></span>
## Solution comparison


|**Dimension** |**Current solution** |**Lance solution** |
|---|---|---|
|Data management |Managed by different file paths and names |Managed through versioning |
|Data storage |Ultimately stores three full copies of the data |Only one copy of the data |
|Data operations |Read and write all data |Only process changed data |
|Data rollback |Relying on human memory |Manage through version rollback capability |


<span id="42c538d4"></span>
## Code example

```Python
df = pd.DataFrame({"a": [10]})
tbl = pa.Table.from_pandas(df)
## Create the first version
dataset = lance.write_dataset(tbl, "/tmp/test.lance")

## Create the second version
dataset = lance.write_dataset(parquet, "/tmp/test.lance", mode="append")

## List all versions of the dataset
dataset.versions()


## Read the first version
ds = lance.dataset('/tmp/test.lance', version=1).to_table().to_pandas()

## Read the second version
ds = lance.dataset('/tmp/test.lance', version=2).to_table().to_pandas()

## Switch the dataset of version 2 back to version 1
ds = ds.checkout_version(1)

## Rolling back the dataset to version 1 actually creates version 3, but its content is the same as version 1
ds.restore()
```
