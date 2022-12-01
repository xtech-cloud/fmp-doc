---
description: 媒体中心
---

# XTC\_MediaCenter

## 术语约定

TODO

## 功能特性

TODO

## 配置说明

标准范例：

```markup
<?xml version="1.0" encoding="utf-8"?>
<MyConfig version="1.0">
  <!-- UI 
      visible: 预加载完成后是否显示
      slot: ui根节点在主Canvas中的挂载路径
    -->
  <UI visible="true" slot="[root]"/>
  <!-- 远程过程调用
      address: 地址
    -->
  <GRPC address="https://localhost:19000"/>
  <!-- 样式列表
      name: 名称
      primaryColor: 主色系
      Summary: 简介说明文字
      Summary.beginDelay: 开始滚动前的延迟时间
      Summary.endDelay: 结束滚动后的延时时间
      Summary.speed: 滚动速度
      HomeContainer: 主页容器
      HomeContainer.Padding:  节点与容器的边距
      HomeContainer.CellSize: 节点的尺寸
      HomeContainer.Spacing:  节点间的间隔
      HomeContainer: 浏览器容器
      HomeContainer.Padding:  节点与容器的边距
      HomeContainer.CellSize: 节点的尺寸
      HomeContainer.Spacing:  节点间的间隔
      ToolBar.VideoProgress.width:  视频进度条长度
      ToolBar.VideoLoop.mode:  视频初始循环模式，可选值为（none, single）
      ToolBar.VideoLoop.visible:  视频循环按钮是否可见
    -->
  <Styles>
    <Style name="default" primaryColor="#DAB757FF">
      <Summary beginDelay="5" endDelay="5" speed="30"/>
      <HomeContainer row="3">
        <Padding left="36" right="36" top="36" bottom="36"/>
        <CellSize width="300" height="300"/>
        <Spaceing x="16" y="16"/>
      </HomeContainer>
      <ViewerContainer>
        <Padding left="24" right="24" top="24" bottom="24"/>
        <CellSize width="128" height="128"/>
        <Spaceing x="16" y="16"/>
      </ViewerContainer>
      <ToolBar>
        <VideoProgress width="300"/>
        <VideoLoop mode="none" visible="false"/>
      </ToolBar>
    </Style>
  </Styles>
  <!-- 预创建的实例列表
      uid: 实例的唯一ID
      style: 使用的样式名
    -->
  <Instances>
    <Instance uid="default" style="default"/>
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
      <Subject message="/XTC/MediaCenter/Open">
        <Parameters>
          <Parameter key="uid" value="default" type="string"/>
          <Parameter key="source" value="assloud://" type="string"/>
          <Parameter key="uri" value="XTC.MediaCenter/_resources/1.mc" type="string"/>
          <Parameter key="delay" value="0" type="float"/>
        </Parameters>
      </Subject>
    </Subjects>
  </Preload>
</MyConfig>

```



## 消息订阅

TODO

## 依赖插件&#x20;

oelMVCS

AVProVideoPlugin



## 更新日志

### 0.9.0

* 新增：

支持视频循环，对应配置为：

```markup
<VideoLoop mode="none" visible="false"/>
```

