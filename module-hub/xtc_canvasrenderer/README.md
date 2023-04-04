---
description: 画布渲染器
---

# XTC\_CanvasRenderer

## 术语约定

TODO


## 配置说明

```xml
<?xml version="1.0" encoding="utf-8"?>
<MyConfig version="1.0">
  <!-- UI 
      visible: 预加载完成后是否显示
      slot: ui根节点在主Canvas中的挂载路径
    -->
  <UI visible="true" slot="[root]"/>
  <!-- World
      visible: 预加载完成后是否显示
      slot: world根节点的挂载路径
    -->
  <World visible="true" slot="[root]"/>
  <!-- 远程过程调用
      address: 地址
    -->
  <GRPC address="https://localhost:19000"/>
  <!-- 样式列表
      name: 名称
      Targer.path: 目标Canvas的路径，需可见
      Targer.mode: 目标Canvas的渲染模式， 可选值为[Overlay, Camera, World]
    -->
  <Styles>
    <Style name="default">
      <Target path="MainCanvas" mode="Overlay">
        <OverlayMode/>
        <CameraMode camera="Main Camera"/>
      </Target>
    </Style>
  </Styles>
  <!-- 预创建的实例列表
      uid: 实例的唯一ID
      style: 使用的样式名
      uiRoot: UI挂载的根节点（需可见），空值时等于UI.slot
      uiSlot: UI在uiRoot下的挂载路径
      worldRoot: World挂载的根节点（需可见），空值时等于World.slot
      worldSlot: World在worldRoot下的路径
    -->
  <Instances>
    <Instance uid="default" style="default" uiRoot="" uiSlot="" worldRoot="" worldSlot=""/>
  </Instances>
  <!-- 预加载 -->
  <Preload>
  </Preload>
</MyConfig>

```

## 消息订阅


## 依赖插件


## 更新日志

### 0.3.0

* 新增：默认是用1080P样式


