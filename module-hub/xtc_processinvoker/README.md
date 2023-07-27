---
description: 程序调用器
---

# XTC\_ProcessInvoker

## 术语约定


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
	  target.file: 目标程序的文件路径
	  target.workdir: 目标程序的工作目录
	  target.arguments: 目标程序的运行参数
    -->
	<Styles>
		<Style name="default">
			<Target file="notepad" workdir="" arguments=""/>
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
			<Subject message="/XTC/ProcessInvoker/Open">
				<Parameters>
					<Parameter key="uid" value="default" type="string"/>
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

