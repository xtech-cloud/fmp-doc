---
description: 2D热点
---

# XTC\_Hotspot2D

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
    slot: ui根节点在主Canvas中的挂载路径
  -->
  <World visible="true" slot="[root]"/>
  <!-- 远程过程调用
      address: 地址
  -->
  <GRPC address="https://localhost:19000"/>
  <!-- 样式列表
    name: 名称
  -->
  <Styles>
    <Style name="default">
      <!-- 图层
		image: 位于themes/XTC_Hotspot2D路径的图片
        horizontalAlign: 水平对齐方式，可选值为（left,center,right）
        verticalAlign: 垂直对齐方式，可选值为（top,center,bottom）
	  -->
      <MainLayer image="MainLayer_default.jpg" horizontalAlign="center" verticalAlign="center"/>
      <ExtraLayerS>
      <!--
        <ExtraLayer image="Layer0_default.jpg"/>
      -->
      </ExtraLayerS>
      <!-- 热点
			  image: 位于themes/XTC_Hotspot2D路径的图片
        key: 内容的键值对的键
        debugFrameColor: 用于调试的填充颜色
			  x: 横坐标，屏幕中为0，左方为负数，右方为正
			  y: 纵坐标，屏幕中为0，下方为负数，上方为正
			-->
      <Hotspot image="Hotspot_default.png" key="ImageAtlas3D" debugFrameColor="#00000000">
        <Anchor marginH="0" marginV="0" width="144" height="144"/>
        <OnSubjects>
          <Subject message="/XTC/ImageAtlas3D/Open">
            <Parameters>
              <Parameter key="uid" value="default" type="string"/>
              <Parameter key="source" value="assloud://" type="string"/>
              <Parameter key="uri" value="{{uri}}" type="string"/>
              <Parameter key="delay" value="0" type="float"/>
            </Parameters>
          </Subject>
          <Subject message="/XTC/Hotspot2D/Forward">
            <Parameters>
              <Parameter key="uid" value="default" type="string"/>
            </Parameters>
          </Subject>
        </OnSubjects>
        <OffSubjects>
          <Subject message="/XTC/ImageAtlas3D/Close">
            <Parameters>
              <Parameter key="uid" value="default" type="string"/>
              <Parameter key="delay" value="0" type="float"/>
            </Parameters>
          </Subject>
          <Subject message="/XTC/Hotspot2D/Back">
            <Parameters>
              <Parameter key="uid" value="default" type="string"/>
            </Parameters>
          </Subject>
        </OffSubjects>
      </Hotspot>
      <Board>
        <BackButton image="Back_default.png">
          <Anchor horizontal="left" vertical="top" marginH="32" marginV="32" width="152" height="72"/>
        </BackButton>
      </Board>
      <!-- 信息框
        active: 是否启用，启用后点击热点将打开信息框，在信息框中点击打开按钮后才会触发OnSubjects
      -->
      <InfoBox active="true">
        <!-- 面板
        -->
        <Panel image="InfoBox_Panel_default.png">
          <Anchor width="512" height="320"/>
        </Panel>
        <!-- 关闭按钮
        -->
        <CloseButton image="InfoBox_Close_default.png">
          <Anchor marginH="100" marginV="-100" width="180" height="36"/>
        </CloseButton>
        <!-- 打开按钮
        -->
        <OpenButton image="InfoBox_Open_default.png">
          <Anchor marginH="-100" marginV="-100" width="180" height="36"/>
        </OpenButton>
      </InfoBox>
    </Style>
  </Styles>
  <!-- 预创建的实例列表
      uid: 实例的唯一ID
      style: 使用的样式名
    -->
  <Instances>
    <Instance uid="default" style="default" uiSlot="" worldRoot=""/>
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
      <Subject message="/XTC/Hotspot2D/Open">
        <Parameters>
          <Parameter key="uid" value="default" type="string"/>
          <Parameter key="source" value="" type="string"/>
          <Parameter key="uri" value="" type="string"/>
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

### 0.5.0

* 修改：更新框架到1.83.0
* 修改：可配置工具栏的显示方式

