---
description: '客户端工具 #开发指南'
---

# Cli

##

## 安装

TODO



## 基础教程

### 创建项目

fmp-cli创建的模块项目，需要做版本管理，所以需要目录是git库。

在项目的git库所在目录中，使用命令行运行以下命令

```
fmp-cli
```

TODO

项目创建完成后，会自动生成项目文件fmp.yaml，内容如下

```yaml
org_name: XTC
module_name: Demo
generate:
  active: true
  database_driver: none
  debug: false
  unity_solution: true
publish:
  active: true
  environment: product
  repository: grpc://localhost:18000
deploy:
  active: true
  environment: product
  repository: grpc://localhost:18000
  agent_port: 28000
  
```

字段说明如下

| 字段                        | 说明                        |
| ------------------------- | ------------------------- |
| org\_name                 | 组织名称                      |
| module\_name              | 模块名称                      |
| generate                  | 项目生成的执行任务                 |
| generate.active           | 运行fmp-cli时是否执行此任务         |
| generate.database\_driver | 数据库驱动，可选值为 none, mongodb  |
| generate.debug            | 是否打印调试信息                  |
| generate.unity\_solution  | 是否生成unity的项目文件            |
| publish                   | 发布的执行任务                   |
| publish.active            | 运行fmp-cli时是否执行此任务         |
| publish.environment       | 发布的环境，可选值为develop,product |
| publish.repository        | 仓库的地址                     |
| deploy                    | 部署的执行任务                   |
| deploy.active             | 运行fmp-cli时是否执行此任务         |
| deploy.environment        | 部署的环境，可选值为develop,product |
| deploy.repository         | 仓库的地址                     |
| deploy.agent\_port        | 微服务运行时的默认端口号              |

### 生成基础框架

复制fmp.yaml为.fmp.yaml，修改内容如下

```yaml
org_name: XTC
module_name: Demo
generate:
  active: true
  database_driver: none
  debug: false
  unity_solution: false
```

执行fmp-cli时，会优先寻找.fmp.yaml文件，所以可以使用.fmp.yaml作为自己本机的项目配置，并且在git中忽略此文件，而将fmp.yaml作为CI/CD使用的文件。

修改完的内容，将只生成一个基础框架。

在命令终端中运行命令，生成项目文件

```
fmp-cli
```

fmp-cli执行完成后，在当前的目录，会自动生成vs2022和proto的文件夹，现在整个项目的文件结构像这样。

```
FMP-MOD-Demo
  |- .git
  |- proto
  |- vs2022
  |- .fmp.yaml
  |- fmp.yaml
  |- ...
```

### 编译基础框架

使用Visual Studio 2022 打开vs2022/fmp-xtc-demo.sln解决方案文件。

TODO&#x20;



### 发布模块

发布模块需要在项目配置文件中，存在并激活publish任务，修改.fmp.yaml为如下内容

```yaml
org_name: XTC
module_name: Demo
generate:
  active: true
  database_driver: none
  debug: false
  unity_solution: false
publish:
  active: true
  environment: develop
  repository: grpcs://api.xtech.cloud:29000
```

product环境发布的模块，在仓库中会以版本号作为标识，例如_**XTC\_Demo@1.0.0**_，并且一旦发布成功，仓库中的模块将自动锁定，无法再次发布相同版本号的内容。而develop环境发布的模块，会在仓库中以develop作为特殊的版本标识，例如_**XTC\_Demo@develop**_，并且不会锁定。

发布功能需要根据git的版本号自动构建，所以在发布前，需要先打上git标签，例如

```
git tag 0.1.0
```

推荐使用GNU风格的版本号标识，也就是 _**主要版本.次要版本.修正版本**_，推荐一次提交只做一件事情，缺陷的修复可将修正版本加1，功能的更新可将次要版本加1并将修正版本置0。大版本的迭代可将主要版本加1并将次要版本和修正版本置0。

打上git标签后，可使用fmp-cli发布模块。

```bash
fmp-cli
```

完成后可登录console.xtech.cloud，在XTC\_Repository中的Module中查看已发布的模块信息。

### 添加Unity项目

修改.fmp.yaml，将Unity的项目生成的选项打开，并将发布暂时关闭。

```yaml
org_name: XTC
module_name: Demo
generate:
  active: true
  database_driver: none
  debug: false
  unity_solution: true
publish:
  active: false
  environment: develop
  repository: grpcs://api.xtech.cloud:29000
```

再次运行fmp-cli

```bash
fmp-cli
```

完成后，会得到一个名为unity2021的新的文件夹，目前的文件结构应该像这样。

```
FMP-MOD-Demo
  |- .git
  |- proto
  |- unity2021
  |- vs2022
  |- .fmp.yaml
  |- fmp.yaml
  |- ...
```

### 编译Unity框架

先运行unity2021/copy-dll.bat文件，此操作将重新编译vs2022下的解决方案，并将一些dll文件拷贝到unity2021/Demo/Assets/3rd/fmp-dependency目录中。

使用Unity 2021.3.8f1打开unity2021/Demo文件夹。

TODO

## 进阶教程

### 数据库

TODO

### 微服务单元测试

TODO

### Web前端界面

TODO

### 微服务部署

TODO

