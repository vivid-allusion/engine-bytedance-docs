---
title: "Access Monitoring Data"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Access-monitoring-data"
---

This article explains how to obtain TOS\-related monitoring data through the APIs or SDK provided by cloud monitoring.

<span id="dff86e70"></span>
## Access method

You can obtain TOS\-related monitoring data through APIs or SDKs provided by cloud monitoring. For more details, please refer to [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData).

<span id="2f089f50"></span>
## Key parameter description


|Parameters |Description |
|---|---|
|StartTime |The start time of the query time period is a second\-level timestamp, such as 1632904500. |
|EndTime |The end time of the query time period is a second\-level timestamp, such as 1632904801.<br><br><br>* EndTime \> StartTime.<br><br>* EndTime must not be a future time.<br><br>* EndTime must be less than the allowed number of query days plus StartTime. |
|Instances |Information on monitoring metrics to be queried.<br><br><br>* When multiple instances exist, the logical relationship between instances is "or".<br><br>* If the 'instance' parameter is not provided, monitoring data for all instances in the region will be returned. Large data volumes may impact business operations and should be handled with caution. |
|MetricName |Name of the monitoring metric to query. For details, please refer to [Monitoring Metrics Description](https://docs.byteplus.com/en/docs/tos/Monitoring-indicator-description) under **MetricName**. |
|Namespace |To query the product space to which the monitoring metric belongs, TOS is `VCM_TOS`. |
|SubNamespace |To query the dimensions to which the metric belongs. For details, please refer to the [Monitoring Metrics Description](https://docs.byteplus.com/en/docs/tos/Monitoring-indicator-description) under **SubNamespace.**  |
|Period |Query data granularity supports seconds (s), minutes (m), hours (h), days (d), and weeks (w). For detailed explanation, please refer to [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData). |


<span id="93ae702c"></span>
## API Query Examples

The following request is used to query the total number of objects in the storage bucket `210015********`, with the query period being `(1648048800, 1648049400]` and the cycle set to `1h`.

```JSON
POST https://open.volcengineapi.com?Action=GetMetricData&Version=2018-01-01
ServiceName: Volc_Observe
Region: cn-beijing
AccessKey: xxx
SecretKey: xxx

{
    "MetricName": "BucketObjectCount",
    "StartTime": 1648048800,
    "EndTime": 1648049400,
    "Period": "1h",
    "Namespace": "VCM_TOS",
    "Instances": [
        {
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "Value": "210015****"
                }
            ]
        }
    ],
    "SubNamespace": "bucket_overview"
}
```


<span id="f0c6dd4d"></span>
## SDK query example

The following request is used to query the total number of objects in the storage bucket `210015****` for the period `(1648048800, 1648049400]`, with a cycle of `1h`.

```Java
import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.volcobserve.VolcObserveApi;
import com.volcengine.volcobserve.model.*;

import java.util.ArrayList;
import java.util.List;

public class GetMetricData {
    public static void main(String[] args)throws Exception {
        //Set up your ak.
        String ak = "Your AK";
        //Set up your sk.
        String sk = "Your SK";
        //Set the region you want to access.
        String region = "cn-beijing";
        //Initialize apiclient
        ApiClient apiClient = new ApiClient()
                .setCredentials(Credentials.getCredentials(ak,sk))
                .setRegion(region);
        VolcObserveApi api = new VolcObserveApi(apiClient);
        //Create an interface parameter.
        GetMetricDataRequest request = new GetMetricDataRequest();
        //Set interface input parameters.
        request.setStartTime(1671783***);
        request.setEndTime(1671786***);
        request.setNamespace("VCM_TOS");
        request.setSubNamespace("bucket_overview");
        request.setMetricName("BucketObjectCount");
        request.setPeriod("1h");
        DimensionForGetMetricDataInput dimension = new DimensionForGetMetricDataInput();
        dimension.setName("ResourceID");
        dimension.setValue("210015****");
        InstanceForGetMetricDataInput instance = new InstanceForGetMetricDataInput();
        List<DimensionForGetMetricDataInput> dimensionList = new ArrayList<>();
        dimensionList.add(dimension);
        instance.setDimensions(dimensionList);
        List<InstanceForGetMetricDataInput> instanceList = new ArrayList<>();
        instanceList.add(instance);
        request.setInstances(instanceList);

        try {
            //Call the interface.
            GetMetricDataResponse response = api.getMetricData(request);
            System.out.println(response);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```
