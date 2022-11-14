---
description: 集成面板
---

# XTC\_IntegrationBoard

集成面板可以将多个模块整合进一个面板中，用多个模块为一个内容提供多样的显示形态和交互体验。

## 术语约定

TODO

## 功能特性

TODO

## 配置说明

TODO

## 消息订阅

* /XTC/IntegrationBoard/DirectOpen

此消息将首先创建一个集成面板，然后刷新内容并显示，最后对齐到网格。

| 参数          | 类型     | 说明                    |
| ----------- | ------ | --------------------- |
| uid         | string | 准备创建的实例的uid           |
| style       | string | 准备创建的实例的样式            |
| source      | string | 内容的源类型，可选项为assloud:// |
| uri         | string | 内容在源中的访问地址            |
| delay       | float  | 延时打开的时间，单位为秒          |
| position\_x | float  | 打开的位置的x坐标             |
| position\_y | float  | 打开的位置的y坐标             |

* /XTC/IntegrationBoard/DirectClose

此消息将关闭并销毁一个集成面板

| 参数    | 类型     | 说明           |
| ----- | ------ | ------------ |
| uid   | string | 准备创建的实例的uid  |
| delay | float  | 延时关闭的时间，单位为秒 |
|       |        |              |

## 依赖插件



