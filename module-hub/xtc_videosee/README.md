---
description: 视频播放器
---

# XTC\_VideoSee

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
      Background: 背景
      Background.visible: 是否可见
      Background.color: 颜色，RGBA的HEX值
      Pending: 加载图片
      ToolBar: 工具栏
      ToolBar.visibleMode: 显示模式，可选值为（auto,show,hide）
      ToolBar.SliderProgress.width: 进度条宽度
      ToolBar.ButtonLoop.mode: 初始循环模式，可选值为（none, single）
      ToolBar.ButtonLoop.visible: 循环按钮是否可见
      ToolBar.ButtonLoop.icon: 循环按钮的图片，建议大小和ToolBar.Anchor.height一致
      ToolBar.ButtonPlay.icon: 开始按钮的图片,建议大小和ToolBar.Anchor.height一致
      ToolBar.ButtonPause.icon: 暂停按钮的图片,建议大小和ToolBar.Anchor.height一致
    -->
	<Styles>
		<Style name="default">
			<Background visible="true" color="#00000088"/>
			<Pending image="pending#default.png">
				<Anchor width="128" height="128"/>
			</Pending>
			<ToolBar visibleMode="auto">
				<Anchor horizontal="center" vertical="bottom" marginH="0" marginV="0" width="1920" height="80"/>
				<ButtonLoop icon="btnLoop#default.png" mode="none" visible="false"/>
				<ButtonPlay icon="btnPlay#default.png"/>
				<ButtonPause icon="btnPause#default.png"/>
				<ButtonVolume icon="btnVolume#default.png"/>
				<TextTime fontSize="22" width="120"/>
				<SliderTime height="48">
					<Background image="sliderTime_bg#default.png">
						<Border left="0" right="0" top="0" bottom="0"/>
					</Background>
					<Fill image="sliderTime_fill#default.png">
						<Border left="0" right="0" top="0" bottom="0"/>
					</Fill>
					<Handle image="sliderTime_handle#default.png"/>
				</SliderTime>
				<SliderVolume width="48" height="168">
					<Background image="sliderVolume_bg#default.png">
						<Border left="0" right="0" top="0" bottom="0"/>
					</Background>
					<Fill image="sliderVolume_fill#default.png">
						<Anchor width="48" height="136"/>
					</Fill>
					<Handle image="sliderVolume_handle#default.png">
						<Anchor width="48" height="48"/>
					</Handle>
				</SliderVolume>
			</ToolBar>
		</Style>
		<Style name="small">
			<Background visible="true" color="#00000088"/>
			<Pending image="pending#default.png">
				<Anchor width="64" height="64"/>
			</Pending>
			<ToolBar visibleMode="auto">
				<Anchor horizontal="center" vertical="bottom" marginH="0" marginV="0" width="656" height="48"/>
				<ButtonLoop icon="btnLoop#default.png" mode="none" visible="false"/>
				<ButtonPlay icon="btnPlay#default.png"/>
				<ButtonPause icon="btnPause#default.png"/>
				<ButtonVolume icon="btnVolume#default.png"/>
				<TextTime fontSize="16" width="80"/>
				<SliderTime height="28">
					<Background image="sliderTime_bg#default.png">
						<Border left="0" right="0" top="0" bottom="0"/>
					</Background>
					<Fill image="sliderTime_fill#default.png">
						<Padding left="0" right="0" top="0" bottom="0"/>
					</Fill>
					<Handle image="sliderTime_handle#default.png"/>
				</SliderTime>
				<SliderVolume width="40" height="120">
					<Background image="sliderVolume_bg#default.png">
						<Border left="0" right="0" top="0" bottom="0"/>
					</Background>
					<Fill image="sliderVolume_fill#default.png">
						<Anchor width="40" height="97"/>
					</Fill>
					<Handle image="sliderVolume_handle#default.png">
						<Anchor width="36" height="36"/>
					</Handle>
				</SliderVolume>
			</ToolBar>
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
			<Subject message="/XTC/VideoSee/Open">
				<Parameters>
					<Parameter key="uid" value="default" type="string"/>
					<Parameter key="source" value="assloud://" type="string"/>
					<Parameter key="uri" value="XTC.VideoSee/_attachments/test.mp4" type="string"/>
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

### 0.3.0

* 新增：默认是用1080P样式


