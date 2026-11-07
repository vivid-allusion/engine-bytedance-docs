---
title: "Basic Concept"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Basic-Concept"
---

<span id="一-初阶"></span>
# Beginner

<span id="_1-ab实验"></span>
## 1. AB testing, experimental group, control group


|**Related concepts** |**Concept introduction** |
|---|---|
|**AB testing** |The basic idea of A/B experiment is to take **a small part** of the online traffic (lower risk), completely **randomly** divide it into the original strategy A and the new strategy B (excluding interference), and then combine certain **statistical methods** to obtain an accurate estimate of the relative effect of the two strategies (quantitative results).<br><br>This set of experimental methods based on small samples is A/B experiments, also known as " **controlled experiment" or "small traffic randomized experiment"** , while meeting the requirements of **low risk**, **anti\-interference** and **quantified results**, so it is widely used in both Internet Product Research & Development and scientific research.<br><br>For more AB testing application scenarios, please refer to [What is A/B Testing?](https://docs.byteplus.com/docs/DataTester/What-is-A-B-Testing). |
|**Experimental group, control group** |Experimental group and control group are relative concepts, and A/B experiments are usually conducted to verify the effectiveness of a new strategy. Suppose that in the experiment, the selected users are randomly assigned to groups A and B, group A users experience the new policy in the product, and group B users experience the old policy in the experiment. During this experiment, group A was the experimental group, and group B was the control group. |


<span id="1e02e3be"></span>
## 2. Client side experiment, server side experiment


|**Comparison description** |**Client side experiment** |**Server side experiment** |
|---|---|---|
|**Experimental description** |Refers to the experiment that obtains the experimental grouping information through the client side and controls the configuration to take effect. |Refers to the experiment that obtains the experimental packet information through the server side and controls the configuration to take effect or issue. |
|**Features and Scenarios** |* Features: When the APP is evoked, the AB related configuration needs to take effect immediately<br><br>* Scene:<br><br><br>Required to start the exposure of the scene, for example, we want to open the APP screen page for A/B experiments, the user has just opened the APP, the client side needs to show the user the screen interface. In this case, the client side may not have time to request configuration parameters from the server side. |* Features: The hit and exposure logic is handled at the server side, and the experimental configuration takes effect when the APP is not required to be evoked. The client side has enough time to make a request to the server side, obtain the experimental configuration, and then present the policy to the user.<br><br>* Scene:<br><br>   * Recommended policy, pure server side configuration experiment, usually uid shunting, does not require the APP to be invoked to make the experimental configuration take effect.<br><br>   * Some functions can only be controlled by the server side, such as information delivery algorithms (such as what users will see in the feed stream after opening Jinri Toutiao), product functions controlled by server side logic (such as push), etc. |


<span id="6127e5e5"></span>
## 3. Experimental traffic and traffic allocation


* In the Internet industry's A/B experiments, traffic is often used to describe the overall number of users a product has.

* When opening A/B experiments, they are generally tested for a small amount of traffic. After seeing the effect of a certain experimental group, they will test the large traffic and finally roll out 100%.


When distributing experimental traffic to AB testing, it is necessary to estimate the appropriate traffic data in combination with experimental objectives, experimental calibration sensitivity, etc. You can use the traffic calculator to estimate, please refer to the details [Traffic Calculator](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator).

<span id="c3d0dd32"></span>
## 4. Experimental traffic layer: mutual exclusion experiment, traffic orthogonal

The following is an introduction to the basic concepts of mutual exclusion experiments and traffic orthogonality. Please refer to more application scenarios and configuration operation instructions [Traffic Layer and Mutual Exclusion Domain](https://docs.byteplus.com/docs/DataTester/Traffic-Layer-and-Mutual-Exclusion-Domain).


* Mutual exclusion experiment


Mutual exclusion experiment means that all experiments in the mutual exclusion group do not share users. In multiple experiments in the same traffic layer, the traffic can only hit one of them, that is, the traffic of the same layer experiment is mutually exclusive. If a user/device hits Experiment A, it will not hit the other experiments in the mutual exclusion group.

Basic principle: Experiments with the same or related content that may affect each other are recommended to be added to the same mutual exclusion group. For example, if you want to experiment with button color and button shape simultaneously, you need to add the two experiments to a mutual exclusion group.

> If there are now four experiments to be conducted, each experiment requires 30% of the traffic to produce reliable experimental results. In order to run these four experiments simultaneously, 4 \* 30% = 120% of the traffic is required, which means that 100% of the traffic is not enough to be allocated to these four experiments simultaneously.

> So at this point, we can only choose to sort the experiments and let several experiments be completed one after the other, but this will cause the experimental efficiency to be low.

> Experimental layer technology can perfectly solve this problem.

> The experimental layer technology is a traffic stratification technology developed to enable multiple experiments to be parallel without interfering with each other, and to obtain enough traffic.

> We "replicate" the overall traffic countless times to form countless traffic layers, so that the overall traffic can be reused countless times, thus improving experimental efficiency. The traffic between the layers is orthogonal, which can be simply understood as: under the premise of selecting the correct traffic layer, the traffic is scientifically allocated to ensure that the results of each experiment will not be disturbed by experiments at other layers.


* Orthogonal experiment


Mutual exclusion group = mutual exclusion layer = experimental layer

Each independent experiment is a layer, and when a traffic passes through each layer of the experiment, it will be randomly broken up and reassembled to ensure that the amount of traffic in each layer is the same.

**How to understand traffic orthogonality?** 

> Let me give you an example. Suppose I have two experiments now. Experiment A (experimental group labeled A1, control group labeled A2) is distributed in experimental layer 1 and takes 100% of the traffic of this layer; Experiment B (experimental group labeled B1, control group labeled B2) is distributed in experimental layer 2 and also takes 100% of the traffic of this layer. (Note that Experimental Layer 1 and Experimental Layer 2 are actually the same batch of users, and Experimental Layer 2 simply reuses the traffic of Experimental Layer 1.)

> If you divide the traffic of group A1 into two halves, one into group B1 and one into group B2, then divide the traffic of group A2 into two halves, one into group B1 and one into group B2. Then the call to traffic for the two experiments will be as shown in the figure below. At this point, between Experiment A and Experiment B, a **traffic "orthogonal" is formed**.


<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3MDVweCIgaGVpZ2h0PSIzNTVweCIgdmlld0JveD0iLTAuNSAtMC41IDcwNSAzNTUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDIyNyAyNjEuNSBMIDIxNyAyNjEuNSBMIDIxNyAyMDYuNSBMIDIwNi41IDIwNi41IEwgMjIyIDE4Ny41IEwgMjM3LjUgMjA2LjUgTCAyMjcgMjA2LjUgWiIgZmlsbD0iIzk5MDAwMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTgyIiB5PSI1NyIgd2lkdGg9IjM0MCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2NjY2NjYyIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTgyIiB5PSIxNTciIHdpZHRoPSIzNDAiIGhlaWdodD0iMzAiIGZpbGw9IiNjY2NjY2MiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE4MiIgeT0iNTciIHdpZHRoPSIxNzAiIGhlaWdodD0iMzAiIGZpbGw9IiMwMDMzNjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjI2MiIgeT0iMTU3IiB3aWR0aD0iOTAiIGhlaWdodD0iMzAiIGZpbGw9IiMwMDMzNjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQzMiIgeT0iMTU3IiB3aWR0aD0iOTAiIGhlaWdodD0iMzAiIGZpbGw9IiMwMDMzNjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDQ3IC0zOCBMIDQyNyAtMzggTCA0MjcgMTIwIEwgNDQ3IDEyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgdHJhbnNmb3JtPSJyb3RhdGUoOTAsNDM3LDQxKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjc3IC0zOCBMIDI1NyAtMzggTCAyNTcgMTIwIEwgMjc3IDEyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgdHJhbnNmb3JtPSJyb3RhdGUoOTAsMjY3LDQxKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDQ2IDEyMSBMIDQyNiAxMjEgTCA0MjYgMjc5IEwgNDQ2IDI3OSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgdHJhbnNmb3JtPSJyb3RhdGUoLTkwLDQzNiwyMDApIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNzcgMTIwIEwgMjU3IDEyMCBMIDI1NyAyODAgTCAyNzcgMjgwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiB0cmFuc2Zvcm09InJvdGF0ZSgtOTAsMjY3LDIwMCkiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDIyNC41IDg3IEwgMzAyLjE0IDE1Mi44OCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMwNi4xNSAxNTYuMjggTCAyOTguNTUgMTU0LjQyIEwgMzAyLjE0IDE1Mi44OCBMIDMwMy4wNyAxNDkuMDggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ4My45MiA4Ny45OSBMIDM5OS4yMSAxNTMuMTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzOTUuMDUgMTU2LjMyIEwgMzk4LjQ2IDE0OS4yOCBMIDM5OS4yMSAxNTMuMTIgTCA0MDIuNzMgMTU0LjgzIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMzIgODcgTCA0NzAuODggMTU1LjI1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDc1LjkzIDE1Ni42OSBMIDQ2OC4yMyAxNTguMTQgTCA0NzAuODggMTU1LjI1IEwgNDcwLjE2IDE1MS40IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0ODYuOTggODkuMDEgTCAyMjguMTcgMTU1LjQyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjIzLjA4IDE1Ni43MiBMIDIyOC45OSAxNTEuNTkgTCAyMjguMTcgMTU1LjQyIEwgMjMwLjczIDE1OC4zNyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE4MiIgeT0iMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTJweDsgbWFyZ2luLWxlZnQ6IDE4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FeHBlcmltZW50YWwgZ3JvdXAgQTE8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjY3IDIyIEwgMjY3IDIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjY3IDIyIEwgMjY3IDIyIEwgMjY3IDIyIEwgMjY3IDIyIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzUxIiB5PSIyIiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMnB4OyBtYXJnaW4tbGVmdDogMzUycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkV4cGVyaW1lbnRhbCBncm91cCBBMjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iNjIiIHdpZHRoPSIxNzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDcycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FeHBlcmltZW50YWwgbGF5ZXIgMTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iMTY3IiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNzdweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkV4cGVyaW1lbnRhbCBsYXllciAyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxODEiIHk9IjIxMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjIycHg7IG1hcmdpbi1sZWZ0OiAxODJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RXhwZXJpbWVudGFsIGdyb3VwIEIxPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI2NiAyMzIgTCAyNjYgMjMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjY2IDIzMiBMIDI2NiAyMzIgTCAyNjYgMjMyIEwgMjY2IDIzMiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM1MiIgeT0iMjEyIiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMjJweDsgbWFyZ2luLWxlZnQ6IDM1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FeHBlcmltZW50YWwgZ3JvdXAgQjI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE4MiIgeT0iMjYyIiB3aWR0aD0iMzQwIiBoZWlnaHQ9IjkwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMzM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzA3cHg7IG1hcmdpbi1sZWZ0OiAxODRweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogbGVmdDsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTVweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICM5OTAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSBpbXBhY3Qgb2YgRXhwZXJpbWVudCBBIG9uIEV4cGVyaW1lbnQgQiBpcyBldmVubHkgZGlzcGVyc2VkIGFuZCBkaXN0cmlidXRlZCBiZXR3ZWVuIHRoZSB0d28gZ3JvdXBzIG9mIEV4cGVyaW1lbnQgQi4gQXQgdGhpcyBwb2ludCwgdGhlIGluZGljYXRvcnMgb2YgR3JvdXAgQjEgaGF2ZSBpbmNyZWFzZWQsIGFuZCBpdCBubyBsb25nZXIgaGFzIGFueXRoaW5nIHRvIGRvIHdpdGggQSAuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1NDIiIHk9IjEwNyIgd2lkdGg9IjE2MCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDE1OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogNTQ0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGxlZnQ7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjOTkwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48YiBzdHlsZT0iZm9udC1zaXplOjE2cHgiPlRyYWZmaWM8L2I+wqA8Yj5pczwvYj7CoDxiIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWw7Zm9udC1zaXplOjE2cHgiPm9ydGhvZ29uYWw8YnIgc3R5bGU9ImZvbnQtc2l6ZToxNnB4IiAvPjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" />

**What is the significance of traffic orthogonality?** 

We can see that because half of the traffic in group A1 is in B1 and the other half in B2, even if A1's policy affects experiment B, the impact is evenly distributed between the two groups of experiment B.

In this case, if the metric of group B1 rises, then it can be ruled out that B1 is influenced by A1 to form an increase. This is the meaning of traffic orthogonality.

<span id="38dc3b84"></span>
## 5. Experiment duration/test period

The duration of the experiment, also known as the test period, refers to the duration of the experiment. Generally, in order to avoid differences in user behavior during different time periods (weekdays and weekends), it is recommended to observe at least two complete test periods.

For example, when considering the impact of weekdays and weekends, the test period takes at least one week, and the recommended duration of the experiment is 14 days.

Determining the testing schedule for an AB experiment requires considering several factors, including the purpose of the experiment, audience behavior patterns, business requirements, and so on. Here are some common considerations:


* Objective of the experiment: To clarify what the main objective of the experiment is. If you are testing for short\-term effects, the testing schedule can be shorter; if you are evaluating long\-term effects, it may take longer to observe.

* Audience behavior patterns: Consider the audience's behavior and reaction time. For example, if it's an online advertising experiment, you might want to observe users' clicks, conversions, and other behaviors over a period of days or weeks.

* Business requirements: Determine the test period based on the time sensitivity and resource constraints of the business. If it is a seasonal event or limited promotion period, the testing schedule may need to match.

* Statistical significance: Typically, the test period should be long enough to ensure that enough data is collected to achieve statistical significance. This can be calculated based on the expected effect size, sample size, and confidence level.

* Speed of change: The test period can be shorter if you expect the effect to appear quickly; if the effect takes longer to appear, a longer test period may be required.


In general, the period of AB experiments can range from a few days to several months. When determining the test period, the above factors can be comprehensively considered and adjusted according to the actual situation. Also, during the experiment, data and effects are closely monitored in order to make timely decisions and make possible adjustments.

<span id="9589cb00"></span>
## 6. Experimental parameters

When running an experiment, you need an identifier to distinguish the control group from the experimental group, and we use parameters to solve the problem of identification. In the experiment of A/B testing, each control group and experimental group can have one parameter or multiple parameters, each parameter will have parameter types (currently, String, Number, Boolean are supported), and each parameter will also have parameter values.


* For example, for the registered copy experiment, we can create a String type parameter (name as: register_name), the control group parameter value is "one\-click registration", and the experimental group parameter value is "immediate registration".


See more configuration instructions for experimental parameters [How to Configure Experimental Parameters](https://docs.byteplus.com/docs/DataTester/How-to-Configure-Experimental-Parameters).

<span id="011cc1ce"></span>
## 7. Experimental metrics


* Experimental metrics

   When conducting an experiment, the purpose is to compare one or more metrics of the control group and the experimental group. For example, when analyzing the number of clicks on the button, you need to report the click event of the registration button, and then configure the metric on the "A/B Test" product.

   DataTester recommends that you plan and set AB testing experimental metrics from the business goals, and provides you with optimization planning functions to assist you in better planning and setting experimental metrics.

* Common metric: WAU

   WAU (Weekly Active Users), Weekly Active Users, the number of users who started using the product in the last week (7 days including of the day), is generally calculated according to the natural week.

* Common metric: MAU

   MAU (Monthly Active Users), the number of monthly active users, the number of users who started using the product in the last month (30 days including of the day), generally calculated according to the natural month.


<span id="f69580c8"></span>
## 8. Experimental debugging, whitelist users

Before the experiment is officially launched, it is usually necessary to select a few users to enter the testing phase (experimental debugging) to observe whether the experiment can normally obtain the data to be collected, or whether there are bugs on the client side. Users who participate in this step are called "whitelist users".

For more introduction and configuration instructions for whitelist users, see [User Testing Whitelist](https://docs.byteplus.com/docs/DataTester/User-Testing-Whitelist).

<span id="72cef1b5"></span>
## 9. Experimental report and experimental result data


* Variance and standard deviation

   * Variance: Variance is the average of the squares of the distance between each data value and the center value in the data set.

> Formula for calculating variance: In the formula, x is the average of the data, N is the number of data, and s ² is the variance.

> <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8efc37a9f1d23266901e956ec978251e.png) </span>


* Standard deviation: The standard deviation is the square root of the variance, i.e. s.


<span id="ab52bea0"></span>
# Intermediate

<span id="485fea3e"></span>
## DataTester Product Function Logic

<span id="fa44e7e8"></span>
### A/B testing distribution service, vid

To set up an A/B experiment, as the name implies, we need at least one group A and one group B. So what exactly determines which users are hit by the experiment and which users enter the group A/B? It relies on A/B experimental streaming services.


* The streaming service will help the experimenter to extract part of the traffic from the overall traffic and randomly assign the extracted traffic into groups A and B to minimize sampling error.

* It is important to note that when the offloading service is completed, the user selected to enter the experiment will be given an "identity information" \- ab_version (also known as vid), which indicates which group of the experiment the traffic should go to.


<span id="ee739ecc"></span>
### Distribution principle: input & output of distribution service

The task of the distribution service is to randomly sample the users and evenly distribute them to the experimental group and the control group, so that they can take effect different functions.

Let's start by thinking of triage services as a "black box". That is to say, regardless of the specific processes and logic involved in the distribution service, consider the distribution service as a whole. Then, we explain its working principle through input and output.


* Input: The business side makes a request to the distribution service, telling the distribution service who the user is

* Output: The triage service returns whether the user on the business side hit the experiment and which experiment group the user was assigned to.


In the simplest and most colloquial terms: **In an experiment, we make a request to the streaming service, telling the streaming service who the user is, and then the streaming service will tell us whether the user has been hit by the experiment and which group the user has been assigned to**.


* **Offload service input**

   When we make a request to the streaming service, the information we want to tell the streaming service is called "**request parameters**". The information contained in it is: **who the user is (the user's shunt id [decisionID]), where the user is from (appkey), and what conditions the user meets (filter)** .

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>decisionID:</strong> shunt id, it needs to be a unique identifier id, you can use uuid, did. In the course of the experiment, it is necessary for the business side to decide by itself what id to use to label the user in combination with the experimental scenario.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">\*\*appkey: \*\*The unique identifier of the application. The appkey in the request parameter marks which application the user comes from.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">\*\*filter: \*\*It is actually a filter condition. When setting up an experiment, the experimenter may add some restrictions to the traffic entering the experiment, stipulating that the users hit by the experiment must meet (or not meet) these conditions, so as to achieve the purpose of narrowing the client base and accurately finding users. This restriction is the filter. When making a request to the streaming service, the user information must contain attribute information corresponding to the filter conditions. For example, in one experiment, the experimenter stipulated that the user who was hit by the experiment must be a Beijing user. Then when making a request, if the request information does not contain the user's location information/the location information is not for Beijing, the user will be filtered out and cannot be hit by the experiment.   </div>
   

   With this information, the triage service has "raw materials" and processes them internally to triage users.

* **Distribution service output**

   If a user is hit by an experiment, the streaming service will output the user's identity information **vid (ab_version)/vid list** (a user may hit multiple experiments at different layers at the same time, so it will output vid list) and the corresponding **experiment configuration** of the user. If the user is not hit by the experiment, the streaming service will not output any information.


<span id="b0f59a4a"></span>
### Distribution principle: web\-traffic bucketing

When the streaming service distributes traffic, it first distributes the traffic of each layer into 1,000 copies, each of which is called a "hash bucket". Why is it called a "hash bucket"? When a user enters the experimental layer, the streaming service assigns the user to a bucket through a "hash function" and a "modulo operation".

> "Hash": Hash, generally translated as hash, hash, transliterated as hash. The hash function can transform an input of any length into a fixed\-length output through a hashing algorithm, which is the hash value. Let's explain this in human language. In the streaming service, we combine the user's uid/did and the name of the user's experimental layer to calculate the hash value. For example, according to the experiment layer of the did shunt, the distribution service will use "did: layer_name" as the input value, and after hashing, it will obtain a fixed\-length "value string".

> "Modulo": a Mod b, which represents the remainder of a divided by b. The remainder of a divided by b has a total of b values of 0, 1, 2, 3... (b\-1), so the modulo function is often used to allocate a data set into b parts. In the shunting principle, we divide the traffic into 1000 parts, so we modulo the output of the hash function by 1000, so that the uid/did that has been broken up by the hash function can be randomly assigned to these 1000 traffic buckets.

> The purpose of hashing and modulo is to enable users to be randomly and evenly assigned to the 1000 buckets we divide, and to ensure that they are assigned to the same bucket every time.


After processing the streaming service, we threw all the users into the bucket, so each of these 1000 buckets has 0.1% of the traffic. When different experiments on the same layer call traffic, they will randomly receive different numbers of buckets according to the percentage of traffic required by the experiment (and the buckets do not overlap).

Suppose the experiment I set up calls 2% of the traffic, then I will receive 20 buckets. If a user entering the experimental layer falls into these 20 buckets, then that user will proceed to the next traffic screening step; if not in these 20 buckets, the user will not be hit by the experiment.

<span id="348f8b7e"></span>
### Diversion principle: web\-traffic layering

In order to ensure the large\-scale reuse of traffic, the core idea is to layer traffic into multiple experimental layers (mutual exclusion groups), and maintain the following properties:

&nbsp;

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI2OTVweCIgaGVpZ2h0PSIzNTVweCIgdmlld0JveD0iLTAuNSAtMC41IDY5NSAzNTUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDIyNyAyNjEuNSBMIDIxNyAyNjEuNSBMIDIxNyAyMDYuNSBMIDIwNi41IDIwNi41IEwgMjIyIDE4Ny41IEwgMjM3LjUgMjA2LjUgTCAyMjcgMjA2LjUgWiIgZmlsbD0iIzk5MDAwMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTgyIiB5PSI1NyIgd2lkdGg9IjM0MCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2NjY2NjYyIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTgyIiB5PSIxNTciIHdpZHRoPSIzNDAiIGhlaWdodD0iMzAiIGZpbGw9IiNjY2NjY2MiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE4MiIgeT0iNTciIHdpZHRoPSIxNzAiIGhlaWdodD0iMzAiIGZpbGw9IiMwMDMzNjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjI2MiIgeT0iMTU3IiB3aWR0aD0iOTAiIGhlaWdodD0iMzAiIGZpbGw9IiMwMDMzNjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQzMiIgeT0iMTU3IiB3aWR0aD0iOTAiIGhlaWdodD0iMzAiIGZpbGw9IiMwMDMzNjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDQ3IC0zOCBMIDQyNyAtMzggTCA0MjcgMTIwIEwgNDQ3IDEyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgdHJhbnNmb3JtPSJyb3RhdGUoOTAsNDM3LDQxKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjc3IC0zOCBMIDI1NyAtMzggTCAyNTcgMTIwIEwgMjc3IDEyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgdHJhbnNmb3JtPSJyb3RhdGUoOTAsMjY3LDQxKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDQ2IDEyMSBMIDQyNiAxMjEgTCA0MjYgMjc5IEwgNDQ2IDI3OSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgdHJhbnNmb3JtPSJyb3RhdGUoLTkwLDQzNiwyMDApIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNzcgMTIwIEwgMjU3IDEyMCBMIDI1NyAyODAgTCAyNzcgMjgwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiB0cmFuc2Zvcm09InJvdGF0ZSgtOTAsMjY3LDIwMCkiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDIyNC41IDg3IEwgMzAyLjE0IDE1Mi44OCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMwNi4xNSAxNTYuMjggTCAyOTguNTUgMTU0LjQyIEwgMzAyLjE0IDE1Mi44OCBMIDMwMy4wNyAxNDkuMDggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ4My45MiA4Ny45OSBMIDM5OS4yMSAxNTMuMTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzOTUuMDUgMTU2LjMyIEwgMzk4LjQ2IDE0OS4yOCBMIDM5OS4yMSAxNTMuMTIgTCA0MDIuNzMgMTU0LjgzIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMzIgODcgTCA0NzAuODggMTU1LjI1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDc1LjkzIDE1Ni42OSBMIDQ2OC4yMyAxNTguMTQgTCA0NzAuODggMTU1LjI1IEwgNDcwLjE2IDE1MS40IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0ODYuOTggODkuMDEgTCAyMjguMTcgMTU1LjQyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjIzLjA4IDE1Ni43MiBMIDIyOC45OSAxNTEuNTkgTCAyMjguMTcgMTU1LjQyIEwgMjMwLjczIDE1OC4zNyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE4MiIgeT0iMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTJweDsgbWFyZ2luLWxlZnQ6IDE4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FeHBlcmltZW50YWwgZ3JvdXAgQTE8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjY3IDIyIEwgMjY3IDIyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjY3IDIyIEwgMjY3IDIyIEwgMjY3IDIyIEwgMjY3IDIyIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzUxIiB5PSIyIiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMnB4OyBtYXJnaW4tbGVmdDogMzUycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkV4cGVyaW1lbnRhbCBncm91cCBBMjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iNjIiIHdpZHRoPSIxNzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDcycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FeHBlcmltZW50YWwgbGF5ZXIgMTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iMTY3IiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNzdweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkV4cGVyaW1lbnRhbCBsYXllciAyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxODEiIHk9IjIxMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjIycHg7IG1hcmdpbi1sZWZ0OiAxODJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RXhwZXJpbWVudGFsIGdyb3VwIEIxPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI2NiAyMzIgTCAyNjYgMjMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjY2IDIzMiBMIDI2NiAyMzIgTCAyNjYgMjMyIEwgMjY2IDIzMiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM1MiIgeT0iMjEyIiB3aWR0aD0iMTcwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMjJweDsgbWFyZ2luLWxlZnQ6IDM1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FeHBlcmltZW50YWwgZ3JvdXAgQjI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE4MiIgeT0iMjYyIiB3aWR0aD0iMzQwIiBoZWlnaHQ9IjkwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMzM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzA3cHg7IG1hcmdpbi1sZWZ0OiAxODRweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogbGVmdDsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTVweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICM5OTAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSBpbXBhY3Qgb2YgRXhwZXJpbWVudCBBIG9uIEV4cGVyaW1lbnQgQiBpcyBldmVubHkgZGlzcGVyc2VkIGFuZCBkaXN0cmlidXRlZCBiZXR3ZWVuIHRoZSB0d28gZ3JvdXBzIG9mIEV4cGVyaW1lbnQgQi4gQXQgdGhpcyBwb2ludCwgdGhlIGluZGljYXRvcnMgb2YgR3JvdXAgQjEgaGF2ZSBpbmNyZWFzZWQsIGFuZCBpdCBubyBsb25nZXIgaGFzIGFueXRoaW5nIHRvIGRvIHdpdGggQSAuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1NDIiIHk9IjEwNyIgd2lkdGg9IjE1MCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDE0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogNTQ0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGxlZnQ7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjOTkwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48YiBzdHlsZT0iZm9udC1zaXplOjE2cHgiPlRyYWZmaWM8L2I+wqA8YiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsO2ZvbnQtc2l6ZToxNnB4Ij5vcnRob2dvbmFsaXR5PGJyIHN0eWxlPSJmb250LXNpemU6MTZweCIgLz48L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" />


* **Mutual exclusion:**  mutual exclusion within the experimental layer, that is, in multiple experiments in the same traffic layer, the traffic can only hit one of them.

* **Orthogonality:**  The experimental layer is orthogonal in pairs, that is, the experiments opened in different experimental layers are independent of each other, and the traffic is randomly hit.

* **Stability:**  The experimental hit is stable, that is, the same traffic passes through the distribution service twice, and the experimental hit situation remains consistent.


<span id="a141fd4d"></span>
### Diversion principle: Enter one group and not enter another group

Basic concept:


* Entering a group: A user hits a version of an experiment and is called entering the experimental version.

* Out of group: The user hits a version in the experiment, and will not hit the version in the experiment in the future.

* Skip group: The user hits one version of the experiment and another version of the experiment at another moment.

* Enter one group and not enter another group (experience consistency): If a user hits one version of the experiment, they will not hit another version of the experiment.

   When creating an experiment, you can set whether you need to turn on the switch of experience consistency.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e59e165160d402aaca781d40f47260f~tplv-goo7wpa0wc-image.image) </span>

* Traffic: is the ratio of the traffic entering the experiment configured by the customer.


Frequently Asked Questions \- Skip Groups Appear:


* Skip group: The same user hits experimental group A first, and is diverted to experimental group B again

* Possible reasons: The traffic allocation between the experimental versions was modified/the total traffic of the experiment was reduced

* Solution: During the operation of the experiment, the user binds the first shunt into the group information, and the subsequent shunt will keep the incoming group information unchanged.

* Implementation method:

   * The client side experiment uses the SDK to cache. After calling the distribution service, the incoming group information is cached on the end side. Subsequent calls to the distribution service will carry the cached incoming group information

   * The server side experiment needs to rely on external storage. After integrating the server side SDK, the query and save interfaces are realized, and the user entry information is cached through external storage


<span id="e614b9ce"></span>
### Diversion principle: Diversion traffic chart

After understanding the inputs and outputs of the distribution service, let's take a look at how the distribution service works internally.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05079c56a7534f11944632d3fb68c4de~tplv-goo7wpa0wc-image.image) </span>

**Step 1: Check the whitelist of users**

First, the streaming service checks the experimental layer to see if any experiments are configured with whitelist users.

> Whitelist users: Before the experiment is officially launched, it is usually necessary to select a few users to enter the test to observe whether the experiment can obtain data normally, whether the experimental configuration takes effect normally, or whether there are bugs on the client side. Users who participate in this step are called "test users". If the experiment needs to test users, you need to provide the ssid/decisionid of each group of test users first.

> If the ssid/decision id in the request parameter is in the list of test users for a group and the experiment is in the debug state, then only test users will hit the group to obtain the experimental configuration.


**Step 2: traffic bucketing**

When the streaming service distributes traffic, it first distributes the traffic of each layer into 1,000 copies, each of which is called a "hash bucket". Why is it called a "hash bucket"? Because when the user enters the experimental layer, the streaming service will allocate the user to a bucket through the "hash function" and "modulo operation". For details, please refer to the traffic sharing section above.

**Step 3: Check the filter conditions**

In this step, the offloading service filters the traffic again according to the filter conditions configured by the experiment. Users who meet the filter criteria will be hit by the experiment, while those who do not meet the filter criteria will not be hit by the experiment.

**Step 4: Calculate the grouping**

Now, we want to group the traffic that is experimentally hit. At this point, we still have to rely on the power of the "hash function". In this step, we will take the user's ID and the experiment name as input values (e.g. "did: flight_name"), operate the hash function, and take modulo to randomly divide the users hit by the experiment into different groups.

The above is the code call sequence for drilling down, and the actual user entry process sequence should be reversed:

**Step 1: Whether the user is a whitelist user.** 

**Step 2: Whether the user belongs to the experimental layer.**  Determine the experimental laminar shunt, if there is no laminar shunt, proceed to the next step to bucketing. In the case of layer shunting, the layer parameter is bucketing when the user's shunted decision_id is hashed.

**Step 3: Determine the logic of not entering the group.**  If the group is turned on, first check the customer configuration of the third\-party group information store. If there is, the shunt information in the repository is returned. If not, proceed to the next step.

**Step 4: Determine the target audience.**  Determine whether the user meets the conditions set by the target audience. If satisfied, proceed downward.

**Step 5: Determine whether the user hits the bucket corresponding to the experiment.**  Hash the user's decision_id to obtain the bucket number where the user is located, and determine whether the user will be in the list of bucket numbers assigned by the experiment.

**Step 6: Obtain the experimental version number.**  Each experimental version has its own corresponding list of bucket numbers, and which bucket the user falls in is the user of that version. If you don't have the bucket number corresponding to the experimental version, you won't hit the experiment.

<span id="8c59a3cb"></span>
### Distribution principle: Differences in client side & server side experiments


|**Differential segmentation** |**Client side experiment** |**Server side experiment** |
|---|---|---|
|**In the group but not in the group** |Client side experiment default group not group |The server side experiment will not enter the group by default. If you want to use this feature, you need to implement the relevant interface according to the sdk access document. |
|**Configure delivery traffic chart** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/633bcf49a31548d1b4655aa7d2c631f8~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a87c2eb18c1a4035abec354a22beceb5~tplv-goo7wpa0wc-image.image) </span> |
|**Configuration take effect steps** |1. Client app integration ABS client side SDK and initialization.<br><br>2. After initializing the AB client side SDK, call the AB offload service regularly to obtain the experimental group information of the current device user and cache it locally.<br><br>3. The client app executes the code in the exposure area, calls the AB client side SDK to obtain the experimental group information, the AB client side SDK reports the exposure event, and the exposure event carries the vid information of the user hitting the experimental configuration.<br><br>4. The user operates in the customer app, and the customer app uses the AB client side SDK for event tracking reporting. The event tracking will carry the vid information of the experimental configuration. |1. Client Server integration ABS server side SDK and initialization.<br><br>2. After initializing the AB server side SDK, call the AB metadata service regularly to obtain the experimental metadata information.<br><br>3. Client Front Request Client Server.<br><br>4. After the Client Server side calls the AB server side SDK, the AB server side SDK uses the experimental meta\-information to return the experimental group information after calculation, and reports the exposure event at the same time. The exposure event carries the vid information of the user hitting the experimental configuration. |


<span id="f0296861"></span>
## AB testing data calculation logic

<span id="1e79a0ce"></span>
### 1. Retention rate

The retention rate in the experimental report refers to the "retention rate split by group entry time", which is based on [the time when the user first entered the experimental group] as the starting point, and the user returns to the App as a return visit to calculate the user's n\-day retention.

The statistical methods are as follows:


|Rule |Processing logic |
|---|---|
|Grouping |Users entering the experimental group for the first time |
|Attribution method |The retained users are divided according to the time of entering the group and attributed to the time of first entering the group |
|Return visit rule |Returning to the APP is considered a return visit. |


> Let me give you an example.

> * The number of users in experimental group A on the first day is: 10,000, and the base_user on the first day is 10,000.

> * The number of users in experimental group A on the second day is: 10400, of which 9200 users are users who have been in A on the first day, and 1200 users are new users on the same day; the second day base_user is 1200, and the next day of the first day The retention is 9200/10000 = 92%.

> * The number of users in experimental group A on the third day is: 10200, of which 8000 users are users who have been in A on the first day, 1100 users are users who enter A on the second day, and 1100 is users who enter A on the third day; The base_user of the third day is 1100, the retention of the second day is 8000/10000 = 80%, and the retention of the next day is 1100/1200 = 91.67%.

> * Then, the index of each entry date is weighted and averaged with base_user to obtain the Day Retention Ratio at Day 1 and Day 2.


"Entered users" on the day represents the total number of users exposed to the group that day, including old users who have been in the group before and "new users" who are visiting for the first time.

<span id="78ae8b84"></span>
### 2. Confidence intervals

The confidence score interval is the range used to estimate the overall parameters of a set of experimental data.

> For example, we are now running an experiment to optimize the purchase rate of users on product pages. In the experimental group that adopted the new strategy B, the purchase rate improved by an average of 5%, and the confidence interval was [\-3%, 13%].

> How do we understand the confidence interval here?

> Due to the small traffic sampling method used in the A/B experiment, the sample cannot fully represent the overall traffic, so in fact, if strategy B takes effect in the overall traffic, it may not achieve a 5% increase. If we assume that the true growth rate caused by the implementation of strategy B in the overall traffic is μ, then in this case, the true value of μ will be between [\-3%, 13%].


It is worth noting that μ is not 100% likely to fall in this interval. In the process of calculating the confidence interval, we will first take a confidence level and calculate the confidence interval at this confidence level. In A/B experiments, we usually calculate the confidence interval at the 95% confidence score. Returning to the previous example, we can see that if we repeat the experiment 100 times, 95 times the value of μ will fall within [\-3%, 13%].

<span id="28507a06"></span>
### 3. Multi\-day cumulative metrics

"Multi\-day cumulative metric" is the cumulative value of the corresponding metrics combined over multiple days within the selected experimental date range.

> For example, let's now look at the metric of user readings for users A, B, and C from June 1 to June 3:



| |June 1st |June 2nd |June 3rd |multi\-day cumulative metric |
|---|---|---|---|---|
|User A |13 |0 |16 |29 |
|User B |5 |3 |4 |12 |
|User C |7 |8 |12 |27 |


> The numerical relationships in the table above clearly demonstrate the logic (i.e., adding up) between the multi\-day cumulative and single\-day metrics.


In the A/B experiment, if the metrics we test support multi\-day cumulative metrics, then we should basically **take the multi\-day cumulative metrics as the criterion**, and do not pay too much attention to the single\-day metrics in the test period.

The accumulation of data over multiple days means that as the experiment progresses, the overall sample of the experiment continues to increase, and the test sensitivity of the experiment continues to improve.

<span id="三-高阶"></span>
# Advanced

<span id="_1-假设检验"></span>
## 1. Hypothesis testing

The core statistical theory of A/B experiments is the (two\-sample) hypothesis test. Hypothesis testing involves first making a hypothesis and then using data to test whether the hypothesis holds. It is important to note that when we test hypotheses, we logically use the method of contradiction. Through A/B experiments, we are actually trying to test a pair of opposing hypotheses: the null hypothesis and the alternative hypothesis.


* **A null hypothesis** is a hypothesis that the experimenter wants to gather evidence against. The null hypothesis in A/B experiments is that "the new strategy has no effect."

* **Alternative hypothesis:**  is a hypothesis that the experimenter wants to collect evidence to support, with mutual exclusion from the null hypothesis. The alternative hypothesis in A/B experiments is that "the new strategy works."


To test a hypothesis by contradiction means using existing data to prove that the null hypothesis is false (false) and that the alternative hypothesis is true (true). This set of methods is statistically known as null hypothesis significance testing (NHST).

> Here's an example.

> We're going to do an experiment with a buy button on a page. I believe that changing the color of the purchase button from blue to red can increase the purchase rate by 3%. In this experiment, the "null hypothesis" we want to test statistically is that "changing the purchase button to red does not increase the purchase rate"; the "alternative hypothesis" is that "changing the purchase button to red does increase the purchase rate". This is a hypothesis of mutual exclusion. In other words, what we are actually trying to prove is that "changing to red does not increase the purchase rate" is wrong.


<span id="_2-第一类错误和显著性水平（α）"></span>
## 2. Type 1 error and significance level (α)


* The first type of error is when the null hypothesis is correct (true), but the conclusion of our hypothesis test shows that the null hypothesis is wrong. We reject the correct null hypothesis in this process, so the first type of error is "discarding truth."

* The first type of error is manifested in practice as follows: The experimental conclusion shows that my new strategy works, but in fact my new strategy does not work.


In statistics, we use the significance level (α) to describe the probability that an experimenter will make a Type I error.

When the metrics of a certain experimental group are significant, it indicates that the experimental results are likely to be reliable. This probability is 95%, which means that the system has 95% confidence that the experimental result is accurate.

**What is the significance level of existence?** 

> A button changes from blue to red, a window moves from left to right, will the user experience get better or worse? We're not sure, so we're trying to transform this uncertainty using A/B experiments \- looking at how old and new strategies perform in low\-traffic tests to determine their strengths and weaknesses.

> But would that eliminate the uncertainty entirely? The answer is no, because of **sampling error** .

> * For example, if the per capita income of Switzerland is ten times that of China, then randomly selecting three Swiss and three Chinese can guarantee that the average income of the three Swiss in the sample is ten times that of the three Chinese? What if these three Chinese are Ma Yun, Wang Jianlin and a primary school student?

> * On the other hand, suppose that at 1% of the traffic, Group A (buttons are red) has a higher purchase rate than Group B (buttons are blue), and expanding the traffic to 100% guarantees that Strategy A will still perform better than Strategy B? Obviously, we're still not sure.

> **The uncertainty caused by sampling error makes it impossible to guarantee that the conclusion is completely correct when doing a low\-traffic test. Fortunately, for the uncertainty of sampling, in statistics, we have a way to quantify the degree of uncertainty, which is why the significance level (α) exists.** 


<span id="_3-第二类错误-β-和统计功效（statistics-power）"></span>
## 3. Type II errors (β) and statistics power


* The second type of error refers to the null hypothesis error (false), but the conclusion of our hypothesis test shows that "the null hypothesis is correct (true), and the alternative hypothesis is wrong". In this process, we accept the wrong null hypothesis, so the second type of error is "false".

* The second type of error manifests itself in practice as: my new strategy actually works, but the experiment fails to detect it.


In statistics, statistical power = 1 \- the probability of type 2 errors. Statistical power is expressed in reality as: my new strategy is effective, and how likely I am to detect it in an experiment.

<span id="_4-统计显著性-置信水平-置信度-置信系数"></span>
## 4. Statistical significance/confidence level/confidence score/confidence coefficient


* Confidence level (also known as confidence score, confidence coefficient, statistical significance), refers to the probability that there is a real difference in performance between the experimental group and the control group, and the difference between the experimental group and the control group is not due to randomness. Confidence levels allow us to understand when the results are correct, and **for most businesses, generally speaking, a confidence level higher than 95% can be understood as the experimental results are correct.**  **Therefore, by default, the "A/B Test" product sets the confidence level parameter value to 95%.** 

* In the A/B experiment, we can only do small sample experiments because we can only extract traffic. The distribution of sample traffic will not be exactly the same as the overall traffic, which means that none of the experimental results can be 100% accurate \- even if the data goes up, it may be due solely to sampling error, regardless of our strategy. In statistics, the **confidence score exists to describe the reliability of experimental results.** 


In the process of the experiment, the sample traffic we extracted will actually be slightly different from the overall traffic, and these differences determine that there will be some "errors" in the conclusions we draw through the experiment.

> For example, in the experiment, I increased the purchase rate by 3% by changing the color of the landing page, but because the sample traffic does not fully represent the overall traffic, it is possible that "my strategy of changing the color was useless, and the purchase rate increased by 3% due to the sampling results."

> So what are the chances of this "my strategy didn't work" event happening? In statistics, we use "significance level (α) " to describe the probability of this event occurring. And confidence score = 1\-α.

> On "A/B test" products, according to industry standards, the significance level α is 0.05. In an A/B experiment, if the probability of "my strategy actually didn't work" is less than 0.05, we say the conclusion is "statistically significant/believable." This means that your new strategy has a high probability (greater than 95% in A/B experiments) of being effective. Conversely, if the probability of this event is greater than 0.05, the experimental conclusion is said to be "not significant/unbelievable."


<span id="_5-中心极限定理"></span>
## 5. Central limit theorem

**The theoretical basis of significance level is the central limit theorem. We can quantify the sampling error based on the existence of the central limit theorem.** 

**What is the Central Limit Theorem?** 


> * Due to the existence of sampling error, the index results we obtain in each experiment may be inaccurate with the actual results we expect. Suppose we take a sample from a population and calculate the mean of its metrics. For each calculation, the sample mean is affected by sampling error. If we do countless experiments, then theoretically, one of the countless sample means should always be "true" and not affected by sampling error. This value is called "true value" in statistics.

> * The central limit theorem tells us that if we continuously take samples from the total traffic and do countless low\-traffic tests, the average observed by these countless samples will approximately exhibit a normal distribution (the distribution shown in the figure below). This distribution is centered on the true value, and the closer the mean is to the true value, the higher the probability of occurrence; conversely, the more the mean deviates from the true value, the lower the probability of occurrence.


PS: Here, for ease of understanding, the concept of explaining statistics is abandoned, and the central limit theorem is explained only from the context of A/B experiments.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/54e36e7b87fc4c1581286fba7dac970d~tplv-em5hxbkur4-noop.image?width=1374&height=436) </span>

**Why does the closer the sample mean is to the true value, the higher the probability of occurrence?** 

> For example, if you take many, many samples of the entire Chinese population and calculate the average income many, many times.

> It is foreseeable that we will obtain many different average income values depending on the sample. It is indeed possible that these numbers are higher because of the occasional draw of the top rich, or lower because of the draw of the very poor. However, the above two cases are rare after all (the more the mean deviates from the true value, the less likely it is to occur). As the number of samples increases, we will find that the number of times the average income falls within the income range of most ordinary people will increase significantly (the mean is close to the true value, and the probability of occurrence is high). And with the help of the central limit theorem, we can determine the probability of each mean.


<span id="_6-校验灵敏度mde"></span>
## 6. Calibration Sensitivity MDE


* **What is MDE:**  Minimum Detectable Effect (MDE), Minimum Detectable Effect, that is, test sensitivity, is an metric diff amplitude that can be effectively detected by experiments under current conditions. Current conditions refer to the current sample size, metric value, and metric distribution, and assume that the sample variance is close enough to the overall metric variance. Valid detection, indicating a detection probability greater than or equal to 80% (type II error less than or equal to 20%).

* **What MDE can be used for:**  By comparing the target improvement rate of the metric MDE with the target improvement rate of the metric, the experiment can be avoided by premature non\-significant conclusions in the case of insufficient sensitivity, missing potential features .

> Suppose your expected target improvement rate for a metric is 1%.

> * If MDE = 0.5% at this time, MDE < expected increase value, indicating that the metric change is really not significant, please combine business ROI and other dimensions such as user experience, long\-term strategic value, etc. to comprehensively judge whether it is worth going online;

> * If MDE = 2% at this time, MDE \> the expected increase value, indicating that the current minimum difference that can be detected as significant is 2%, which cannot be detected due to insufficient sensitivity (i.e., calibration effectiveness). In this case, it is recommended to increase the sample size, such as expanding the traffic and observing the accumulation of more users over a period of time. There is still a possibility of confidence in the metric.

* **How to set it:**  The smaller the MDE, the higher the sensitivity you require for the test and the larger the sample size required. If the MDE setting is too detailed, not only will unnecessary traffic be wasted, but the actual benefits may not make up for the development and promotion costs of the new strategy. Insufficient sensitivity (e.g. 1% is expected to meet the standard, but experimental sensitivity can only detect 5% or more) may lead to missing potential features.
