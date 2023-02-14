---
description: 'Unity应用程序 #部署指南'
---

# UnityApp

## 应用配置

UnityApp的应用的配置文件为AppConfig.xml，此文件存在于AppData/LocalLow/XTC/FMP目录中，其中XTC/FMP会根据衍生应用的定义而不同，衍生应用的概念请参阅设计文档中的UnityApp一章。AppConfig.xml的内容如下：

```markup
<?xml version="1.0"?>
<Schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Body>
    <VendorSelector active="default" />
    <Logger level="4" />
  </Body>
  <Header>
    <Field attribute="LogLevel.level" values="日志等级，可选值为：0(NONE), 1(EXCEPTION), 2(ERROR), 3(WARNING), 4(INFO), 5(DEBUG)5, 6(TRACE), 7(ALL)" />
    <Field attribute="Vendor.Selector.active" values="激活的虚拟环境的目录，如果没有激活的虚拟环境，会显示虚拟环境选择界面" />
  </Header>
</Schema>
```

| 字段                    | 说明      | 默认值     |
| --------------------- | ------- | ------- |
| VendorSelector.active | 激活的虚拟环境 | default |
| Logger.level          | 日志的等级   | 4       |

AppConfig.xml如果不存在，程序在运行时会自动创建。



## 虚拟环境配置

UnityApp运行后，会从激活的虚拟环境中加载模块和资源。激活虚拟环境的方式主要有：

* 命令行设置`-vendor=`
* 应用配置文件AppConfig.xml中设置`VendorSelector.active`字段

优先级别为命令行方式高于应用配置文件方式。

默认的vendor的名称为default。

每一个vendor具有自己的元数据定义文件meta.json，此文件内定义内容如下：

```json
{
    "Name": "XTC.Demo.CultureWall",
    "Display": "演示/文化墙",
    "SkinSplashBackground": "",
    "SkinSplashSlogan": "",
    "GraphicsFPS": 60,
    "GraphicsQuality": 3,
    "GraphicsPixelResolution": "6480x1920",
    "GraphicsReferenceResolutionWidth": 1920,
    "GraphicsReferenceResolutionHeight": 1080,
    "GraphicsReferenceResolutionMatch": 1.0,
    "Application": "",
    "DependencyConfig":"",
    "BootloaderConfig":"",
    "UpdateConfig":"",
    "ModuleConfigS": {},
    "ModuleCatalogS": {},
    "ModuleThemeS": {},
    "Uuid": ""
}
```

| 字段                                | 说明                                              |
| --------------------------------- | ----------------------------------------------- |
| Name                              | 虚拟环境的名称                                         |
| Display                           | Vendor选单显示的名称                                   |
| SkinSplashBackground              | 过场阶段显示的背景图，图片模式为循环平铺                            |
| SkinSplashSlogan                  | 过场阶段显示的标语图，图片模式为原始大小                            |
| GraphicsFPS                       | 画质帧数，一般为30或60，帧数越高对硬件性能要求越高                     |
| GraphicsQuality                   | 画面质量，1=非常低，2=低，3=中，4=高，5=非常高，6=极高               |
| GraphicsPixelResolution           | 画面物理分辨率                                         |
| GraphicsReferenceResolutionWidth  | UI界面适配分辨率的宽度                                    |
| GraphicsReferenceResolutionHeight | UI界面适配分辨率的高度                                    |
| GraphicsReferenceResolutionMatch  | UI界面适配分辨率的权重，取值范围为\[0.0, 1.0]，0为完全适配宽度，1为完全适配高度 |
| Application                       | 启动的应用程序的路径（Web平台有效）                             |
| DependencyConfig                  | 模块依赖配置的base64编码，空值时加载DependencyConfig.xml文件     |
| BootloaderConfig                  | 模块引导配置的base64编码，空值时加载BootloaderConfig.xml文件     |
| UpdateConfig                      | 框架更新配置的base64编码，空值时加载UpdateConfig.xml文件         |
| ModuleConfigS                     | 各个模块的配置的base64编码，空值时加载configs目录下的xml配置文件        |
| ModuleCatalogS                    | 各个模块的资源目录的base64编码，空值时加载catalogs目录下的json配置文件    |
| ModuleThemeS                      | 各个模块主题文件的读取地址列表                                 |

UnityApp会依据此元数据文件，进行更新框架、聚合资源、加载模块、解析配置等操作。

## 更新配置

### 默认vendor的快速配置

默认的vendor可以直接在目录中创建url.txt文件。

```
AppData/LocalLow/XTC/FMP
  |- default
    |- url.txt
```

在url.txt中写入vendor的meta.json的下载地址即可。

```
http://oss.xtech.cloud/xxxxxxxxxxxxxxxxxxxxxxxxxxxx.json
```

运行程序后，会自动从此地址下载vendor的meta文件，然后更新框架、聚合资源。

### 合并本地资源

`此功能1.22.0以上版本支持`

UnityApp启动后，会从远端资源库中拉取所有catalog中contentS字段中的资源，如果部分资源希望使用离线方式，跳过聚合，可按以下方式配置：

1. 在指定的vendor目录，新建.syndication文件夹
2. 在.syndication中新建以资源包的uuid命名的ignore文件，例如0d949fc4-4a4e-4c77-bb5e-e5d0485c56f9.ignore。

完成配置后，目录结构如下：

```
|- {name_of_vendor}
  |- meta.json
  |- .syndication
    |- 0d949fc4-4a4e-4c77-bb5e-e5d0485c56f9.ignore
  |- ...
```

UnityApp启动后，在资源聚合阶段，检测到存在聚合忽略文件，则会跳过对应的整个资源包的下载。


## 使用Vendor选单

UnityApp支持在程序启动后，自动读取所有的vendor目录下的meta.json文件形成一个选单列表，在选单中选择一个vendor进入。

要使用vendor选单的方式，需要注意以下几点：

* vendor文件夹中必须存在至少包含Name和Display两个字段的meta.json文件。
* vendor文件夹的名字和meta.json的Name字段名字必须一致。
* 不使用命令行参数设置vendor
* AppConfig.xml中的VendorSelector.active为空。
