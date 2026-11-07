---
title: "Enable autoscaling capability for KubeRay clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Enable_autoscaling_capability_for_KubeRay_clusters"
---

Automatic cluster scaling can be achieved by configuring the Ray Autoscaler. The Autoscaler adjusts the number of nodes (Ray Pods) in the cluster based on the resources required by tasks, actors, or placement groups. The Autoscaler uses logical resource requests (expressed as ray.remote), rather than physical resource utilization, to scale the cluster.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Autoscaler can reduce workload costs, but increases node startup overhead.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed0ebee3873c443bf1da99b0b6978f8e.png) </span>

The Ray Autoscaler operates as a separate entity within a sidecar container in the Ray head Pod.

<span id="ray-cluster方式使用指导"></span>
## Ray cluster mode usage guide


1. Enable scaling functionality


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5b289759584d37cfd912f1130c36835c.png) </span>


2. Start a job and configure 8 workers


```python
import os
from typing import Dict

from ray.runtime_env import RuntimeEnv
import torch
from filelock import FileLock
from torch import nn
from torch.utils.data import DataLoader
from torchvision import datasets, transforms
from torchvision.transforms import Normalize, ToTensor
from tqdm import tqdm

import ray.train
from ray.train import ScalingConfig
from ray.train.torch import TorchTrainer


def get_dataloaders(batch_size):
    # Transform to normalize the input images
    transform = transforms.Compose([ToTensor(), Normalize((0.5,), (0.5,))])

    with FileLock(os.path.expanduser("~/data.lock")):
        # Download training data from open datasets
        training_data = datasets.FashionMNIST(
            root="~/data",
            train=True,
            download=True,
            transform=transform,
        )

        # Download test data from open datasets
        test_data = datasets.FashionMNIST(
            root="~/data",
            train=False,
            download=True,
            transform=transform,
        )

    # Create data loaders
    train_dataloader = DataLoader(training_data, batch_size=batch_size)
    test_dataloader = DataLoader(test_data, batch_size=batch_size)

    return train_dataloader, test_dataloader


# Model Definition
class NeuralNetwork(nn.Module):
    def __init__(self):
        super(NeuralNetwork, self).__init__()
        self.flatten = nn.Flatten()
        self.linear_relu_stack = nn.Sequential(
            nn.Linear(28 * 28, 512),
            nn.ReLU(),
            nn.Dropout(0.25),
            nn.Linear(512, 512),
            nn.ReLU(),
            nn.Dropout(0.25),
            nn.Linear(512, 10),
            nn.ReLU(),
        )

    def forward(self, x):
        x = self.flatten(x)
        logits = self.linear_relu_stack(x)
        return logits


def train_func_per_worker(config: Dict):
    lr = config["lr"]
    epochs = config["epochs"]
    batch_size = config["batch_size_per_worker"]

    # Get dataloaders inside the worker training function
    train_dataloader, test_dataloader = get_dataloaders(batch_size=batch_size)

    # [1] Prepare Dataloader for distributed training
    # Shard the datasets among workers and move batches to the correct device
    # =======================================================================
    train_dataloader = ray.train.torch.prepare_data_loader(train_dataloader)
    test_dataloader = ray.train.torch.prepare_data_loader(test_dataloader)

    model = NeuralNetwork()

    # [2] Prepare and wrap your model with DistributedDataParallel
    # Move the model to the correct GPU/CPU device
    # ============================================================
    model = ray.train.torch.prepare_model(model)

    loss_fn = nn.CrossEntropyLoss()
    optimizer = torch.optim.SGD(model.parameters(), lr=lr, momentum=0.9)

    # Model training loop
    for epoch in range(epochs):
        model.train()
        for X, y in tqdm(train_dataloader, desc=f"Train Epoch {epoch}"):
            pred = model(X)
            loss = loss_fn(pred, y)

            optimizer.zero_grad()
            loss.backward()
            optimizer.step()

        model.eval()
        test_loss, num_correct, num_total = 0, 0, 0
        with torch.no_grad():
            for X, y in tqdm(test_dataloader, desc=f"Test Epoch {epoch}"):
                pred = model(X)
                loss = loss_fn(pred, y)

                test_loss += loss.item()
                num_total += y.shape[0]
                num_correct += (pred.argmax(1) == y).sum().item()

        test_loss /= len(test_dataloader)
        accuracy = num_correct / num_total

        # [3] Report metrics to Ray Train
        # ===============================
        ray.train.report(metrics={"loss": test_loss, "accuracy": accuracy})


def train_fashion_mnist(num_workers=2, use_gpu=False):
    global_batch_size = 32

    train_config = {
        "lr": 1e-3,
        "epochs": 10,
        "batch_size_per_worker": global_batch_size // num_workers,
    }

    # Configure computation resources
    scaling_config = ScalingConfig(num_workers=num_workers, use_gpu=use_gpu)

    # Initialize a Ray TorchTrainer
    trainer = TorchTrainer(
        train_loop_per_worker=train_func_per_worker,
        train_loop_config=train_config,
        scaling_config=scaling_config,
    )

    # [4] Start distributed training
    # Run `train_func_per_worker` on all workers
    # =============================================
    result = trainer.fit()
    print(f"Training result: {result}")


if __name__ == "__main__":
    #rv = RuntimeEnv(pip={"packages":["torch", "torchvision", "requests"], "pip_check": False})
    #ray.init( runtime_env=rv)
    train_fashion_mnist(num_workers=8, use_gpu=False)
```



3. Check the number of workers


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5e37e6ee538f55e3335da12ba00fe2a5.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2bcd1e1fe955f9faa0fb91c767ec9575.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03be09b004a6e2455ef7e086813a1b8d.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because the Autoscaler exists as a sidecar container in the Ray head Pod, after modifying enable_in_tree_autoscaling on the EMR management page and clicking the restart operation, the management system will delete and recreate the head pod of the ray cluster. Therefore, it is recommended to modify this parameter when there are no jobs running.</div>


<span id="ray-job方式使用指南"></span>
## Ray job mode usage guide

Define a YAML file for the job and enable the Autoscaler functionality in the YAML file

```python
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
spec:
  entrypoint: python /home/ray/samples/sample_code.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 300

  # RuntimeEnvYAML represents the runtime environment configuration provided as a multi-line YAML string.
  # See https://docs.ray.io/en/latest/ray-core/handling-dependencies.html for details.
  # (New in KubeRay version 1.0.)
  runtimeEnvYAML: |
    pip:
      - requests==2.26.0
      - pendulum==2.1.2
    env_vars:
      counter_name: "test_counter"


  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.7.0' # should match the Ray version in the image of the containers
    enableInTreeAutoscaling: true
    # Ray head pod template
    headGroupSpec:
      # The `rayStartParams` are used to configure the `ray start` command.
      # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
      # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
      rayStartParams:
        dashboard-host: '0.0.0.0'
      #pod template
      template:
        spec:
          containers:
            - name: ray-head
              image: emr-cn-beijing.cr.volces.com/huleilei/ray:2.9.1
              ports:
                - containerPort: 6379
                  name: gcs-server
                - containerPort: 8265 # Ray dashboard
                  name: dashboard
                - containerPort: 10001
                  name: client
              resources:
                limits:
                  cpu: "1"
                requests:
                  cpu: "200m"
              volumeMounts:
                - mountPath: /home/ray/samples
                  name: code-sample
          volumes:
            # You set volumes at the Pod level, then mount them into containers inside that Pod
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 30
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            containers:
              - name: ray-worker # must consist of lower case alphanumeric characters or '-', and must start and end with an alphanumeric character (e.g. 'my-name',  or '123-abc'
                image: emr-cn-beijing.cr.volces.com/huleilei/ray:2.9.1
                lifecycle:
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                  requests:
                    cpu: "200m"

######################Ray code sample#################################
# this sample is from https://docs.ray.io/en/latest/cluster/job-submission.html#quick-start-example
# it is mounted into the container and executed to show the Ray job at work
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import os
    from typing import Dict

    import torch
    from filelock import FileLock
    from torch import nn
    from torch.utils.data import DataLoader
    from torchvision import datasets, transforms
    from torchvision.transforms import Normalize, ToTensor
    from tqdm import tqdm

    import ray.train
    from ray.train import ScalingConfig
    from ray.train.torch import TorchTrainer


    def get_dataloaders(batch_size):
        # Transform to normalize the input images
        transform = transforms.Compose([ToTensor(), Normalize((0.5,), (0.5,))])

        with FileLock(os.path.expanduser("~/data.lock")):
            # Download training data from open datasets
            training_data = datasets.FashionMNIST(
                root="~/data",
                train=True,
                download=True,
                transform=transform,
            )

            # Download test data from open datasets
            test_data = datasets.FashionMNIST(
                root="~/data",
                train=False,
                download=True,
                transform=transform,
            )

        # Create data loaders
        train_dataloader = DataLoader(training_data, batch_size=batch_size)
        test_dataloader = DataLoader(test_data, batch_size=batch_size)

        return train_dataloader, test_dataloader


    # Model Definition
    class NeuralNetwork(nn.Module):
        def __init__(self):
            super(NeuralNetwork, self).__init__()
            self.flatten = nn.Flatten()
            self.linear_relu_stack = nn.Sequential(
                nn.Linear(28 * 28, 512),
                nn.ReLU(),
                nn.Dropout(0.25),
                nn.Linear(512, 512),
                nn.ReLU(),
                nn.Dropout(0.25),
                nn.Linear(512, 10),
                nn.ReLU(),
            )

        def forward(self, x):
            x = self.flatten(x)
            logits = self.linear_relu_stack(x)
            return logits


    def train_func_per_worker(config: Dict):
        lr = config["lr"]
        epochs = config["epochs"]
        batch_size = config["batch_size_per_worker"]

        # Get dataloaders inside the worker training function
        train_dataloader, test_dataloader = get_dataloaders(batch_size=batch_size)

        # [1] Prepare Dataloader for distributed training
        # Shard the datasets among workers and move batches to the correct device
        # =======================================================================
        train_dataloader = ray.train.torch.prepare_data_loader(train_dataloader)
        test_dataloader = ray.train.torch.prepare_data_loader(test_dataloader)

        model = NeuralNetwork()

        # [2] Prepare and wrap your model with DistributedDataParallel
        # Move the model to the correct GPU/CPU device
        # ============================================================
        model = ray.train.torch.prepare_model(model)

        loss_fn = nn.CrossEntropyLoss()
        optimizer = torch.optim.SGD(model.parameters(), lr=lr, momentum=0.9)

        # Model training loop
        for epoch in range(epochs):
            model.train()
            for X, y in tqdm(train_dataloader, desc=f"Train Epoch {epoch}"):
                pred = model(X)
                loss = loss_fn(pred, y)

                optimizer.zero_grad()
                loss.backward()
                optimizer.step()

            model.eval()
            test_loss, num_correct, num_total = 0, 0, 0
            with torch.no_grad():
                for X, y in tqdm(test_dataloader, desc=f"Test Epoch {epoch}"):
                    pred = model(X)
                    loss = loss_fn(pred, y)

                    test_loss += loss.item()
                    num_total += y.shape[0]
                    num_correct += (pred.argmax(1) == y).sum().item()

            test_loss /= len(test_dataloader)
            accuracy = num_correct / num_total

            # [3] Report metrics to Ray Train
            # ===============================
            ray.train.report(metrics={"loss": test_loss, "accuracy": accuracy})


    def train_fashion_mnist(num_workers=2, use_gpu=False):
        global_batch_size = 32

        train_config = {
            "lr": 1e-3,
            "epochs": 10,
            "batch_size_per_worker": global_batch_size // num_workers,
        }

        # Configure computation resources
        scaling_config = ScalingConfig(num_workers=num_workers, use_gpu=use_gpu)

        # Initialize a Ray TorchTrainer
        trainer = TorchTrainer(
            train_loop_per_worker=train_func_per_worker,
            train_loop_config=train_config,
            scaling_config=scaling_config,
        )

        # [4] Start distributed training
        # Run `train_func_per_worker` on all workers
        # =============================================
        result = trainer.fit()
        print(f"Training result: {result}")


    if __name__ == "__main__":
        #train_fashion_mnist(num_workers=8, use_gpu=False)
        #ray.init(runtime_env={"pip":["torch","torchvision", "torchaudio"]})
        train_fashion_mnist(num_workers=8, use_gpu=False)
```


In this example, 1 worker is started by default, but the task requires 8 workers. Therefore, as the task load increases, workers are dynamically added, as can be seen from the following logs:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fb8fafe1f619b9368efb0a6f2cdc3fe.png) </span>
