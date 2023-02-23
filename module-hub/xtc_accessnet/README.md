---
description: 接入网
---

# XTC\_AccessNet

接入网可将多个接入点组成一个网络。接入点在接入网络后，会上传自身的硬件、系统、程序等相关信息。并在使用过程中保持心跳。

## 术语约定

* 接入点 (Access Point)

在一个设备上运行的衍生应用，称为一个接入点。接入点以SerialNumber作为身份识别。

接入点和应用相关，和硬件无关。

* 序列号 (SerialNumber)

序列号和设备码(Device Code)不同，它们的主要区别为:

设备码由硬件信息生成，保证物理上的不可篡改性和不可复制性，设备码主要用于激活授权等敏感操作。

序列号由业务实际使用场景预先生成，配置到AppConfig.xml中，在物理上可篡改，可复制。主要用于设备身份识别操作。

在不配置序列号时，序列号的值默认为设备码。

## 功能特性

### 接入点三态

接入点有`在线`、`离线`、`异常`三种状态。

### 接入点信息上报

接入点将以下硬件信息上报给服务端：

* 设备名称
* 设备型号
* 设备类型

接入点将以下系统信息上报给服务端：

* 操作系统系列
* 操作系统版本

接入点将以下程序信息上报给服务端：

* 应用程序组织名
* 应用程序产品名
* 应用程序版本号
* 应用程序授权时间
* 应用程序授权有效期

### 接入点上线 (Access Point Online)

当客户端应用运行AccessNet模块后，会向服务端发送上线消息，并发送当前的硬件、系统、程序的相关信息。并获取自身的UUID用于后续通信。

### 接入点心跳 (Access Point HeartBeat)

客户端模块上线完成后，再每隔一段时间向服务端发送心跳，告知服务端自身的健康状态。服务端将客户端的状态更改为`在线`。

### 接入点下线 (Access Point Offline)

客户端应用程序退出时，告知服务端自己主动下线。服务端收到下线消息后，将客户端的状态更改为`离线`。如果服务端未收到客户端的离线消息，并在一段时候后也未收到客户端的心跳消息，那么服务端将客户端的状态更改为`异常`。


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
    <GRPC address="https://localhost:19000"/>
    <!-- 样式列表
      name: 名称
    -->
    <Styles>
        <Style name="default">
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
            <Subject message="/XTC/AccessNet/Open">
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

无

## 通信协议

通信协议以Protobuf定义，文件见 [Github](https://github.com/xtech-cloud/FMP-MOD-AccessNet/proto)

## 依赖插件

无

## 更新日志

无
