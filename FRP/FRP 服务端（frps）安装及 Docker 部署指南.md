------

# 🚀 FRP 服务端（frps）安装及 Docker 部署指南

> **FRP（Fast Reverse Proxy）** 是一款高性能的反向代理应用，主要用于将位于 NAT 或防火墙后的局域网服务器暴露到互联网。
>  🔗 详细信息请参阅 [**GitHub - fatedier/frp**](https://github.com/fatedier/frp)。

------

## 📦 前期准备

在开始操作之前，请确认已安装并配置好：

- [✅ Docker](https://docs.docker.com/get-docker/)
- [✅ Docker Compose](https://docs.docker.com/compose/install/)

如需详细安装步骤，可参考官方文档。

------

## 🛠️ 1. 创建工作目录及配置文件

### 📁 创建目录

```bash
cd /opt
mkdir frp
cd frp/
```

------

### 📝 1.1 编写 FRP 服务端配置文件

使用编辑器创建 `frps.ini` 文件：

```bash
vi frps.ini
```

🔧 推荐配置内容如下：

```ini
[common]
# 🚪 FRP 服务端监听端口（客户端连接使用）
bind_port = 7000

# 🖥️ 管理面板配置
dashboard_port = 7500
dashboard_user = admin
dashboard_pwd = admin

# 🔐 身份验证令牌（客户端也要一致）
token = admin

# 🌐 支持基于域名的 HTTP/HTTPS 映射
vhost_http_port = 80
vhost_https_port = 443

# 🪵 日志设置
log_level = info
log_file = /var/log/frps.log
log_max_days = 3

# ⚙️ 高级配置（可选）
# kcp_bind_port = 7000
# max_pool_count = 5
# server_name = my-frps
```

💡 **配置说明：**

- `bind_port`: 客户端连接使用的端口。
- `vhost_http_port` / `vhost_https_port`: 用于将本地服务通过域名暴露为网站访问。
- `dashboard_*`: 登录面板的账号和密码。
- `token`: 身份验证令牌，客户端也需保持一致。
- `log_file`: 日志文件路径（可选）。

> 💾 编辑完成后，输入 `:wq` 保存退出。

------

## ⚙️ 2. 编写 Docker Compose 文件

创建 `docker-compose.yml` 文件：

```bash
vi docker-compose.yml
```

📄 配置内容如下：

```yaml
version: "3.3"
services:
  frps:
    image: registry.cn-hangzhou.aliyuncs.com/dgx_00/frps
    container_name: frps
    network_mode: "host"  # ☝️ 使用主机网络模式，确保端口直通公网
    volumes:
      - ./frps.ini:/etc/frp/frps.ini
    restart: always
```

> 💾 保存退出：`:wq`

------

## ▶️ 3. 启动 Docker 容器

### 🔄 3.1 拉取镜像并启动容器

```bash
docker compose up -d
```

### 🔍 3.2 检查容器运行状态

```bash
docker ps
```

✅ 成功运行时输出示例：

```
CONTAINER ID   IMAGE                                           COMMAND                  CREATED       STATUS       NAMES
f9303f6ff4f6   registry.cn-hangzhou.aliyuncs.com/dgx_00/frps   "/bin/sh -c '/usr/bi…"   7 hours ago   Up 4 hours   frps
```

------

## 🌐 4. 访问 FRP 管理面板

打开浏览器，访问以下地址（将 `你的IP` 替换为服务器公网 IP）：

```
http://你的IP:7500
```

🔐 默认账号密码：

```
用户名：admin
密码：admin
```

------

## 🖼️ 截图示例

> 请确认图片路径正确，或上传至图床使用外链形式展示。

![FRP 管理面板](file:///C:/%5CUsers%5C34861%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20250416172821909.png)

------

## ✅ 总结

🎉 以上就是通过 **Docker 快速部署 FRP 服务端（frps）** 的完整流程。配置简单，部署高效。

如需进一步定制，推荐阅读官方文档 👉 https://github.com/fatedier/frp

------

