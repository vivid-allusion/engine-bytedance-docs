---
title: "Billing Item"
product: "Dramagic"
product_code: "Dramagic"
source: "https://docs.byteplus.com/en/docs/Dramagic/ResourcePackages"
---

**Billing Item Description**

> **Description**

> **To ensure Users obtain superior model capabilities and service experience, the platform will continuously update the points consumption rules for each model based on model capabilities, service costs, and market conditions.**

## Image Generation

|**Module** |**Feature Module** |**Model name** |**Parameter Select** |**Billing Item (Unit:  Points/Image)**  |**Equivalent Price (Unit: $/Image)**  |**Billing Rule Description** |
|---|---|---|---|---|---|---|
|<br>Image generation<br> |Scene image, prop image Generation (text\-to\-image, image\-to\-image, multi\-image reference Generation) |Seedream\-5.0\-Lite |\- |3 |0.03 |Billed by the number of successfully output images.<br><br>Multi\-image scenes are billed by the actual number of generated images.<br><br>Only successfully generated images are billed.<br><br>Images not output due to review or other reasons are not billed. |
|||Seedream\-4.5 |\- |4 |0.04 ||
||Character image (main image + three\-view) Generation (text\-to\-image, image\-to\-image, multi\-image reference Generation) |Seedream\-5.0\-Lite |\- |6 |0.06 ||
|||Seedream\-4.5 |\- |8 |0.08 ||
||Character image, scene image, prop image Generation (text\-to\-image, image\-to\-image, multi\-image reference Generation) |Seedream 5.0 Pro |1K |4 |0.05 ||
||||2K |9 |0.09 ||
|||Nano\-Banana\-Pro |1k/2k |20 |0.20 ||
||||4k |35 |0.35 ||
|||GPT\-Image\-2 |Low\-1k |3 |0.03 ||
||||Low\-2k |4 |0.04 ||
||||Medium\-1k |8 |0.08 ||
||||Medium\-2k |18 |0.18 ||
||||High\-1k |26 |0.26 ||
||||High\-2k |65 |0.65 ||

## Video Generation

|<br>**Category**<br> |<br>**Feature Module**<br> |<br>**Model name**<br> |<br>**Resolution**<br> |<br>**Billing Price (Unit: Points/sec)**<br> |<br>**Equivalent Price (Unit: $/sec)**<br> |
|---|---|---|---|---|---|
|<br>Video generation<br> |<br>Shot video Generation (without video input)<br> |<br>Seedance\-2.5<br> |<br>1080P<br> |<br>85<br> |0.85 |
||||<br>720P<br> |<br>35<br> |0.35 |
||||<br>480P<br> |<br>16<br> |0.16 |
|||<br>Seedance\-2.0<br> |<br>4k<br> |<br>117<br> |1.17 |
||||<br>1080P<br> |<br>56<br> |0.56 |
||||<br>720P<br> |<br>23<br> |0.23 |
||||<br>480P<br> |<br>11<br> |0.11 |
|||<br>Seedance\-2.0\-Fast<br> |<br>720P<br> |<br>18<br> |0.18 |
||||<br>480P<br> |<br>8<br> |0.08 |
|||<br>Seedance\-2.0\-Mini<br> |<br>720P<br> |<br>11<br> |0.11 |
||||<br>480P<br> |<br>5<br> |0.05 |
|<br><br> |<br>Shot video Generation (with video input)<br><br><br><br>When input covers video, the points consumed per shot = (input video duration + output video duration) \* unit price<br><br><br><br><br><br><br><br>Note: When input covers video, there is a minimum points consumption limit for different video output durations. If the points consumed per shot are less than the minimum points consumption limit, the minimum points will be deducted.<br> |<br>Seedance\-2.5<br> |<br>1080P<br> |<br>51<br> |0.51 |
||||<br>720P<br> |<br>21<br> |0.21 |
||||<br>480P<br> |<br>9<br> |0.09 |
|||<br>Seedance\-2.0<br> |<br>4k<br> |<br>70<br> |0.70 |
||||<br>1080P<br> |<br>34<br> |0.34 |
||||<br>720P<br> |<br>14<br> |0.14 |
||||<br>480P<br> |<br>6<br> |0.06 |
|||<br>Seedance\-2.0\-Fast<br> |<br>720P<br> |<br>11<br> |0.11 |
||||<br>480P<br> |<br>5<br> |0.05 |
|||<br>Seedance\-2.0\-Mini<br> |<br>720P<br> |<br>7<br> |0.07 |
||||<br>480P<br> |<br>3<br> |0.03 |

> **Notice**

> When input covers video, the points consumed per shot = (input video duration + output video duration) \* unit price

> When input covers video, there is a minimum points consumption limit for different video output durations. If the points consumed per shot are less than the minimum points consumption limit, the minimum points will be deducted.

|<br>**When input covers video,  minimum points consumption limits for different video output Durations**<br> |||||||
|---|---|---|---|---|---|---|
|<br>Resolution<br> |<br>Video output Duration<br> |If the input video total duration of video is less than this value, the minimum points will be deducted. |Seedance 2.5 Minimum points consumption |Seedance 2.0 Minimum points consumption |Seedance 2.0 fast Minimum points consumption  |Seedance 2.0 mini Minimum points consumption |
|<br>480P<br> |<br>4<br> |<br>3<br> |<br>63<br> |<br>42<br> |<br>35<br> |<br>21<br> |
||<br>5<br> |<br>4<br> |<br>81<br> |<br>54<br> |<br>45<br> |<br>27<br> |
||<br>6<br> |<br>4<br> |<br>90<br> |<br>60<br> |<br>50<br> |<br>30<br> |
||<br>7<br> |<br>5<br> |<br>108<br> |<br>72<br> |<br>60<br> |<br>36<br> |
||<br>8<br> |<br>6<br> |<br>126<br> |<br>84<br> |<br>70<br> |<br>42<br> |
||<br>9<br> |<br>6<br> |<br>135<br> |<br>90<br> |<br>75<br> |<br>45<br> |
||<br>10<br> |<br>7<br> |<br>153<br> |<br>102<br> |<br>85<br> |<br>51<br> |
||<br>11<br> |<br>8<br> |<br>171<br> |<br>114<br> |<br>95<br> |<br>57<br> |
||<br>12<br> |<br>8<br> |<br>180<br> |<br>120<br> |<br>100<br> |<br>60<br> |
||<br>13<br> |<br>9<br> |<br>198<br> |<br>132<br> |<br>110<br> |<br>66<br> |
||<br>14<br> |<br>10<br> |<br>216<br> |<br>144<br> |<br>120<br> |<br>72<br> |
||<br>15<br> |<br>10<br> |<br>225<br> |<br>150<br> |<br>125<br> |<br>75<br> |
||<br>16<br> |<br>11<br> |<br>243<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>17<br> |<br>12<br> |<br>261<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>18<br> |<br>12<br> |<br>270<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>19<br> |<br>13<br> |<br>288<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>20<br> |<br>14<br> |<br>306<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>21<br> |<br>14<br> |<br>315<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>22<br> |<br>15<br> |<br>333<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>23<br> |<br>16<br> |<br>351<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>24<br> |<br>16<br> |<br>360<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>25<br> |<br>17<br> |<br>378<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>26<br> |<br>18<br> |<br>396<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>27<br> |<br>18<br> |<br>405<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>28<br> |<br>19<br> |<br>423<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>29<br> |<br>20<br> |<br>441<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>30<br> |<br>20<br> |<br>450<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
|<br>720P<br> |<br>4<br> |<br>3<br> |<br>147<br> |<br>98<br> |<br>77<br> |<br>49<br> |
||<br>5<br> |<br>4<br> |<br>189<br> |<br>126<br> |<br>99<br> |<br>63<br> |
||<br>6<br> |<br>4<br> |<br>210<br> |<br>140<br> |<br>110<br> |<br>70<br> |
||<br>7<br> |<br>5<br> |<br>252<br> |<br>168<br> |<br>132<br> |<br>84<br> |
||<br>8<br> |<br>6<br> |<br>294<br> |<br>196<br> |<br>154<br> |<br>98<br> |
||<br>9<br> |<br>6<br> |<br>315<br> |<br>210<br> |<br>165<br> |<br>105<br> |
||<br>10<br> |<br>7<br> |<br>357<br> |<br>238<br> |<br>187<br> |<br>119<br> |
||<br>11<br> |<br>8<br> |<br>399<br> |<br>266<br> |<br>209<br> |<br>133<br> |
||<br>12<br> |<br>8<br> |<br>420<br> |<br>280<br> |<br>220<br> |<br>140<br> |
||<br>13<br> |<br>9<br> |<br>462<br> |<br>308<br> |<br>242<br> |<br>154<br> |
||<br>14<br> |<br>10<br> |<br>504<br> |<br>336<br> |<br>264<br> |<br>168<br> |
||<br>15<br> |<br>10<br> |<br>525<br> |<br>350<br> |<br>275<br> |<br>175<br> |
||<br>16<br> |<br>11<br> |<br>567<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>17<br> |<br>12<br> |<br>609<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>18<br> |<br>12<br> |<br>630<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>19<br> |<br>13<br> |<br>672<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>20<br> |<br>14<br> |<br>714<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>21<br> |<br>14<br> |<br>735<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>22<br> |<br>15<br> |<br>777<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>23<br> |<br>16<br> |<br>819<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>24<br> |<br>16<br> |<br>840<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>25<br> |<br>17<br> |<br>882<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>26<br> |<br>18<br> |<br>924<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>27<br> |<br>18<br> |<br>945<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>28<br> |<br>19<br> |<br>987<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>29<br> |<br>20<br> |<br>1029<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>30<br> |<br>20<br> |<br>1050<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
|<br>1080P<br> |<br>4<br> |<br>3<br> |<br>357<br> |<br>238<br> |<br>NA<br> |<br>NA<br> |
||<br>5<br> |<br>4<br> |<br>459<br> |<br>306<br> |<br>NA<br> |<br>NA<br> |
||<br>6<br> |<br>4<br> |<br>510<br> |<br>340<br> |<br>NA<br> |<br>NA<br> |
||<br>7<br> |<br>5<br> |<br>612<br> |<br>408<br> |<br>NA<br> |<br>NA<br> |
||<br>8<br> |<br>6<br> |<br>714<br> |<br>476<br> |<br>NA<br> |<br>NA<br> |
||<br>9<br> |<br>6<br> |<br>765<br> |<br>510<br> |<br>NA<br> |<br>NA<br> |
||<br>10<br> |<br>7<br> |<br>867<br> |<br>578<br> |<br>NA<br> |<br>NA<br> |
||<br>11<br> |<br>8<br> |<br>969<br> |<br>646<br> |<br>NA<br> |<br>NA<br> |
||<br>12<br> |<br>8<br> |<br>1020<br> |<br>680<br> |<br>NA<br> |<br>NA<br> |
||<br>13<br> |<br>9<br> |<br>1122<br> |<br>748<br> |<br>NA<br> |<br>NA<br> |
||<br>14<br> |<br>10<br> |<br>1224<br> |<br>816<br> |<br>NA<br> |<br>NA<br> |
||<br>15<br> |<br>10<br> |<br>1275<br> |<br>850<br> |<br>NA<br> |<br>NA<br> |
||<br>16<br> |<br>11<br> |<br>1377<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>17<br> |<br>12<br> |<br>1479<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>18<br> |<br>12<br> |<br>1530<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>19<br> |<br>13<br> |<br>1632<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>20<br> |<br>14<br> |<br>1734<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>21<br> |<br>14<br> |<br>1785<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>22<br> |<br>15<br> |<br>1887<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>23<br> |<br>16<br> |<br>1989<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>24<br> |<br>16<br> |<br>2040<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>25<br> |<br>17<br> |<br>2142<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>26<br> |<br>18<br> |<br>2244<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>27<br> |<br>18<br> |<br>2295<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>28<br> |<br>19<br> |<br>2397<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>29<br> |<br>20<br> |<br>2499<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
||<br>30<br> |<br>20<br> |<br>2550<br> |<br>NA<br> |<br>NA<br> |<br>NA<br> |
|<br>4k<br> |<br>4<br> |<br>3<br> |<br>NA<br> |<br>490<br> |<br>NA<br> |<br>NA<br> |
||<br>5<br> |<br>4<br> |<br>NA<br> |<br>630<br> |<br>NA<br> |<br>NA<br> |
||<br>6<br> |<br>4<br> |<br>NA<br> |<br>700<br> |<br>NA<br> |<br>NA<br> |
||<br>7<br> |<br>5<br> |<br>NA<br> |<br>840<br> |<br>NA<br> |<br>NA<br> |
||<br>8<br> |<br>6<br> |<br>NA<br> |<br>980<br> |<br>NA<br> |<br>NA<br> |
||<br>9<br> |<br>6<br> |<br>NA<br> |<br>1050<br> |<br>NA<br> |<br>NA<br> |
||<br>10<br> |<br>7<br> |<br>NA<br> |<br>1190<br> |<br>NA<br> |<br>NA<br> |
||<br>11<br> |<br>8<br> |<br>NA<br> |<br>1330<br> |<br>NA<br> |<br>NA<br> |
||<br>12<br> |<br>8<br> |<br>NA<br> |<br>1400<br> |<br>NA<br> |<br>NA<br> |
||<br>13<br> |<br>9<br> |<br>NA<br> |<br>1540<br> |<br>NA<br> |<br>NA<br> |
||<br>14<br> |<br>10<br> |<br>NA<br> |<br>1680<br> |<br>NA<br> |<br>NA<br> |
||<br>15<br> |<br>10<br> |<br>NA<br> |<br>1750<br> |<br>NA<br> |<br>NA<br> |

## Video  Enhancement

|<br>**Category**<br> |<br>**Function Module**<br> |<br>**Target resolution**<br> |<br>**Billing Price (Unit: Points/sec)**<br> |<br>**Equivalent Price (Unit: $/sec)**<br> |
|---|---|---|---|---|
|<br>Video enhancement<br> |<br>Improve resolution for videos<br> |720P |<br>1<br> |0.01 |
|||1080P |<br>2<br> |0.02 |
|||2K |<br>3<br> |0.03 |
|||4K |<br>6<br> |0.06 |
