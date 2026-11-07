---
title: "ByteHouse Dimension Table Widening Feature"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/ByteHouse_Dimension_Table_Widening_Feature"
---

<span id="548d1bee"></span>
## 1. Overview

<span id="cfd21a98"></span>
### 1.1 Dimension Table Query

Flink SQL tasks in real\-time dimension table widening is a very common streaming computation scenario, which involves real\-time association with external dimension tables through real\-time data streams, without additional state management, featuring simple semantics and supporting high QPS throughput. Common dimension table query scenarios include but are not limited to:


1. **User Behavior Analysis**: User behavior logs associated with user's usernames, basic information, and historical behaviors.

2. **Real\-time Recommendation Systems**: User's real\-time actions are associated with feature data in the recommendation model, generating personalized recommendation results.

3. **Financial Risk Control**: Transaction data is associated with risk control rule libraries to detect and alert abnormal transaction behaviors in real time.

4. **IoT Monitoring**: Device data is associated with device configurations or status information to monitor device operations in real time and promptly identify faults.


<span id="34cfe555"></span>
### 1.2 ByteHouse\-CDW as an Advantage in Dimension Tables

Dimension tables scaled wide generally require introducing remote storage for high QPS point queries. In some business scenarios, dimension table data also needs to support downstream OLAP analysis requirements. ByteHouse, as a high\-performance OLAP query engine, supports downstream business queries while effectively handling dimension table queries with second\-level latency.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI4MzVweCIgaGVpZ2h0PSIyNTVweCIgdmlld0JveD0iLTAuNSAtMC41IDgzNSAyNTUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDMyIDE4IEMgMzIgLTMuMzMgOTIgLTMuMzMgOTIgMTggTCA5MiA2NiBDIDkyIDg3LjMzIDMyIDg3LjMzIDMyIDY2IFoiIGZpbGw9IiNlNmU2ZTYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzMiAxOCBDIDMyIDM0IDkyIDM0IDkyIDE4IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxlbGxpcHNlIGN4PSIyODciIGN5PSI0MiIgcng9Ijc1IiByeT0iNDAiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQycHg7IG1hcmdpbi1sZWZ0OiAyMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Qnl0ZUhvdXNlLUNEVzxiciAvPkRJTTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PGVsbGlwc2UgY3g9IjI5MiIgY3k9IjE4MiIgcng9IjcwIiByeT0iNDAiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4MnB4OyBtYXJnaW4tbGVmdDogMjIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk9EUzxiciAvPlJlYWwtdGltZSBEYXRhIFN0cmVhbTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PGVsbGlwc2UgY3g9IjUxMiIgY3k9IjExMiIgcng9IjgwIiByeT0iNTAiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxlbGxpcHNlIGN4PSI3NTIiIGN5PSIxMDIiIHJ4PSI4MCIgcnk9IjQwIiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDJweDsgbWFyZ2luLWxlZnQ6IDY3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EV0Q8YnIgLz5XaWRlIFRhYmxlIERhdGE8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQ4MiIgeT0iMTEyIiB3aWR0aD0iNzAiIGhlaWdodD0iNDAiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMzJweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Sb2Nrc0RCPGJyIC8+Q2FjaGU8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQ4MiIgeT0iODIiIHdpZHRoPSI3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA5MnB4OyBtYXJnaW4tbGVmdDogNDgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZsaW5rIFNRTDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1OTIgMTEyIEwgNjYyLjU5IDExMS41NiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY2Ny44NCAxMTEuNTMgTCA2NjAuODYgMTE1LjA3IEwgNjYyLjU5IDExMS41NiBMIDY2MC44MiAxMDguMDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDM2MiAxODIgTCA0NDkuNDYgMTQ5LjU3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDU0LjM4IDE0Ny43NCBMIDQ0OS4wNCAxNTMuNDYgTCA0NDkuNDYgMTQ5LjU3IEwgNDQ2LjYgMTQ2LjkgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ1NS40MyA3Ni42NCBMIDM2Ny45NyA0NC4yMSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzYzLjA1IDQyLjM5IEwgMzcwLjgzIDQxLjU0IEwgMzY3Ljk3IDQ0LjIxIEwgMzY4LjM5IDQ4LjEgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOTYiIHk9IjMyIiB3aWR0aD0iNzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDJweDsgbWFyZ2luLWxlZnQ6IDM5N3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Mb29rdXAgSm9pbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjM0LjUiIHk9IjIzMiIgd2lkdGg9IjExNSIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTEzcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjQycHg7IG1hcmdpbi1sZWZ0OiAyMzZweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TG9ncyAvIEthZmthIC8gQ0RDPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyMiIgeT0iODIiIHdpZHRoPSIxMDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogOTJweDsgbWFyZ2luLWxlZnQ6IDIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk15U1FMIC8gUG9zdGdyZXM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTIgNDIgTCAyMDUuNjMgNDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMTAuODggNDIgTCAyMDMuODggNDUuNSBMIDIwNS42MyA0MiBMIDIwMy44OCAzOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTAyIiB5PSIxMiIgd2lkdGg9IjkwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAxMDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RmxpbmsgQ0RDPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSIxNDIiIHdpZHRoPSIxNDAiIGhlaWdodD0iODAiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTgycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+VXNlciBiZWhhdmlvcjwvZGl2PjxkaXY+U2VjdXJpdHkgZXZlbnRzPC9kaXY+PGRpdj5UcmFuc2FjdGlvbiBkYXRhPC9kaXY+PGRpdj5Jb1QgZGV2aWNlIHNpZ25hbHM8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTQyIDE4MiBMIDIxNS42MyAxODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMjAuODggMTgyIEwgMjEzLjg4IDE4NS41IEwgMjE1LjYzIDE4MiBMIDIxMy44OCAxNzguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=" />

The advantages of using ByteHouse\-CDW tables directly as dimension tables include:


* **High performance**: Supports high QPS point queries and offers second\-level real\-time dimension table services

* **Diverse scenarios**: Supports business queries and point query capabilities for dimension tables, simplifying dimension table maintenance workflows

* **Lower cost**: ByteHouse\-CDW (cloud data warehouse version) supports compute\-storage separation, providing high elasticity and lower storage costs.


<span id="a887eec5"></span>
## 2. Basic examples

**Note**: To use this feature, ensure Flink version 1.16 or above and ByteHouse\-CDW Connector version 1.27.109 or above.

<span id="10f4f6c6"></span>
### 2.1 Creating a dimension table

In the following SQL, we have constructed a dim_orders table as a dimension table for order information. The primary key and bucket key of the order table are both order_id, namely the order ID. In the subsequent process of expanding the real\-time dimension table, we will associate based on the order ID to obtain the related information of the order.

```SQL
-- Create dimension table data table
CREATE TABLE IF NOT EXISTS
  `dim_orders` (
    `order_id` INT,
    `order_name` STRING,
    `order_product_id` INT,
    `create_date` TIMESTAMP,
    PRIMARY key (`order_id`) NOT ENFORCED
  )
WITH
  (
    'connector' = 'bytehouse-cdw',
    'jdbc.enable-gateway-connection' = 'true',
    -- ByteHouse-CDW Connection Information
    'bytehouse.gateway.region' = 'xxxxxxx',
    'bytehouse.gateway.host' = '${secret_values.bh-host}',
    'bytehouse.gateway.port' = '19000',
    'bytehouse.gateway.api-token' = '${secret_values.bh-api-key}',
    'bytehouse.gateway.virtual-warehouse' = '${secret_values.bh-vw}',
    -- Dimension Table Query Parameters
    'lookup.async.scale-factor' = '16', -- SYNC mode
    'lookup.cache.max-rows' = '10000', -- set '0' to disable caching
    'lookup.cache.ttl' = '1 hour',
    -- ByteHouse Database Table
    'database' = 'bh_db',
    'table-name' = 'dim_orders'
  );
```


<span id="95b71047"></span>
### 2.2 Simulate Real\-Time Data Streams

First, we use `datagen` to simulate real\-time data streams. Note that here `create_date` is used as the processing time.

```SQL
-- Simulate Data Stream
CREATE TABLE
  datagen_source (
    `product_id` INT,
    `product_name` STRING,
    `product_order_id` INT,
    `create_date` AS proctime ()
  )
WITH
  ('connector' = 'datagen');
  
-- The Wide Table Downstream After Real-Time Data Expansion, Using Print to Print to the Console During Testing
CREATE TABLE
  print_sink (
    `product_id` INT,
    `product_name` STRING,
    `product_order_id` INT,
    `create_date` TIMESTAMP,
    `order_name` STRING
  )
WITH
  ('connector' = 'print');
```


<span id="6b7d9745"></span>
### 2.4 Real\-time Lookup Join

The following SQL statement defines a real\-time expanded view `trade_orde_view`, which realizes real\-time data expansion by associating the streaming data source `datagen_source` with the ByteHouse\-CDW dimension table `dim_orders`.

```SQL
-- After Real-Time Expansion, Filter the Data with Non-Empty Order Names and Write to Downstream
INSERT INTO
  print_sink
SELECT
  gen.product_id, gen.product_name, 
  gen.product_order_id, gen.create_date,
  orders.order_name
FROM
  datagen_source AS gen
  JOIN `dim_orders` 
  FOR SYSTEM_TIME AS OF gen.create_date AS orders 
  ON gen.product_order_id = orders.order_id
WHERE
  orders.order_name IS NOT NULL;  
```


The specific logic of the dimension table association is explained as follows:


* **Dimension table**: `dim_orders` is the ByteHouse\-CDW dimension table defined above.

* **Temporal semantics**: `FOR SYSTEM_TIME AS OF gen.create_date` means using the `create_date` field from the stream data to find the snapshot data of the dimension table at the moment of `create_date`.

* **Join condition**: `gen.product_order_id = orders.order_id` involves linking the `product_order_id` from the stream data with the `order_id` in the dimension table.


<span id="861c27a8"></span>
## 3. Tuning Techniques

ByteHouse CDW dimension table lookup supports synchronous and asynchronous modes, and offers various caching strategies (full caching, partial caching, no caching). Practical choices primarily involve balancing between **real\-time dimensions** and **query latency/throughput**, selecting the appropriate dimension table join method based on business characteristics.


* Asynchronous lookup: Set `lookup.async.scale-factor` to greater than 1.

   * Suitable for scenarios with high dimension table real\-time performance (updates visible in real\-time), medium query throughput (~2k QPS), and large dimension tables (over 20 million rows). High data freshness, high dimension table join performance.

* Full caching lookup: Set `lookup.cache.max-rows` to \-1.

   * Suitable for scenarios with medium dimension table real\-time performance (dimension table updates synchronized periodically, like every minute), high query throughput (~50k QPS), and small dimension tables (less than 500,000 rows). Data freshness is low; dimension table join performance is high.

* Partial cache lookup: Set \*\*\*\* `lookup.cache.max-rows` greater than 0.

   * Suitable for scenarios where dimension table has high real\-time requirements (cache eviction policy can be customized, like every 30 seconds or 1,000 rows LRU), high query throughput (~20,000 QPS), and dimension table queries follow a normal distribution (e.g., 90% of queries hit 10% of data). Data freshness is medium; dimension table join performance is medium.

* Real\-time lookup: Set \*\*\*\* `lookup.cache.max-rows` equal to 0.

   * Suitable for scenarios where dimension table has extremely strict real\-time requirements (updates in dimension table are immediately visible), lower query throughput (less than 1k QPS), and small dimension tables. Data freshness is high.


<span id="bf490629"></span>
## 4. Detailed parameter explanation

Here are common settings for WITH parameters in creating dimension tables:


|**Parameter** |**Mandatory** |**Default Value** |**Value Type** |**Description** |
|---|---|---|---|---|
|`lookup.async.scale-factor` |No |`1` |Integer |If it equals 1, it is synchronous lookup;<br><br>If it's greater than 1, it is asynchronous lookup, and this value represents the lookup concurrency of a single subtask. |
|`lookup.cache.max-rows` |No |`0` |Integer |If it is greater than 0, it indicates the maximum number of rows for the dimension table cache. If this value is exceeded, the oldest row records will expire.<br><br>If set to 0, the cache is disabled, and all queries will run on the ByteHouse Server, ensuring the utmost data freshness of the dimension table.<br><br>If set to \-1, the entire table's data is cached into memory, ensuring maximum performance, but be careful about excessive memory usage. |
|`lookup.cache.ttl` |No |`none` |Duration |The maximum retention time of a record after it has been written to the cache. |
|`lookup.max-retries` |No |`3` |Integer |The maximum number of retries after a database query fails. |
|`lookup.cache.skip-missing-key` |No |`false` |Boolean |Whether to skip keys with null values in the dimension table to maximize joining with non\-null values. |
