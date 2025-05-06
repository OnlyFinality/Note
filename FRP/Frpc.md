### Docker-Compose文件

`docker-compose.yml` 文件的内容

```yaml
version: '3.8'

services:
  frpc:
    image: snowdreamtech/frpc
    container_name: frpc
    restart: unless-stopped
    volumes:
      - ./frpc.toml:/etc/frp/frpc.toml
    network_mode: "host"
```

### Frpc 配置文件 (`frpc.toml`)

以下是 `frpc.toml` 文件的示例配置，用于连接 FRP 服务并配置代理：

```toml
# FRP 服务器地址与端口
serverAddr = "frp.freefrp.net"
serverPort = 7000

# 身份验证配置
auth.method = "token"
auth.token = "freefrp.net"

# Web 控制台配置
webServer.addr = "0.0.0.0"
webServer.port = 7400
webServer.user = "admin"
webServer.password = "12345678"
webServer.pprofEnable = false

# HTTP 代理配置
[[proxies]]
name = "nas_hhfynbtumnytg_http" # 随便写
type = "http"
localIP = "127.0.0.1"
localPort = 80
customDomains = ["*.demo.com"]

# HTTPS 代理配置
[[proxies]]
name = "nas_bryhayjjryjttu_https"
type = "https"
localIP = "127.0.0.1"
localPort = 443
customDomains = ["*.demo.com"]

# TLS 配置 (可选)
# transport.tls.certFile = "/etc/frp/ssl/client.crt"
# transport.tls.keyFile = "/etc/frp/ssl/client.key"
# transport.tls.trustedCaFile = "/etc/frp/ssl/ca.crt"
```
   

---

### 安装步骤

1. **编写 `docker-compose.yml` 文件**  
    创建 `docker-compose.yml
2. **编写 `frpc.toml` 配置文件**  
    创建 `frpc.toml` 的文件
3. **启动容器**  
	```BASH
	docker compose up -d	
```
1. **访问 Web 管理界面**  
    访问 `http://<your-server-ip>:7400`
---
[[Frps]]