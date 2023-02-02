---
description: '客户端工具 #开发指南'
---

# Cli

version: 1.70.2

## 开发环境配置

### 方式一：conda


创建环境

```bash
conda create --name fmp python=3.8.3
```

安装依赖包

```bash
conda activate fmp

conda config --add channels https://mirrors.aliyun.com/anaconda/cloud/conda-forge
conda config --set show_channel_urls yes

conda install grpcio==1.46.0 -c conda-forge
conda install grpcio-tools==1.46.0 -c conda-forge
conda install pyyaml==5.1.2 -c conda-forge
conda install colorama==0.4.0 -c conda-forge
conda install requests==2.23.0 -c conda-forge
conda install pyinstaller==5.6.2 -c conda-forge
```

编译

```bash
conda activate fmp
pyinstaller fmp-cli.spec
```

编译产物位于dist/fmp-cli.exe

## 安装

将fmp-cli.exe安装到可执行目录，例如 `C:\Windows\System32`

## 升级

### 更新proto

```bash
python -m grpc_tools.protoc -I./proto/Repository --python_out=./mygrpc --grpc_python_out=./mygrpc ./proto/Repository/*.proto
```



## 运行错误解决方法

- 提示pyinstaller无法找到

使用pip进行安装
```bash
pip install pyinstaller==5.6.2
```


- assertion failed: pem_root_certs != nullptr

在fmp-cli.spec中加入
```
datas=[
('roots.pem', 'grpc/_cython/_credentials/'),
],
```
