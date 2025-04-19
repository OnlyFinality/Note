###  **修改 DockerHub 镜像源**

1. 进入 Docker 配置目录：

```bash
cd /etc/docker
```

1. 编辑配置文件 `daemon.json`：

```bash
sudo vi daemon.json
```

1. 添加如下内容（如已有内容请合并）：

```json
{
  "registry-mirrors": ["https://docker.1ms.run"]
}
```

1. 保存并退出 `vi`：
    在命令模式下输入：

```
:wq
```

1. 重载并重启 Docker 服务：

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

