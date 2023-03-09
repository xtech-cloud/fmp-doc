---
description: 模块总览
---

# SUMMARY

图示：

✓：迭代版本已完成

✐：计划近期更新

✕：更新暂停

|          库名          |       用途        | 微服务 | Unity模块 | Blazor模块 | 默认端口 |
| --------------------- | :-- | :-- | :-- | :-- | :-- |
| AccessNet     | 接入网             | ⚫    | ⚫        | ⚫         | 28003         |
| Analytics| 统计分析 | ⚫    | ⚫        | ⚫         | 28004 |
| Assloud       | 资源云             | ⚫    | ⚫        | ⚫         | 28001    |
| DocumentSee | 文档浏览器 |     | ⚫        |          | |
| Hotspot2D     | 二维热点           |       | ⚫        |          |          |
| Hotspot3D     | 三维热点           |       | ⚫        |          |          |
| ImageSee | 图片浏览器 |       | ⚫        |          |          |
| IntegrationBoard | 集成面板 |     | ⚫        |          |          |
| LuaEnv | Lua脚本环境 |     | ⚫        |          |          |
| MediaCenter | 媒体中心 |     | ⚫        |          |          |
| PanoramicImageSee | 全景图片浏览器 |     | ⚫        |          |          |
| Profiler| 性能分析器 |     | ⚫        |          |          |
| Repository    | 模块仓库           | ⚫    |           | ⚫         | 28000    |
| Retrieval| 文件检索 |     |            ⚫         | | |
| Search | 资源搜索|     | ⚫        |          |          |
| SecretDock | 隐藏功能区|     |   ⚫       |          |          |
| SideMenu | 侧边栏 |     |   ⚫      |          |          |
| Vendor        | 资源云             | ⚫    |           | ⚫         | 28002    |
| VideoSee | 视频浏览器 | |⚫ | ⚫ | |
| VisionLayout  | 视觉布局           |     | ⚫        |          |          |
| VisualScripts | 可视化脚本         |       | ⚫        |          |          |
| VRLobby       | VR大厅             |       | ⚫        |          |          |
| WingMenu | 翼形菜单 |       | ⚫         | |          |
| WorldRenderer| 世界渲染器 |       | ⚫        |          |          |


## 架构说明

所有的模块都是使用FMP-Cli（FMP解决方案客户端工具）生成的框架，所以存在很多通用的结构。

### 实例

模块在载入到运行时后，在使用时，是以实例（instance）为单位进行工作。一个实例拥有自己独立的界面、3D空间、资源管理、配置等。

实例默认拥有4个生命期。

* 初始化

此生命期完成以下工作：

    * 创建新的UI对象和世界对象，并挂载到指定的槽。
    * 初始化主题内存管理器
    * 使用主题内存管理器加载主题文件
    * 应用样式表

* 打开资源

此生命期完成以下工作：

    * 初始化资源内存管理器
    * 使用资源内存管理器加载资源文件
    * 运行资源逻辑

* 关闭资源

此生命期完成以下工作：

    * 结束资源逻辑
    * 使用资源内存管理器释放资源文件
    * 释放资源内存管理器

* 销毁

此生命期完成以下工作：

    * 使用主题内存管理器释放主题文件
    * 释放主题内存管理器
    * 销毁UI对象和世界对象

#### 样式

为了让不同的实例拥有不同的主题风格，模块支持创建多个样式，实例在创建时需要指定一个样式。

样式的配置在配置文件中的以下字段

```xml
<Style>
</Style> 
```

#### 挂载槽

模块在创建实例后，需要将生成的ui和世界的根节点挂载到指定的对象下，被挂载的对象被称为挂载槽（Slot）。

模块的根节点的挂载配置如下

```xml
<UI slot="[root]" ...>
<World slot="[root]" ...>
<Instances>
    <Instance uid="default" style="default" uiRoot="" uiSlot="" worldRoot="" worldSlot=""/>
</Instances>
```

在以上配置中，UI.slot和World.slot的值是相对于默认根节点的相对路径，Ui的默认根节点是MainCanvas，World的默认根节点是MainWorld。

| | 根节点 | 挂载槽 | 挂载完成后的全路径 |
| --- | --- | --- | --- |
| UI | MainCanvas | [root] | MainCanvs/[root]/[UI_Root_({ModuleName})] |
| World | MainWorld| [root] | MainCanvs/[root]/[World_Root_({ModuleName})] |

根节点挂载完成后，在创建实例时，如果没有指定挂载相关的参数，实例将默认挂载到根节点下，例如创建名为default的节点，节点的路径如下：

> default实例的UI的挂载路径：MainCanvas/[root]/[UI_Root_({ModuleName})]/defualt
> default实例的世界的挂载路径：MainWorld/[root]/[World_Root_({ModuleName})]/defualt

默认挂载槽一般在模块内部使用时较为方便，但是实际使用中，会遇到需要将一个模块挂载到另一个模块中的情况，此时就需要指定实例的挂载参数，例如如下配置：

```xml
<UI slot="[root]" ...>
<World slot="[root]" ...>
<Instances>
    <Instance uid="my_default" style="default" uiRoot="MainCanvas/[root]" uiSlot="[UI_Root_ModuleA]/default/slot" worldRoot="" worldSlot=""/>
</Instances>
```

uiRoot和uiSlot的值不为空时，实例使用参数指定的挂载槽，忽略模块的根节点。

UI.slot和World.slot一般情况下不建议修改。Instance.uiRoot字段指定当前实例的ui挂载的根节点，此节点必须可见。Instance.uiSlot字段指定在Instance.uiRoot下的路径，此路径中的节点支持不可见。
如上的配置文件中的my_default实例，ui挂载完成后的路径为 MainCanvas/[root]/[UI_Root_ModuleA]/defualt/slot/my_default

### 消息订阅

每个模块默认包含以下可订阅的消息

* /{OrgName}/{ModuleName}/Create

创建一个新的实例

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 新实例的uid|
| style | string | 实例的样式 |
| uiRoot | string | UI挂载的根对象，需要可见|
| uiSlot | string | UI在uiRoot下的挂载路径 |
| worldRoot | string | 世界挂载的根对象，需要可见|
| worldSlot | string | 世界在worldRoot下的挂载路径 |


* /{OrgName}/{ModuleName}/Open

显示实例，并打开一个资源

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 实例的uid|
| source | string | 资源的源，一般为assloud://或file://|
| uri | string | 资源在source中的路径 |
| delay | float | 延迟打开的时间，单位秒|


* /{OrgName}/{ModuleName}/Show

仅显示实例，不执行其他任何操作

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 实例的uid|
| delay | float | 延迟打开的时间，单位秒|

* /{OrgName}/{ModuleName}/Hide

仅隐藏实例，不执行其他任何操作

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 实例的uid|
| delay | float | 延迟打开的时间，单位秒|


* /{OrgName}/{ModuleName}/Close

隐藏实例，并关闭一个资源

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 实例的uid|
| delay | float | 延迟打开的时间，单位秒|

* /{OrgName}/{ModuleName}/Delete

销毁实例

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 实例的uid|


