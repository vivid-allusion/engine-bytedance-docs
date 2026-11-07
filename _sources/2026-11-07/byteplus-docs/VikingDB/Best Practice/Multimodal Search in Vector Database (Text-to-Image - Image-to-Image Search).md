---
title: "Multimodal Search in Vector Database (Text-to-Image / Image-to-Image Search)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Multimodal_Search_in_Vector_Database"
---

<span id="3f666e4f"></span>
# 1. Background Introduction

<span id="4ea81e2d"></span>
## 1.1 Requirements Scenario

With the rapid development of data intelligence technologies, image search is being increasingly applied across a wide range of industries. Traditional image search methods mostly rely on metadata or labels, which suffer from issues such as outdated information, limited knowledge scope, and insufficient search accuracy. Enhancing the precision and efficiency of image search has therefore become a critical issue to address.

Against this backdrop, vector\-based image search technology is emerging as a breakthrough solution. By converting images into high\-dimensional vectors and calculating similarities in the vector space, this approach significantly improves the efficiency and accuracy of image search, effectively overcoming the limitations of traditional methods. BytePlus Vector DataBase, a vector database designed for large\-scale data scenarios, offers outstanding performance, high availability, and robust big data processing capabilities. With extensive experience in supporting massive\-scale retrieval needs, BytePlus Vector DataBase has become a leading solution for image search in the era of big data.

BytePlus Vector DataBase integrates the cutting\-edge Doubao multimodal embedding model, enabling it to effectively handle both textual and visual data. Through efficient vector retrieval, it empowers users in scenarios such as e\-commerce platforms, image libraries, content moderation, and security monitoring to achieve accurate image search and analysis. By combining BytePlus Vector DataBase’s powerful performance with Doubao’s multimodal capabilities, enterprises can build smarter, more precise, and highly efficient image search solutions, driving broader adoption of image search technology across various industries and business domains.

<span id="419900bf"></span>
## 1.2 Scene example


1. **E\-commerce intelligent search**


Search for pictures in text: The user enters "retro\-style leather shoes". Even if there is no word "retro" in the title of the product, the system can match similar styles of leather shoes according to the semantics of the picture.

Search by picture: The user uploads a photo of the clothes worn by the star, and the system automatically finds products of similar styles or the same brand to help accurate shopping recommendations.


2. **social media content discovery**


Search for pictures in text: Users search for "forest wedding photography", the system understands the concept of "forest", and returns wedding photos with natural and green backgrounds, rather than pictures that simply match the labels of "forest" or "wedding dress".

Search by picture: Users upload a picture of their favorite illustration style, and the system recommends illustration works of similar style or related creators to improve the accuracy of content discovery.


3. **Copyright protection and content moderation**


Search for pictures in text: Enter "Van Gogh\-style night scene oil paintings", and the system searches the database for pictures with the same painting style, not just works related to "Van Gogh" tags.

Search by image: Upload a work of art, and the system can find similar compositions, styles, and even modified versions, helping to detect potential infringement.


4. **Medical Image Intelligent Retrieval**


Search for pictures in text: The doctor enters "CT shows ground glass shadow in the lungs", and the system searches the medical images of similar lesions in the database to assist the doctor in referring to similar cases.

Search by picture: The doctor uploads the patient's CT image, and the system finds highly similar cases from the database, recommends relevant diagnosis and treatment plans, and improves the efficiency of diagnosis and treatment.

<span id="42599a07"></span>
## 1.3 Scheme ideas

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMTU1cHgiIGhlaWdodD0iNjQxcHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMTU1IDY0MSI+PGRlZnMvPjxnPjxyZWN0IHg9IjI3Mi4zMiIgeT0iNjcuNSIgd2lkdGg9IjE1MC45NyIgaGVpZ2h0PSI3OC4xMyIgcng9IjExLjcyIiByeT0iMTEuNzIiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwN3B4OyBtYXJnaW4tbGVmdDogMjczcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkltYWdlIHRvIEJlIEluZGV4ZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjcyLjMyIDI3MC4xMSBMIDI3Mi4zMiAyMTguMDMgQyAyNzIuMzIgMjEwLjg0IDMwNi4xMiAyMDUuMDEgMzQ3LjgxIDIwNS4wMSBDIDM4OS41IDIwNS4wMSA0MjMuMjkgMjEwLjg0IDQyMy4yOSAyMTguMDMgTCA0MjMuMjkgMjcwLjExIEMgNDIzLjI5IDI3Ny4zMSAzODkuNSAyODMuMTMgMzQ3LjgxIDI4My4xMyBDIDMwNi4xMiAyODMuMTMgMjcyLjMyIDI3Ny4zMSAyNzIuMzIgMjcwLjExIFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDI3Mi4zMiAyMTguMDMgQyAyNzIuMzIgMjI1LjIyIDMwNi4xMiAyMzEuMDUgMzQ3LjgxIDIzMS4wNSBDIDM4OS41IDIzMS4wNSA0MjMuMjkgMjI1LjIyIDQyMy4yOSAyMTguMDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDlweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNDRweDsgbWFyZ2luLWxlZnQ6IDI3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE3cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48YnIgc3R5bGU9ImZvbnQtc2l6ZToxN3B4IiAvPlRPUyBCdWNrZXQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzQ3LjgxIDE0NS42MyBMIDM0Ny44MSAxOTguNjQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzNDcuODEgMjAzLjg5IEwgMzQ0LjMxIDE5Ni44OSBMIDM0Ny44MSAxOTguNjQgTCAzNTEuMzEgMTk2Ljg5IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1NTcuNDggMzgwLjEgTCA1NTcuNDggMzI4LjAyIEMgNTU3LjQ4IDMyMC44MyA1OTEuMjggMzE1IDYzMi45NyAzMTUgQyA2NzQuNjYgMzE1IDcwOC40NSAzMjAuODMgNzA4LjQ1IDMyOC4wMiBMIDcwOC40NSAzODAuMSBDIDcwOC40NSAzODcuMyA2NzQuNjYgMzkzLjEyIDYzMi45NyAzOTMuMTIgQyA1OTEuMjggMzkzLjEyIDU1Ny40OCAzODcuMyA1NTcuNDggMzgwLjEgWiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTU3LjQ4IDMyOC4wMiBDIDU1Ny40OCAzMzUuMjEgNTkxLjI4IDM0MS4wNCA2MzIuOTcgMzQxLjA0IEMgNjc0LjY2IDM0MS4wNCA3MDguNDUgMzM1LjIxIDcwOC40NSAzMjguMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDlweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNTRweDsgbWFyZ2luLWxlZnQ6IDU1OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE3cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48YnIgLz5WZWN0b3IgRGF0YUJhc2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzQ3LjgxIDI4My4xMyBMIDM0Ny44IDM1NC4xIEwgNTUxLjEyIDM1NC4wNiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU1Ni4zNyAzNTQuMDYgTCA1NDkuMzcgMzU3LjU2IEwgNTUxLjEyIDM1NC4wNiBMIDU0OS4zNyAzNTAuNTYgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDYzMi45NyAxNDUuNjMgTCA2MzIuOTcgMzA4LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjMyLjk3IDMxMy44OCBMIDYyOS40NyAzMDYuODggTCA2MzIuOTcgMzA4LjYzIEwgNjM2LjQ3IDMwNi44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjU1Ny40OCIgeT0iNjcuNSIgd2lkdGg9IjE1MC45NyIgaGVpZ2h0PSI3OC4xMyIgcng9IjExLjcyIiByeT0iMTEuNzIiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwN3B4OyBtYXJnaW4tbGVmdDogNTU4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTdweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlF1ZXJ5PGJyIC8+SW1hZ2UvVGV4dDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTU3LjQ4IiB5PSI1MzUiIHdpZHRoPSIxNTAuOTciIGhlaWdodD0iNzguMTMiIHJ4PSIxMS43MiIgcnk9IjExLjcyIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDlweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NzRweDsgbWFyZ2luLWxlZnQ6IDU1OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE3cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5SZXRyaWV2ZWQgUmVzdWx0IEltYWdlczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MzIuOTcgMzkzLjEzIEwgNjMyLjk3IDUyOC42NCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDYzMi45NyA1MzMuODkgTCA2MjkuNDcgNTI2Ljg5IEwgNjMyLjk3IDUyOC42NCBMIDYzNi40NyA1MjYuODkgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI1OTEuMDMiIHk9IjUiIHdpZHRoPSI4My44NyIgaGVpZ2h0PSIzMS4yNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODJweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMXB4OyBtYXJnaW4tbGVmdDogNTkycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMjBweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkltYWdlIFJldHJpZXZhbDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzA1Ljg3IiB5PSI1IiB3aWR0aD0iODMuODciIGhlaWdodD0iMzEuMjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDgycHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjFweDsgbWFyZ2luLWxlZnQ6IDMwN3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDIwcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5JbWFnZSBJbmdlc3Rpb248L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjI4My4xMyIgd2lkdGg9IjM1MCIgaGVpZ2h0PSI3MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDM0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMxOHB4OyBtYXJnaW4tbGVmdDogNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBsZWZ0OyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxN3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Mi4gU2VuZCBpbWFnZSBVUkxzIGluIFRPUyB0byBWaWtpbmdEQjsgaW1hZ2VzIHdpbGwgYmUgYXV0b21hdGljYWxseSB2ZWN0b3JpemVkIGFuZCBzdG9yZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDkyIDYzNSBMIDQ5MiA1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iNiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIxOCAxOCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxyZWN0IHg9IjIiIHk9IjE2NSIgd2lkdGg9IjM3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDM2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE3NXB4OyBtYXJnaW4tbGVmdDogNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBsZWZ0OyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxN3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+MS4gVXBsb2FkIHRoZSBpbWFnZSB0byBiZSBpbmRleGVkIGludG8gVE9TPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NDIiIHk9IjIxNSIgd2lkdGg9IjM5MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDM4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyNXB4OyBtYXJnaW4tbGVmdDogNjQ0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGxlZnQ7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE3cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj4zLiBJbnB1dCBxdWVyeSBpbWFnZSBvciB0ZXh0IHRvIHBlcmZvcm0gc2VhcmNoPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTIiIHk9IjQ0NSIgd2lkdGg9IjUwMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDQ5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ1NXB4OyBtYXJnaW4tbGVmdDogNjU0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGxlZnQ7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE3cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj40LiBWZWN0b3IgRGF0YUJhc2UgcmV0dXJucyByZXN1bHQgaW1hZ2VzIG1hdGNoaW5nIHRoZSBxdWVyeTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

<span id="1cea298b"></span>
## 1.4 Scheme advantages


1. **Precise visual matching**: \*\*\*\* With the help of deep\-level feature extraction, images with similar styles, scenes, and objects can be accurately retrieved.

2. **Very Large Efficient Search**: For billions of images, the BytePlus Vector DataBase can complete similarity matching very quickly, doubling the retrieval efficiency.

3. **cross\-modal search**: \*\*\*\* It can not only receive and index new images in real time, but also search with text information, which is convenient for quickly locating and analyzing target materials.


<span id="a6602755"></span>
# 2. Quickly Build

<span id="d29e80ba"></span>
## 2.1 Case scenario and data

Next, we will use the Vector DataBase for text retrieval and image retrieval, that is, enter text or pictures to retrieve the corresponding pictures. This case uses pic_search_1000_images.zip data, which contains 1000 wildlife pictures.

Please download the compressed data package and unzip it. The unzipped image folder needs to be placed in the same directory as the Python code.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0566b538a47c4523923f1327f0a2d1a4~tplv-goo7wpa0wc-image.image" name="pic_search_1000_images.zip">pic_search_1000_images.zip</Attachment>


> This data sample was published on Kaggle by Sourav Banerjee *Animal Image Dataset*Dataset, the data source is: https://www.kaggle.com/datasets/iamsouravbanerjee/animal\-image\-dataset\-90\-different\-animals.


<span id="46aee7b3"></span>
## 2.2 Service provisioning, key and environment preparation

Please note that each of the following steps is necessary to complete a multimodal search and should not be omitted.


1. Vector DataBase account registration and service activation;

2. TOS (Torch Object Storage) service activation: [Go to activate](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1). After activation, you can store images in your TOS bucket.

3. Authorize the Vector DataBase service to access your TOS permissions：[To authorize](https://console.byteplus.com/iam/service/attach_role/?ServiceName=ml_platform). After authorization, Vector DataBase can access the images in TOS;

4. Obtain the security credentials Access Key ID (abbreviated as AK) and Secret Access Key (abbreviated as SK): [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey);

5. Python 3.7 and above are recommended.

6. To prepare the runtime environment, enter the following command at terminal:



|**Vector DataBase SDK installation** |pip3 install \-\-upgrade volcengine |Services for using Vector DataBase |
|---|---|---|
|**TOS installation** |pip3 install \-\-upgrade tos |For using TOS services |
|**Installation requests** |pip3 install \-\-upgrade requests |HTTP request library |
|**AioHTTP installation** |pip3 install \-\-upgrade aiohttp |Asynchronous HTTP communication framework |
|**TQDM installation** |pip3 install \-\-upgrade tqdm |Used for progress bar display |


<span id="2c84fe64"></span>
## 2.3 Data preparation

<span id="31abf19a"></span>
### 2.3.1 create a TOS bucket

Initialize the Python SDK of the TOS service here, and then create a TOS bucket named "best\-practice\-pic\-search\-tos".

> **What is TOS?** 

> TOS (Torch Object Storage) is a massive, secure, low\-cost, easy\-to\-use, highly reliable and highly available distributed cloud storage service provided by BytePlus. You can use TOS in various forms through RESTful API interfaces, SDKs and tools. Through the network, you can manage and access data on BytePlus TOS from any application, anytime, anywhere.

> More information on TOS can be found at [TOS Help Documentation](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos).


 **【Precautions】** 


* bucket [Naming Convention](https://docs.byteplus.com/en/docs/tos/docs-common-concepts) As follows:

   * Only lowercase letters a to z, numbers, and dashes (\-) can be included.

   * The beginning and end can only be numbers or letters.

   * The length must be between 3 and 63 characters.

* When accessing TOS through other BytePlus products in the same region as TOS, it is recommended that you use the intranet endpoint. For more information on regions and endpoints, see [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a bucket, you need to ensure that your account has `tos: CreateBucket`permission. You can grant appropriate permissions through IAM policies. For specific steps, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


```Python
## 2.3.1 create a TOS bucket
import tos # pip3 install --upgrade tos


## ↓↓Input Section↓↓ ##
ak = "*"  # Enter your Access Key here, e.g., ak = "your-ak", make sure to keep the double quotes
sk = "*"  # Enter your Secret Key here, e.g., sk = "your-sk", make sure to keep the double quotes

# Fill in "your endpoint" and "your region" with the corresponding Endpoint of the region where your Bucket is located. Taking the example of North China 2 (Beijing), fill in "your endpoint" with tos-cn-beijing.volces.com and "your region" with cn-beijing.
# https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint
endpoint = "tos-ap-southeast-1.bytepluses.com"
region = "ap-southeast-1"
bucket_name = "best-practice-pic-search-tos"
## ↑↑Input Section↑↑ ##


try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Specify the storage class when creating a storage space, optional parameter storage_class
    # Specify the bucket access permission when creating a storage space, optional parameter acl
    # Specify the bucket AZ redundancy when creating a storage space, optional parameter az_redundancy
    # Use the configuration of bucket as standard storage type, private access permission, and 3AZ data redundancy as an example.
    client.create_bucket(bucket_name, acl=tos.ACLType.ACL_Private,
                         storage_class=tos.StorageClassType.Storage_Class_Standard,
                         az_redundancy=tos.AzRedundancyType.Az_Redundancy_Multi_Az)
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, catch server error, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # request id can be used to locate specific issues, it is strongly recommended to save it in the log.
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


At this point, your TOS bucket has been successfully created.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dfe36f3953f448bbbabd1e2f03ab8ab~tplv-goo7wpa0wc-image.image) </span>

<span id="7ba2cf03"></span>
### 2.3.2 upload picture folder

Upload the image folder pic_search_1000_images the TOS bucket created in the previous step, so you need to put pic_search_1000_images folder and the Python code in the same directory.

You need to fill in your ak and sk at the beginning of the code.

```Python
## 2.3.2 upload picture folder
import tos  # pip3 install --upgrade tos
import os
from tqdm import tqdm  # pip3 install --upgrade tqdm, used for progress bar display


## ↓↓Input Section↓↓ ##
ak = "*"  # Enter your Access Key here, e.g., ak = "your-ak", make sure to keep the double quotes
sk = "*"  # Enter your Secret Key here, e.g., sk = "your-sk", make sure to keep the double quotes

# Fill in "your endpoint" and "your region" with the corresponding Endpoint of the region where your Bucket is located. Taking the example of North China 2 (Beijing), fill in "your endpoint" with tos-cn-beijing.volces.com and "your region" with cn-beijing.
# https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint
endpoint = "tos-ap-southeast-1.bytepluses.com"
region = "ap-southeast-1"
bucket_name = "best-practice-pic-search-tos"  # TOS bucket name
file_dir = "pic_search_1000_images"  # Current local directory containing the files
## ↑↑Input Section↑↑ ##


# Start uploading images
try:
    # Create a TosClientV2 object. All operations on the bucket and objects are performed through TosClientV2.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Recursively retrieve all file paths
    def get_all_files(root_dir):
        file_paths = []
        for root, dirs, files in os.walk(root_dir):
            for file in files:
                file_paths.append(os.path.join(root, file))
        return file_paths

    all_files = get_all_files(file_dir)

    # Use tqdm to display the progress bar
    for file_path in tqdm(all_files, desc="Image Upload Progress", unit="file"):
        client.put_object_from_file(bucket_name, file_path, file_path)

except tos.exceptions.TosClientError as e:
    # Operation failed, client-side exception caught. Usually caused by invalid request parameters or network errors.
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server-side exception caught. Detailed error info can be obtained from the response.
    print('fail with server error, code: {}'.format(e.code))
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


After the script finishes running, you will see that the image folder has been successfully uploaded to your TOS bucket.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a099c8dd74248c8bd8ded3deae512ea~tplv-goo7wpa0wc-image.image) </span>

<span id="6e41c20c"></span>
### 2.3.3 export the path of the image in TOS

When using Vector DataBase for image retrieval, instead of passing the image itself directly to Vector DataBase, the address of the image in the TOS bucket is stored in Vector DataBase. Vector DataBase will access the TOS address of the image, automatically vectorize the image, and also store the vector in Vector DataBase.

The purpose of the following code is to export the tos address of the picture you save in TOS and save it as a jsonl file.

You need to fill in your ak and sk at the beginning of the code.

```Python
## 2.3.3 export the path of the image in TOS
import tos  # pip3 install --upgrade tos
import json


## ↓↓Input Section↓↓ ##
ak = "*" # Enter your Access Key here, e.g., ak = "your-ak", make sure to keep the double quotes
sk = "" # Enter your Secret Key here, e.g., sk = "your-sk", make sure to keep the double quotes
# Fill in "your endpoint" and "your region" with the corresponding Endpoint of the region where your Bucket is located. Taking the example of North China 2 (Beijing), fill in "your endpoint" with tos-cn-beijing.volces.com and "your region" with cn-beijing.
endpoint = "tos-ap-southeast-1.bytepluses.com"
region = "ap-southeast-1"

bucket_name = "best-practice-pic-search-tos"  # TOS bucket name
prefix = "pic_search_1000_images/"  # Prefix, which is your image folder name plus a slash. If uploading images directly (not in a folder), set prefix to an empty string: prefix = ""
output_file = "best_practice_pic_search_1000_image.jsonl"  # Output file
## ↑↑Input Section↑↑ ##


try:
    # Create a TosClientV2 object. All operations on the bucket and objects are performed through TosClientV2.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    truncated = True
    continuation_token = ''
    image_id = 1  # Initial image ID

    # Open file for writing in JSONL format
    with open(output_file, "w", encoding="utf-8") as f:
        while truncated:
            result = client.list_objects_type2(bucket_name, prefix=prefix, continuation_token=continuation_token)
            for item in result.contents:
                record = {
                    "image_id": str(image_id),
                    "animal_image": f"tos://{bucket_name}/{item.key}"  # Image path format: tos://{bucket}/{object_key}. Can be used for vectorization.
                }
                # Write a line of JSON
                f.write(json.dumps(record, ensure_ascii=False) + "\n")
                image_id += 1

            truncated = result.is_truncated
            continuation_token = result.next_continuation_token

except tos.exceptions.TosClientError as e:
    # Operation failed, client-side exception caught. Usually caused by invalid request parameters or network errors.
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server-side exception caught. Detailed error info can be obtained from the response.
    print('fail with server error, code: {}'.format(e.code))
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


After the code is completed, a file named best_practice_pic_search_1000_image .jsonl is generated in the directory where the code is located.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27ea76094a004065b5be318e7e6d0975~tplv-goo7wpa0wc-image.image" name="best_practice_pic_search_1000_image.jsonl">best_practice_pic_search_1000_image.jsonl</Attachment>


&nbsp;

There are 1000 JSON in the file, each JSON contains the ID of the picture ("image_id") and the tos address of the picture ("animal_image"). The tos address will be passed to Vector DataBase in the following steps. The specific form of JSON is as follows:

```Python
{"image_id": "1", "animal_image": "tos://best-practice-pic-search-tos/pic_search_1000_images/0009fc27d9.jpg"}
```


<span id="1f30e0e3"></span>
## 2.4 Field Configuration and Creating Vector DataBase Collection

The code here is used to configure the fields, and then create a collection in Vector DataBase. The previous image TOS address will be stored in the dataset that will be created soon.

> **What are fields?** 

> * **field definition**: Fields are the basic units in a data table, and each field stores a specific type of data, such as the "name" field stores the name of the person, and the "age" field stores numerical information.

> * **field name**: In the field name ("field_name") of the code below, the "image_id" field is used to store the id of the picture, and the "animal_image" field stores the tos address of the picture.

> * **field type**: Different fields can be configured with different field types ("field_type"), for example, the type of the "image_id" field is "int64", which is a 64\-bit integer\*\*,\*\*The type of the "animal_image" field is "image", that is, it stores an image (TOS address).


You need to fill in your ak and sk at the beginning of the code.

```Python
## 2.4 Field Configuration and Creating Vector DataBase Collection
import json
import sys
import requests  # pip3 install --upgrade requests
from volcengine.auth.SignerV4 import SignerV4  # pip3 install --upgrade volcengine
from volcengine.base.Request import Request  # pip3 install --upgrade volcengine
from volcengine.Credentials import Credentials  # pip3 install --upgrade volcengine


## ↓↓Input Section↓↓ ##
AK = "*" # Enter your Access Key here, e.g., ak = "your-ak", make sure to keep the double quotes
SK = "*" # Enter your Secret Key here, e.g., sk = "your-sk", make sure to keep the double quotes
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com"
# https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
# https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)

COLLECTION_NAME = "best_practice_pic_search" # Name of the dataset (collection)
DESCRIPTION = "Demonstrates Vector DataBase's text-to-image and image-to-image capabilities" # Description of the dataset

## ↑↑Input Section↑↑ ##


# Signature generation function
def prepare_request(method, path, ak, sk, params=None, data=None, doseq=0):
    if params:
        for key in params:
            if (
                    type(params[key]) == int
                    or type(params[key]) == float
                    or type(params[key]) == bool
            ):
                params[key] = str(params[key])
            elif sys.version_info[0] != 3:
                if type(params[key]) == unicode:
                    params[key] = params[key].encode("utf-8")
            elif type(params[key]) == list:
                if not doseq:
                    params[key] = ",".join(params[key])
    r = Request()
    r.set_shema("https")
    r.set_method(method)
    r.set_connection_timeout(10)
    r.set_socket_timeout(10)
    mheaders = {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "Host": "api-vikingdb.mlp.ap-mya.byteplus.com",
        # https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
        # https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)
    }
    r.set_headers(mheaders)
    if params:
        r.set_query(params)
    r.set_host("api-vikingdb.mlp.ap-mya.byteplus.com")
    # https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
    # https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)
    r.set_path(path)
    if data is not None:
        r.set_body(json.dumps(data))
    # Generate signature
    credentials = Credentials(ak, sk, "air", "ap-southeast-1")
    SignerV4.sign(r, credentials)
    return r

# Create Collection
request_params = {
    "collection_name": COLLECTION_NAME,  # Name of the dataset (collection)
    "description": DESCRIPTION,  # Description of the dataset
    "primary_key": "image_id",  # Declare "image_id" as the primary key
    "fields": [  # Define and declare each field
        {
            "field_name": "image_id",
            "field_type": "int64",
        },
        {
            "field_name": "animal_image",
            "field_type": "image",
        },
        {
            "field_name": "other_text",
            "field_type": "text",
        }
    ],
    "vectorize": [  # Fields to be vectorized
        {
            "dense": {
                "image_field": "animal_image",
                "text_field": "other_text",
                "model_name": "bge-visualized-m3",
                "dim": 1024
            }
        }
    ]
}

# Generate and sign the request using prepare_request
info_collection_req = prepare_request(
    method="POST",
    path="/api/collection/create",
    ak=AK,
    sk=SK,
    data=request_params,
)

# Send the request
r = requests.request(
    method=info_collection_req.method,
    url="https://{}{}".format(DOMAIN, info_collection_req.path),
    headers=info_collection_req.headers,
    params=info_collection_req.query,
    data=info_collection_req.body,
)

# Print the result
print(r.text)
```


After the dataset is successfully created, the dataset can be seen on the Vector DataBase web page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcbdfa075665403baff26d3dc631579a~tplv-goo7wpa0wc-image.image) </span>

<span id="b9dd6830"></span>
## 2.5 Import image TOS address into Vector DataBase collection

Here the code uploads the picture tos address in best_practice_pic_search_1000_image .jsonl to the "animal_image" field in best_practice_pic_search collection.

When the TOS address is passed into Vector DataBase, the corresponding image will be automatically vectorized (Embedding), so that the vector similarity can be retrieved later. The rate of vectorization here is limited, about 15 images per second.

You need to fill in your ak and sk at the beginning of the code.

```Python
## 2.5 Import image TOS address into Vector DataBase collection
import json
import sys
from tqdm import tqdm  # pip install --upgrade tqdm
import requests  # pip3 install --upgrade requests
from volcengine.auth.SignerV4 import SignerV4  # pip3 install --upgrade volcengine
from volcengine.base.Request import Request  # pip3 install --upgrade volcengine
from volcengine.Credentials import Credentials  # pip3 install --upgrade volcengine

## ↓↓Input Section↓↓ ##
AK = "*" # Enter your Access Key here, e.g., ak = "your-ak", make sure to keep the double quotes
SK = "*" # Enter your Secret Key here, e.g., sk = "your-sk", make sure to keep the double quotes
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com"
# https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
# https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)

COLLECTION_NAME = "best_practice_pic_search" # Name of the dataset (collection)
FILE_PATH = "best_practice_pic_search_1000_image.jsonl"
## ↑↑Input Section↑↑ ##



# Signature generation function
def prepare_request(method, path, ak, sk, params=None, data=None, doseq=0):
    if params:
        for key in params:
            if (
                    type(params[key]) == int
                    or type(params[key]) == float
                    or type(params[key]) == bool
            ):
                params[key] = str(params[key])
            elif sys.version_info[0] != 3:
                if type(params[key]) == unicode:
                    params[key] = params[key].encode("utf-8")
            elif type(params[key]) == list:
                if not doseq:
                    params[key] = ",".join(params[key])
    r = Request()
    r.set_shema("https")
    r.set_method(method)
    r.set_connection_timeout(10)
    r.set_socket_timeout(10)
    mheaders = {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "Host": "api-vikingdb.mlp.ap-mya.byteplus.com",
        # https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
        # https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)
    }
    r.set_headers(mheaders)
    if params:
        r.set_query(params)
    r.set_host("api-vikingdb.mlp.ap-mya.byteplus.com")
    # https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
    # https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)
    r.set_path(path)
    if data is not None:
        r.set_body(json.dumps(data))
    # Generate signature
    credentials = Credentials(ak, sk, "air", "ap-southeast-1")
    SignerV4.sign(r, credentials)
    return r


def send_batch(batch_data, collection_name, ak, sk, domain):
    """
    Upload a batch of data to the specified Collection
    """
    # Construct request payload
    request_params = {
        "collection_name": collection_name,
        "fields": batch_data
    }

    # Generate a signed request
    req_data = prepare_request(
        method="POST",
        path="/api/collection/upsert_data",
        ak=ak,
        sk=sk,
        data=request_params,
    )

    # Construct the full URL and send the request
    url = f"https://{domain}{req_data.path}"
    response = requests.request(
        method=req_data.method,
        url=url,
        headers=req_data.headers,
        data=req_data.body,
    )

    try:
        resp_json = response.json()
    except Exception as e:
        # Output error if response cannot be parsed as JSON
        tqdm.write("Response for this batch could not be parsed as JSON: " + response.text)
        return

    # Output response if message is not "success"
    if resp_json.get("message") != "success":
        tqdm.write("Response for this batch: " + response.text)

def batch_upload(file_path, collection_name, ak, sk, domain, batch_size):
    """
    Read data from the specified JSONL file and upload in batches of batch_size.
    Each line in the file should look like:
        {"image_id": "1", "animal_image": "tos://bucket/path/to/image.jpg"}
    """
    batch = []
    # Count total lines for tqdm progress bar
    with open(file_path, "r", encoding="utf-8") as f:
        total_lines = sum(1 for _ in f)

    with open(file_path, "r", encoding="utf-8") as f:
        for line in tqdm(f, total=total_lines, desc="Upload Progress"):
            line = line.strip()
            if not line:
                continue
            try:
                record = json.loads(line)
                # If the field "other_text" is missing or empty, assign a single space as default
                if not record.get("other_text"):
                    record["other_text"] = " "
                batch.append(record)
            except Exception as e:
                tqdm.write(f"Failed to parse this line: {line}\nError: {e}")
                continue

            # Upload once batch_size is reached
            if len(batch) >= batch_size:
                send_batch(batch, collection_name, ak, sk, domain)
                batch = []  # Reset batch

    # Handle any remaining data not reaching batch_size
    if batch:
        send_batch(batch, collection_name, ak, sk, domain)

if __name__ == "__main__":
    batch_upload(FILE_PATH, COLLECTION_NAME, AK, SK, DOMAIN, batch_size=5)
```


The data was uploaded successfully. It may take some time for the data to sync. You can proceed with the next step to create an index, and come back later to check the updated data volume in the `best_practice_pic_search` collection on the Vector Database – Collection page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99ab371ac406459a8a8ce4b3fd0eb3d2~tplv-goo7wpa0wc-image.image) </span>

<span id="94a95be3"></span>
## 2.6 Creating an index

This code creates an index called best_practice_pic_search_index for the data just now. An index is a quick lookup structure for certain fields in the data, and a Vector DataBase index supports mixed search requirements for vectors and scalars.

> **Vector index parameter description:** 

> * **Distance**: Refers to the algorithm for measuring the distance (similarity) between vectors, you can choose IP (calculate the inner product of vectors, the larger the inner product, the higher the degree of similarity), L2 (calculate the Euclidean distance between vectors, the smaller the Euclidean distance, the higher the vector similarity), COSINE (calculate the cosine similarity between vectors, the greater the cosine similarity, the higher the vector similarity).

> * **index_type**: Vector index type, the types that can be selected are HNSW, HNSW_HYBRID, FLAT, IVF, DISKANN. In this case, the HNSW Algorithm is selected. HNSW reduces the number of nodes that need to be visited during the search process by building a multi\-layer network, and realizes fast and efficient search for nearest neighbors, which is suitable for scenarios that require high search efficiency.

> * **Quant**: Quantization method refers to the compression method of vectors in the index, which can reduce the complexity of the similarity calculation between vectors. Optional types are Int8, Float, Fix16, PQ. In this case, choose Float, that is, do not compress the vector and preserve the full precision of the vector.

> * **cpu_quota**: Refers to the CPU quota consumed by index retrieval, 1CPU core is about 100QPS, and the value range is 2 to 10240.

> * **Description**: A description of the index.


You need to fill in your ak and sk at the beginning of the code.

```Python
## 2.6 Creating an index
import json
import sys
import requests  # pip3 install --upgrade requests
from volcengine.auth.SignerV4 import SignerV4  # pip3 install --upgrade volcengine
from volcengine.base.Request import Request  # pip3 install --upgrade volcengine
from volcengine.Credentials import Credentials  # pip3 install --upgrade volcengine


## ↓↓Input Section↓↓ ##
AK = "*" # Enter your Access Key here, e.g., ak = "your-ak", make sure to keep the double quotes
SK = "*" # Enter your Secret Key here, e.g., sk = "your-sk", make sure to keep the double quotes
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com"
# https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
# https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)
COLLECTION_NAME = "best_practice_pic_search"
## ↑↑Input Section↑↑ ##

# Signature generation function
def prepare_request(method, path, ak, sk, params=None, data=None, doseq=0):
    if params:
        for key in params:
            if (
                    type(params[key]) == int
                    or type(params[key]) == float
                    or type(params[key]) == bool
            ):
                params[key] = str(params[key])
            elif sys.version_info[0] != 3:
                if type(params[key]) == unicode:
                    params[key] = params[key].encode("utf-8")
            elif type(params[key]) == list:
                if not doseq:
                    params[key] = ",".join(params[key])
    r = Request()
    r.set_shema("https")
    r.set_method(method)
    r.set_connection_timeout(10)
    r.set_socket_timeout(10)
    mheaders = {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "Host": "api-vikingdb.mlp.ap-mya.byteplus.com",
        # https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
        # https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)
    }
    r.set_headers(mheaders)
    if params:
        r.set_query(params)
    r.set_host("api-vikingdb.mlp.ap-mya.byteplus.com")
    # https://api-vikingdb.mlp.cn-hongkong.bytepluses.com(for Hong Kong)
    # https://api-vikingdb.mlp.ap-mya.byteplus.com (for Johor)
    r.set_path(path)
    if data is not None:
        r.set_body(json.dumps(data))
    # Generate signature
    credentials = Credentials(ak, sk, "air", "ap-southeast-1")
    SignerV4.sign(r, credentials)
    return r



# Create Index
request_params = {
    "collection_name": "best_practice_pic_search",
    "index_name": "best_practice_pic_search_index",
    "cpu_quota": 1,
    "description": "Demonstrates Vector DataBase's image-to-image and text-to-image capabilities",
    "vector_index": {
        "index_type": "hnsw",
        "distance": "cosine",
        "quant": "int8",
    },
}

# Generate and sign the request using prepare_request
info_req = prepare_request(
    method="POST",
    path="/api/index/create",
    ak=AK,
    sk=SK,
    data=request_params,
)

# Send the request
r = requests.request(
    method=info_req.method,
    url="https://{}{}".format(DOMAIN, info_req.path),
    headers=info_req.headers,
    data=info_req.body,
)

# Print the result
print(r.text)
```


After the code runs successfully, enter the indexes page on the Vector DataBase web page, and you can see the index best_practice_pic_search_index. Generally, when it is just created, its execution status is "initializing". After a while, refresh the page, and the status will become "ready". Next, you can search for pictures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fde4974c1b554f208ea82ead3b69fd57~tplv-goo7wpa0wc-image.image) </span>

<span id="5ade05f1"></span>
## 2.7 Search by picture & search by text

After successfully completing the above steps, you can use the API to search, and you can also perform quick search on the page.


1. Click "Retrival Test" to the right of the corresponding index (best_practice_pic_search_index).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08f491b997f848b887dad43ec8e57d56~tplv-goo7wpa0wc-image.image) </span>


2. Enter text and query for pictures.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a54632347e9945f79a69a2275b27c45e~tplv-goo7wpa0wc-image.image) </span>


3. You can also enter a picture to retrieve pictures.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/499307e1c3af43aeb228fcb739f0e290~tplv-goo7wpa0wc-image.image) </span>

Note that if you delete the image in the TOS bucket or the TOS bucket itself, the image cannot be displayed during image retrieval.
