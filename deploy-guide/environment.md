---
description: '环境配置 #部署指南'
---

# Environment

## Certifications

开发和测试环境推荐使用自带的自签名证书，生产环境务必使用权威CA的证书。

如果需要创建自己的自签名证书，方法如下

```shell
PARENT="xtech.cloud"
openssl req \
-x509 \
-newkey rsa:4096 \
-sha256 \
-days 36500 \
-nodes \
-keyout $PARENT.key \
-out $PARENT.crt \
-subj "/CN=${PARENT}" \
-extensions v3_ca \
-extensions v3_req \
-config <( \
  echo '[req]'; \
  echo 'default_bits= 4096'; \
  echo 'distinguished_name=req'; \
  echo 'x509_extension = v3_ca'; \
  echo 'req_extensions = v3_req'; \
  echo '[v3_req]'; \
  echo 'basicConstraints = CA:FALSE'; \
  echo 'keyUsage = nonRepudiation, digitalSignature, keyEncipherment'; \
  echo 'subjectAltName = @alt_names'; \
  echo '[ alt_names ]'; \
  echo "DNS.1 = www.${PARENT}"; \
  echo "DNS.2 = ${PARENT}"; \
  echo '[ v3_ca ]'; \
  echo 'subjectKeyIdentifier=hash'; \
  echo 'authorityKeyIdentifier=keyid:always,issuer'; \
  echo 'basicConstraints = critical, CA:TRUE, pathlen:0'; \
  echo 'keyUsage = critical, cRLSign, keyCertSign'; \
  echo 'extendedKeyUsage = serverAuth, clientAuth')

openssl x509 -noout -text -in $PARENT.crt
```

## Docker

说明：本章中的地址localhost请使用实际部署的地址进行替换。

### 基础容器

```shell
cd ~
git clone http://github.com/xtechcloud/fmp-docker
cd  fmp-docker/wsl
install-all.sh
```

等待安装完成，输入`docker ps` 查看安装完成的容器

使用浏览器分别访问以下地址：

* web容器

> http://localhost
> https://localhost

* pmc容器

> http://localhost:8080
> https://localhost:8443

* daemon容器

> localhost:16166



### Repository

初始系统需要手动部署仓库模块

使用`fmp-cli -p`发布模块，将service-grpc/bin/目录下的XTC.Repository.zip拷贝到fmp-daemon/apps目录下，同时拷贝证书到fmp-daemon/cers目录，形成以下结构

```
|- /fmp/fmp-daemon
  |- cers
    |- xtc.crt
    |- xtc.key
  |- apps
    |- XTC.Repository
      |- application.json
      |- *.dll
      | ...
```

重启fmp-daemon容器，完成后使用浏览器访问 localhost:16166

## 存储初始化

使用浏览器访问localhost:9000，输入默认账号密码（在fmp-docker库的docker-compose-dsc.yml文件中）

创建名为fmp.repository的私有存储桶，并在访问规则中添加前缀为`/`的只读访问策略。
