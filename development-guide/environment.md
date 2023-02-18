---
description: '环境配置 #开发指南'
---

# Environment

## windows


* WSL

TODO 安装Debian 10.10，并安装docker

进入Debian

```shell
cd ~
git clone http://github.com/xtechcloud/fmp-docker
cd  fmp-docker/wsl
install-all.sh
```

等待安装完成，输入`docker ps` 查看安装完成的容器

使用浏览器分别访问以下地址：

* localhost

web容器

* localhost:8080

pmc容器

* localhost:16166

daemon容器
