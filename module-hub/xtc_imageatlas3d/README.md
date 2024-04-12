---
description: 全景图集播放器
---

# XTC\_ImageAtlas3D

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
  <!-- 远程过程调用
      address: 地址
    -->
  <GRPC address="https://localhost:19000"/>
  <!-- 样式列表
      name: 名称
      renderer: 渲染器，可选值为 skybox
    -->
  <Styles>
    <Style name="default" renderer="skybox">
      <VoiceButton image="button_bg.png">
        <Anchor horizontal="right" vertical="bottom" marginH="50" marginV="50" width="187" height="64"/>
      </VoiceButton>
    </Style>
  </Styles>
  <!-- 预创建的实例列表
      uid: 实例的唯一ID
      style: 使用的样式名
    -->
  <Instances>
    <_Instance uid="default" style="default"/>
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
      <_Subject message="/XTC/ImageAtlas3D/Open">
        <Parameters>
          <Parameter key="uid" value="default" type="string"/>
          <Parameter key="source" value="assloud://" type="string"/>
          <Parameter key="uri" value="XTC.ImageAtlas3D/_resources/XTC.ImageAtlas3D.1.ai3" type="string"/>
          <Parameter key="delay" value="0" type="float"/>
        </Parameters>
      </_Subject>
    </Subjects>
  </Preload>
</MyConfig>
```

### 资源配置方式

文件结构
```
assets
  |- XTC.ImageAtlas3D
    |- _resources
      |- XTC.ImageAtlas3D.1.ai3
        |- 1.JPG
        |- 1.mp3
        |- bgm.mp3
        |- format.json
```

如上例中，文件存放在资源的包文件夹XTC.ImageAtlas3D的_resources目录下，整个数据包的文件夹名为XTC.ImageAtlas3D.1.ai3，其中包含4中类型的文件，分别为全景图、语音、背景音乐、格式配置。全景图、语音、背景音乐通过格式配置文件进行关联。

格式配置文件如下：

```json
{
    "__remarks__": [
        "分段切换时，如果配置有指定背景音乐，则会播放新文件"
    ],
    "verison": "v1",
    "bgm": {
        "file": "bgm.mp3",
        "volume": 100
    },
    "blocks": [{
        "image": {
            "file": "1.jpg",
            "rotation_y": 0
        },
        "voice": {
            "file": "1.mp3",
            "volume": 100,
            "duration": "3.03"
        },
        "bgm": {
            "file": "",
            "volume": 20
        }
    }],
    "actions": {
        "auto_rotate": {
            "speed_y": 10
        }
    }
}
```

其中voice.duration是语音的时间，如果设置为0，程序会在运行时进行计算（但不一定准确）。

## 消息订阅


## 依赖插件


## 更新日志

### 1.5.0

* 修改：更新框架为1.88
* 修改：更新ui为UI KIT

