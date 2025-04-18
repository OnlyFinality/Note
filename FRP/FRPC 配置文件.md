------

## frpc 配置文件示例

### 什么是 frpc？

`frpc` 是 [frp](https://github.com/fatedier/frp) 的客户端部分，主要运行在内网环境中。它的作用是把内网中的服务（比如 Web 应用、SSH 服务等）通过配置好的代理规则，转发到公网中的 `frps` 服务端。

常见的使用场景包括：

- 远程访问家里的 NAS、路由器或开发环境
- 给本地开发环境映射一个公网地址用于调试
- 内网穿透，实现反向代理

下面是一个常用的 `frpc.ini` 配置示例，包含了基本的连接设置、Web 控制台配置，以及几种代理规则。

```ini
[common]
server_addr = xx.xx.xx.xx # frps 服务端地址
server_port = 7000

auth.token = "admin"

# Web服务器的配置
[webServer]
webServer.addr = "0.0.0.0"
webServer.port = 7400
webServer.user = "admin" 
webServer.password = "12345678"
webServer.pprofEnable = false # 是否启用 pprof 性能分析接口

[[proxies]]
name = "ssh-proxy"
type = "tcp"
localIP = "127.0.1.0" #本机IP
localPort = 22 
remotePort = 8822 # 转发端口

[[proxies]]
name = "nas_http"
type = "http"
localIP = "127.0.0.1"
localPort = 80
customDomains = ["*.example.com"] # 自定义域名，需配置DNS解析

[[proxies]]
name = "nas_https"
type = "https"
localIP = "127.0.0.1"
localPort = 443
customDomains = ["*.example.com"] # 与HTTP一致，支持HTTPS
```