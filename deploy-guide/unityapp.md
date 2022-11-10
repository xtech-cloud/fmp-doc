---
description: 'Unity应用程序 #部署指南'
---

# UnityApp

## 联机模式

在vendor目录中创建url.txt文件，写入vendor的meta.json的下载地址，例如：

```
http://oss.xtech.cloud/xxxxxxxxxxxxxxxxxxxxxxxxxxxx.json
```

运行程序后，会自动从此地址下载vendor的meta文件，然后更新框架、聚合资源。



## 脱机模式

备注：当前版本暂未实现此功能

创建vendor/meta.json文件，内容如下

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
    "Uuid": ""
}
```

其中DependencyConfig，BootloaderConfig、UpdateConfig、ModuleConfigS、ModuleCatalogS五个字段都留空。应用程序在运行时，如果对应字段为空，则会从vendor目录加载对应的配置文件。



| 字段               | 配置文件地址                       |
| ---------------- | ---------------------------- |
| DependencyConfig | vendor/Dependency.xml        |
| BootloaderConfig | vendor/Bootloader.xml        |
| UpdateConfig     | vendor/Update.xml            |
| ModuleConfigS    | vendor/config/{module}.xml   |
| ModuleCatalogS   | vendor/catalog/{module}.json |

## 使用Vendor选单

UnityApp支持在程序启动后，自动读取所有的vendor目录下的meta.json文件形成一个选单列表，在选单中选择一个vendor进入。

要使用vendor选单的方式，需要注意以下几点：

* vendor文件夹中必须存在至少包含Name和Display两个字段的meta.json文件。
* vendor文件夹的名字和meta.json的Name字段名字必须一致。
* 不使用命令行参数设置vendor
* AppConfig.xml中的VendorSelector.active为空。
