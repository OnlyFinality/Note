## Docker-CE 安装指南

### 1. **Ubuntu（使用 apt-get 进行安装）**

#### 步骤 1: 安装必要的系统工具

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```

#### 步骤 2: 信任 Docker 的 GPG 公钥

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

#### 步骤 3: 写入软件源信息

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### 步骤 4: 安装 Docker

```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### 安装指定版本的 Docker-CE

1. 查找 Docker-CE 的版本：

```bash
apt-cache madison docker-ce
```

例如：

```bash
docker-ce | 17.03.1~ce-0~ubuntu-xenial | https://mirrors.aliyun.com/docker-ce/linux/ubuntu xenial/stable amd64 Packages
docker-ce | 17.03.0~ce-0~ubuntu-xenial | https://mirrors.aliyun.com/docker-ce/linux/ubuntu xenial/stable amd64 Packages
```

1. 安装指定版本的 Docker-CE：

```bash
sudo apt-get -y install docker-ce=[VERSION]
```

------

### 2. **CentOS（使用 yum 进行安装）**

#### 步骤 1: 安装必要的系统工具

```bash
sudo yum install -y yum-utils
```

#### 步骤 2: 添加软件源信息

```bash
yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

#### 步骤 3: 安装 Docker

```bash
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### 步骤 4: 启动 Docker 服务

```bash
sudo service docker start
```

#### 注意：

- 默认情况下，官方软件源启用了最新的软件版本。如果你需要其他版本，可以通过编辑源文件来启用不同版本。例如，开启测试版本：

```bash
vim /etc/yum.repos.d/docker-ce.repo
# 将 [docker-ce-test] 下方的 enabled=0 修改为 enabled=1
```

#### 安装指定版本的 Docker-CE

1. 查找 Docker-CE 的版本：

```bash
yum list docker-ce.x86_64 --showduplicates | sort -r
```

例如：

```bash
docker-ce.x86_64  17.03.1.ce-1.el7.centos  docker-ce-stable
docker-ce.x86_64  17.03.0.ce-1.el7.centos  docker-ce-stable
```

1. 安装指定版本的 Docker-CE：

```bash
sudo yum -y install docker-ce-[VERSION]
```

------

### 3. **安装校验**

运行以下命令，验证 Docker 是否安装成功：

```bash
docker version
```

输出示例：

```bash
Client:
 Version:      17.03.0-ce
 API version:  1.26
 Go version:   go1.7.5
 Git commit:   3a232c8
 Built:        Tue Feb 28 07:52:04 2017
 OS/Arch:      linux/amd64

Server:
 Version:      17.03.0-ce
 API version:  1.26 (minimum version 1.12)
 Go version:   go1.7.5
 Git commit:   3a232c8
 Built:        Tue Feb 28 07:52:04 2017
 OS/Arch:      linux/amd64
 Experimental: false
```

### 4. **官方主页**

更多详情请参考 Docker 官方文档：[Docker 官方安装指南](https://docs.docker.com/engine/install/)