---
title: "Configuring endpoint generator"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Configure_the_endpoint_generator"
---

This topic describes how to configure a Vortex IP proxy for an Elastic Compute Service (ECS) and access the target site.

## Configure a proxy

### Step 1: Generate an endpoint

1. Log in to the [Vortex IP console](https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips).

2. In the top menu bar, select the region.

3. In the Vortex IP list, click **Endpoint generator** to the right of the target Vortex IP to pop up the Endpoint generator window.

4. Configure parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Country/region |Select your target country and region. For details, see [Vortex IP service scope](https://docs.byteplus.com/en/docs/gavi-sept-test1/Vortex_IP_service_scope_list).<br><br>> **tip**<br><br><br>> Currently, Vortex IPs with a service type of **Video\-specific proxy** do not support selecting country/region.<br> |us |
   |City |Select your target city. |Random |
   |Session persistence |Specify whether to enable session persistence.<br><br><br>* Enable: Requests with the same session ID (Security Identifier) use the same Elastic IP Address (EIP) to access. You can customize the session persistence duration in minutes. After the duration expires, the system automatically changes the IP for access requests.​<br><br>* Disable: The EIP changes with each request by default. |Disable |
   |Output format |Select the output format for the egress IP. Supports **Endpoint: Port** and three access protocols: **HTTP**, **HTTPS**, and **SOCKS5**.<br><br>> **tip**<br><br><br>> For Vortex IP instances in Internet access mode, we recommended selecting the **HTTPS** format to improve network reliability.<br> |HTTPS |

5. Click **Generate** to automatically generate endpoint information.

6. Copy the endpoint information to configure a proxy for the ECS instance using Vortex IP.

### Step 2: Configure a proxy

Select a proper configuration according to your application scenario.

**Linux**

All applications on the Linux ECS instance support using Vortex IP to access target websites.

Log in to the ECS instance where you want to access the target website and set global environment variables.

```Plain Text
export http_proxy=<Copied Endpoint Information>
export https_proxy=<Copied Endpoint Information>
```

To access non\-target websites with the ECS instance, you need to configure no_proxy, and separate multiple domains or IPs with commas (,).

```Plain Text
export no_proxy=*.example.com,*.example.cn
```

**Docker configuration for regular install**

If you need Docker containers on an ECS instance to access target websites, configure the proxy settings based on your installation mode by selecting the appropriate content. For more information, see [the official Docker documentation](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy).

The Docker configuration for regular install is as follows:

1. Run the following command to create a directory for the Docker service.

`sudo mkdir -p /etc/systemd/system/docker.service.d`

2. Run the following command to create a new proxy file.

`sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf`

3. Press `i` to enter edit mode and add the following content:

```Plain Text
[Service]
Environment="HTTP_PROXY=<Copied Endpoint Information>"
Environment="HTTPS_PROXY=<Copied Endpoint Information>"
```

4. Press `ESC` to exit edit mode, enter `:wq`, and press `Enter` to save and exit.

5. If you need to access non\-target websites, set environment variable to NO_PROXY. Separate multiple IPs or domains with commas (,). Reference format is as follows:

   * IP address (e.g., `12.XX.XX.89`).

   * Domain name (e.g., `foo.example.com`, `*.example.com`).

   * The domain name can match the domain and all sub\-domains. The domain name starting with "." can only match sub\-domains. For example, the given domain names are `foo.example.com` and `example.com`:

      * `example.com` matches both `example.com` and `foo.example.com`.

      * `.example.com` only matches `foo.example.com`.

   * The asterisk (`*`) indicates that all IPs and domains registered with Docker do not require FastTrack proxy access.

   * IP address (`12.XX.XX.89:80`) and domain name (`foo.example.com:80`) support adding ports.

Configuration example:

```Plain Text
[Service]
Environment="HTTP_PROXY=<Copied Endpoint Information>"
Environment="HTTPS_PROXY=<Copied Endpoint Information>"
Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp"
```

> **tip**

> You can modify the docker\-registry.example.com,.corp in this example as needed.

6. Refresh and restart Docker.

```Plain Text
sudo systemctl daemon-reload
sudo systemctl restart docker
```

7. Verify.

```Plain Text
sudo systemctl show --property=Environment docker
Environment=HTTP_PROXY=<Copied Endpoint Information> HTTPS_PROXY=<Copied Endpoint Information> NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp
```

**Docker configuration for rootless mode**

If you need Docker containers on an ECS instance to access target websites, configure the proxy settings based on your installation mode by selecting the appropriate content. For more information, see [the official Docker documentation](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy).

The following is the Docker configuration for rootless mode:

1. Run the following command to create the systemd drop\-in directory for the Docker service.

`mkdir -p ~/.config/systemd/user/docker.service.d`

2. Run the following command to create a new proxy file.

`vim ~/.config/systemd/user/docker.service.d/http-proxy.conf`

3. Press `i` to enter edit mode and add the following content:

```Plain Text
[Service]
Environment="HTTP_PROXY=<Copied Endpoint Information>"
Environment="HTTPS_PROXY=<Copied Endpoint Information>"
```

4. Press `ESC` to exit edit mode, enter `:wq`, and press `Enter` to save and exit.

5. If you need to access non\-target websites, set environment variable to `NO_PROXY`. Separate multiple IPs or domains with commas (,). Reference format is as follows:

   * IP address (e.g., `12.XX.XX.89`).

   * Domain name (e.g., `foo.example.com`, `*.example.com`).

   * The domain name can match the domain and all sub\-domains. The domain name starting with "." can only match sub\-domains. For example, the given the domain names are `foo.example.com` and `example.com`:

      * `example.com` matches both `example.com` and `foo.example.com`.

      * `.example.com` only matches `foo.example.com`.

   * The asterisk (`*`) indicates that all IPs and domains registered with Docker do not require FastTrack proxy access.

   * IP address (`12.XX.XX.89:80`) and domain name (`foo.example.com:80`) support adding ports.

Configuration example:

```Plain Text
[Service]
Environment="HTTP_PROXY=<Copied Endpoint Information>"
Environment="HTTPS_PROXY=<Copied Endpoint Information>"
Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp"
```

> **tip**

> You can modify the docker\-registry.example.com,.corp in this example as needed.

6. Run the following command to refresh and restart Docker.

```Plain Text
systemctl --user daemon-reload
systemctl --user restart docker
```

7. Run the following command to verify.

```Plain Text
systemctl --user show --property=Environment docker
Environment=HTTP_PROXY=http://proxy.example.com:80 HTTPS_PROXY=https://proxy.example.com:443              NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp
```

**Containerd configuration**

If you need the containerd of an ECS instance to access the target website, follow the configuration procedure below.

1. Run the following command to create a new proxy file.

`sudo vim /etc/systemd/system/containerd.service.d/http-proxy.conf`

2. Press i to enter edit mode and add the following content:

```Plain Text
[Service]
Environment="HTTP_PROXY=<Copied Endpoint Information>"
Environment="HTTPS_PROXY=<Copied Endpoint Information>"
```

3. Press `ESC` to exit edit mode, enter `:wq`, and press `Enter` to save and exit.

4. If you need to access non\-target websites, set environment variable to `NO_PROXY`. Separate multiple IPs or domains with commas (,). Reference format is as follows:

   * IP address (e.g., `12.XX.XX.89`).

   * Domain name (e.g., `foo.example.com`, `*.example.com`).

   * The domain name can match the domain and all sub\-domains. The domain name starting with "." can only match sub\-domains. For example, the given domain names are `foo.example.com` and `example.com`:

      * `example.com` matches both `example.com` and `foo.example.com`.

      * `.example.com` only matches `foo.example.com`.

   * The asterisk (`*`) indicates that all IPs and domains registered with Docker do not require FastTrack proxy access.

   * IP address (`12.XX.XX.89:80`) and domain name (`foo.example.com:80`) support adding ports.

Configuration example:

```Plain Text
[Service]
Environment="HTTP_PROXY=<Copied Endpoint Information>"
Environment="HTTPS_PROXY=<Copied Endpoint Information>"
Environment="NO_PROXY=localhost,127.0.0.1,*.example.com,.corp"
```

> **tip**

> You can modify \*.example.com,.corp in this example as needed.

5. Run the following command to refresh and restart containerd.

```Plain Text
systemctl daemon-reload
systemctl restart containerd
```

## Access the target site

After configuring the Vortex IP proxy, you can refer to the following code examples to access the target site.

### Curl

**http**

#### Access code

```HTTP
curl DESTHOST -x http://proxy-cot-COUNTRY-sid-SESSIONID:PASSWORD@ENDPOINT
```

* `DESTHOST`: Target site.

* `COUNTRY`: Country of the public egress.

* `SESSIONID`: Session persistence ID. (A string of 8 random digits, and each `SESSIONID` corresponds to one egress IP address.)

* `PASSWORD`: Password of the Vortex IP instance.

* `ENDPOINT`: Endpoint information of the Vortex IP instance.

#### Access example

```HTTP
curl https://ipinfo.io -x http://proxy-cot-us-sid-57141777:ps9ang1f***@vortex-3o63sg3g18h6o87eayewacr6m.vortexip.ap-southeast-1.volces.com:8080
```

**https**

#### Access code

```HTTP
curl DESTHOST -x https://proxy-cot-COUNTRY-sid-SESSIONID:PASSWORD@ENDPOINT
```

* `DESTHOST`: Target site.

* `COUNTRY`: Country of the public egress.

* `SESSIONID`: Session persistence ID. (A string of 8 random digits, and each `SESSIONID` corresponds to one egress IP address.)

* `PASSWORD`: Password of the Vortex IP instance.

* `ENDPOINT`: Endpoint information of the Vortex IP instance.

#### Access example

```HTTP
curl https://ipinfo.io -x https://proxy-cot-us-sid-97251277:ps9ang1f***@vortex-3o63sg3g18h6o87eayewacr6m.vortexip.ap-southeast-1.volces.com:18080
```

**socks5**

#### Access code

```HTTP
curl DESTHOST -x socks5h://proxy-cot-COUNTRY-sid-SESSIONID:PASSWORD@ENDPOINT
```

* `DESTHOST`: Target site.

* `COUNTRY`: Country of the public egress.

* `SESSIONID`: Session persistence ID. (A string of 8 random digits, and each `SESSIONID` corresponds to one egress IP address.)

* `PASSWORD`: Password of the Vortex IP instance.

* `ENDPOINT`: Endpoint information of the Vortex IP instance.

#### Access example

```HTTP
curl https://ipinfo.io -x socks5h://proxy-cot-us-sid-34755344:ps9ang1f***@vortex-3o63sg3g18h6o87eayewacr6m.vortexip.ap-southeast-1.volces.com:28080
```

### Python

**http**

#### Access code example

```Python
import requests
# Replace with the endpoint information of your VortexIP instance.
proxy_host = 'vortex-xxxxxx.vortexip.ap-southeast-1.volces.com'
# Select the country of the egress IP as needed. Leave an empty string '' if no specific country is required.
proxy_country = 'us'
# One session persistence ID corresponds to one egress IP, so generate sid randomly for large-scale access.
proxy_session_id = '12345678'
proxy_user = 'proxy'
proxy_password = 'xxxxxx'
http_port = 8080
request_timeout = 30

if proxy_country != '':
    proxy_user = f'{proxy_user}-cot-{proxy_country}'
if proxy_session_id != '':
    proxy_user = f'{proxy_user}-sid-{proxy_session_id}'

http_proxy_endpoint = f'http://{proxy_user}:{proxy_password}@{proxy_host}:{http_port}'

# Build the proxy
proxies = {
   'http': http_proxy_endpoint
}

# Target URL to access
url = 'https://ipinfo.io'

try:
    print("Connecting through proxy...")
    response = requests.get(url, proxies=proxies, timeout=request_timeout)  # Set 10-second timeout
    response.raise_for_status()  # Throw an exception if request fails (returns a non-2xx status code).

    print(f"Site Response: {response.text}")

except requests.exceptions.ProxyError as e:
    print(f"Proxy connection failed: {e}")
except requests.exceptions.ConnectTimeout as e:
    print(f"Proxy connection timed out: {e}")
except requests.exceptions.RequestException as e:
    print(f"Request error occurred: {e}")
except Exception as e:
    print(f"--- An unexpected error occurred ---")
    print(f"Error type: {type(e).__name__}")
    print(f"Error message: {e}")
```

**https**

#### Access code example

```Python
import requests
# Replace with the endpoint information of your VortexIP instance.
proxy_host = 'vortex-xxxxxx.vortexip.ap-southeast-1.volces.com'
# Select the country of the egress IP as needed. Leave an empty string '' if no specific country is required.
proxy_country = 'us'
# One session persistence ID corresponds to one egress IP, so generate sid randomly for large-scale access.
proxy_session_id = '12345678'
proxy_user = 'proxy'
proxy_password = 'xxxxxx'
https_port = 18080
request_timeout = 30

if proxy_country != '':
    proxy_user = f'{proxy_user}-cot-{proxy_country}'
if proxy_session_id != '':
    proxy_user = f'{proxy_user}-sid-{proxy_session_id}'

https_proxy_endpoint = f'https://{proxy_user}:{proxy_password}@{proxy_host}:{https_port}'

# Build the proxy
proxies = {
   'https': http_proxy_endpoint
}

# Target URL to access
url = 'https://ipinfo.io'

try:
    print("Connecting through proxy...")
    response = requests.get(url, proxies=proxies, timeout=request_timeout)  # Set 10-second timeout
    response.raise_for_status()  # Throw an exception if request fails (returns a non-2xx status code).

    print(f"Site Response: {response.text}")

except requests.exceptions.ProxyError as e:
    print(f"Proxy connection failed: {e}")
except requests.exceptions.ConnectTimeout as e:
    print(f"Proxy connection timed out: {e}")
except requests.exceptions.RequestException as e:
    print(f"Request error occurred: {e}")
except Exception as e:
    print(f"--- An unexpected error occurred ---")
    print(f"Error type: {type(e).__name__}")
    print(f"Error message: {e}")
```

**socks5**

#### Access code example

```Python
import requests
# Replace with the endpoint information of your VortexIP instance.
proxy_host = 'vortex-xxxxxx.vortexip.ap-southeast-1.volces.com'
# Select the country of the egress IP as needed. Leave an empty string '' if no specific country is required.
proxy_country = 'us'
# One session persistence ID corresponds to one egress IP, so generate sid randomly for large-scale access.
proxy_session_id = '12345678'
proxy_user = 'proxy'
proxy_password = 'xxxxxx'
socks5_port = 28080
request_timeout = 30

if proxy_country != '':
    proxy_user = f'{proxy_user}-cot-{proxy_country}'
if proxy_session_id != '':
    proxy_user = f'{proxy_user}-sid-{proxy_session_id}'

# Using a socks5 proxy requires installing a Python package that supports socks.
socks5_proxy_endpoint = f'socks5h://{proxy_user}:{proxy_password}@{proxy_host}:{socks5_port}'

# Build the proxy
proxies = {
   'socks5': socks5_proxy_endpoint
}

# Target URL to access
url = 'https://ipinfo.io'

try:
    print("Connecting through proxy...")
    response = requests.get(url, proxies=proxies, timeout=request_timeout)  # Set 10-second timeout
    response.raise_for_status()  # Throw an exception if request fails (returns a non-2xx status code).

    print(f"Site Response: {response.text}")

except requests.exceptions.ProxyError as e:
    print(f"Proxy connection failed: {e}")
except requests.exceptions.ConnectTimeout as e:
    print(f"Proxy connection timed out: {e}")
except requests.exceptions.RequestException as e:
    print(f"Request error occurred: {e}")
except Exception as e:
    print(f"--- An unexpected error occurred ---")
    print(f"Error type: {type(e).__name__}")
    print(f"Error message: {e}")
```

### Golang

**http**

#### Access code example

```Go
package main

import (
        "fmt"
        "io"
        "log"
        "net/http"
        "net/url"
        "golang.org/x/net/proxy"
)

func main() {
        // Target website to access
        targetURL := "https://ipinfo.io"
        proxy_host := "vortex-xxxxxx.vortexip.ap-southeast-1.volces.com"
        // Select the country of the egress IP as needed. Leave empty string "" if no specific country is required.
        proxy_country := "us"
        // One session persistence ID corresponds to one egress IP, so generate sid randomly for large-scale access.
        proxy_session_id := "12345678"
        proxy_user := "proxy"
        proxy_password := "xxxxxxx"     
        http_port := 8080

        if proxy_country != "" {
                proxy_user = proxy_user + "-cot-" + proxy_country
        }

        if proxy_session_id != "" {
                proxy_user = proxy_user + "-sid-" + proxy_session_id
        }

        httpProxyEdnpoint := fmt.Sprintf("http://%s:%s@%s:%d", proxy_user, proxy_password, proxy_host, http_port)
        
        fmt.Println(httpProxyEdnpoint)
        
        proxyURL, err := url.Parse(httpProxyEdnpoint)
        if err != nil {
                log.Fatalf("Failed to parse proxy address: %v", err)
        }
        // Create a custom Transport and set the Proxy field.
        transport := &http.Transport{
                Proxy: http.ProxyURL(proxyURL),
        }       

        // Create an http.Client using this Transport.
        client := &http.Client{
                Transport: transport,
        }

        fmt.Printf("Connecting through proxy%s...\n", targetURL)

        // Send requests using a custom Client.
        resp, err := client.Get(targetURL)
        if err != nil {
                log.Fatalf("Request failed: %v", err)
        }
        defer resp.Body.Close()

        // Read and print response content.
        body, err := io.ReadAll(resp.Body)
        if err != nil {
                log.Fatalf("Failed to read response body: %v", err)
        }

        fmt.Printf("Status code: %s\n", resp.Status)
        fmt.Printf("Response: %s\n", string(body))
}
```

**https**

#### Access code example

```Go
package main

import (
        "fmt"
        "io"
        "log"
        "net/http"
        "net/url"
        "golang.org/x/net/proxy"
)

func main() {
        // Target website to access
        targetURL := "https://ipinfo.io"
        proxy_host := "vortex-xxxxxx.vortexip.ap-southeast-1.volces.com"
        // Select the country of the egress IP as needed. Leave an empty string "" if no specific country is required.
        proxy_country := "us"
        // One session persistence ID corresponds to one egress IP, so generate sid randomly for large-scale access.
        proxy_session_id := "12345678"
        proxy_user := "proxy"
        proxy_password := "xxxxxxx"
        https_port := 18080
        
        if proxy_country != "" {
                proxy_user = proxy_user + "-cot-" + proxy_country
        }

        if proxy_session_id != "" {
                proxy_user = proxy_user + "-sid-" + proxy_session_id
        }
        
        httpsProxyEdnpoint := fmt.Sprintf("https://%s:%s@%s:%d", proxy_user, proxy_password, proxy_host, https_port)

        fmt.Println(httpsProxyEdnpoint)
        
        proxyURL, err := url.Parse(httpsProxyEdnpoint)
        if err != nil {
                log.Fatalf("Failed to parse proxy address: %v", err)
        }
        // Create a custom Transport and set the Proxy field.
        transport := &https.Transport{
                Proxy: https.ProxyURL(proxyURL),
        }
        // Create an http.Client using this Transport.
        client := &http.Client{
                Transport: transport,
        }


        fmt.Printf("Connecting through proxy%s...\n", targetURL)

        // Send requests using a custom Client.
        resp, err := client.Get(targetURL)
        if err != nil {
                log.Fatalf("Request failed: %v", err)
        }
        defer resp.Body.Close()

        // Read and print response content.
        body, err := io.ReadAll(resp.Body)
        if err != nil {
                log.Fatalf("Failed to read response body: %v", err)
        }

        fmt.Printf("Status code: %s\n", resp.Status)
        fmt.Printf("Response: %s\n", string(body))
}
```

**socks5**

#### Access code example

```Go
package main

import (
        "fmt"
        "io"
        "log"
        "net/http"
        "net/url"
        "golang.org/x/net/proxy"
)

func main() {
        // Target website to access
        targetURL := "https://ipinfo.io"
        proxy_host := "vortex-xxxxxx.vortexip.ap-southeast-1.volces.com"
        // Select the country of the egress IP as needed. Leave an empty string "" if no specific country is required.
        proxy_country := "us"
        // One session persistence ID corresponds to one egress IP, so generate sid randomly for large-scale access.
        proxy_session_id := "12345678"
        proxy_user := "proxy"
        proxy_password := "xxxxxxx"
        socks5_port := 28080

        if proxy_country != "" {
                proxy_user = proxy_user + "-cot-" + proxy_country
        }

        if proxy_session_id != "" {
                proxy_user = proxy_user + "-sid-" + proxy_session_id
        }

        proxyAddr := fmt.Sprintf("%s:%d", proxy_host, socks5_port)
        auth := &proxy.Auth{
                User:     proxy_user,
                Password: proxy_password,
        }
        dialer, err := proxy.SOCKS5("tcp", proxyAddr, auth, proxy.Direct)
        
        if err != nil {
                log.Fatalf("Failed to create SOCKS5 dialer: %v", err)
        }
        
        transport := &http.Transport{
                // Use DialContext instead of Dial because Dial is deprecated.
                DialContext: func(ctx context.Context, network, addr string) (net.Conn, error) {
                        return dialer.Dial(network, addr)
                },
        }

        // Create an http.Client using this Transport.
        client := &http.Client{
                Transport: transport,
        }

        fmt.Printf("Connecting through proxy%s...\n", targetURL)

        // Send requests using a custom Client.
        resp, err := client.Get(targetURL)
        if err != nil {
                log.Fatalf("Request failed: %v", err)
        }
        defer resp.Body.Close()

        // Read and print response content.
        body, err := io.ReadAll(resp.Body)
        if err != nil {
                log.Fatalf("Failed to read response body: %v", err)
        }

        fmt.Printf("Status code: %s\n", resp.Status)
        fmt.Printf("Response: %s\n", string(body))
}
```
