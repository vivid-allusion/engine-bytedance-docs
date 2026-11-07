---
title: "Isaac simulation environment tutorial"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Isaac"
---

<span id="7e9c9b0a"></span>
# Objective overview

By reading this documentation, you will be able to:


1. Understand Isaac Sim

2. Start Isaac Streaming visualization and use 3D assets to build environments

3. Use Isaac Sim's core functionality Replicator to randomize environments

4. Use visualization to validate results


<span id="1965509e"></span>
# Background

Isaac Sim is an open\-source reference application built on NVIDIA Omniverse, enabling developers to simulate and test AI\-driven robotics development solutions in physics\-based virtual environments. Users can build their own custom simulators based on the universal scene description (OpenUSD), or integrate core Isaac Sim technologies into existing testing and validation workflows.

IsaacSim provides three main usage modes: deployment on workstations equipped with GPUs and monitors, deployment on headless servers with streaming to terminals equipped with monitors, and fully on headless servers (pure Python environment, no GUI). The first two modes are suitable for interactive modeling and rendering, while the last is suitable for large\-scale data synthesis and training.

<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71695ea138b24c3bb58869db974ae8d1~tplv-goo7wpa0wc-image.image" controls></video>


<span id="procedure"></span>
# **Procedure**

<span id="6ed94028"></span>
## Connect the development machine to Isaac Streaming

<span id="22bea72a"></span>
### API gateway and security group configuration

After creating resource groups and queues, API gateway and security group configuration is required to connect to Isaac Streaming.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please refer to the following rules to check and configure Isaac visualization features.</div>



1. <div data-tips="true" data-tips-type="tip">Check the global configuration for the private network VPC, select the dedicated gateway for the API gateway; check the network mode of the resource group, select dedicated network + VPC interconnection.</div>


2. <div data-tips="true" data-tips-type="tip">The version number of the API gateway instance must be ≥ 3.1.0, <a href="https://docs.byteplus.com/en/docs/apig/Version_Management">upgrade documentation</a>.</div>


3. <div data-tips="true" data-tips-type="tip">The maximum number of API gateway consumers is 100, <a href="https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=apig">quota application link</a>.</div>


1. Create [API gateway](https://console.byteplus.com/veapig/region:veapig+ap-southeast-1/gateways) (skip this step if already created)

> This bandwidth will be used for Isaac visualization network connections; it is recommended to set according to requirements. Default 1080p 60FPS video quality; 15 Mbps is recommended.


2. In the left navigation bar of the machine learning platform, select "Global settings", enter the private network where the development machine is located, edit the network VPC authorization, select "Public network configuration" as `Allow public network access`; "Public network type" as `Exclusive network`; and set "API gateway" to the existing API gateway.

3. Configure security groups: In the left navigation bar of the private network, select "Security Group", then select the security group corresponding to the development machine's private network or create a security group. Go to "Access Rules" in "Security Group" and set the listening port according to the Isaac version.



|Description |protocol type |version:port |
|---|---|---|
|Isaac visualization command |TCP |4.5:49100<br><br>5.0:49100<br><br>5.1:49100 |
|Isaac visualization media |UDP |4.5:1024<br><br>5.0:47998<br><br>5.1:47998 |


<span id="c99c23c9"></span>
### Start Isaac Streaming

Use the development machine in BytePlus to connect to Isaac Streaming.


1. Turn on Isaac visualization in the development machine settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fec7c8f81e249599f13b48919dece14~tplv-goo7wpa0wc-image.image) </span>


2. Log in to WebIDE and start the following command to remotely display streaming visualization in Isaac Streaming.


```Bash
# Navigate to the directory where isaac-sim.streaming.sh is located
cd /workspace/isaaclab/_isaac_sim && ./isaac-sim.streaming.sh --allow-root
```



3. Click "Connect to Isaac via public network" to access Isaac Streaming.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efceea6cb2a749e4855e3d0df35d96ad~tplv-goo7wpa0wc-image.image) </span>

<span id="5f32c240"></span>
## Build a simulation environment

By using existing 3D assets from BytePlus, you can build a personalized simulation environment.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b5fbe6da6e54e529c95b0ac5832fd63~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<div style="text-align: center">
P1\-Scene setup example\-Warehouse (Warehouse)</div>


As shown in the figure above, drag the `Assets/ArchVis/Industrial/Stages/IsaacWarehouse.usd` asset to build a warehouse.

<span id="c5a75d86"></span>
### 3D asset directory

The asset location is shown in P2 below. The 3D cloud assets are located at `https://omniverse-content-staging.s3.us-west-2.amazonaws.com/`. You can directly view the assets, drag and load them into the scene.

At the same time, BytePlus comes with tens of thousands of assets (P3). In the Content panel, you can see the asset directory of downloaded assets located at `/preset-datasets/robotics/omniverse-content-production/`, and its structure is the same as that of AWS cloud assets (P2). AWS resources need to be downloaded. It is recommended to search only in the NVIDIA Assets and Isaac Assets (Beta) panels, and directly load resources from the Content panel.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6484a2d7551147e09634576125bf6b13~tplv-goo7wpa0wc-image.image" width="630px" /></div>


<div style="text-align: center">
P2\-Asset location\-NVIDIA</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ab352a8a0d04d339aeef3f83d83f62d~tplv-goo7wpa0wc-image.image" width="638px" /></div>


<div style="text-align: center">
P3\-Asset location\-preset\-datasets</div>


<span id="bc5a3af4"></span>
## Replicator environment randomization

Using the built\-in Replicator enables environment randomization. Replicator can randomize properties including but not limited to an object's **material, color, size, position, angle, camera angle**.

Click Isaac's Window\-\>Script Editor to bring up the code editor interface. You can directly write code in external .py files.

Write a Python script and call Replicator using `rep.create.` Create objects that can be generated by replication, or add semantic tags to existing assets. Obtain Prim objects via `rep.get.prims(semantics=[...])`. You can refer to the Nvidia documentation [Omniverse Replicator](https://docs.omniverse.nvidia.com/extensions/latest/ext_replicator/basic_functionalities.html).

The figure below (P4) shows a scene built with Replicator. The main subject is a coffee table. When running the script, the position and angle of the book on the left, the size of the plate, the direction of the foreground light source, and the color of the background light will change; the camera angle can also change.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eef2c5f8bce74e45b448285ba905fd60~tplv-goo7wpa0wc-image.image" width="592px" /></div>


<div style="text-align: center">
P4\-Replicator example\-CoffeeTable</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db0dce81880e46e5b4630bd379ecafc8~tplv-goo7wpa0wc-image.image" width="2110px" /></div>


<div style="text-align: center">
P5\-Background light with a reddish tint</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65708169811046ebb53299c8db444a08~tplv-goo7wpa0wc-image.image" width="2250px" /></div>


<div style="text-align: center">
P7\-Different camera angles\-1</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba0bc05f5c1e4fd9b53e474fdc7e116a~tplv-goo7wpa0wc-image.image" width="2248px" /></div>


<div style="text-align: center">
P6\-Background light with a greenish tint</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb751e46f0c84e3e8edeb9487faac603~tplv-goo7wpa0wc-image.image" width="2246px" /></div>


<div style="text-align: center">
P8\-Different camera angles\-2</div>


<span id="4c461dd7"></span>
## Effect validation

<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c92e7ee5271b469ebbc6aef4d2a16bea~tplv-goo7wpa0wc-image.image" controls></video>


<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f5182f72248442397e10243f0653772~tplv-goo7wpa0wc-image.image" controls></video>


<div style="text-align: center">
V3\-Camera roaming on Isaac Streaming</div>


<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b7e1dd3068d4416942d5fe6951cbbe8~tplv-goo7wpa0wc-image.image" controls></video>


<div style="text-align: center">
V4\-Camera roaming on RDP</div>


Using assets provided by BytePlus, Isaac Sim physical simulation rendering environments can be quickly built to perform large\-scale physical simulation data synthesis, providing large\-scale data for embodied intelligence training and boosting the efficiency of large model development. At the same time, Nvidia officially provides richer tutorials and use cases. With these resources, quick implementation can also be performed on machine learning platforms.
