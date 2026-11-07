---
title: "Using Python to query and write data in workspaces"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Using_Python_to_query_and_write_data_in_workspaces"
---

This topic is intended for Python developers who are connecting to VMP workspaces for the first time. It covers both BasicAuth and AK/SK authentication methods and provides complete sample code to demonstrate how to query or write metric data in a workspace using Python.

<span id="QT07LdQE"></span>
## Prerequisites

Before you start, confirm that all of the following conditions are met:


* You have created a VMP workspace and obtained its **query URL (query_url)**  and **write URL** (remote_write_url). For details, see [Obtaining workspace URLs](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL?lang=en).

* One of the following authentication methods is used as needed:

   
   |**Authentication method** |**Applicable scenario** |Description |
   |---|---|---|
   |BasicAuth |Suitable for scenarios where a username/password is already provisioned for the workspace, and you need to complete access verification quickly. Example scenarios include joint debugging and sample validation. |Access a workspace via BasicAuth authentication. The credentials are the BasicAuth account and password configured on the workspace details page. |
   |AK/SK |Suitable for formal integration scenarios that require unified use of the BytePlus signature authentication system. It supports access via IAM user accounts and temporary credentials (an additional sessionToken is needed for temporary credential access). |Access a workspace via AK/SK authentication. The account must have the VMPRemoteWriteAccess or VMPQueryAccess permission.  |
   

* Your development environment must meet the following conditions:

   
   |**Dependency** |**Purpose** |**Required** |
   |---|---|---|
   |Python 3.9 or later |Runs sample code |Yes |
   |requests |Serves as the HTTP request base library |Yes |
   |volcengine |AK/SK signature authentication |Required only for the AK/SK mode |
   |python\-snappy |Compresses Remote Write data |Required only for write scenarios |
   |protobuf |Serializes Remote Write data |Required only for write scenarios |
   

   We recommend installing dependencies based on your scenario:

   ```Bash
   # For query-only scenarios
   pip install requests volcengine
   
   #  To write metrics, install this dependency additionally.
   pip install python-snappy protobuf
   ```
   


<span id="waUaq3MN"></span>
## Procedure

<span id="K2ehKifS"></span>
### Encapsulate VMP workspace access APIs

Save the following code as the `client.py` file. This file provides a minimal viable encapsulation for accessing VMP workspaces. All query examples or write examples invoke capabilities based on this file, including:


* WorkspaceConfig: Centrally manages workspace configurations, such as workspace URLs, authentication methods, and timeout settings.

* VmpWorkspaceClient: Provides lightweight encapsulation of Prometheus Query API and Remote Write capabilities.


```Python
#!/usr/bin/env python3
"""VMP Workspace Python SDK: Query API + Remote Write with BasicAuth / AK-SK authentication."""

from __future__ import annotations

import base64
import os
from collections import OrderedDict
from dataclasses import dataclass
from datetime import datetime, timezone
from typing import Dict, List, Optional, Sequence, Tuple
from urllib.parse import parse_qsl, urlparse

import requests
from requests.auth import AuthBase

@dataclass
class WorkspaceConfig:
    """VMP workspace access configuration."""

    query_url: str = ""
    remote_write_url: str = ""
    auth_mode: str = "aksk"
    region: Optional[str] = None
    service: str = "vmp"
    access_key: Optional[str] = None
    secret_key: Optional[str] = None
    session_token: str = ""
    username: Optional[str] = None
    password: Optional[str] = None
    timeout_seconds: int = 30

    @classmethod
    def from_env(cls) -> "WorkspaceConfig":
        """Load configuration from environment variables."""
        return cls(
            query_url=os.environ.get("VMP_QUERY_URL", ""),
            remote_write_url=os.environ.get("VMP_REMOTE_WRITE_URL", ""),
            auth_mode=os.environ.get("VMP_AUTH_MODE", "aksk").lower(),
            region=os.environ.get("VOLCENGINE_REGION") or os.environ.get("VMP_REGION"),
            service=os.environ.get("VMP_SERVICE", "vmp"),
            access_key=os.environ.get("VOLCENGINE_ACCESS_KEY") or os.environ.get("VMP_ACCESS_KEY"),
            secret_key=os.environ.get("VOLCENGINE_SECRET_KEY") or os.environ.get("VMP_SECRET_KEY"),
            session_token=os.environ.get("VOLCENGINE_SESSION_TOKEN", ""),
            username=os.environ.get("VMP_BASIC_AUTH_USERNAME"),
            password=os.environ.get("VMP_BASIC_AUTH_PASSWORD"),
            timeout_seconds=int(os.environ.get("VMP_TIMEOUT_SECONDS", "30")),
        )

class BasicAuth(AuthBase):
    """BasicAuth adapter."""

    def __init__(self, username: str, password: str) -> None:
        token = base64.b64encode(f"{username}:{password}".encode()).decode()
        self._header = f"Basic {token}"

    def __call__(self, request: requests.PreparedRequest) -> requests.PreparedRequest:
        request.headers["Authorization"] = self._header
        return request

class VolcSigV4Auth(AuthBase):
    """Volcengine AK/SK SignV4 authentication adapter."""

    def __init__(self, access_key: str, secret_key: str, region: str, service: str = "vmp", session_token: str = "") -> None:
        from volcengine.Credentials import Credentials
        self._credentials = Credentials(access_key, secret_key, service, region, session_token)

    def __call__(self, request: requests.PreparedRequest) -> requests.PreparedRequest:
        from volcengine.auth.SignerV4 import SignerV4
        from volcengine.base.Request import Request as VolcRequest

        parsed = urlparse(request.url)
        volc_request = VolcRequest()
        volc_request.set_shema(parsed.scheme)
        volc_request.set_method(request.method.upper())
        volc_request.set_connection_timeout(10)
        volc_request.set_socket_timeout(10)
        volc_request.set_host(parsed.netloc)
        volc_request.set_path(parsed.path or "/")
        if parsed.query:
            volc_request.set_query(OrderedDict(parse_qsl(parsed.query, keep_blank_values=True)))

        # Only pass minimal required headers for signing to avoid signature mismatch
        sign_headers = OrderedDict()
        sign_headers["Host"] = parsed.netloc
        content_type = request.headers.get("Content-Type")
        if content_type:
            sign_headers["Content-Type"] = content_type
        volc_request.set_headers(sign_headers)

        body = request.body or b""
        if isinstance(body, str):
            body = body.encode("utf-8")
        volc_request.set_body(body)

        SignerV4.sign(volc_request, self._credentials)

        for key, value in volc_request.headers.items():
            request.headers[key] = value
        return request

def build_vmp_auth(config: WorkspaceConfig) -> AuthBase:
    """Build auth adapter from config."""
    if config.auth_mode == "basic":
        if not config.username or not config.password:
            raise ValueError("basic auth mode requires username and password")
        return BasicAuth(config.username, config.password)
    if config.auth_mode == "aksk":
        if not config.access_key or not config.secret_key or not config.region:
            raise ValueError("aksk auth mode requires access_key, secret_key and region")
        return VolcSigV4Auth(
            access_key=config.access_key,
            secret_key=config.secret_key,
            region=config.region,
            service=config.service,
            session_token=config.session_token,
        )
    raise ValueError(f"unsupported auth mode: {config.auth_mode}")

class PrometheusHttpApiClient:
    """Generic Prometheus HTTP Query API client (auth-agnostic)."""

    def __init__(self, base_url: str, session: requests.Session, timeout_seconds: int = 30) -> None:
        self.base_url = base_url.rstrip("/")
        self.session = session
        self.timeout = timeout_seconds

    def _get(self, path: str, params: Optional[List[Tuple[str, str]]] = None) -> Dict:
        response = self.session.get(self.base_url + path, params=params, timeout=self.timeout)
        if not response.ok:
            raise requests.HTTPError(
                f"GET {path} failed: HTTP {response.status_code}, response: {response.text}",
                response=response,
            )
        return response.json()

    def query(self, promql: str, ts: Optional[datetime] = None) -> Dict:
        params: List[Tuple[str, str]] = [("query", promql)]
        if ts is not None:
            params.append(("time", _to_rfc3339(ts)))
        return self._get("/api/v1/query", params)

    def query_range(self, promql: str, start: datetime, end: datetime, step: str) -> Dict:
        params = [("query", promql), ("start", _to_rfc3339(start)), ("end", _to_rfc3339(end)), ("step", step)]
        return self._get("/api/v1/query_range", params)

    def series(self, matches: Sequence[str], start: Optional[datetime] = None, end: Optional[datetime] = None) -> Dict:
        if not matches:
            raise ValueError("series requires at least one match selector")
        params: List[Tuple[str, str]] = [("match[]", m) for m in matches]
        if start:
            params.append(("start", _to_rfc3339(start)))
        if end:
            params.append(("end", _to_rfc3339(end)))
        return self._get("/api/v1/series", params)

    def labels(self, start: Optional[datetime] = None, end: Optional[datetime] = None, matches: Optional[Sequence[str]] = None) -> Dict:
        params: List[Tuple[str, str]] = []
        if matches:
            params.extend(("match[]", m) for m in matches)
        if start:
            params.append(("start", _to_rfc3339(start)))
        if end:
            params.append(("end", _to_rfc3339(end)))
        return self._get("/api/v1/labels", params)

    def label_values(self, label_name: str, start: Optional[datetime] = None, end: Optional[datetime] = None, matches: Optional[Sequence[str]] = None) -> Dict:
        if not label_name:
            raise ValueError("label_values requires a non-empty label_name")
        params: List[Tuple[str, str]] = []
        if matches:
            params.extend(("match[]", m) for m in matches)
        if start:
            params.append(("start", _to_rfc3339(start)))
        if end:
            params.append(("end", _to_rfc3339(end)))
        return self._get(f"/api/v1/label/{label_name}/values", params)

class VmpWorkspaceClient:
    """VMP workspace client: auth + Query API + Remote Write."""

    def __init__(self, config: WorkspaceConfig) -> None:
        self.config = config
        self.session = requests.Session()
        self.session.auth = build_vmp_auth(config)
        self.timeout = config.timeout_seconds
        self.http_api = PrometheusHttpApiClient(config.query_url, self.session, config.timeout_seconds)

    def query(self, promql: str, ts: Optional[datetime] = None) -> Dict:
        return self.http_api.query(promql, ts)

    def query_range(self, promql: str, start: datetime, end: datetime, step: str) -> Dict:
        return self.http_api.query_range(promql, start, end, step)

    def series(self, matches: Sequence[str], start: Optional[datetime] = None, end: Optional[datetime] = None) -> Dict:
        return self.http_api.series(matches, start=start, end=end)

    def labels(self, start: Optional[datetime] = None, end: Optional[datetime] = None, matches: Optional[Sequence[str]] = None) -> Dict:
        return self.http_api.labels(start=start, end=end, matches=matches)

    def label_values(self, label_name: str, start: Optional[datetime] = None, end: Optional[datetime] = None, matches: Optional[Sequence[str]] = None) -> Dict:
        return self.http_api.label_values(label_name, start=start, end=end, matches=matches)

    def write_samples(self, series: Sequence[Tuple[Dict[str, str], float, int]]) -> Dict:
        """Write samples via Remote Write. Each element is (labels_dict, value, timestamp_ms)."""
        import snappy
        remote_write_pb2 = _get_remote_write_pb2()

        payload = remote_write_pb2.WriteRequest()
        for labels, value, timestamp_ms in series:
            ts = payload.timeseries.add()
            for key, label_value in labels.items():
                label = ts.labels.add()
                label.name = key
                label.value = label_value
            sample = ts.samples.add()
            sample.value = float(value)
            sample.timestamp = int(timestamp_ms)

        body = snappy.compress(payload.SerializeToString())
        headers = {
            "Content-Type": "application/x-protobuf",
            "Content-Encoding": "snappy",
            "X-Prometheus-Remote-Write-Version": "0.1.0",
        }
        response = self.session.post(self.config.remote_write_url, data=body, headers=headers, timeout=self.timeout)
        if not response.ok:
            raise requests.HTTPError(
                f"Remote Write failed: HTTP {response.status_code}, response: {response.text}",
                response=response,
            )
        return {"status_code": response.status_code, "body": response.text}

def _to_rfc3339(value: datetime) -> str:
    if value.tzinfo is None:
        value = value.replace(tzinfo=timezone.utc)
    return value.astimezone(timezone.utc).isoformat().replace("+00:00", "Z")

# Embedded Prometheus Remote Write protobuf definition to avoid external _pb2.py dependency
_REMOTE_WRITE_PB2 = None

def _get_remote_write_pb2():
    global _REMOTE_WRITE_PB2
    if _REMOTE_WRITE_PB2 is not None:
        return _REMOTE_WRITE_PB2
    from google.protobuf import descriptor_pool as _descriptor_pool
    from google.protobuf.internal import builder as _builder
    import types

    DESCRIPTOR = _descriptor_pool.Default().AddSerializedFile(
        b'\n\x1dprometheus_remote_write.proto\x12\nprometheus\":\n\x0cWriteRequest\x12*\n\ntimeseries\x18\x01 \x03(\x0b\x32\x16.prometheus.TimeSeries\"T\n\nTimeSeries\x12!\n\x06labels\x18\x01 \x03(\x0b\x32\x11.prometheus.Label\x12#\n\x07samples\x18\x02 \x03(\x0b\x32\x12.prometheus.Sample\"$\n\x05Label\x12\x0c\n\x04name\x18\x01 \x01(\t\x12\r\n\x05value\x18\x02 \x01(\t\"*\n\x06Sample\x12\r\n\x05value\x18\x01 \x01(\x01\x12\x11\n\ttimestamp\x18\x02 \x01(\x03\x62\x06proto3'
    )
    _globals = {}
    _builder.BuildMessageAndEnumDescriptors(DESCRIPTOR, _globals)
    _builder.BuildTopDescriptorsAndMessages(DESCRIPTOR, 'prometheus_remote_write_pb2', _globals)

    module = types.SimpleNamespace(**_globals)
    _REMOTE_WRITE_PB2 = module
    return module
```


<span id="v0Cu95t1"></span>
## Query metric data

<span id="PQr7BdvM"></span>
#### API descriptions and call examples


|**Method** |**API path** |Typical purpose |Description |
|---|---|---|---|
|query(promql, ts) |/api/v1/query |Instant query |Queries the current value at a specific time point. |
|queryRange(promql, start, end, step) |/api/v1/query_range |Range queries |Queries data within a specified time period to reflect trends. |
|series(matches, start, end) |/api/v1/series |Queries matching time series |Suitable for confirming whether a metric or label combination exists. |
|labels(start, end, matches) |/api/v1/labels |Queries label keys |Suitable for querying available labels in the current workspace. |
|labelValues(labelName, start, end, matches) |/api/v1/label/<name\>/values |Queries label values |Suitable for querying the set of existing values for a specific label key. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Key fields in responses to API calls are described as follows:</div>



* <div data-tips="true" data-tips-type="default">status: Indicates whether the request is successful.</div>


* <div data-tips="true" data-tips-type="default">data.resultType: Indicates the result type.</div>


* <div data-tips="true" data-tips-type="default">data.result: Contains the actual metric query result.</div>



<span id="xXcCvRZw"></span>
#### Query metrics through basic authentication

```Python
from datetime import datetime, timedelta, timezone
from client import WorkspaceConfig, VmpWorkspaceClient

# 1. Construct a workspace configuration:
#    - query_url: Prometheus Query API URL.
#    - auth_mode="basic": Indicates BasicAuth.
#    - username/password: The BasicAuth username and password configured for the workspace.
config = WorkspaceConfig(
    query_url="<your-query-url>",
    auth_mode="basic",
    username="<your-username>",
    password="<your-password>",
)

# 2. Create a client.
client = VmpWorkspaceClient(config)

# 3. Perform an instant query:
#    Query the result of the up metric at the current time.
result = client.query("up")
print(result)

# 4. Perform a range query:
#    Query changes of the up metric in the last 5 minutes, returning one data point every 30 seconds.
end = datetime.now(tz=timezone.utc)
start = end - timedelta(minutes=5)
result = client.query_range("up", start, end, "30s")
print(result)

# 5. Query time series:
#    Query all time series matching the condition {__name__="up"}.
series = client.series(['{__name__=\"up\"}'], start=start, end=end)
print(series)

# 6. Query label keys:
#    Return the list of label keys that appeared within the specified time range.
labels = client.labels(start=start, end=end)
print(labels)

# 7. Query label values:
#    Query the values of the job label that appeared within the specified time range.
values = client.label_values("job", start=start, end=end)
print(values)
```


<span id="6dFRWtnB"></span>
#### Query metrics through AK/SK authentication

```Python
from datetime import datetime, timedelta, timezone
from client import WorkspaceConfig, VmpWorkspaceClient

# 1. Construct a workspace configuration:
#    - query_url: Prometheus Query API URL.
#    - auth_mode="aksk": Indicates BytePlus AK/SK signature authentication.
#    - region: The region of the workspace, for example, cn-beijing.
#    - access_key/secret_key: Credentials with the VMPQueryAccess permission.
config = WorkspaceConfig(
    query_url="<your-query-url>",
    auth_mode="aksk",
    region="cn-beijing",
    access_key="<your-access-key>",
    secret_key="<your-secret-key>",
)

# 2. Create a client.
client = VmpWorkspaceClient(config)

# 3. Perform an instant query:
#    Query the result of the up metric at the current time.
result = client.query("up")
print(result)

# 4. Perform a range query:
#    Query changes of the up metric in the last 5 minutes, returning one data point every 30 seconds.
end = datetime.now(tz=timezone.utc)
start = end - timedelta(minutes=5)
result = client.query_range("up", start, end, "30s")
print(result)

# 5. Query time series:
#    Query all time series matching the condition {__name__="up"}.
series = client.series(['{__name__=\"up\"}'], start=start, end=end)
print(series)

# 6. Query label keys:
#    Return the list of label keys that appeared within the specified time range.
labels = client.labels(start=start, end=end)
print(labels)

# 7. Query label values:
#    Query the values of the job label that appeared within the specified time range.
values = client.label_values("job", start=start, end=end)
print(values)
```


<span id="FQ9QzLxh"></span>
### Write metric data

<span id="W59XU3p6"></span>
#### Write metrics through basic authentication

```Python
from datetime import datetime, timezone
from client import WorkspaceConfig, VmpWorkspaceClient

# 1. Construct a workspace configuration:
#    - remote_write_url: The Remote Write URL.
#    - auth_mode="basic": Indicates BasicAuth.
#    - username/password: The BasicAuth username and password configured for the workspace.
config = WorkspaceConfig(
    remote_write_url="<your-remote-write-url>",
    auth_mode="basic",
    username="<your-username>",
    password="<your-password>",
)

# 2. Create a client based on the configuration.
client = VmpWorkspaceClient(config)

# 3. Assemble sample data and write samples.
#    The input parameter for write_samples is a list, with each element being:
#    (labels_dict, value, timestamp_ms)
#    - labels_dict: Metric labels (The "__name__" label must be included as the metric name)
#    - value: Metric value
#    - timestamp_ms: Timestamp in milliseconds
resp = client.write_samples([
    (
        {
            "__name__": "demo_metric",  # Metric name
            "job": "example",           # Job label (Replace it as needed)
            "env": "test",              # Environment label
        },
        42.0,  # Metric value
        int(datetime.now(tz=timezone.utc).timestamp() * 1000),  # Current UTC in milliseconds
    )
])

# 4. Print the write result.
#    A successful execution typically returns an HTTP status code and other information.
print(resp)
```


<span id="GjTDkSeb"></span>
#### Write metrics through AK/SK authentication

```Python
from datetime import datetime, timezone
from client import WorkspaceConfig, VmpWorkspaceClient

# 1. Construct a workspace configuration:
#    - remote_write_url: The Remote Write URL.
#    - auth_mode="aksk": Indicates BytePlus AK/SK signature authentication.
#    - region: The region of the workspace, for example, cn-beijing.
#    - access_key/secret_key: Credentials with the VMPRemoteWriteAccess permission.
config = WorkspaceConfig(
    remote_write_url="<your-remote-write-url>",
    auth_mode="aksk",
    region="cn-beijing",
    access_key="<your-access-key>",
    secret_key="<your-secret-key>",
)

# 2. Create a client based on the configuration.
client = VmpWorkspaceClient(config)

# 3. Assemble sample data and write samples.
#    The input parameter for write_samples is a list, with each element being:
#    (labels_dict, value, timestamp_ms)
#    - labels_dict: Metric labels (The "__name__" label must be included as the metric name)
#    - value: Metric value
#    - timestamp_ms: Timestamp in milliseconds
resp = client.write_samples([
    (
        {
            "__name__": "demo_metric",  # Metric name
            "job": "example",           # Job label (Replace it as needed)
            "env": "test",              # Environment label
        },
        42.0,  # Metric value
        int(datetime.now(tz=timezone.utc).timestamp() * 1000),  # Current UTC in milliseconds
    )
])

# 4. Print the write result.
#    A successful execution typically returns an HTTP status code and other information.
print(resp)
```


<span id="mCCCTkAR"></span>
## FAQ and troubleshooting suggestions

<span id="Jqz0pbCA"></span>
### Q1: Why does authentication fail with the 401 or 403 error?

**Possible causes:** 


* The BasicAuth username or password is incorrect.

* The AK, SK, or region configuration is invalid.

* The current account or credentials lack access permission for the target workspace.


**Troubleshooting suggestions:** 


* Check whether the authentication method matches the actual configuration.

* Verify that the copied access URL matches the workspace.


<span id="LFp6I3q2"></span>
### Q2: Why do queries succeed but return empty results?

**Possible causes:** 


* The PromQL query did not match any data.

* The query time range is too narrow, or the time point is inappropriate.

* Written metric data has not been synchronized to the query side.


**Troubleshooting suggestions:** 


* Use a simpler metric name.

* Expand the time range (for example, from the last 5 minutes to the last 30 minutes).

* Wait 5 to 10 minutes and then retry the query.


<span id="3fTpLVet"></span>
### Q3: Why does Remote Write fail?

**Possible causes:** 


* The provided remote_write_url is incorrect.

* The python\-snappy or protobuf dependency is not installed.

* A network policy or permission restriction blocks access.


**Troubleshooting suggestions:** 


* Confirm whether the write URL is complete (usually ending with /api/v1/write).

* Confirm whether the dependencies are successfully installed.

* Check network policies or permission restrictions.


<span id="Fwk89JCL"></span>
### Q4: Why does AK/SK authorization fail?

**Possible causes:** 


* The specified region does not match the actual region of the workspace.

* Temporary credentials were used, but the SessionToken was missing.

* The service name was mistakenly changed, causing a signature mismatch.


**Troubleshooting suggestions:** 


* Keep "vmp" as the default service.

* When using temporary credentials, provide AccessKey, SecretKey, and SessionToken together.
