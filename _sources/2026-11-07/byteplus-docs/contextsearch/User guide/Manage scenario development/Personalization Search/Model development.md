---
title: "Model development"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Model_development"
---

In personalization search scenarios, after you import a dataset, you can perform feature engineering and sample engineering on it to develop models. This topic describes how to develop models.

## Prerequisites

* A personalization search scenario has been created. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario).

* Data has been imported. For more information, see [Import data](https://docs.byteplus.com/en/docs/contextsearch/Import_data).

## Create a development task

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) Icon on the top\-right corner on the target personalized search and recommendation scenario page, then select the **Model dDevelopment** tab.

5. In the **Development task** section, click **Create**.

6. In the new model development task dialog, enter the task name and click **Create**.

   > **tip**

   > Task name rules are as follows:

   * > Cannot start with a number or a hyphen (\-).

   * > Length must be between 1 and 128 characters.

   * > Contain letters, digits, underscores (_), and hyphens (\-).

## Develop model

1. In the created development task, click **Dataset**, then select the added dataset from the dropdown list.

   > **tip**

   * > You can preview data in the dataset in the **Item data preview** area.

   * > To add a new dataset, click **Add dataset**. For detailed steps, see [Add dataset](https://docs.byteplus.com/en/docs/contextsearch/Add_a_dataset).

2. In the created development task, click **Feature processing**, check the fields to use in the **Whether to adopt** column of each table, and configure the **Feature type**.

   > **tip**

   > The feature types of fields are as follows:

   * > Sparse features: non\-continuous features such as String or non\-numeric fields, names, or properties.

   * > Dense features: continuously varying features that must be numeric fields, such as price or visit count.

   * > Variable\-length sparse features: lists of sparse features, for example, the list of interacted items `item_id_list`.

   * > Variable\-length dense features: lists of dense features, such as the list of prices of interacted items `item_price_list`.

   > Note that fields like `id` are sparse features because they do not vary continuously; for example, `id=3` does not represent a specific number, `id=3` is not greater than `id=2`. Only numeric values that can be compared, like prices, can serve as dense features.

3. In the created development task, click **Sample project**, then configure the following parameters.

   |Parameter |Description |
   |---|---|
   |Positive sample |The expected values that meet the demand output can be represented by the same field indicating whether the expectation is met, for example, `clicked=0/1` indicates whether the user clicked the item, and `purchase=0/1` indicates whether the item was purchased. |
   |Positive sample ratio |Enter the proportion of positive samples, unit: % |
   |Fields |Select the field used to split the dataset from the dropdown list. |
   |ratio |Set the ratio of training, validation, and test sets. The total ratio equals 10. |

4. In the created development task, click **Model training**, then configure the following parameters.

   |Parameter |Description |
   |---|---|
   |Model type |Currently fixed to **recall + fine ranking**. |
   |Recall model algorithm |**DSSM ** is a fixed option. DSSM (Deep Structured Semantic Model) is a deep learning model used to learn the semantic matching relationship between two types of objects, such as users and items, or queries and documents. You can click **Hyperparameter configuration** to configure the algorithm’s hyperparameters. For details, see [DSSM hyperparameters](https://docs.byteplus.com/en/docs/contextsearch/Model_development#rjCElXIP).<br><br>You can also click **Add** and then select other models from the dropdown list. |
   |ranking model algorithm |Currently supports only DeepFM. DeepFM (Deep Factorization Machine) is a recommendation model that learns both low\-order feature combinations and high\-order feature interactions. You can click **Hyperparameter configuration** to configure algorithm hyperparameters. For details, see [DeepFM hyperparameters](https://docs.byteplus.com/en/docs/contextsearch/Model_development#qpt7K3jp). |

5. In the created development task, click **Model evaluation**, then configure the following parameters.

   |Parameter |Description |
   |---|---|
   |Enable deployment access control |Select whether to turn on deployment access control. Once turned on, tasks that do not meet the metric rules cannot be deployed. |
   |Recall model metric |Configure deployment access for the recall model. You can click **Add indicator rule** to configure multiple rules. Rules within the same stage are effective under an AND relationship.<br><br>> **tip**<br><br><br>> This parameter is only visible when deployment access is turned on.<br> |
   |Refined model metrics |Set deployment access control for the refined model. You can click **Add indicator rule** to configure multiple rules. Rules within the same stage take effect with AND logic.<br><br>> **tip**<br><br><br>> This parameter is visible only when deployment access control is enabled.<br> |

6. In the created development task, click **Model inference deployment**, then configure the following parameters.

   |Parameter |Description |
   |---|---|
   |Tag (optional) |Add tags to model services for easier identification and management. You can click **Add tag** multiple times to add multiple tags, up to 20 tags in total. |
   |Scenario resources ||
   |Resource type |Currently, only **CPU** is supported. |
   |Specification |Select the specification of the scenario resource from the dropdown list. |
   |Quantity |Set the quantity of scenario resources. Selectable quantity range: 1–200. |
   |Inference resource ||
   |Resource type |Currently, only **GPU** is supported. |
   |Specification |Select the specification of the inference resource from the dropdown list. |
   |Quantity |Set the quantity of inference resources. The selectable quantity is limited by the remaining stock of the chosen specification. |
   |Access point rate limiting |Turn on to set rate limiting for each access point. |
   |RPM |Turning on access point rate limiting requires configuring RPM (Requests Per Minute), which is the number of requests processed per minute. |
   |User\-defined parameter (optional) |Supports configuring user\-defined parameters for inference services. Click **Add custom parameters**, then configure the parameter name and value. |
   |Cache acceleration |Select whether to enable cache acceleration. |
   |Redis instance |Select the Redis instance used for cache acceleration from the dropdown list.<br><br>> **tip**<br><br><br><br>* > This parameter is only visible when **Cache acceleration** is turned on.<br><br><br>* > To create a new Redis instance, see [Create an instance](https://docs.byteplus.com/en/docs/redis/create-instance).<br><br><br>* > For more information about Redis instances, see [What is Cache for Redis](https://docs.byteplus.com/en/docs/redis/about-redis).<br> |
   |User name |Enter the username of the Redis instance.<br><br>> **tip**<br><br><br>> This parameter is only visible when **Cache acceleration** is turned on.<br> |
   |Password |Enter the password for the Redis instance.<br><br>> **tip**<br><br><br>> This parameter is only visible when **Cache acceleration** is turned on.<br> |
   |Adjust grayscale traffic |Set the proportion of grayscale traffic for each stage. You can click **Add stage** to perform multi\-stage grayscale upgrade. The flow rate at each stage must be strictly incremented, ranging from 1% to 99%; the final 100% is completed by the system. |
   |Minimum observation time per phase |During phased rollout, each traffic stage runs and is observed for the specified duration before progressing to the next stage. |
   |Deployment failure retry interval |Set the wait time before the system automatically retries after a deployment failure. |
   |Maximum online error rate |Set the maximum allowed online error rate for each grayscale stage. Value range: 0–1. |
   |Online indicator wait timeout |Set the maximum wait time after deployment for online monitoring metrics to appear. If timed out without metrics, handle according to the strategy below. |
   |Online indicator timeout handling |Set the action the system takes after the online indicator wait timeout. Valid values: **Auto rollback** or **Pend and wait for manual processing**. |

### DSSM hyperparameters

|Parameter |Type |Required |Description |
|---|---|---|---|
|batch_size |INTEGER |Yes |Data for each training batch. |
|dropout |FLOAT |Yes |Dropout rate to prevent overfitting (default value means randomly dropping 10% of neurons). |
|early_stop_patience |INTEGER |Yes |Early stopping patience: The default value means training stops if there is no improvement in validation metrics for 5 consecutive epochs. |
|embedding_dim |INTEGER |Yes |Embedding vector dimension for categorical features. |
|epochs |INTEGER |Yes |Training epochs. |
|fe_block_layer_dim |INTEGER |Yes |Hidden layer dimension of the feature extraction module (FE Block). |
|full_reg |BOOLEAN |Yes |Enable full regularization. |
|item_head |INTEGER |Yes |Number of output heads for the item tower. |
|learning_rate |FLOAT |Yes |learning rate. |
|seed |INTEGER |Yes |Random seed to ensure experiment reproducibility. |
|sparse |BOOLEAN |Yes |Enable sparse training? |
|tau |FLOAT |Yes |Temperature coefficient used for similarity scaling in contrastive learning / two\-tower matching. |
|user_head |INTEGER |Yes |The number of output heads in the user tower. |

### DeepFM hyperparameters

|Parameter |Type |Required |Description |
|---|---|---|---|
|adagrad |BOOLEAN |Yes |Enable AdaGrad optimizer. |
|batch_size |INTEGER |Yes |Data for each training batch. |
|dcn_low_rank_dim |INTEGER |Yes |DCN low\-rank decomposition dimension, used to reduce the number of parameters in the crossing layer. |
|dcn_num_layers |INTEGER |Yes |DCN (Deep & Cross Network) cross layer quantity: 3 layers. |
|embedding_dim |INTEGER |Yes |Embedding vector dimension for categorical features. |
|epochs |INTEGER |Yes |Number of training epochs. |
|learning_rate |FLOAT |Yes |learning rate. |
|lr_decay_start |INTEGER |Yes |Step to start learning rate decay (0 means no decay). |
|lr_decay_steps |INTEGER |Yes |Total number of steps for learning rate decay (0 means no decay). |
|lr_warmup_steps |INTEGER |Yes |Learning rate warm\-up steps (0 means no warm\-up). |
|pin_memory |BOOLEAN |Yes |Enable pinned memory (accelerates GPU data transfer, specific to PyTorch). |

## Run task

1. Click **Run** at the top right corner of the development task.

2. In the run task dialog, configure the following parameters, then click **Submit**.

   |Parameter |Description |
   |---|---|
   |Resource type |Currently fixed to **GPU**. |
   |Specification |Select the resource specification from the dropdown list. |
   |Quantity |Select resource quantity. |
   |Dispatch |Select the running mode. Valid values:<br><br><br>* Run once: run immediately once.<br><br>* Hourly: run once at the specified minute every hour within the specified date range.<br><br>* Daily: run once at the specified time every day within the specified date range. |

   > **tip**

   * > Resources used for running tasks are billed based on actual usage. Please refer to the bill for detailed charges.

## Subsequent operations

### View logs

After the task runs, you can view the running logs to understand the model’s running state and locate issues.

1. Click **Running history** at the top right corner of the page.

2. In the **Task running history** panel, click **Logs** to the right of the desired running record.

3. On the log query page, select filter criteria such as log level, start and end time, file type, and keywords; the system will automatically filter and display matching logs in the list below.

> **tip**

> The system saves logs for a maximum of 7 days.

### Model evaluation

After the task starts running, you can click **Run history** to view the task status. For example, you can view model evaluation after completing model training.

1. In the **Run history** panel, click **Configuration information** next to the target run record.

2. In the pop\-up window, select the **Model evaluation** tab.

3. On the **Model evaluation** tab, view the recall training model metrics and re\-ranking model training metrics for the running tasks.
