---
description: 资源搜索
---

# XTC\_Search

## 术语约定

TODO

## 功能特性

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
      primaryColor: 主颜色，RGBA的HEX值
      Background.visible: 背景是否可见
      Background.color: 背景的颜色，RGBA的HEX值
      Input.marginTop: 输入框的顶部边距
      Input.width: 输入框的宽度
      Input.height: 输入框的高度
      Input.iconSize: 输入框的搜索图标的尺寸
      Input.fontSize: 输入框的字体尺寸
      Keyboard.keyImage: 按键图片，64x64
      Keyboard.width: 键盘的宽度
      Keyboard.height: 键盘的高度
      Keyboard.keySize: 键盘的按键的尺寸
      Keyboard.fontSize: 键盘的按键的字体尺寸
      Keyboard.spacingH: 键盘的按键的水平间隔
      Keyboard.spacingV: 键盘的按键的垂直间隔
      Result.Margin: 搜索结果框的边距
      Result.spacingH: 搜索结果的水平间隔
      Result.spacingV: 搜索结果的垂直间隔
      Record.color: 搜索结果记录的颜色
      Record.capacity: 搜索结果的最大显示数量
      Record.iconVisible: 搜索结果的图标是否可见，（当前版本暂未实现）
      Record.iconImage: 搜索结果的图标的默认图片
      Record.iconSize: 搜索结果的图标的尺寸
      Record.iconMarginLeft: 搜索结果的图标的左边距
      Record.width: 搜索结果的宽度
      Record.height: 搜索结果的高度
      Record.fontSize: 搜索结果的字体尺寸
      Record.TextMargin: 搜索结果的文字的边距
      ActivateSubjects: 搜索结果点击后发布的消息列表
    -->
  <Styles>
    <Style name="default" primaryColor="#49DDE4FF">
      <Background visible="true" color="#282828FF"/>
      <Input marginTop="24" width="500" height="36" iconSize="28" fontSize="22"/>
      <Keyboard keyImage="key_default.png" width="580" height="140" keySize="32" fontSize="14" spacingH="12" spacingV="12"/>
      <Result spacingH="16" spacingV="12">
        <Margin top="80" bottom="140" left="44" right="44"/>
      </Result>
      <Record color="#1F1F1FFF" capacity="30" iconVisible="true" iconImage="icon-default.png" iconSize="36" iconMarginLeft="12" width="234" height="48" fontSize="16">
        <TextMargin top="1" bottom="0" left="58" right="10"/>
      </Record>
      <ActivateSubjects>
        <Subject message="/XTC/Search/Clean">
          <Parameters>
            <Parameter key="uid" value="{{uid}}" type="string"/>
            <Parameter key="source" value="assloud://" type="string"/>
            <Parameter key="bundle_uuid" value="{{bundle_uuid}}" type="string"/>
            <Parameter key="content_uuid" value="{{content_uuid}}" type="string"/>
          </Parameters>
        </Subject>
      </ActivateSubjects>
    </Style>
  </Styles>
  <!-- 预创建的实例列表
      uid: 实例的唯一ID
      style: 使用的样式名
      uiSlot: UI挂载的路径
      worldSlot: World挂载的路径
    -->
  <Instances>
    <Instance uid="default" style="default" uiSlot="" worldSlot=""/>
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
      <Subject message="/XTC/Search/Open">
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

### 变量

* ActivateSubjects

| 变量 | 类型 | 说明 |
| --- | --- | --- |
| {{uid}} | string | 实例的uid |
| {{bundle_uuid}} | string | 激活的搜索结果的包的uuid |
| {{content_uuid}} | string | 激活的搜索结果的内容的uuid |

## 消息订阅

* /XTC/Search/Inlay

嵌入一个搜索的新实例

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 新实例的uid|
| style | string | 新实例的样式名 |
| uiSlot | UnityEngine.GameObject | 新实例的ui挂载槽 |
| worldSlot | UnityEngine.GameObject | 新实例的世界挂载槽 |

* /XTC/Search/Refresh

刷新一个搜索的实例

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 新实例的uid|

* /XTC/Search/Clean

清空一个搜索的实例

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 新实例的uid|

## 依赖插件

NPinyin.Core


## 更新日志

### 0.2.3

* 更新

增加消息订阅的变量

### 0.2.1

* 更新

更新样式


### 0.2.0

* 新增

预加载catalog中的所有内容的meta.json和icon.png

