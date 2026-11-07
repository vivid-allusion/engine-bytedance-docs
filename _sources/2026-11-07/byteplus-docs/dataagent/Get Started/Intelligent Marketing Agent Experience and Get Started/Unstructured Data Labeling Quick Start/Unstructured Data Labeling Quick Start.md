---
title: "Unstructured Data Labeling Quick Start"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Unstructured_Data_Labeling_Quick_Start_"
---

Visual modeling is used to process data such as articles, audio, and video. Another is to standardize data such as conversations.

<span id="e086d803"></span>
# Operation flow chart

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI2MDZweCIgaGVpZ2h0PSI4NjZweCIgdmlld0JveD0iLTAuNSAtMC41IDYwNiA4NjYiPjxkZWZzLz48Zz48cmVjdCB4PSIxNjIiIHk9IjcyMyIgd2lkdGg9IjQ0MCIgaGVpZ2h0PSIxNDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxODIiIHk9IjQwMyIgd2lkdGg9IjQwMCIgaGVpZ2h0PSIxNDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDYyIDkzIEwgNjIgMjA2LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjIgMjExLjg4IEwgNTguNSAyMDQuODggTCA2MiAyMDYuNjMgTCA2NS41IDIwNC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjUzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiM2NjY2ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDczcHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTVweCI+PGI+UHJlcmVxdWlzaXRlPC9iPjwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzgyIDUzIEwgMzgyIDg2LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzgyIDkxLjg4IEwgMzc4LjUgODQuODggTCAzODIgODYuNjMgTCAzODUuNSA4NC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjMyMiIgeT0iMTMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzNweDsgbWFyZ2luLWxlZnQ6IDMyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3BhbiBzdHlsZT0iZm9udC1zaXplOjE1cHgiPjxiPkFjdGl2YXRlIFZlQ0RQPC9iPjwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMyMiIgeT0iOTMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTEzcHg7IG1hcmdpbi1sZWZ0OiAzMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxNXB4Ij48Yj5BdXRob3JpemF0aW9uIENvbmZpZ3VyYXRpb248L2I+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzODIgMjEzIEwgMzgyIDI0Ni42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM4MiAyNTEuODggTCAzNzguNSAyNDQuODggTCAzODIgMjQ2LjYzIEwgMzg1LjUgMjQ0Ljg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzIyIiB5PSIxNzMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTkzcHg7IG1hcmdpbi1sZWZ0OiAzMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxNXB4Ij48Yj5VcGxvYWQgRGF0YTwvYj48L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMjIiIHk9IjI1MyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNzNweDsgbWFyZ2luLWxlZnQ6IDMyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3BhbiBzdHlsZT0iZm9udC1zaXplOjE1cHgiPjxiPkFjY2VzcyBEYXRhPC9iPjwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzgyIDM3MyBMIDM4MiA0MDYuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzODIgNDExLjg4IEwgMzc4LjUgNDA0Ljg4IEwgMzgyIDQwNi42MyBMIDM4NS41IDQwNC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjMyMiIgeT0iMzMzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM1M3B4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTVweCI+PGI+Q3JlYXRlIERhdGEgQ29ubmVjdGlvbjwvYj48L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMjIiIHk9IjQxMyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0MzNweDsgbWFyZ2luLWxlZnQ6IDMyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjEycHgiPkNvbmZpZ3VyZSBEYXRhIFByb2Nlc3NpbmcgT3BlcmF0b3JzPC9mb250PjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE5MiIgeT0iNDkzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDUxM3B4OyBtYXJnaW4tbGVmdDogMTkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTNweCI+QmFzaWMgSW5mb3JtYXRpb248L2ZvbnQ+PC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzODIgNTMzIEwgMzgyIDU2Ni42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM4MiA1NzEuODggTCAzNzguNSA1NjQuODggTCAzODIgNTY2LjYzIEwgMzg1LjUgNTY0Ljg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzIyIiB5PSI0OTMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTEzcHg7IG1hcmdpbi1sZWZ0OiAzMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToxM3B4Ij5EZXBlbmRlbmN5IENvbmZpZ3VyYXRpb248L2ZvbnQ+PC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDUyIiB5PSI0OTMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTEzcHg7IG1hcmdpbi1sZWZ0OiA0NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToxM3B4Ij5BZHZhbmNlZCBDb25maWd1cmF0aW9uPC9mb250PjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzgyIDYxMyBMIDM4MiA2NDYuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzODIgNjUxLjg4IEwgMzc4LjUgNjQ0Ljg4IEwgMzgyIDY0Ni42MyBMIDM4NS41IDY0NC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjMyMiIgeT0iNTczIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5M3B4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTNweCI+Q29uZmlndXJlIERhdGEgT3V0cHV0IE9wZXJhdG9yczwvZm9udD48L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMjIiIHk9IjY1MyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA2NzNweDsgbWFyZ2luLWxlZnQ6IDMyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3BhbiBzdHlsZT0iZm9udC1zaXplOjEzcHgiPjxiPlJ1biBUYXNrPC9iPjwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzgyIDc3MyBMIDM4MiA4MDYuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzODIgODExLjg4IEwgMzc4LjUgODA0Ljg4IEwgMzgyIDgwNi42MyBMIDM4NS41IDgwNC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjMyMiIgeT0iNzMzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc1M3B4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweCI+PGI+RXhwb3J0IE91dGNvbWU8L2I+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzIyIiB5PSI4MTMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODMzcHg7IG1hcmdpbi1sZWZ0OiAzMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4Ij48Yj5BbmFseXNpcyAmYW1wOyBVc2U8L2I+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MiAyNTMgTCA2MiA0ODYuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2MiA0OTEuODggTCA1OC41IDQ4NC44OCBMIDYyIDQ4Ni42MyBMIDY1LjUgNDg0Ljg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMjEzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiM2NjY2ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIzM3B4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjE1cHgiPjxiPkRhdGEgUHJlcGFyYXRpb248L2I+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MiA1MzMgTCA2MiA3NjYuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2MiA3NzEuODggTCA1OC41IDc2NC44OCBMIDYyIDc2Ni42MyBMIDY1LjUgNzY0Ljg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iNDkzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiM2NjY2ZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDUxM3B4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3BhbiBzdHlsZT0iZm9udC1zaXplOjE1cHgiPjxiPlZpc3VhbCBNb2RlbGluZyBUYXNrIENyZWF0aW9uPC9iPjwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9Ijc3MyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjNjY2NmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3OTNweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxNXB4Ij48Yj5Vc2FnZSBPdXRjb21lPC9iPjwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE2MiIgeT0iMyIgd2lkdGg9IjQ0MCIgaGVpZ2h0PSIxNDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxNjIiIHk9IjE2MyIgd2lkdGg9IjQ0MCIgaGVpZ2h0PSIxNDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxNjIiIHk9IjMyMyIgd2lkdGg9IjQ0MCIgaGVpZ2h0PSIzODAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PC9zdmc+" />

<span id="3087bd05"></span>
# Prerequisite


* You have opened **VeCDP** , please refer to [Open VeCDP ](https://www.volcengine.com/docs/6356/1131835).

* You have opened project **editing** or **permissions \- by content management \- module \- data connection \- new connection** permissions, please refer to the specific operation [Authorization Configuration](https://docs.byteplus.com/docs/dataagent/Authorization_Configuration).


<span id="d8902af7"></span>
# Prepare data

Before using the unstructured data marking function, you need to create the unstructured data to be labeled as a dataset of VeCDP. For more types of data connection operations, see [Common Data Source Access ](https://www.volcengine.com/docs/6356/130758)and [Data Entry ](https://www.volcengine.com/docs/6356/1222748).


1. Log into **the Customer Data Platform** and select **Data Management \- Data Connections.** 

2. Click on the **New Data Connection** icon, select **Unstructured Data** , and select Upload File or the corresponding object storage

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c44692ee2b94f9d9ca913c7584ac593~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   * **Upload file** : Fill in the data connection name, upload the file, the file supports docx, doc, pptx, ppt and other formats, and there is no limit to the number and size.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba7b23d821114139a26215a972ed9318~tplv-goo7wpa0wc-image.image) </span>

   * **Volcanic cloud TOS_ meta information**:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26bbac5fda5c415f8e911b401c07c99f~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Specify |
      |---|---|
      |AccessKey |Request security credentials for the Volcano Engine API, which you can obtain through the **System Configuration \- Access Control \- API credentials** in the upper right corner of the avatar, see [Access Key Management ](https://www.volcengine.com/docs/6291/65568)for details. |
      |SecretKey |Request security credentials for the Volcano Engine API, which you can obtain through the **System Configuration \- Access Control \- API credentials** in the upper right corner of the avatar, see [Access Key Management ](https://www.volcengine.com/docs/6291/65568)for details. |
      |Access point (endpoint) |Corresponding to the access domain name of S3Endpoint, and add https://in front of it, for example, TOS Beijing corresponds to https://tos\-s3\-cn\-beijing.volces.com.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0401cdb22baa444a93e053c99dc6c1a3~tplv-goo7wpa0wc-image.image) </span> |
      |Bucket name (bucket) |Bucket name, such as test\-bucket\-123 |
      |Area (region) |Regions, such as cn\-Beijing. |
      |File directory |The storage directory for data files, such as data/test/. |
      

   * **Tencent Cloud COS_ Meta Information:** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b0e08c2ba844d9cab8d4294a5077f56~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Specify |
      |---|---|
      |AccessKey |To request an API security credential, please go to the API Key Management page of Tencent Cloud Access Management Console to create and obtain it. |
      |SecretKey |To request an API security credential, please go to the API Key Management page of Tencent Cloud Access Management Console to create and obtain it. |
      |Access point (endpoint) |Corresponding to the access domain name of the Endpoint, and add https://in front of it, such as COS Beijing corresponding [https://cos.ap-beijing.myqcloud.com ](https://cos.ap-beijing.myqcloud.com). |
      |Bucket name (bucket) |Bucket names, such as my\-cos\-bucket\-125xxxx0000 |
      |Area (region) |Region, the distribution area of Tencent cloud hosting computer room |
      |File directory |The storage directory of the data file, be careful not to start with/when filling in here |
      

   * **Alibaba Cloud OSS_ information:** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5119044c04754b6797f8680e57efa6e0~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Specify |
      |---|---|
      |AccessKey |Request security credentials for the API. For information on how to obtain an AccessKey, please refer to the official Alibaba Cloud documentation "Creating an AccessKey". |
      |SecretKey |Request security credentials for the API. |
      |Access point (endpoint) |Corresponds to the access domain name of the Endpoint, and adds https://in front of it, such as the OSS Beijing corresponding [https://oss-beijing.aliyuncs.com ](https://oss-beijing.aliyuncs.com). |
      |Bucket name (bucket) |Bucket name, such as hangzhou\-static |
      |Area (region) |Regions, such as cn\-Beijing. |
      |File directory |The storage directory for data files, such as data/test/. |
      

4. Click **Test Connection** to take the data source connectivity test.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c7afc57ed58497eb388304e9d0fba6d~tplv-goo7wpa0wc-image.image) </span>

5. After the test is successful, click **Save** . Click on **one\-click access** and the system will automatically create a dataset and start synchronizing meta information according to your configuration.

6. After the access is complete, you can click to **view data sets** , jump to the data set management page, unstructured data has been written into a structured table.


<span id="2e4f04c0"></span>
# Add data connection


1. In the top navigation bar of the **Customer Data Platform** , select **Data Management \> Visual Modeling**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/701ed652a374447d8b667d49160579e0~tplv-goo7wpa0wc-image.image) </span>

   You can also log in to the [Intelligent Marketing Agent ](https://console.volcengine.com/cdp/marketing_agent)page and click **Experience Now** in the **Unstructured Data Marking** card, which will jump to the **Visual Modeling** page of the **Customer Data Platform**.

2. Click **Task List** in the left navigation bar of the Customer Data Platform page, then click **New \> New Offline Task** to start creating an offline type of visual modeling task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The current unstructured data marking function only supports label output based on offline visual modeling tasks, so please select "New Offline Task" here.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b22047280fe94ac4a9e3a782046b2e52~tplv-goo7wpa0wc-image.image) </span>

3. Click the ➕ icon at the top left of the New Task page to add a data connection, select the created dataset in the **Add Data Connection** pop\-up window, and add the dataset to the left list of visual modeling tasks.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3d65809b1ba4184add6b9004694d407~tplv-goo7wpa0wc-image.image) </span>

4. Select the dataset of unstructured data to be marked and pull it from the left list into the right panel.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43d626df28f14110b8668336084a407f~tplv-goo7wpa0wc-image.image) </span>

   If you need to remove a data connection, click the Delete button to the right of a specific data connection in the data connection list on the Visual Modeling Task Creation page to remove the data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/530a032164be46f2a033d7b6ae5ec8f8~tplv-goo7wpa0wc-image.image) </span>


<span id="f1a8da6b"></span>
# Configuring unstructured data processing operators

After adding a data connection, you need to add an unstructured data processing operator to process the data. VeCDP supports the following unstructured data processing operators:


* REST API 2.0 operators

* Volcano Ark Large Model operator

* knowledge segmentation

* DeepSeek Large Model

* Tongyi Qianwen large model operator


<span id="99941048"></span>
## REST API operator

If your unstructured dataset contains audio data that has not been converted to text, you need to call the ASR capability through the REST API operator to convert it to text. The current REST API operator feature is turned off by default, so if you need to use it, you need to contact the Volcano Engine account manager to manually enable the REST API operator. For detailed usage of this operator, see [REST API 2.0 ](https://www.volcengine.com/docs/7139/1558215).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When preparing data, it is currently recommended that you convert the audio & video file to text first and then access the VeCDP dataset. It is not recommended that you directly access the audio & video file directly to VeCDP and then use the data processing operator to operate. See the specific operation <a href="https://docs.byteplus.com/docs/dataagent/Data_Preparation">Data Preparation</a>.</div>



1. Contact the Volcano Engine account manager to turn on the REST API operator function switch.

2. Click "Operator" on the left, drop down and select "Featured Area Operator", select "REST API 2.0 Call", and pull it into the right panel.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/192305986344435789929685687d3c75~tplv-goo7wpa0wc-image.image) </span>

3. Configure ASR task parameters. For a detailed description of parameter configuration, see [REST API 2.0](https://www.volcengine.com/docs/7139/1558215).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f93ad96e2b746acab2e3fdae41b9df6~tplv-goo7wpa0wc-image.image) </span>

4. Preview ASR processing results.


<span id="9ce3dda0"></span>
## **Volcano Ark Large Model Operator**

After introducing the dataset, you can introduce large model operators to the downstream of the dataset to intelligently label the connected data. For detailed use of this operator, please refer to the [Volcano Ark Large Model ](https://www.volcengine.com/docs/7139/1829075).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only the Volcano Ark large model operator is supported. Connect to your Ark large model platform through the operator, and call the large model on the platform that supports the OpenAPI protocol for intelligent marking.</div>



1. Click "Operator" on the left, drop down and select "Featured Area Operator", select " **Volcano Ark Large Model** ", and pull it into the right panel.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34d422667feb47b498f27f6c750ca8c9~tplv-goo7wpa0wc-image.image) </span>

2. Click on the Ark big model operator that has been dragged into the task, click the "Customize Volcano Ark Model" button at the bottom of the task window, configure the access point of the Ark and the API key, and see the [Volcano Ark big model ](https://www.volcengine.com/docs/7139/1829075#%E5%8A%9F%E8%83%BD%E6%A6%82%E8%BF%B0)for detailed parameter configuration instructions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/159812c00f7948ee82d5dffa2aa678ca~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Explain |
   |---|---|
   |Inference access point |Configure the inference access point for your Ark large model platform, the general format is ep\-xxxxxxxxxx\-yyyy, please refer to the [Volcano Ark documentation ](https://www.volcengine.com/docs/82379/1099522)for the operation of the inference access point. |
   |API Key |Configure the API Key for your Ark big model OpenAPI call, the general format is xxxxxxxx\-yyyy\-xxxx\-yyyy\-xxxxxxxxxxxx, refer to the [Volcano Ark official website documentation ](https://www.volcengine.com/docs/82379/1263279)for the way to get it. |
   |Generative randomness |Temperature: Increasing the temperature will make the output of the model more diverse and innovative, while reducing the temperature will make the output content more compliant with the instruction requirements but less diverse. It is recommended not to adjust it at the same time as "Top p". |
   |Top P |Top p is the cumulative probability: When the model generates the output, it selects the words with the highest probability until the total probability of these words accumulates to the top p value. This allows the model to choose only these high\-probability words, thus controlling the diversity of the output. It is recommended not to adjust at the same time as "generating randomness". |
   

3. Configure the prompt word associated with the reply logic.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ff0b510be9d43c997454a4ea18e3391~tplv-goo7wpa0wc-image.image) </span>

   It needs to include the following four parts:

   * Role definition: such as tag extraction expert.

   * Skill description: such as what label to extract.

   * Output format: as required by JSON format.

   * Other limitations: such as focusing on extraction tasks without divergence.

      The following is an example for reference only:

   ```Markdown
   # Role
   You are a precise and efficient chatbot for bank consumer loan customer service, 
   capable of quickly and accurately extracting corresponding tags from customer 
   service chat records, helping banks to gain a deeper understanding of customer needs 
   and provide more personalized services.
   
   ## Skill
   ### Skill 1: Analyze chat content and extract tags
   1. Carefully study customer service chat records to accurately understand the 
   customer's expression intentions.
   2. Based on the customer's statement, determine the label of their loan (demand):
       - Immediate processing: The customer clearly stated that they need to apply for a consumer loan immediately.
       - Recent considerations: The client has revealed plans to apply for a consumer loan in the near future.
       - No current demand: The customer has clearly expressed that they do not currently have a need to apply for a consumer loan.
   3. Based on the customer's statement, determine the label to which their (customerType) belongs:
       - Personal: Personal user.
       - Enterprise: Enterprise user.
       - Unknown: Unable to clearly determine the customer type.
   4. Based on the customer's statement, determine the label to which their (focus) belongs:
       -Interest rate: Customers mainly inquire or discuss about loan interest rates.
       - Limit: The customer emphasized the situation related to the loan limit.
       - Repayment method: The customer shows interest in the repayment method.
       - Approval process: Customers are concerned about loan approval processes and related issues.
       - Other: The content that customers are concerned about does not belong to the clear categories mentioned above.
   5. Based on the customer's statement, determine the label to which their (loanUsage) belongs:
       - Daily consumption: The customer stated that the loan is mainly used for daily consumption.
       - Education expenditure: The client emphasizes that the loan is used for education related expenses.
       - Medical expenses: The customer mentioned that the loan is used for medical purposes.
       - Other uses: The loan purpose mentioned by the customer does not belong to the above category.
       - Not mentioned: The customer did not mention any information related to the purpose of the loan.
   6. Freely extract other valuable tags from chat records, such as customer preferences for loan terms, special requirements, etc. (output null if not available).
   
   Output content in JSON format, as shown in the following example:
   
   {
       "demand": "Recently considered",
       "customerType": "Personal",
       "focus": "Quota",
       "loanUsage": "Consumption",
       "otherValuableTags": null
   }
   
   If there is no matching label, null can be output.
   
   ## Restrictions
   -Only analyze customer service chat content, extract exact tags, and do not perform any other unrelated operations.
   -Strictly follow the established label classification for judgment, and do not create new label categories on your own.
   -It is essential to ensure the accuracy and objectivity of the analysis results.
   -The freely extracted tags must be truly valuable and relevant to customer needs or bank consumer loans.
   ```
   

4. Configure template variables with user input. After selecting the field column for unstructured data in "Upstream Fields" of "Template Variables", configure the rules for the variable in "User Input".

   * Upstream field: Select the input field that needs to be labeled as the output of the large model. Use ${field name} to refer to the data in the upstream field, and use < ID \> to identify the input content type. For example, `${context} < text >`is used to refer to the data of the upstream content column and is of text type. The following logos are currently supported:

      
      |Type |logo |
      |---|---|
      |Text |`<text>` |
      |Picture |`<image>` |
      |Audio |`<audio>` |
      |Video |`<video>` |
      |Do not fill in the logo |The system default is `< text >` |
      

      After selecting an upstream field, ${field name} is used to refer to the data of the upstream field, for example, ${conversation content} is used to refer to the data of the upstream field "conversation content" column, for example:

      * When the upstream data set is text\-based outbound call conversation data and WeCom session data, the text data loaded upstream can be selected, that is, the conversation content column.

      * The upstream data set is the outbound call conversation data of the audio class. When processing with ASR, the processed text data, that is, the processed conversation content column, can be selected.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the upstream field name is the same as the system variable, the value of the upstream field will be overwritten. Therefore, you need to avoid using fields with the same name as system variables.      </div>
      

      * User input: After selecting an upstream field, the selected upstream field is automatically used as a variable for user input. You can add examples of user input to debug the effect of large model extraction when different inputs are used. Input format: ${conversation content | example: xxxx}.

5. Click "Test Execution" at the bottom of the page, and the system will extract the label according to the field name entered by the user and give an example result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7644d040992348d0a35ac3d54911de2d~tplv-goo7wpa0wc-image.image) </span>

   You can set the field settings for the desired label according to the example.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7168bff7cffb463a87aea3fdc48f5dfa~tplv-goo7wpa0wc-image.image) </span>


<span id="f1bd4c59"></span>
# Configuration processing result output

<span id="e1c201b0"></span>
## Output as a dataset

If the extraction results are used for analysis, the data can be output to the dataset, and output to Hive/ByteHouse is supported.


1. In the Visual Modeling Edit screen, click the Add Operator button, and in Output Type, click Select **Output \- Output Dataset** .

2. Configure the relevant parameters on the configuration page of the output dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b85b18cdd1364302be63aa2f1e62b8cb~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Explain |
   |---|---|
   |Name/Description |Custom name and description. |
   |Open project |Configure to open a dataset to other projects, allowing dataset administrators to use it as a data source in visual modeling tasks for other projects. |
   |CDP application |Support CDP application marking, define the application scenarios of the dataset while outputting the dataset, automatically match different storage logic based on different scenarios, automatically constrain the format, and avoid repeated data extraction.<br><br>Note: Due to the special query logic in some applications downstream of CDP, please select the appropriate application scenario as needed.<br><br>Common dataset:<br><br>Without special restrictions, it can be used as a data source to repeatedly participate in the production process in the visual modeling, but it is not possible to register the data file or configure the IDM.<br><br>IDMapping map configuration:<br><br>Used to configure an IDMapping graph, it only supports outputting Hive datasets and generally requires partitioning the full amount of data per day.<br><br>Data Files \- Business Details/Behavioral Event Files:<br><br>For registering detailed/behavioral data files, this type of dataset requires the main benchmark OneID field, and the system will automatically store the OneID field as a sharding key and cannot be changed. IDM operators can be added to the canvas process in advance to generate a baseline ID (OneID) field, which generally requires partitioning to store incremental data every day.<br><br>Data File \- Subject Attribute File:<br><br>For registering the data file of the subject attribute, this type of data set needs to fill in the subject benchmark OneID field, and the system will automatically deduplicate according to the OneID field to ensure that the attribute value is unique. You can add the IDM operator conversion to generate the benchmark ID (OneID) field in the canvas process in advance. Generally, it is required to store the full amount of data every day.<br><br>Data Archive \- Business Dimension Archive:<br><br>For registering business dimension data archives, this type of data set requires the dimension primary key field, and the system will store the full amount of data in each sharding node (server) and deduplicate the primary key field, which cannot be directly used in any other module of CDP. Generally, it is required to store the full amount of data in partitions every day.<br><br>Data Archive \- Session Archive:<br><br>For registering session files, this type of dataset requires a required session ID field, typically an incremental partition table. |
   |Type |You can choose ByteHouse or Hive. |
   |Data lifecycle |The number of valid retention days extracted to the data in the system storage, the non\-partitioned table retains the data according to the data update time, and the date partition retains the data according to the partition date. The data outside the lifecycle is automatically cleared at 0 o'clock every day, and the default value is 7 days. |
   |Partition |Optional date or other values can be enumerated as a partition, the first\-level partition must be of type date, if there is no suitable field, you can choose "system default partition" (the value of the day, week, month level routine synchronization tasks is the day before the routine execution of the task, the value of the hour and minute level routine synchronization tasks is the day of the routine execution of the task, and the value of the manually run task is the business time selected at runtime), the second\-level partition can be selected as hours or other values can be enumerated as a partition (dynamic partitioning must be turned on in the advanced settings). |
   |Cluster |Select the cluster where the dataset is stored. |
   |Sort key |Setting the field that is most often used as a filter to the sort key makes the query faster. You can set multiple fields as sorting keys, with the first field having the greatest effect, and the rest decreasing in turn. It is recommended that there be no more than three. You cannot use a partition field as a sort key. |
   |Sample field |In the visualized query module, you can sample and query according to this field, and only fields of type int, float, and string are supported. |
   |Table type |You can choose a normal table or a bucketing table. A normal table is a conventional form of data storage, with a relatively simple and straightforward structure. The bucketing table divides data into different buckets according to specific rules to improve query performance. |
   

3. Advanced configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31b6e25f935244939a1f611a73803332~tplv-goo7wpa0wc-image.image) </span>

   The dataset of the HIVE data source needs to select the run queue and the run priority in the queue. Select a queue, and the corresponding HIVE query will be executed on the specified queue before importing the dataset. Queue selection affects dataset synchronization time, but does not affect visualized query performance.

   Operating parameters: Support setting the operating parameters of dataset synchronization according to requirements to ensure successful synchronization or synchronization performance.


<span id="851d327e"></span>
## Output as label

If the extraction result needs to be used for the circle group, it can be output as a label. The data is exported to the labeling system, allowing users to customize the data processing flow, and finally the processing results are integrated into the labeling system.


1. In the visual modeling editing interface, click the Add operator button, and in Output Type, click Select **Output \- Output tab** .

2. Configure the relevant parameters on the configuration page of the output tag.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/531b4eebab6d43d9bf1055ef0636d18b~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Parameter description |
   |---|---|
   |Subject |Select the principal configured in VeCDP, the target object for ID\-Mapping OneID |
   |Source ID type |The ID Code of a certain type of ID of the subject in the ID\-Mapping graph |
   |Corresponding field |Select the field in the data source corresponding to the ID\-Mapping source ID type as the data input |
   |Tag Configuration |After the label is submitted, the relevant label will be automatically built in the label system, and it will really take effect after saving the task. |
   |Label field |Select the field name that needs to be defined as a label, and special type fields such as Map are not supported for the time being. |
   |Label name |Define the label's understandable name, Chinese or English |
   |Label description |Define the descriptive information that the label can understand |
   |Online service |After opening, the tag can query relevant data in high\-speed OpenAPI to achieve high concurrency queries |
   |Advanced Configuration |Reasonable configuration of operating parameters can help improve the efficiency of the task, and the advanced parameters are only valid when there is a "data cleaning" operator in the front node or the output data set configuration "CDP reference ID field". |
   |Dirty data setup |After opening, the subsequent system will automatically collect dirty data, and you can set an upper limit on the number of dirty data collected per second. After setting up, check the dirty data details in the task monitor for easy dirty data monitoring and analysis.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is only supported in a private environment, but not in a SaaS environment.</div><br> |
   


<span id="82c71333"></span>
# Output result

The above visual modeling output task for data set export or label output, or BI Kanban analysis.
