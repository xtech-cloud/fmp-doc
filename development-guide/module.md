---
description: '模块 #开发指南'
---

# Module

## 基础教程

### 创建项目

fmp-cli创建的模块项目，需要做版本管理，所以需要目录是git库。

在项目的git库所在目录中，使用命令行运行以下命令

```
fmp-cli
```

```
****************************************************
* FMP Client - ver 1.84.0.18
****************************************************
1. create
2. deploy
3. publish
4. utility
enter you choice:
```

输入 1 创建模块，然后按提示输入组织名和模块名。

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

直接无参数运行fmp-cli时，如果目录中存在fmp.yaml或.fmp.yaml文件，则fmp-cli会逐个运行文件中激活的任务。

### 生成基础框架

复制fmp.yaml为.fmp.yaml，将所有任务的active改为false，将所有任务的environment改为develop。

执行fmp-cli时，会优先寻找.fmp.yaml文件，所以可以使用.fmp.yaml作为自己本机的项目配置，并且在git中忽略此文件，而将fmp.yaml作为CI/CD使用的文件。

修改完的内容，将只生成一个基础框架。

在命令终端中使用-g参数运行命令（-g是任务generate的首字母），生成项目文件

```
fmp-cli -g
```

fmp-cli执行完成后，在当前的目录，会自动生成vs2022和proto的文件夹，现在整个项目的文件结构像这样。

```
FMP-MOD-Demo
  |- .git
  |- cers
  |- proto
  |- vs2022
  |- unity2021
  |- .fmp.yaml
  |- fmp.yaml
  |- .gitignore
  |- .generated.log
  |- ...
```

### 编译基础框架

使用Visual Studio 2022 打开vs2022/fmp-xtc-demo.sln解决方案文件。


### 发布模块

在命令终端中使用-p参数运行命令（-p是任务publish的首字母），发布项目文件

```
fmp-cli -p
```

product环境发布的模块，在仓库中会以版本号作为标识，例如_**XTC\_Demo@1.0.0**_，并且一旦发布成功，仓库中的模块将自动锁定，无法再次发布相同版本号的内容。而develop环境发布的模块，会在仓库中以develop作为特殊的版本标识，例如_**XTC\_Demo@develop**_，并且不会锁定。

发布功能需要根据git的版本号自动构建，所以在发布前，需要先打上git标签，例如

```
git tag 0.1.0
```

推荐使用GNU风格的版本号标识，也就是 _**主要版本.次要版本.修正版本**_，推荐一次提交只做一件事情，缺陷的修复可将修正版本加1，功能的更新可将次要版本加1并将修正版本置0。大版本的迭代可将主要版本加1并将次要版本和修正版本置0。

打上git标签后，可使用fmp-cli发布模块。

完成后可登录console.xtech.cloud，在XTC\_Repository中的Module中查看已发布的模块信息。

如果在存在.fmp.yaml文件时希望使用fmp.yaml发布，则可以使用-pi参数忽略.fmp.yaml（i为ignore的首字母）。

```
fmp-cli -pi
```

建议fmp.yaml配置为生产环境，.fmp.yaml配置为开发环境，在日常开发中使用`fmp-cli -p`发布，正式发布时使用`fmp-cli -pi`。

### 添加Unity项目

fmp.yaml文件中默认打开了unity的项目生成，所以在生成项目时，会自动生成unity工程。

### 编译Unity框架

先运行unity2021/copy-dll.bat文件，此操作将重新编译vs2022下的解决方案，并将一些dll文件拷贝到unity2021/{模块名}/Assets/3rd/fmp-dependency目录中。

使用Unity 2021.3.8f1打开unity2021/{模块名}文件夹。

创建文件unity2021/.UNITY_HOME.env，文件内容为Unity编辑器的绝对路径，例如
```
D:\Unity-2021.3.8f1
```
运行unity2021/compile.dll编译模块对应的unity库。

### 发布

运行Unity菜单栏的BuildTools/AssetBunlde，构建webgl、android、windows三个平台的uab文件。
使用fmp-cli发布。

## 进阶教程

### 数据库

TODO

### 微服务单元测试

TODO

### Web前端界面

TODO

### 微服务部署

TODO

