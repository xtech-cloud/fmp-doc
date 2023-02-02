---
description: Lua脚本环境
---

# XTC\_LuaEnv

lua脚本环境模块可在程序运行时以热插拔的方式加载执行lua脚本编写的脚本化微应用程序。


## 术语约定

### 脚本化微应用

一个包含了lua脚本文件和图片、视频、音乐、模型等多种媒体文件打包而成的归档文件，可在加载运行后提供和主程序一致的交互体验。

### 根脚本

微应用程序至少需要包含一个名为root.lua的根脚本文件，微应用加载后，会执行root.lua，微应用的所有逻辑都从根脚本开始。

一个根脚本需要包含以下结构:

```lua
local function run()
    G_LOGGER:Info("lua root.Run ...")
    G_LOGGER:Info(G_SLOT_UI.name)
    G_LOGGER:Info(G_SLOT_WORLD.name)
end

local function update()
end

local function stop()
    G_LOGGER:Info("lua root.Stop ...")
end

local function handleEvent(_event, _data)
    G_LOGGER:Info(_event)
end

root = {
    Run = run,
    Update = update,
    Stop = stop,
    HandleEvent = handleEvent,
}
```

## 功能特性

### 运行时热插拔

模块可在运行时从外部插入微应用运行，同时可将微应用从运行时拔除。


### 全局导出

模块中已经导出了一些常用的可访问成员到lua空间，在lua代码中可以直接调用。

| 导出名 | 类型 | 说明 |
| --- | --- | --- |
| G_LOGGER | XTC.FMP.LIB.MVCS.Logger | 日志的实例 |
| G_SLOT_UI | UnityEngine.GameObject | UI挂载槽的实例 |
| G_SLOT_WORLD | UnityEngine.GameObject | 3D世界挂载槽的实例 |
| G_API_PROXY| XTC.FMP.MOD.LuaEnv.LIB.APIProxy| API代理的实例 |
| G_FONT_MAIN| UnityEngine.Font | 主要的字体 |


## 配置说明

标准范例：

## 消息订阅

TODO

## 依赖插件

oelMVCS

XLuaPlugin


## 模板列表

### Karaoke

* 可更改主题皮肤
* 可切换人声和伴唱两种模式
* 可控制播放进度
* 可控制音量大小



## 更新日志

### 0.9.0

  [更新] 关闭时结束读取线程

### Karaoke/6.0.1

  [修正] 播放进度无法点击的问题
  [更新] 自动循环播放

