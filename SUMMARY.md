# Table of contents

* [概述](README.md)

FMP(Fast Modular Product)是一个快速模块化产品的解决方案。核心功能为通过标准的开发框架，快速的进行功能定制，并将构建出的模块包发布到仓库中，提供给不同的应用端以模块组合的方式形成定制化的产品。

FMP解决方案主要包含以下组成部分：

* Cli
  客户端工具，主要用于模块的创建、代码生成、编译、发布等。也包含一些辅助的工具。

* UnityApp
  使用Unity构建的应用端，主要用于内容的呈现和交互，支持PC、移动、web等平台。

* BlazorApp
  使用Blazor构建的应用端，主要用于模块的后台管理，仅支持Web平台。

* MauiApp
  使用Maui构建的应用端，主要用于将web平台的BlazorApp适配为PC原生应用。

* DaemonApp
  微服务的守护应用端，主要用于在容器内或原生系统中启动微服务。

* ShieldApp
  PC应用程序的安全应用端，主要用于防止系统桌面暴露，以及应用程序的启动监控等。

* XRApp
  XR设备上的应用程序，属于UnityApp的超集。

## Design Document

* [Cli](design-document/cli.md)
* [UnityApp](design-document/unityapp.md)
* [BlazorApp](design-document/blazorapp.md)
* [MauiApp](design-document/mauiapp.md)
* [DaemonApp](design-document/daemonapp.md)
* [ShieldApp](design-document/shieldapp.md)

## Development Guide

* [Environment](development-guide/environment.md)
* [Cli](development-guide/cli.md)
* [UnityApp](development-guide/unityapp.md)

## Deploy Guide

* [Environment](deploy-guide/environment.md)
* [BlazorApp](deploy-guide/blazorapp.md)
* [UnityApp](deploy-guide/unityapp.md)
* [ShieldApp](deploy-guide/shieldapp.md)
* [MauiApp](deploy-guide/mauiapp.md)
* [DaemonApp](deploy-guide/daemonapp.md)
* [XRApp](deploy-guide/xrapp.md)

## User Manual

* [UnityApp](user-manual/unityapp.md)
* [BlazorApp](user-manual/blazorapp.md)
* [MauiApp](user-manual/mauiapp.md)
* [XRApp](user-manual/xrapp.md)

## Module Hub

* [XTC\_Repository](module-hub/xtc\_repository.md)
* [XTC\_Vendor](module-hub/xtc\_vendor.md)
* [XTC\_Assloud](module-hub/xtc\_assloud.md)
* [XTC\_VisionLayout](module-hub/xtc\_visionlayout.md)
* [XTC\_VRLobby](module-hub/xtc\_vrlobby.md)
* [XTC\_Hotspot2D](module-hub/xtc\_hotspot2d.md)
