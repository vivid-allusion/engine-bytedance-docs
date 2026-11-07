---
title: "Link Training and Evaluation Tasks Through Workflow"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Tandem_training_and_evaluation_tasks_through_workflows"
---

<span id="概述"></span>
# Overview

The workflow module of the machine learning platform supports users to orchestrate multiple custom tasks. Users can use workflow to link model training and model evaluation tasks, provide different computing specifications for each task, and flexibly complete training and evaluation tasks in a single workflow task.

This article introduces a simple training + evaluation workflow demo. This workflow uses the PytorchDDP framework to launch a multi\-machine GPU training task and stores the model files to TOS after training. Then it launches a single\-machine CPU task, reads the trained model files, and evaluates the model performance on the test dataset.

<span id="开发训练与评估代码"></span>
# Develop training and evaluation code

Assume the user has already written the model's training and evaluation code on the development machine or local computer. The following is an example of model training and evaluation code for image classification on the CIFAR dataset, used for the function demonstration below.

```python
import argparse
import torch
import torchvision
import torchvision.transforms as transforms

import torch.nn as nn
import torch.nn.functional as F
import torch.distributed as dist

import torch.optim as optim

transform = transforms.Compose(
    [transforms.ToTensor(),
     transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))])

batch_size = 4

classes = ('plane', 'car', 'bird', 'cat',
           'deer', 'dog', 'frog', 'horse', 'ship', 'truck')


class Net(nn.Module):
    def __init__(self):
        super().__init__()
        self.conv1 = nn.Conv2d(3, 6, 5)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(6, 16, 5)
        self.fc1 = nn.Linear(16 * 5 * 5, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)

    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        x = torch.flatten(x, 1)  # flatten all dimensions except batch
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x


def train(trainloader, epochs, save_path, device):
    print('Running Training')
    net = Net()
    net.to(device)
    criterion = nn.CrossEntropyLoss()
    optimizer = optim.SGD(net.parameters(), lr=0.001, momentum=0.9)

    for epoch in range(epochs):  # loop over the dataset multiple times

        running_loss = 0.0
        for i, data in enumerate(trainloader, 0):
            # get the inputs; data is a list of [inputs, labels]
            inputs, labels = data
            inputs, labels = inputs.to(device), labels.to(device)

            # zero the parameter gradients
            optimizer.zero_grad()

            # forward + backward + optimize
            outputs = net(inputs)
            loss = criterion(outputs, labels)
            loss.backward()
            optimizer.step()

            # print statistics
            running_loss += loss.item()
            if i % 2000 == 1999:  # print every 2000 mini-batches
                print(f'[{epoch + 1}, {i + 1:5d}] loss: {running_loss / 2000:.3f}')
                running_loss = 0.0

    print('Finished Training')
    torch.save(net.state_dict(), save_path)
    print('Model Saved')


def test(testloader, model_path, device):
    print('Running Testing')
    dataiter = iter(testloader)
    images, labels = next(dataiter)
    net = Net()
    net.load_state_dict(torch.load(model_path, map_location=device))
    net.to(device)

    correct = 0
    total = 0
    # since we're not training, we don't need to calculate the gradients for our outputs
    with torch.no_grad():
        for data in testloader:
            images, labels = data
            images, labels = images.to(device), labels.to(device)
            # calculate outputs by running images through the network
            outputs = net(images)
            # the class with the highest energy is what we choose as prediction
            _, predicted = torch.max(outputs.data, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()

    print(f'Accuracy of the network on the 10000 test images: {100 * correct // total} %')


def main():
    parser = argparse.ArgumentParser(description="PyTorch MNIST Example")
    parser.add_argument(
        "--epochs",
        type=int,
        default=10,
        metavar="N",
        help="number of epochs to train (default: 10)",
    )
    parser.add_argument(
        "--model_path",
        type=str,
        help="model path",
        required=True,
    )
    parser.add_argument(
        "--data_path",
        type=str,
        help="data path",
        required=True,
    )
    parser.add_argument(
        "--train",
        action="store_true",
        default=False,
        help="run train func if true",
    )
    parser.add_argument(
        "--test",
        action="store_true",
        default=False,
        help="run test func if true",
    )
    parser.add_argument("--local-rank", default=-1, type=int)
    args = parser.parse_args()

    device = torch.device('cuda:0' if torch.cuda.is_available() else 'cpu')
    print(f"use device={device}, local_rank={args.local_rank}")
    if args.local_rank >= 0:
        torch.cuda.set_device(args.local_rank)
        dist.init_process_group(backend="nccl")

    if args.train:
        trainset = torchvision.datasets.CIFAR10(root=args.data_path, train=True,
                                                download=False, transform=transform)
        trainloader = torch.utils.data.DataLoader(trainset, batch_size=batch_size,
                                                  shuffle=True, num_workers=2)

        train(trainloader, args.epochs, args.model_path, device)
    elif args.test:
        testset = torchvision.datasets.CIFAR10(root=args.data_path, train=False,
                                               download=False, transform=transform)
        testloader = torch.utils.data.DataLoader(testset, batch_size=batch_size,
                                                 shuffle=False, num_workers=2)
        test(testloader, args.model_path, device)
    else:
        print("Either train or test flag must be set")
        exit(1)


if __name__ == "__main__":
    main()
```


<span id="定义工作流"></span>
# Define workflow

Currently, users need to use YAML to define workflow tasks. The following is a workflow demo that chains training and evaluation tasks.


* This workflow has three workflow run inputs: queue name, generated model file name, and number of training epochs. Among them, the number of training epochs specifies a default value of 2.

* This workflow defines 2 custom task templates. `train_task_template` launches two single\-GPU V100 computing nodes, mounts TOS into the task container, uploads local training code files into the container, uses PyTorch for distributed training, and then saves the model file back to TOS. `evaluate_task_template` launches a CPU\-spec computing node, also mounts TOS into the task container, uploads local evaluation code into the container, and evaluates the model file generated by the training task.

* This workflow chains the above two custom tasks, defines dependencies between tasks, and specifies input parameter values for each task.


```yaml
version: v1
kind: PipelineTemplate
inputs:
  - name: queue
    type: string
    hint: queue name
  - name: model_name
    type: string
    hint: model name
  - name: epochs
    type: int
    hint: train epochs
    default_value: 2
task_templates:
  - name: train_task_template
    type: CustomTask
    inputs:
      - name: queue
        type: string
        hint: queue name
      - name: model_name
        type: string
        hint: model name
      - name: epochs
        type: int
        hint: train epochs
    spec:
      Entrypoint: |
        python -m torch.distributed.launch \
        --nproc_per_node $MLP_WORKER_GPU \
        --master_addr $MLP_WORKER_0_HOST \
        --node_rank $MLP_ROLE_INDEX \
        --master_port $MLP_WORKER_0_PORT \
        --nnodes $MLP_WORKER_NUM \
        /root/code/code.py \
        --epochs {{inputs.epochs}} \
        --model_path /data/model/{{inputs.model_name}} \
        --data_path /data/cifar-10-python/ \
        --train
      Framework: PyTorchDDP
      UserCodePath: samples/pipeline/code/cifar_training_and_evaluation_demo/code.py
      RemoteMountCodePath: /root/code
      ImageUrl: vemlp-cn-beijing.cr.volces.com/preset-images/pytorch:2.0.0
      ResourceQueueName: '{{inputs.queue}}'
      Storages:
        - Type: "Tos"
          MountPath: "/data"                                      # Mount Directory in the Container
          Bucket: "pipeline-demo"                                 # To-be-mounted TOS Bucket
          Prefix: "/"                                             # Directory Path under the To-be-mounted TOS Bucket
      TaskRoleSpecs:
        - Flavor: ml.g1v.2xlarge
          RoleName: worker
          RoleReplicas: 2
  - name: evaluate_task_template
    type: CustomTask
    inputs:
      - name: queue
        type: string
        hint: queue message 
      - name: model_name
        type: string
        hint: model name
    spec:
      Entrypoint: |
        python /root/code/code.py \
        --model_path /data/model/{{inputs.model_name}} \
        --data_path /data/cifar-10-python/ \
        --test
      Framework: Custom
      ImageUrl: vemlp-cn-beijing.cr.volces.com/preset-images/pytorch:2.0.0
      ResourceQueueName: '{{inputs.queue}}'
      UserCodePath: samples/pipeline/code/cifar_training_and_evaluation_demo/code.py
      RemoteMountCodePath: /root/code
      Storages:
        - Type: "Tos"
          MountPath: "/data"                                      # Mount Directory in the Container
          Bucket: "pipeline-demo"                                 # To-be-mounted TOS Bucket
          Prefix: "/"                                             # Directory Path under the To-be-mounted TOS Bucket
      TaskRoleSpecs:
        - Flavor: ml.g1ie.4xlarge
          RoleName: worker
          RoleReplicas: 1
tasks:
  - name: train_task
    task_template_name: train_task_template
    inputs:
      - name: queue
        value: '{{pipeline.inputs.queue}}'
      - name: model_name
        value: '{{pipeline.inputs.model_name}}'
      - name: epochs
        value: '{{pipeline.inputs.epochs}}'
  - name: evaluate_task
    task_template_name: evaluate_task_template
    inputs:
      - name: queue
        value: '{{pipeline.inputs.queue}}'
      - name: model_name
        value: '{{pipeline.inputs.model_name}}'
    dependencies:
      - train_task
```


<span id="运行工作流"></span>
# Run workflow

Users can create and run workflows in the console, and can track the workflow's running information on the frontend after submitting the workflow.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1eeca119f7464219881f5daceddb736c~tplv-goo7wpa0wc-image.image) </span>

Clicking "Run process (table) \- Subtask name" navigates to the custom task details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abaea031228748129373033cc9a8e93f~tplv-goo7wpa0wc-image.image) </span>

Clicking `Log` on the task node navigates to the log page to view training and evaluation results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e72c760b9930494c9275a2beffe50545~tplv-goo7wpa0wc-image.image) </span>

After a workflow is created, users can run it directly on the workflow details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1865138125048e484fd1631fbed5925~tplv-goo7wpa0wc-image.image) </span>
