---
description: 图片播放器
---

# XTC\_ImageSee

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
      Background: 背景层
      ToolBar.maxScale: 图片的最大放大倍数
      ToolBar.visible: 工具栏可见行，可选值为[auto, alwaysOn, alwaysOff]
      Pending.size: 加载提示图片的尺寸
    -->
  <Styles>
    <Style name="default">
      <Background visible="true" color="#333333FF"/>
      <Pending image="Pending.png" size="160"/>
      <ToolBar visible="auto" maxScale="4.0">
        <Anchor horizontal="right" vertical="bottom" marginH="36" marginV="24"/>
      </ToolBar>
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
    <!-- 消息订阅的主题
          message: 消息
          Parameter.key: 参数的键
          Parameter.value: 参数的值
          Parameter.type: 参数的类型，支持的类型为string,int,float,bool
        -->
    <Subjects>
      <Subject message="/XTC/ImageSee/Open">
        <Parameters>
          <Parameter key="uid" value="default" type="string"/>
          <Parameter key="source" value="assloud://" type="string"/>
          <Parameter key="uri" value="XTC.ImageSee/1/1.jpg" type="string"/>
          <Parameter key="delay" value="0" type="float"/>
        </Parameters>
      </Subject>
    </Subjects>
  </Preload>
</MyConfig>
```

## 消息订阅


## 依赖插件


## 更新日志

### 0.7.0

* 修改：更新ui为UI KIT

### 0.5.0

* 修改：更新框架到1.83.0
* 修改：可配置工具栏的显示方式

