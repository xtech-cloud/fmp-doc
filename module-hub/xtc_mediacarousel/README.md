---
description: 多媒体跑马灯
---

# XTC\_MediaCarrousel

## 术语约定

TODO

## 功能特性

TODO

## 配置说明

标准范例：

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
      autoSwitch: 是否自动切换，不自动切换时将显示上一个和下一个按钮
      ButtonPrev: 上一个按钮 
      ButtonNext: 下一个按钮 
      ClickArea: 顶层的点击区域，不定义则隐藏
      ClickArea.OnClickSubjectS: 点击区域被点击后发布的订阅主题
      Slide.type: 幻灯片的类型，可选值为(Image,Video)
      Slide.OnCreatedSubjectS: 幻灯片节点被创建后发布的订阅主题
      Slide.OnActivatedSubjectS: 幻灯片节点被激活后发布的订阅主题
    -->
  <Styles>
    <Style name="default" autoSwitch="false">
      <ClickArea>
        <OnClickSubjectS>
        </OnClickSubjectS>
      </ClickArea>
      <ButtonPrev image="btnPrev.png">
        <Anchor horizontal="left" vertical="center" marginH="0" marginV="0" width="100" height="100"/>
      </ButtonPrev>
      <ButtonNext image="btnNext.png">
        <Anchor horizontal="right" vertical="center" marginH="0" marginV="0" width="100" height="100"/>
      </ButtonNext >
      <SlideS>
        <Slide type="Image">
          <OnCreatedSubjectS>
            <Subject message="/XTC/ImageSee/Create">
              <Parameters>
                <Parameter key="uid" value="{{slide_uuid}}" type="_"/>
                <Parameter key="style" value="XTC_MediaCarousel" type="string"/>
                <Parameter key="uiRoot" value="MainCanvas/[root]" type="string"/>
                <Parameter key="uiSlot" value="{{slide_slot}}" type="string"/>
                <Parameter key="worldRoot" value="" type="string"/>
                <Parameter key="worldSlot" value="" type="string"/>
              </Parameters>
            </Subject>
          </OnCreatedSubjectS>
          <OnActivatedSubjectS>
            <Subject message="/XTC/ImageSee/Open">
              <Parameters>
                <Parameter key="uid" value="{{slide_uuid}}" type="_"/>
                <Parameter key="source" value="assloud://" type="string"/>
                <Parameter key="uri" value="{{slide_uri}}" type="string"/>
                <Parameter key="delay" value="0" type="float"/>
              </Parameters>
            </Subject>
          </OnActivatedSubjectS>
          <OnClosedSubjectS>
            <Subject message="/XTC/ImageSee/Close">
              <Parameters>
                <Parameter key="uid" value="{{slide_uuid}}" type="string"/>
                <Parameter key="delay" value="0" type="float"/>
              </Parameters>
            </Subject>
          </OnClosedSubjectS>
        </Slide>
        <Slide type="Video">
          <OnCreatedSubjectS>
            <Subject message="/XTC/VideoSee/Create">
              <Parameters>
                <Parameter key="uid" value="{{slide_uuid}}" type="_"/>
                <Parameter key="style" value="XTC_MediaCarousel" type="string"/>
                <Parameter key="uiRoot" value="MainCanvas/[root]" type="string"/>
                <Parameter key="uiSlot" value="{{slide_slot}}" type="string"/>
                <Parameter key="worldRoot" value="" type="string"/>
                <Parameter key="worldSlot" value="" type="string"/>
              </Parameters>
            </Subject>
          </OnCreatedSubjectS>
          <OnActivatedSubjectS>
            <Subject message="/XTC/VideoSee/Open">
              <Parameters>
                <Parameter key="uid" value="{{slide_uuid}}" type="_"/>
                <Parameter key="source" value="assloud://" type="string"/>
                <Parameter key="uri" value="{{slide_uri}}" type="string"/>
                <Parameter key="delay" value="0" type="float"/>
              </Parameters>
            </Subject>
          </OnActivatedSubjectS>
          <OnClosedSubjectS>
            <Subject message="/XTC/VideoSee/Close">
              <Parameters>
                <Parameter key="uid" value="{{slide_uuid}}" type="string"/>
                <Parameter key="delay" value="0" type="float"/>
              </Parameters>
            </Subject>
          </OnClosedSubjectS>
        </Slide>
      </SlideS>
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
      <Subject message="/XTC/MediaCarousel/Open">
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

[更新] 升级到框架1.84.0
[新增] 添加autoSwitch配置项
[新增] 添加上一页和下一页两个按钮

