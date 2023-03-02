---
description: 统计分析
---

# XTC\_AccessNet

统计分析模块可以在服务端写入一条记录，

## 术语约定

* 应用ID（AppID）

应用ID用于区分不同的使用场景、组织、群组等，可根据实际业务逻辑进行生成。模块中此字段仅用于记录，分析方法需要业务逻辑自行处理。


## 功能特性

### 记录跟踪

保存一条记录，包含 应用ID、序列号、用户ID、事件ID、时间参数等字段。

### 报表生成

将时间段内的记录生成报表。

## 配置说明

### UnityApp

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
    <GRPC address="http://localhost:18000"/>
    <!-- 样式列表
      name: 名称
      Tracker.appID: 应用id
    -->
    <Styles>
        <Style name="default">
          <Tracker appID="XTC.FMP.UnityApp"/>
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
            <Subject message="/XTC/Analytics/Open">
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

* /XTC/Analytics/TrackerRecord

保存一条记录

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| eventID | string | 事件的ID|
| eventParameter | string | 事件的参数|

## 通信协议

通信协议以Protobuf定义，各服务如下：

* [跟踪器(Tracker)](https://github.com/xtech-cloud/FMP-MOD-Analytics/tree/main/proto/Analytics/tracker.proto)
* [生成器(Generator)](https://github.com/xtech-cloud/FMP-MOD-Analytics/tree/main/proto/Analytics/generator.proto)

## 依赖插件

无

## 更新日志

无
