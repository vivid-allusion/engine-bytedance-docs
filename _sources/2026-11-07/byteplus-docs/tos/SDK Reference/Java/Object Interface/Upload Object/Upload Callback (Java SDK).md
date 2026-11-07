---
title: "Upload Callback (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback-java-sdk"
---

An upload callback refers to the process in which the client includes a callback parameter in its request. After the upload is completed, the server sends a synchronous POST callback request to the third\-party application server specified in the callback parameter. The server waits for the third\-party server to confirm receipt and respond with a result before returning the upload results to the client.

For a detailed introduction to upload callback, see [Upload Callback](https://docs.byteplus.com/docs/tos/Upload-callback).

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

Beginning with version 2.6.0, the Java SDK supports configuring upload callback parameters in the putObject and completeMultipartUpload interfaces.

<span id="f28c75a9"></span>
### Implementation of upload callback via standard upload

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;

public class PutObjectWithCallbackExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        String callback = "your callback param";
        String callbackVar = "your callback custom variable";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            String data = "1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'";
            byte[] dataInBytes = data.getBytes();
            ByteArrayInputStream stream = new ByteArrayInputStream(dataInBytes);
            PutObjectInput putObjectInput = new PutObjectInput()
                    .setBucket(bucketName).setKey(objectKey).setContent(stream)
                    .setCallback(Base64.getEncoder().encodeToString(callback.getBytes(StandardCharsets.UTF_8)))
                    .setCallbackVar(Base64.getEncoder().encodeToString(callbackVar.getBytes(StandardCharsets.UTF_8)));
            PutObjectOutput output = tos.putObject(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="9e7c424c"></span>
### Implementation of upload callbacks for multipart uploads

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.CompleteMultipartUploadV2Input;
import com.volcengine.tos.model.object.CompleteMultipartUploadV2Output;
import com.volcengine.tos.model.object.UploadedPartV2;

import java.nio.charset.StandardCharsets;
import java.util.ArrayList;
import java.util.Base64;
import java.util.List;

public class CompleteMultipartWithCallbackExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        String uploadId = "the specific uploadId";

        String callback = "your callback param";
        String callbackVar = "your callback custom variable";

        List<UploadedPartV2> uploadedParts = new ArrayList<>();

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            CompleteMultipartUploadV2Input complete = new CompleteMultipartUploadV2Input().setBucket(bucketName)
                    .setKey(objectKey).setUploadID(uploadId)
                    .setCallback(Base64.getEncoder().encodeToString(callback.getBytes(StandardCharsets.UTF_8)))
                    .setCallbackVar(Base64.getEncoder().encodeToString(callbackVar.getBytes(StandardCharsets.UTF_8)));
            complete.setUploadedParts(uploadedParts);

            CompleteMultipartUploadV2Output completedOutput = tos.completeMultipartUpload(complete);
            System.out.printf("completeMultipartUpload succeed, etag is %s, crc64 value is %s, location is %s.\n",
                    completedOutput.getEtag(), completedOutput.getHashCrc64ecma(), completedOutput.getLocation());
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="f447cb7f"></span>
### Sample Code for Verifying Callback Signatures

```Java
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLDecoder;
import java.nio.charset.StandardCharsets;
import java.security.*;
import java.security.spec.X509EncodedKeySpec;
import java.util.*;

public class CallbackHandler {
    private static final String AUTHORIZATION = "Authorization";
    private static final String XTOS_PUBLIC_KEY_URL = "x-tos-pub-key-url";

    public void callbackHandler(HttpServletRequest req, HttpServletResponse resp) {
        byte[] sign = getSignature(req);
        if (sign == null) {
            System.out.println("get callback signature error");
            resp.setStatus(HttpServletResponse.SC_BAD_REQUEST);
            return;
        }

        byte[] publicKey = getPublicKey(req);
        if (publicKey == null) {
            resp.setStatus(HttpServletResponse.SC_BAD_REQUEST);
            return;
        }

        String stringToSign;
        try {
            stringToSign = getStringToSign(req);
        } catch (IOException | NoSuchAlgorithmException e) {
            resp.setStatus(HttpServletResponse.SC_BAD_REQUEST);
            return;
        }

        try {
            verifySignature(publicKey, stringToSign, sign);
            resp.setStatus(HttpServletResponse.SC_OK);
            resp.getWriter().write("{\"Status\":\"OK\"}");
        } catch (Exception e) {
            resp.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
        }
    }

    public byte[] getSignature(HttpServletRequest req) {
        String authorization = req.getHeader(AUTHORIZATION);
        if (authorization == null || authorization.isEmpty()) {
            return null;
        }
        return Base64.getDecoder().decode(authorization);
    }

    public byte[] getPublicKey(HttpServletRequest req) {
        byte[] bytePublicKey = null;
        String publicKeyURLBase64 = req.getHeader(XTOS_PUBLIC_KEY_URL);
        if (publicKeyURLBase64 == null || publicKeyURLBase64.isEmpty()) {
            return bytePublicKey;
        }
        byte[] publicKeyURLBytes = Base64.getDecoder().decode(publicKeyURLBase64);

        try {
            URL url = new URL(new String(publicKeyURLBytes));
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            if (connection.getResponseCode() >= HttpURLConnection.HTTP_BAD_REQUEST) {
                throw new IOException("Get public key failed");
            }
            ByteArrayOutputStream buffer = new ByteArrayOutputStream();
            int nRead;
            byte[] data = new byte[16384];
            while ((nRead = connection.getInputStream().read(data, 0, data.length)) != -1) {
                buffer.write(data, 0, nRead);
            }
            buffer.flush();
            bytePublicKey = buffer.toByteArray();
            connection.disconnect();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return bytePublicKey;
    }

    public String getStringToSign(HttpServletRequest req) throws IOException, NoSuchAlgorithmException {
        ByteArrayOutputStream buffer = new ByteArrayOutputStream();
        byte[] buff = new byte[16384];

        int nRead;
        while ((nRead = req.getInputStream().read(buff, 0, buff.length)) != -1) {
            buffer.write(buff, 0, nRead);
        }
        buffer.flush();
        byte[] bodyContent = buffer.toByteArray();
        String stringToSign = calcStringToSign(req, bodyContent);
        System.out.println(stringToSign);
        System.out.println(new String(bodyContent, StandardCharsets.UTF_8));
        return stringToSign;
    }

    public String calcStringToSign(HttpServletRequest req, byte[] body) {
        StringBuilder buf = new StringBuilder();
        String path = req.getRequestURI();
        buf.append(path);

        String queryString = req.getQueryString();
        Map<String, List<String>> sortedParams = new TreeMap<>();
        if (queryString != null && !queryString.isEmpty()) {
            String[] pairs = queryString.split("&");
            for (String pair : pairs) {
                int idx = pair.indexOf("=");
                String key = (idx > 0) ? pair.substring(0, idx) : pair;
                String value = (idx > 0 && pair.length() > idx + 1) ? pair.substring(idx + 1) : "";
                try {
                    key = URLDecoder.decode(key, StandardCharsets.UTF_8.name());
                    value = URLDecoder.decode(value, StandardCharsets.UTF_8.name());
                } catch (UnsupportedEncodingException e) {
                    throw new RuntimeException(e);
                }
                sortedParams.computeIfAbsent(key, k -> new ArrayList<>()).add(value);
            }
        }

        if (!sortedParams.isEmpty()) {
            buf.append('?');
            boolean firstKey = true;
            for (Map.Entry<String, List<String>> entry : sortedParams.entrySet()) {
                String key = entry.getKey();
                List<String> values = entry.getValue();
                Collections.sort(values);
                for (String value : values) {
                    if (!firstKey) {
                        buf.append('&');
                    }
                    buf.append(key).append('=').append(value);
                    firstKey = false;
                }
            }
        }

        buf.append('\n');
        buf.append(new String(body, StandardCharsets.UTF_8));
        return buf.toString();
    }

    public PublicKey loadPublicKey(byte[] publicKeyPEMBytes) throws Exception {
        String publicKeyPEM = new String(publicKeyPEMBytes, StandardCharsets.UTF_8);

        String publicKeyPEMFormatted = publicKeyPEM
                .replace("-----BEGIN PUBLIC KEY-----", "")
                .replace("-----END PUBLIC KEY-----", "")
                .replaceAll("\\s+", ""); 

        byte[] encoded = Base64.getDecoder().decode(publicKeyPEMFormatted);

        KeyFactory keyFactory = KeyFactory.getInstance("RSA");
        X509EncodedKeySpec keySpec = new X509EncodedKeySpec(encoded);
        return keyFactory.generatePublic(keySpec);
    }

    public void verifySignature(byte[] publicKey, String stringToSign, byte[] sign) throws Exception {
        PublicKey pubKey = loadPublicKey(publicKey);

        Signature verifier = Signature.getInstance("MD5withRSA");
        verifier.initVerify(pubKey);
        verifier.update(stringToSign.getBytes(StandardCharsets.UTF_8));

        if (!verifier.verify(sign)) {
            throw new SignatureException("Invalid signature");
        }
    }
}
```
