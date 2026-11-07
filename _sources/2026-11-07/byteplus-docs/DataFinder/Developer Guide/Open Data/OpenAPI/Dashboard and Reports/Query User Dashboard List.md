---
title: "Query User Dashboard List"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_User_Dashboard_List"
---

<span id="b1b2bad5"></span>
## Request description

**Path**: \*\*\*\* /openapi/v1/{app_id}/dashboards/all

**Method**: GET

**Content\-type**: application/json

<span id="3358c6ec"></span>
## Request parameters

**Path\-parameters**: Just refer to the public parameters[API Description and Public Parameters](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters_Dashboard_Reports)

<span id="7e10bc7b"></span>
## return parameters

**Response**:

```json
{
    "code":200,
    "data":[
        {
            "is_core":false,
            "creator":"Data Ranger",
            "partner_info":{},
            "created_at":1568171124,
            "filters":[],
            "is_default":false,
            "partners":[],
            "extra":{},
            "name":"Core data overview",
            "is_public":true,
            "is_subscribed":false,
            "app_id":164314,
            "dashboard_id":"6735243691952177675",
            "status":1
        }
    ],
    "message":"success"
}
```


Field meaning description:

Data returns a JSON list with descriptions for key fields


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|name |string |Yes |core data overview |Dashboard name |
|dashboard_id |string |Yes |6735243691952177675 |Dashboard ID |


<span id="42633b62"></span>
## **Request example**

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7)the language SDK provides a similar interface

Call (Python):

```python
For example, get the user dashboard of app_id= 164314
res = bc.data_finder('/openapi/v1/164314/dashboards/all', method='get')
print(res.content)
```


<span id="18619e4b"></span>
## Back to example

Return result:

```json
{
    "code":200,
    "data":[
        {
            "is_core":false,
            "creator":"Data Ranger",
            "partner_info":{

            },
            "created_at":1568171124,
            "filters":[

            ],
            "is_default":false,
            "partners":[
                "Data Ranger1",
                "Data Ranger2",
                "Data Ranger3",
                "Data Ranger4",
                "Data Ranger5",
                "Data Ranger6",
                "Data Ranger7",
                "Data Ranger8",
                "Data Ranger9",
                "Data Ranger10",
                "Data Ranger11",
                "Data Ranger12",
                "Data Ranger13"
            ],
            "extra":{

            },
            "name":"Core data overview",
            "is_public":true,
            "is_subscribed":false,
            "app_id":164314,
            "dashboard_id":"6735243691952177675",
            "status":1
        },
        {
            "is_core":false,
            "creator":"Data Ranger",
            "partner_info":{

            },
            "created_at":1568707880,
            "filters":[

            ],
            "is_default":false,
            "partners":[
                "Data Ranger1",
                "Data Ranger2",
                "Data Ranger3",
                "Data Ranger4",
                "Data Ranger5",
                "Data Ranger6",
                "Data Ranger7",
                "Data Ranger8",
                "Data Ranger9",
                "Data Ranger10",
                "Data Ranger11",
                "Data Ranger12",
                "Data Ranger13",
                "Data Ranger14",
                "Data Ranger15",
                "Data Ranger16",
                "Data Ranger17",
                "Data Ranger18",
                "Data Ranger19",
                "Data Ranger20",
                "Data Ranger21",
                "Data Ranger22",
                "Data Ranger23",
                "Data Ranger24",
                "Data Ranger25",
                "Data Ranger26",
                "Data Ranger27",
                "Data Ranger28",
                "Data Ranger29"
            ],
            "extra":{

            },
            "name":"lalala",
            "is_public":true,
            "is_subscribed":false,
            "app_id":164314,
            "dashboard_id":"6737549040994484743",
            "status":1
        },
        {
            "is_core":false,
            "creator":"Data Ranger",
            "partner_info":{

            },
            "created_at":1582698954,
            "filters":[

            ],
            "is_default":false,
            "partners":[
                "Data Ranger1",
                "Data Ranger2",
                "Data Ranger3",
                "Data Ranger4",
                "Data Ranger5",
                "Data Ranger6",
                "Data Ranger7",
                "Data Ranger8",
                "Data Ranger9",
                "Data Ranger10",
                "Data Ranger11",
                "Data Ranger12",
                "Data Ranger13",
                "Data Ranger14",
                "Data Ranger15",
                "Data Ranger16",
                "Data Ranger17",
                "Data Ranger18"
            ],
            "extra":{

            },
            "name":"tes333",
            "is_public":true,
            "is_subscribed":false,
            "app_id":164314,
            "dashboard_id":"6797640248915395086",
            "status":1
        }
    ],
    "message":"success"
}
```


&nbsp;
