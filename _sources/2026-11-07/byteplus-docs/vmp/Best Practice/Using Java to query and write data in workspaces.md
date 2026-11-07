---
title: "Using Java to query and write data in workspaces"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Using_Java_to_query_and_write_data_in_workspaces"
---

This topic is intended for Java developers who are connecting to VMP workspaces for the first time. It covers both BasicAuth and AK/SK authentication methods and provides complete sample code to demonstrate how to query or write metric data in a workspace using Java.

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
   |JDK 21 or later |Runs sample code |Yes |
   |OkHttp 4.x |Serves as the HTTP request base library |Yes |
   |Jackson 2.x |Parses JSON |Yes |
   |snappy\-java |Compresses Remote Write data |Required only for write scenarios<br><br> |
   

   Maven dependency configuration:

   ```XML
   <dependencies>
       <dependency>
           <groupId>com.squareup.okhttp3</groupId>
           <artifactId>okhttp</artifactId>
           <version>4.12.0</version>
       </dependency>
       <dependency>
           <groupId>com.fasterxml.jackson.core</groupId>
           <artifactId>jackson-databind</artifactId>
           <version>2.17.0</version>
       </dependency>
       <dependency>
           <groupId>org.xerial.snappy</groupId>
           <artifactId>snappy-java</artifactId>
           <version>1.1.10.5</version>
       </dependency>
   </dependencies>
   ```
   


<span id="9OYFib4E"></span>
## Procedure

<span id="K2ehKifS"></span>
### Encapsulate VMP workspace access APIs

Save the following code as the `VmpWorkspaceClient.java` file. This file provides a minimal viable encapsulation for accessing VMP workspaces. All query examples or write examples invoke capabilities based on this file, including:


* WorkspaceConfig: Centrally manages workspace configurations, such as URLs, authentication methods, and timeout settings.

* VmpWorkspaceClient: Provides lightweight encapsulation of Prometheus Query API and Remote Write capabilities.


```Java
package com.example.vmp;

import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import okhttp3.Credentials;
import okhttp3.HttpUrl;
import okhttp3.Interceptor;
import okhttp3.MediaType;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import org.xerial.snappy.Snappy;

import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.net.URLEncoder;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.time.Duration;
import java.time.Instant;
import java.time.ZoneOffset;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.Locale;
import java.util.Map;
import java.util.TreeMap;

/**
 * VMP Workspace Java SDK: supports Query API and Remote Write with BasicAuth / AK-SK authentication.
 */
public class VmpWorkspaceClient {

    private static final MediaType PROTOBUF = MediaType.parse("application/x-protobuf");
    private static final ObjectMapper MAPPER = new ObjectMapper();

    private final WorkspaceConfig config;
    private final OkHttpClient httpClient;

    public VmpWorkspaceClient(WorkspaceConfig config) {
        this.config = config;
        OkHttpClient.Builder builder = new OkHttpClient.Builder()
                .callTimeout(Duration.ofSeconds(config.timeoutSeconds));

        if ("basic".equalsIgnoreCase(config.authMode)) {
            builder.addInterceptor(new BasicAuthInterceptor(config.username, config.password));
        } else if ("aksk".equalsIgnoreCase(config.authMode)) {
            builder.addInterceptor(new VolcSignatureInterceptor(
                    config.accessKey, config.secretKey, config.region, config.service, config.sessionToken));
        } else {
            throw new IllegalArgumentException("Unsupported auth mode: " + config.authMode);
        }

        this.httpClient = builder.build();
    }

    // ======================== Query API ========================

    public JsonNode query(String promql) throws IOException {
        return query(promql, null);
    }

    public JsonNode query(String promql, Instant ts) throws IOException {
        requireQueryUrl();
        HttpUrl.Builder urlBuilder = HttpUrl.parse(config.queryUrl + "/api/v1/query").newBuilder()
                .addQueryParameter("query", promql);
        if (ts != null) {
            urlBuilder.addQueryParameter("time", toRfc3339(ts));
        }
        return executeGet(urlBuilder.build());
    }

    public JsonNode queryRange(String promql, Instant start, Instant end, String step) throws IOException {
        requireQueryUrl();
        HttpUrl url = HttpUrl.parse(config.queryUrl + "/api/v1/query_range").newBuilder()
                .addQueryParameter("query", promql)
                .addQueryParameter("start", toRfc3339(start))
                .addQueryParameter("end", toRfc3339(end))
                .addQueryParameter("step", step)
                .build();
        return executeGet(url);
    }

    public JsonNode series(List<String> matches, Instant start, Instant end) throws IOException {
        requireQueryUrl();
        if (matches == null || matches.isEmpty()) {
            throw new IllegalArgumentException("series API requires at least one match selector");
        }
        HttpUrl.Builder builder = HttpUrl.parse(config.queryUrl + "/api/v1/series").newBuilder();
        for (String match : matches) {
            builder.addQueryParameter("match[]", match);
        }
        if (start != null) builder.addQueryParameter("start", toRfc3339(start));
        if (end != null) builder.addQueryParameter("end", toRfc3339(end));
        return executeGet(builder.build());
    }

    public JsonNode labels(Instant start, Instant end, List<String> matches) throws IOException {
        requireQueryUrl();
        HttpUrl.Builder builder = HttpUrl.parse(config.queryUrl + "/api/v1/labels").newBuilder();
        if (matches != null) {
            for (String match : matches) builder.addQueryParameter("match[]", match);
        }
        if (start != null) builder.addQueryParameter("start", toRfc3339(start));
        if (end != null) builder.addQueryParameter("end", toRfc3339(end));
        return executeGet(builder.build());
    }

    public JsonNode labelValues(String labelName, Instant start, Instant end, List<String> matches) throws IOException {
        requireQueryUrl();
        if (labelName == null || labelName.isBlank()) {
            throw new IllegalArgumentException("labelValues API requires a non-empty labelName");
        }
        HttpUrl.Builder builder = HttpUrl.parse(config.queryUrl + "/api/v1/label/" + labelName + "/values").newBuilder();
        if (matches != null) {
            for (String match : matches) builder.addQueryParameter("match[]", match);
        }
        if (start != null) builder.addQueryParameter("start", toRfc3339(start));
        if (end != null) builder.addQueryParameter("end", toRfc3339(end));
        return executeGet(builder.build());
    }

    // ======================== Remote Write ========================

    /**
     * Write samples via Remote Write. Each entry is (labels, value, timestampMs).
     */
    public String writeSamples(List<SampleEntry> series) throws IOException {
        if (config.remoteWriteUrl == null) {
            throw new IllegalStateException("remote_write_url is not configured");
        }
        byte[] payload = encodeWriteRequest(series);
        byte[] compressed = Snappy.compress(payload);

        Request request = new Request.Builder()
                .url(config.remoteWriteUrl)
                .post(RequestBody.create(compressed, PROTOBUF))
                .header("Content-Type", "application/x-protobuf")
                .header("Content-Encoding", "snappy")
                .header("X-Prometheus-Remote-Write-Version", "0.1.0")
                .build();

        try (Response response = httpClient.newCall(request).execute()) {
            String body = response.body() == null ? "" : response.body().string();
            if (!response.isSuccessful()) {
                throw new IOException("Remote Write failed: HTTP " + response.code() + ", response: " + body);
            }
            return body;
        }
    }

    private void requireQueryUrl() {
        if (config.queryUrl == null) {
            throw new IllegalStateException("query_url is not configured");
        }
    }

    // ======================== Internal Methods ========================

    private JsonNode executeGet(HttpUrl url) throws IOException {
        Request request = new Request.Builder().url(url).get().build();
        try (Response response = httpClient.newCall(request).execute()) {
            String body = response.body() == null ? "" : response.body().string();
            if (!response.isSuccessful()) {
                throw new IOException("GET " + url.encodedPath() + " failed: HTTP " + response.code() + ", response: " + body);
            }
            return MAPPER.readTree(body);
        }
    }

    private static String toRfc3339(Instant instant) {
        return RFC3339.format(instant);
    }

    // ======================== Inline Protobuf Encoding ========================
    private static byte[] encodeWriteRequest(List<SampleEntry> series) throws IOException {
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        for (SampleEntry entry : series) {
            byte[] tsBytes = encodeTimeSeries(entry);
            // field 1, wire type 2 (length-delimited)
            writeTag(out, 1, 2);
            writeVarint(out, tsBytes.length);
            out.write(tsBytes);
        }
        return out.toByteArray();
    }

    private static byte[] encodeTimeSeries(SampleEntry entry) throws IOException {
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        // labels (field 1) — sorted by key
        List<Map.Entry<String, String>> sorted = new ArrayList<>(entry.labels.entrySet());
        sorted.sort(Map.Entry.comparingByKey());
        for (Map.Entry<String, String> label : sorted) {
            byte[] labelBytes = encodeLabel(label.getKey(), label.getValue());
            writeTag(out, 1, 2);
            writeVarint(out, labelBytes.length);
            out.write(labelBytes);
        }
        // samples (field 2)
        byte[] sampleBytes = encodeSample(entry.value, entry.timestampMs);
        writeTag(out, 2, 2);
        writeVarint(out, sampleBytes.length);
        out.write(sampleBytes);
        return out.toByteArray();
    }

    private static byte[] encodeLabel(String name, String value) throws IOException {
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        // name: field 1, wire type 2
        byte[] nameBytes = name.getBytes(StandardCharsets.UTF_8);
        writeTag(out, 1, 2);
        writeVarint(out, nameBytes.length);
        out.write(nameBytes);
        // value: field 2, wire type 2
        byte[] valueBytes = value.getBytes(StandardCharsets.UTF_8);
        writeTag(out, 2, 2);
        writeVarint(out, valueBytes.length);
        out.write(valueBytes);
        return out.toByteArray();
    }

    private static byte[] encodeSample(double value, long timestampMs) throws IOException {
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        // value: field 1, wire type 1 (64-bit)
        if (Double.doubleToRawLongBits(value) != 0) {
            writeTag(out, 1, 1);
            writeLittleEndian64(out, Double.doubleToRawLongBits(value));
        }
        // timestamp: field 2, wire type 0 (varint)
        if (timestampMs != 0) {
            writeTag(out, 2, 0);
            writeVarint(out, timestampMs);
        }
        return out.toByteArray();
    }

    private static void writeTag(ByteArrayOutputStream out, int fieldNumber, int wireType) {
        writeVarint(out, (fieldNumber << 3) | wireType);
    }

    private static void writeVarint(ByteArrayOutputStream out, long value) {
        while ((value & ~0x7FL) != 0) {
            out.write((int) ((value & 0x7F) | 0x80));
            value >>>= 7;
        }
        out.write((int) value);
    }

    private static void writeLittleEndian64(ByteArrayOutputStream out, long value) {
        for (int i = 0; i < 8; i++) {
            out.write((int) (value & 0xFF));
            value >>= 8;
        }
    }

    // ======================== Data structure ========================

    /** Write sample entries: label set + value + timestamp in milliseconds.  */
    public static class SampleEntry {
        public final Map<String, String> labels;
        public final double value;
        public final long timestampMs;

        public SampleEntry(Map<String, String> labels, double value, long timestampMs) {
            this.labels = labels;
            this.value = value;
            this.timestampMs = timestampMs;
        }
    }

    // ======================== Configuration ========================

    /** VMP workspace access configuration. */
    public static class WorkspaceConfig {
        public final String queryUrl;
        public final String remoteWriteUrl;
        public final String authMode;
        public final String region;
        public final String service;
        public final String accessKey;
        public final String secretKey;
        public final String sessionToken;
        public final String username;
        public final String password;
        public final long timeoutSeconds;

        public WorkspaceConfig(
                String queryUrl,
                String remoteWriteUrl,
                String authMode,
                String region,
                String service,
                String accessKey,
                String secretKey,
                String sessionToken,
                String username,
                String password,
                long timeoutSeconds
        ) {
            this.queryUrl = queryUrl == null || queryUrl.isBlank() ? null : trimTrailingSlash(queryUrl);
            this.remoteWriteUrl = remoteWriteUrl == null || remoteWriteUrl.isBlank() ? null : remoteWriteUrl;
            this.authMode = authMode == null ? "aksk" : authMode.toLowerCase(Locale.ROOT);
            this.region = region;
            this.service = service == null || service.isBlank() ? "vmp" : service;
            this.accessKey = accessKey;
            this.secretKey = secretKey;
            this.sessionToken = sessionToken == null ? "" : sessionToken;
            this.username = username;
            this.password = password;
            this.timeoutSeconds = timeoutSeconds <= 0 ? 30 : timeoutSeconds;

            if ("basic".equals(this.authMode)) {
                required(username, "username");
                required(password, "password");
            } else if ("aksk".equals(this.authMode)) {
                required(region, "region");
                required(accessKey, "access_key");
                required(secretKey, "secret_key");
            }
        }

        /** Load configuration from environment variables. */
        public static WorkspaceConfig fromEnv() {
            return new WorkspaceConfig(
                    env("VMP_QUERY_URL"),
                    env("VMP_REMOTE_WRITE_URL"),
                    envOr("VMP_AUTH_MODE", "aksk"),
                    firstNonBlank(env("VOLCENGINE_REGION"), env("VMP_REGION")),
                    envOr("VMP_SERVICE", "vmp"),
                    firstNonBlank(env("VOLCENGINE_ACCESS_KEY"), env("VMP_ACCESS_KEY")),
                    firstNonBlank(env("VOLCENGINE_SECRET_KEY"), env("VMP_SECRET_KEY")),
                    envOr("VOLCENGINE_SESSION_TOKEN", ""),
                    env("VMP_BASIC_AUTH_USERNAME"),
                    env("VMP_BASIC_AUTH_PASSWORD"),
                    Long.parseLong(envOr("VMP_TIMEOUT_SECONDS", "30"))
            );
        }

        private static String env(String name) {
            return System.getenv(name);
        }

        private static String envOr(String name, String defaultValue) {
            String value = System.getenv(name);
            return (value != null && !value.isBlank()) ? value : defaultValue;
        }

        private static String firstNonBlank(String... values) {
            for (String v : values) {
                if (v != null && !v.isBlank()) return v;
            }
            return null;
        }

        private static String required(String value, String name) {
            if (value == null || value.isBlank()) {
                throw new IllegalArgumentException("Missing required config: " + name);
            }
            return value;
        }

        private static String trimTrailingSlash(String value) {
            while (value.endsWith("/")) value = value.substring(0, value.length() - 1);
            return value;
        }
    }

    // ======================== BasicAuth ========================

    static class BasicAuthInterceptor implements Interceptor {
        private final String authorization;

        BasicAuthInterceptor(String username, String password) {
            this.authorization = Credentials.basic(username, password, StandardCharsets.UTF_8);
        }

        @Override
        public Response intercept(Chain chain) throws IOException {
            return chain.proceed(chain.request().newBuilder()
                    .header("Authorization", authorization)
                    .build());
        }
    }

    // ======================== AK/SK Signature Authentication ========================

    static class VolcSignatureInterceptor implements Interceptor {
        private final String accessKey;
        private final String secretKey;
        private final String region;
        private final String service;
        private final String sessionToken;

        VolcSignatureInterceptor(String accessKey, String secretKey, String region, String service, String sessionToken) {
            this.accessKey = accessKey;
            this.secretKey = secretKey;
            this.region = region;
            this.service = service;
            this.sessionToken = sessionToken == null ? "" : sessionToken;
        }

        @Override
        public Response intercept(Chain chain) throws IOException {
            Request request = chain.request();
            byte[] body = readBody(request);
            HttpUrl url = request.url();
            String xDate = X_DATE.format(Instant.now());
            String shortDate = xDate.substring(0, 8);
            String payloadHash = sha256Hex(body);

            // Collect headers to sign
            Map<String, String> signedHeaders = collectHeaders(request, url, xDate, payloadHash, sessionToken);
            String canonicalHeaders = canonicalHeaders(signedHeaders);
            String signedHeaderNames = String.join(";", signedHeaders.keySet());

            // Build Canonical Request
            String canonicalRequest = request.method() + "\n"
                    + canonicalUri(url.encodedPath()) + "\n"
                    + canonicalQuery(url) + "\n"
                    + canonicalHeaders + "\n"
                    + signedHeaderNames + "\n"
                    + payloadHash;

            // Build String to Sign
            String credentialScope = shortDate + "/" + region + "/" + service + "/request";
            String stringToSign = "HMAC-SHA256\n" + xDate + "\n" + credentialScope + "\n"
                    + sha256Hex(canonicalRequest.getBytes(StandardCharsets.UTF_8));

            // Derive signing key and generate signature
            byte[] signingKey = hmac(hmac(hmac(hmac(
                    secretKey.getBytes(StandardCharsets.UTF_8), shortDate), region), service), "request");
            String signature = toHex(hmac(signingKey, stringToSign));
            String authorization = "HMAC-SHA256 Credential=" + accessKey + "/" + credentialScope
                    + ", SignedHeaders=" + signedHeaderNames
                    + ", Signature=" + signature;

            Request.Builder builder = request.newBuilder()
                    .header("Host", hostHeader(url))
                    .header("X-Date", xDate)
                    .header("X-Content-Sha256", payloadHash)
                    .header("Authorization", authorization);
            if (!sessionToken.isBlank()) {
                builder.header("X-Security-Token", sessionToken);
            }
            return chain.proceed(builder.build());
        }

        private static Map<String, String> collectHeaders(
                Request request, HttpUrl url, String xDate, String payloadHash, String sessionToken) {
            TreeMap<String, String> headers = new TreeMap<>();
            headers.put("host", hostHeader(url));
            headers.put("x-date", xDate);
            headers.put("x-content-sha256", payloadHash);
            if (sessionToken != null && !sessionToken.isBlank()) {
                headers.put("x-security-token", sessionToken);
            }
            if (request.header("Content-Type") != null) {
                headers.put("content-type", request.header("Content-Type"));
            }
            for (String name : request.headers().names()) {
                String lower = name.toLowerCase(Locale.ROOT);
                if (lower.startsWith("x-") || lower.equals("content-type") || lower.equals("host")) {
                    headers.put(lower, request.header(name));
                }
            }
            return headers;
        }
    }

    // ======================== Signing Utilities ========================

    private static final DateTimeFormatter X_DATE = DateTimeFormatter.ofPattern("yyyyMMdd'T'HHmmss'Z'").withZone(ZoneOffset.UTC);
    private static final DateTimeFormatter RFC3339 = DateTimeFormatter.ISO_OFFSET_DATE_TIME.withZone(ZoneOffset.UTC);

    private static String canonicalHeaders(Map<String, String> headers) {
        StringBuilder sb = new StringBuilder();
        headers.forEach((k, v) -> sb.append(k).append(':').append(v.trim()).append('\n'));
        return sb.toString();
    }

    private static String canonicalUri(String path) {
        if (path == null || path.isEmpty()) return "/";
        return encode(path).replace("%2F", "/");
    }

    private static String canonicalQuery(HttpUrl url) {
        List<String> entries = new ArrayList<>();
        for (int i = 0; i < url.querySize(); i++) {
            String name = url.queryParameterName(i);
            String value = url.queryParameterValue(i);
            entries.add(encode(name) + "=" + encode(value == null ? "" : value));
        }
        entries.sort(Comparator.naturalOrder());
        return String.join("&", entries);
    }

    private static byte[] readBody(Request request) throws IOException {
        if (request.body() == null) return new byte[0];
        okio.Buffer buffer = new okio.Buffer();
        request.body().writeTo(buffer);
        return buffer.readByteArray();
    }

    private static String hostHeader(HttpUrl url) {
        int port = url.port();
        boolean std = (url.isHttps() && port == 443) || (!url.isHttps() && port == 80);
        return std ? url.host() : url.host() + ":" + port;
    }

    private static String encode(String value) {
        return URLEncoder.encode(value, StandardCharsets.UTF_8)
                .replace("+", "%20").replace("*", "%2A").replace("%7E", "~");
    }

    private static String sha256Hex(byte[] data) {
        try {
            return toHex(MessageDigest.getInstance("SHA-256").digest(data));
        } catch (Exception e) { throw new RuntimeException(e); }
    }

    private static byte[] hmac(byte[] key, String data) {
        try {
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(new SecretKeySpec(key, "HmacSHA256"));
            return mac.doFinal(data.getBytes(StandardCharsets.UTF_8));
        } catch (Exception e) { throw new RuntimeException(e); }
    }

    private static String toHex(byte[] data) {
        StringBuilder sb = new StringBuilder();
        for (byte b : data) sb.append(String.format("%02x", b));
        return sb.toString();
    }
}
```


&nbsp;

<span id="HXRc0edv"></span>
### Query metric data

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

```Java
package com.example.vmp;

import com.example.vmp.VmpWorkspaceClient.WorkspaceConfig;
import com.fasterxml.jackson.databind.JsonNode;
import java.time.Instant;
import java.util.List;

public class Main {
    public static void main(String[] args) throws Exception {
        // Initialize the workspace configuration (Basic Auth)
        WorkspaceConfig config = new WorkspaceConfig(
            "<query-url>",         // Query URL
            "",   
            "basic",               // Authentication method: basic
            null, null, null, null, null,
            "<your-username>",     // Basic Auth username
            "<your-password>",     // Basic Auth password
            30                     // Request timeout (seconds)
        );

        VmpWorkspaceClient client = new VmpWorkspaceClient(config);

        // All the following examples use demo_metric as the metric to be queried.
        // Replace the example values with your actual information:
        // 1. queryUrl/remoteWriteUrl
        // 2. Username and password
        // 3. PromQL expression
        // 4. Time range (start/end)
        // 5. Query parameters, such as step, label key, and series selector

        // 1. Perform an instant query (query)
        // A PromQL instant query returns the query result at the current time or a specified point in time.
        // This example queries the current value of the metric demo_metric.
        JsonNode result = client.query("demo_metric");
        System.out.println("query result:");
        System.out.println(result);

        // Construct a time range: The end time is the current time, and the start time is 5 minutes ago.
        Instant end = Instant.now();
        Instant start = end.minusSeconds(300);

        // 2. Perform a range query (queryRange)
        // Query time series within a specified time range.
        // Arguments:
        // - "demo_metric": A PromQL expression, which can be replaced with your actual information.
        // - start: The start time.
        // - end: End time.
        // - "30s": The query step. This value indicates that a data sample is returned every 30 seconds.
        JsonNode rangeResult = client.queryRange("demo_metric", start, end, "30s");
        System.out.println("queryRange result:");
        System.out.println(rangeResult);

        // 3. Query a set of time series (series)
        // Query a set of time series within a time range based on match[] conditions.
        // Here, {__name__="demo_metric"} is used to query all time series for this metric.
        // To filter by label, pass in the following value:
        // {__name__="demo_metric", job="example", env="test"}
        JsonNode series = client.series(List.of("{__name__=\"demo_metric\"}"), start, end);
        System.out.println("series result:");
        System.out.println(series);

        // 4. Query label keys (labels)
        // Query label keys that have appeared within a specified time range.
        // The third parameter is used to pass in match[] conditions.
        // This example passes in null as the match condition to apply no time series filtering and query all label keys within the specified time range.
        // To apply filtering, pass in the following value:
        // List.of("{__name__=\"demo_metric\"}")
        JsonNode labels = client.labels(start, end, null);
        System.out.println("labels result:");
        System.out.println(labels);

        // 5. Query all values of a label (labelValues)
        // Query all possible values of a specified label within a time range.
        // This example uses the "job" label.
        // Similarly, the fourth parameter is used to pass in match[] conditions.
        // A value of null indicates that filtering by time series is not applied.
        // To query job values only related to demo_metric, pass in the following value:
        // List.of("{__name__=\"demo_metric\"}")
        JsonNode values = client.labelValues("job", start, end, null);
        System.out.println("labelValues result:");
        System.out.println(values);
    }
}
```


<span id="U33Tw0nk"></span>
#### Query metrics through AK/SK authentication

```Java
package com.example.vmp;

import com.example.vmp.VmpWorkspaceClient.WorkspaceConfig;
import com.fasterxml.jackson.databind.JsonNode;
import java.time.Instant;
import java.util.List;

public class Main {
    public static void main(String[] args) throws Exception {
        // Initialize the workspace configuration (AK/SK authentication)
        WorkspaceConfig config = new WorkspaceConfig(
            "<query-url>",         // Query URL
            "",   
            "aksk",                // Authentication method: AK/SK
            "cn-beijing",          // Region
            "vmp",                 // Service
            "<your-access-key>",   // Access Key
            "<your-secret-key>",   // Secret Key
            "",                    // Session Token (If it is not available, pass the empty string)
            null, null,
            30                     // Request timeout (seconds)
        );

        VmpWorkspaceClient client = new VmpWorkspaceClient(config);

        // All the following examples use demo_metric as the metric to be queried.
        // Replace the example values with your actual information:
        // 1. queryUrl/remoteWriteUrl
        // 2. Region and service
        // 3. Access Key, Secret Key, and Session Token
        // 4. PromQL expression
        // 5. Time range (start/end)
        // 6. Query parameters, such as step, label key, and series selector

        // 1. Instant query (query)
        // A PromQL instant query returns the query result at the current time or a specified point in time.
        // This example queries the current value of the metric demo_metric.
        JsonNode result = client.query("demo_metric");
        System.out.println("query result:");
        System.out.println(result);

        // Construct a time range: The end time is the current time, and the start time is 5 minutes ago.
        Instant end = Instant.now();
        Instant start = end.minusSeconds(300);

        // 2. Perform a range query (queryRange)
        // Query time series within a specified time range.
        // Arguments:
        // - "demo_metric": A PromQL expression, which can be replaced with your actual information.
        // - start: The start time.
        // - end: End time.
        // - "30s": The query step. This value indicates that a data sample is returned every 30 seconds.
        JsonNode rangeResult = client.queryRange("demo_metric", start, end, "30s");
        System.out.println("queryRange result:");
        System.out.println(rangeResult);

        // 3. Query a set of time series (series)
        // Query a set of time series within a time range based on match[] conditions.
        // Here, {__name__="demo_metric"} is used to query all time series for this metric.
        // To filter by label, pass in the following value:
        // {__name__="demo_metric", job="example", env="test"}
        JsonNode series = client.series(List.of("{__name__=\"demo_metric\"}"), start, end);
        System.out.println("series result:");
        System.out.println(series);

        // 4. Query label keys (labels)
        // Query label keys that have appeared within a specified time range.
        // The third parameter is used to pass in match[] conditions.
        // This example passes in null as the match condition to apply no time series filtering and query all label keys within the specified time range.
        // To query label keys only related to demo_metric, pass in the following value:
        // List.of("{__name__=\"demo_metric\"}")
        JsonNode labels = client.labels(start, end, null);
        System.out.println("labels result:");
        System.out.println(labels);

        // 5. Query all values of a label (labelValues)
        // Query all possible values of a specified label within a time range.
        // This example uses the "job" label.
        // Similarly, the fourth parameter is used to pass in match[] conditions.
        // A value of null indicates that filtering by time series is not applied.
        // To query job values only related to demo_metric, pass in the following value:
        // List.of("{__name__=\"demo_metric\"}")
        JsonNode values = client.labelValues("job", start, end, null);
        System.out.println("labelValues result:");
        System.out.println(values);
    }
}
```


<span id="ylByWw43"></span>
### Write metric data

<span id="W59XU3p6"></span>
#### Write metrics through basic authentication

```Java
package com.example.vmp;

import com.example.vmp.VmpWorkspaceClient.WorkspaceConfig;
import com.example.vmp.VmpWorkspaceClient.SampleEntry;
import java.time.Instant;
import java.util.LinkedHashMap;
import java.util.List;
import java.util.Map;

public class Main {
    public static void main(String[] args) throws Exception {
        // Initialize the workspace configuration
        WorkspaceConfig config = new WorkspaceConfig(
            "",         
            "<remotewrite-url>",   // Write URL
            "basic",               // Authentication method: basic
            null, null, null, null, null,
            "<your-username>",     // Basic Auth username
            "<your-password>",     // Basic Auth password
            30                     // Request timeout (seconds)
        );

        VmpWorkspaceClient client = new VmpWorkspaceClient(config);

        // Construct a time series sample:
        // Metric name: demo_metric
        // Labels: job=example, env=test
        // Sample value: 42.0
        // Timestamp: current time (milliseconds)
        //
        // Replace the example values with your actual information:
        // 1. Workspace query/write URL
        // 2. Authentication information
        // 3. Metric name (__name__)
        // 4. Labels
        // 5. Sample value and timestamp
        Map<String, String> labels = new LinkedHashMap<>();
        labels.put("__name__", "demo_metric"); // Metric name
        labels.put("job", "example");          // Job label
        labels.put("env", "test");             // Environment label

        String resp = client.writeSamples(List.of(
            new SampleEntry(
                labels,
                42.0,                         // Sample value
                Instant.now().toEpochMilli()  // Timestamp (milliseconds)
            )
        ));

        System.out.println(resp);
    }
}
```


<span id="a9HtpuZE"></span>
#### Write metrics through AK/SK authentication

```Java
package com.example.vmp;

import com.example.vmp.VmpWorkspaceClient.WorkspaceConfig;
import com.example.vmp.VmpWorkspaceClient.SampleEntry;
import java.time.Instant;
import java.util.LinkedHashMap;
import java.util.List;
import java.util.Map;

public class Main {
    public static void main(String[] args) throws Exception {
        // Initialize the workspace configuration
        WorkspaceConfig config = new WorkspaceConfig(
            "",        
            "<remotewrite-url>",   // Write URL
            "basic",               // Authentication method: basic
            null, null, null, null, null,
            "<your-username>",     // Basic Auth username
            "<your-password>",     // Basic Auth password
            30                     // Request timeout (seconds)
        );

        VmpWorkspaceClient client = new VmpWorkspaceClient(config);

        // Construct a time series sample:
        // Metric name: demo_metric
        // Labels: job=example, env=test
        // Sample value: 42.0
        // Timestamp: current time (milliseconds)
        //
        // Replace the example values with your actual information:
        // 1. Workspace query/write URL
        // 2. Authentication information
        // 3. Metric name (__name__)
        // 4. Labels
        // 5. Sample value and timestamp
        Map<String, String> labels = new LinkedHashMap<>();
        labels.put("__name__", "demo_metric"); // Metric name
        labels.put("job", "example");          // Job label
        labels.put("env", "test");             // Environment label

        String resp = client.writeSamples(List.of(
            new SampleEntry(
                labels,
                42.0,                         // Sample value
                Instant.now().toEpochMilli()  // Timestamp (milliseconds)
            )
        ));

        System.out.println(resp);
    }
}
```


<span id="u3UZ67Cl"></span>
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

* The snappy\-java dependency is not imported.

* A network policy or permission restriction blocks access.


**Troubleshooting suggestions:** 


* Confirm whether the write URL is complete (usually ending with /api/v1/write).

* Confirm whether the dependency is successfully imported.

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
