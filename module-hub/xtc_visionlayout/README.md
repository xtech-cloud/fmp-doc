---
description: 视觉布局
---

# XTC_VisionLayout

## 术语约定

- 布局（Layout）

TODO

- 过渡（Transition）

TODO

- 层（Layer）

一个层由布局、入过渡、出过渡三部分组成。

## 功能特性

- 层模式

TODO

- 进入效果

TODO

- 退出效果

TODO

- 标题定制

TODO

- 简介定制

TODO

- 控制面板

TODO

## 功能说明

- 层模式 （LayerPattern）

层可以定义模式，一个模式由布局列表、入过渡列表、出过渡列表构成，层在每一次切换时，从入过渡列表中随机选择一个过渡，从布局列表中随机选择一种布局，从出过渡列表中随机选择一个出过渡。

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
        slot: world根节点在主世界中的挂载路径
    -->
	<World visible="true" slot="[root]"/>
	<!-- 远程过程调用
        address: 地址
    -->
	<GRPC address="https://localhost:19000"/>
	<!-- 样式列表
        name: 名称
        Style.Background: 背景, 优先级为 video>image>color，全为空时，背景不显示
        Style.ToolBar.clickTrigger: 工具栏触发的点击次数
        Style.ToolBar.logoImage: 工具栏logo图片在themes文件夹中的相对地址
        Style.ToolBar.entryWidth: 入口节点的宽度
        Style.ToolBar.paddingLeft: 左边距
        Style.ToolBar.paddingRight: 右边距
        Style.ToolBar.paddingTop: 上边距
        Style.ToolBar.paddingBottom: 下边距
        Style.ToolBar.spacing: 节点的间隔
        Style.Profile.duration: 图片简介持续显示的时间，超时后隐藏
        Style.LayerPatterns: 层模式的列表
        Style.LayerPattern.name: 层模式的名称
        Style.LayerPattern.interactable: 点击节点是否能打开虚拟面板
        Style.LayerPattern.LayoutActions: 布局的行为列表
        Style.LayerPattern.InActions: 布局进入时的变换的行为列表
        Style.LayerPattern.OutActions: 布局退出时的变换的行为列表
        Style.LayerPattern.Subjects: 当可交互的节点被点击后发布的消息列表
        Style.LayerPattern.Action.name: 行为的名称
        Style.LayerPattern.Action.disable: 行为是否禁用
        Style.LayerPattern.Action.Properties: 行为的属性列表
        Style.LayerPattern.Action.Property."duration": 行为持续的时间
        Style.LayerPattern.Action.Property."speed": 效果的速度
        Style.LayerPattern.Action.Property."space": 节点间的间隔
        Style.LayerPattern.Action.Property."surround": 在打开虚拟面板时，节点自动绕开
        Style.LayerPattern.Action.Property."blank": TransitionIn类型的行为，在持续时间的开始预留的空白时间，过了blank时间后才开始动画
        Style.LayerPattern.Action<name="HorizontalFlowLayout">: 横向流动布局
        Style.LayerPattern.Action<name="HorizontalFlowLayout">.Property."row": 行的数目
        Style.LayerPattern.Action<name="VerticalFlowLayout">: 纵向流动布局
        Style.LayerPattern.Action<name="VerticalFlowLayout">.Property."column": 列的数目
        Style.LayerPattern.Action<name="StackedLayout">: 堆叠布局
        Style.LayerPattern.Action<name="StackedLayout">.Property."span": 虚拟列的跨越像素，数值越小越精细
        Style.LayerPattern.Action<name="StackedLayout">.Property."viewportCount": 视图的数量，视图的序号范围为[0, 视图数量-1]，序号越小，显示在越底层
        Style.LayerPattern.Action<name="StackedLayout">.Property."alpha_{n}": 第n层视图中节点的透明值
        Style.LayerPattern.Action<name="StackedLayout">.Property."speed_{n}": 第n层视图移动的速度
        Style.LayerPattern.Action<name="StackedLayout">.Property."cellMinLength_{n}": 第n层视图节点的最小边长
        Style.LayerPattern.Action<name="StackedLayout">.Property."cellMaxLength_{n}": 第n层视图节点的最大边长
        Style.LayerPattern.Action<name="StackedLayout">.Property."minSpaceX_{n}": 第n层视图节点间的最小横间距
        Style.LayerPattern.Action<name="StackedLayout">.Property."maxSpaceX_{n}": 第n层视图节点间的最大横间距
        Style.LayerPattern.Action<name="StackedLayout">.Property."minSpaceY_{n}": 第n层视图节点间的最小竖间距
        Style.LayerPattern.Action<name="StackedLayout">.Property."maxSpaceY_{n}": 第n层视图节点间的最大竖间距
        Style.LayerPattern.Action<name="FenchLayout">: 栅栏布局
        Style.LayerPattern.Action<name="FenchLayout">.Property."column": 栅栏的列数
        Style.LayerPattern.Action<name="FenchLayout">.Property."moveInterval": 移动效果的间隔时间（秒）
        Style.LayerPattern.Action<name="FenchLayout">.Property."moveDuration": 移动效果的持续时间（秒）
        Style.LayerPattern.Action<name="FrameLayout">: 画框的布局
        Style.LayerPattern.Action<name="FrameLayout">.Property."column": 画框的数量
        Style.LayerPattern.Action<name="FrameLayout">.Property."bgImage": 位于themes目录的背景图片
        Style.LayerPattern.Action<name="FrameLayout">.Property."frameImage": 位于themes目录的画框图片，图标需要满足左右的间距一致并且上下的间距一致
        Style.LayerPattern.Action<name="FrameLayout">.Property."frameBorder": 画框图片的九宫格切割参数
        Style.LayerPattern.Action<name="FrameLayout">.Property."frameMargin": 画框相对图片的间隔
        Style.LayerPattern.Action<name="FrameLayout">.Property."changeInterval": 切换的间隔时间（秒）
        Style.LayerPattern.Action<name="FrameLayout">.Property."moveDuration": 移动效果的持续时间（秒）
        Style.LayerPattern.Action<name="FrameLayout">.Property."maxWidth": 画框的最大宽度（基于1080高度的虚拟分辨率）
        Style.LayerPattern.Action<name="FrameLayout">.Property."maxHeight": 画框的最大高度（基于1080高度的虚拟分辨率）
        Style.LayerPattern.Action<name="Film">: 胶卷布局
        Style.LayerPattern.Action<name="Film">.Property."space": 胶卷中胶片之间的间隔
        Style.LayerPattern.Action<name="Film">.Property."trackCount": 胶卷轨道的数量，轨道的顺序从屏幕后方往前按照轨道的序号排列
        Style.LayerPattern.Action<name="Film">.Property."pictureWidth": 胶卷内部图片的宽度
        Style.LayerPattern.Action<name="Film">.Property."trackWidth": 胶卷轨道的宽度
        Style.LayerPattern.Action<name="Film">.Property."bgImage": 位于themes目录的背景图片
        Style.LayerPattern.Action<name="Film">.Property."trackImage": 位于themes目录的轨道图片，图片宽度需要匹配trackWidth
        Style.LayerPattern.Action<name="Film">.Property."maskImage": 位于themes目录的轨道遮罩图片，图片宽度需要匹配trackWidth
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_x": 轨道n的坐标位置，屏幕左方为-1.0，屏幕右方为1.0，允许设置到屏幕外的范围
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_length": 轨道n的长度，推荐值为虚拟分辨率（默认为1920x1080）高度的6倍左右
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_scale": 轨道n的大小缩放
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_alpha": 轨道n的透明度，范围为[0.0, 1.0]闭区间
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_direction": 轨道n的初始移动方向，1为往屏幕上方，-1为往屏幕下方
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_speed": 轨道n的移动速度
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_angle_z": 轨道n的z轴旋转角度, 垂直方向左方为正数，右方为负
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_angle_x": 轨道n的x轴旋转角度
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_angle_y": 轨道n的y轴旋转角度
        Style.LayerPattern.Action<name="Film">.Property."track_{n}_mask": 轨道n的遮罩透明值，范围为[0.0, 1.0]闭区间
        Style.LayerPattern.Action<name="ZipperLayout">: 拉链的布局
        Style.LayerPattern.Action<name="ZipperLayout">.Property."column": 竖栏的数量
        Style.LayerPattern.Action<name="ScrollLayout">: 卷轴的布局
        Style.LayerPattern.Action<name="ScrollLayout">.Property."hotspot_size": 热点图片的尺寸
        Style.LayerPattern.Action<name="ScrollLayout">.Property."hotspot_animation_interval_min": 热点图片动画的最小间隔时间
        Style.LayerPattern.Action<name="ScrollLayout">.Property."hotspot_animation_interval_max": 热点图片动画的最大间隔时间
        Style.LayerPattern.Action<name="EdgeFlyInTraision">: 边界飞入
        Style.LayerPattern.Action<name="EdgeFlyOutTraision">: 边界飞出
        Style.LayerPattern.Action<name="DragTraision">: 上方掉入
        Style.LayerPattern.Action<name="DropTraision">: 下方掉出
        Style.LayerPattern.Action<name="BreatheInTraision">: 呼入
        Style.LayerPattern.Action<name="BreatheOutTraision">: 吸出
        Style.LayerPattern.Action<name="FilmInTraision">: 胶卷布局进入，胶卷布局专用
        Style.LayerPattern.Action<name="FilmOutTraision">: 胶卷布局退出，胶卷布局专用
        Style.LayerPattern.Action<name="FrameInTraision">: 画框布局进入，画框布局专用
        Style.LayerPattern.Action<name="FrameOutTraision">: 画框布局退出，画框布局专用
        Style.LayerPattern.Action<name="ScrollInTraision">: 卷轴布局进入，卷轴布局专用
        Style.LayerPattern.Action<name="ScrollOutTraision">: 卷轴布局退出，卷轴布局专用
    -->
	<Styles>
		<Style name="default">
			<Background color="#242424FF" image="" video=""/>
			<ToolBar clickTrigger="20" logoImage="" entryWidth="136" paddingLeft="37" paddingRight="37" paddingTop="48" paddingBottom="80" spacing="14"/>
			<Title>
				<Anchor horizontal="left" vertical="top" marginH="64" marginV="0" height="100"/>
			</Title>
			<Profile duration="5">
				<Anchor horizontal="left" vertical="center" marginH="64" marginV="0" width="506" height="788"/>
			</Profile>
			<LayerPatterns>
				<LayerPattern name="Flow" interactable="true">
					<LayoutActions>
						<Action name="HorizontalFlowLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="speed" value="10" type="float"/>
								<Property key="row" value="8" type="int"/>
								<Property key="space" value="10" type="int"/>
								<Property key="surround" value="true" type="bool"/>
							</Properties>
						</Action>
						<Action name="VerticalFlowLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="speed" value="10" type="float"/>
								<Property key="column" value="14" type="int"/>
								<Property key="space" value="10" type="int"/>
								<Property key="surround" value="true" type="bool"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="FadeInTransition" disable="false">
							<Properties>
								<Property key="duration" value="4.5" type="float"/>
								<Property key="blank" value="1.5" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="FadeOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="Film" interactable="true">
					<LayoutActions>
						<Action name="FilmLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="space" value="20" type="int"/>
								<Property key="bgImage" value="layout.film.bg.jpg" type="string"/>
								<Property key="trackImage" value="layout.film.track.png" type="string"/>
								<Property key="maskImage" value="layout.film.mask.png" type="string"/>
								<Property key="trackCount" value="7" type="int"/>
								<Property key="pictureWidth" value="352" type="int"/>
								<Property key="trackWidth" value="552" type="int"/>
								<Property key="track_0_x" value="-0.25" type="float"/>
								<Property key="track_1_x" value="0.35" type="float"/>
								<Property key="track_2_x" value="-0.35" type="float"/>
								<Property key="track_3_x" value="0.75" type="float"/>
								<Property key="track_4_x" value="0.05" type="float"/>
								<Property key="track_5_x" value="-0.78" type="float"/>
								<Property key="track_6_x" value="0.88" type="float"/>
								<Property key="track_0_length" value="6000" type="int"/>
								<Property key="track_1_length" value="6000" type="int"/>
								<Property key="track_2_length" value="6000" type="int"/>
								<Property key="track_3_length" value="6000" type="int"/>
								<Property key="track_4_length" value="6000" type="int"/>
								<Property key="track_5_length" value="6000" type="int"/>
								<Property key="track_6_length" value="6000" type="int"/>
								<Property key="track_0_scale" value="0.4" type="float"/>
								<Property key="track_1_scale" value="0.45" type="float"/>
								<Property key="track_2_scale" value="0.6" type="float"/>
								<Property key="track_3_scale" value="0.6" type="float"/>
								<Property key="track_4_scale" value="0.8" type="float"/>
								<Property key="track_5_scale" value="0.9" type="float"/>
								<Property key="track_6_scale" value="0.8" type="float"/>
								<Property key="track_0_alpha" value="0.2" type="float"/>
								<Property key="track_1_alpha" value="0.4" type="float"/>
								<Property key="track_2_alpha" value="0.6" type="float"/>
								<Property key="track_3_alpha" value="1.0" type="float"/>
								<Property key="track_4_alpha" value="0.9" type="float"/>
								<Property key="track_5_alpha" value="1.0" type="float"/>
								<Property key="track_6_alpha" value="1.0" type="float"/>
								<Property key="track_0_direction" value="-1" type="float"/>
								<Property key="track_1_direction" value="1" type="float"/>
								<Property key="track_2_direction" value="-1" type="float"/>
								<Property key="track_3_direction" value="1" type="float"/>
								<Property key="track_4_direction" value="-1" type="float"/>
								<Property key="track_5_direction" value="1" type="float"/>
								<Property key="track_6_direction" value="-1" type="float"/>
								<Property key="track_0_speed" value="20" type="float"/>
								<Property key="track_1_speed" value="20" type="float"/>
								<Property key="track_2_speed" value="20" type="float"/>
								<Property key="track_3_speed" value="20" type="float"/>
								<Property key="track_4_speed" value="20" type="float"/>
								<Property key="track_5_speed" value="20" type="float"/>
								<Property key="track_6_speed" value="20" type="float"/>
								<Property key="track_0_angle_z" value="-13" type="float"/>
								<Property key="track_1_angle_z" value="14" type="float"/>
								<Property key="track_2_angle_z" value="45" type="float"/>
								<Property key="track_3_angle_z" value="-25" type="float"/>
								<Property key="track_4_angle_z" value="-46" type="float"/>
								<Property key="track_5_angle_z" value="-10" type="float"/>
								<Property key="track_6_angle_z" value="19" type="float"/>
								<Property key="track_0_angle_x" value="0" type="float"/>
								<Property key="track_1_angle_x" value="0" type="float"/>
								<Property key="track_2_angle_x" value="0" type="float"/>
								<Property key="track_3_angle_x" value="0" type="float"/>
								<Property key="track_4_angle_x" value="0" type="float"/>
								<Property key="track_5_angle_x" value="0" type="float"/>
								<Property key="track_6_angle_x" value="0" type="float"/>
								<Property key="track_0_angle_y" value="0" type="float"/>
								<Property key="track_1_angle_y" value="0" type="float"/>
								<Property key="track_2_angle_y" value="0" type="float"/>
								<Property key="track_3_angle_y" value="0" type="float"/>
								<Property key="track_4_angle_y" value="0" type="float"/>
								<Property key="track_5_angle_y" value="0" type="float"/>
								<Property key="track_6_angle_y" value="0" type="float"/>
								<Property key="track_0_mask" value="0.1" type="float"/>
								<Property key="track_1_mask" value="0.1" type="float"/>
								<Property key="track_2_mask" value="0.1" type="float"/>
								<Property key="track_3_mask" value="0.1" type="float"/>
								<Property key="track_4_mask" value="0.1" type="float"/>
								<Property key="track_5_mask" value="0.1" type="float"/>
								<Property key="track_6_mask" value="0.1" type="float"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="FilmInTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
								<Property key="blank" value="0" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="FilmOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
								<Property key="blank" value="0" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="Stacked" interactable="true">
					<LayoutActions>
						<Action name="StackedLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="span" value="40" type="int"/>
								<Property key="viewportCount" value="2" type="int"/>
								<Property key="alpha_0" value="0.2" type="float"/>
								<Property key="speed_0" value="15" type="float"/>
								<Property key="cellMinLength_0" value="200" type="int"/>
								<Property key="cellMaxLength_0" value="400" type="int"/>
								<Property key="minSpaceX_0" value="50" type="int"/>
								<Property key="maxSpaceX_0" value="100" type="int"/>
								<Property key="minSpaceY_0" value="50" type="int"/>
								<Property key="maxSpaceY_0" value="100" type="int"/>
								<Property key="alpha_1" value="1" type="float"/>
								<Property key="speed_1" value="30" type="float"/>
								<Property key="cellMinLength_1" value="150" type="int"/>
								<Property key="cellMaxLength_1" value="300" type="int"/>
								<Property key="minSpaceX_1" value="50" type="int"/>
								<Property key="maxSpaceX_1" value="100" type="int"/>
								<Property key="minSpaceY_1" value="50" type="int"/>
								<Property key="maxSpaceY_1" value="100" type="int"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="BreatheInTransition" disable="false">
							<Properties>
								<Property key="duration" value="4.5" type="float"/>
								<Property key="blank" value="1.5" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="BreatheOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="Fench" interactable="true">
					<LayoutActions>
						<Action name="FenchLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="column" value="6" type="int"/>
								<Property key="moveInterval" value="5" type="int"/>
								<Property key="moveDuration" value="1" type="float"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="DragTransition" disable="false">
							<Properties>
								<Property key="duration" value="4.5" type="float"/>
								<Property key="blank" value="1.5" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="DropTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="Frame" interactable="true">
					<LayoutActions>
						<Action name="FrameLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="column" value="6" type="int"/>
								<Property key="bgImage" value="layout.frame.bg.jpg" type="string"/>
								<Property key="frameImage" value="layout.frame.frame.png" type="string"/>
								<Property key="frameBorderTop" value="256" type="int"/>
								<Property key="frameBorderBottom" value="256" type="int"/>
								<Property key="frameBorderLeft" value="128" type="int"/>
								<Property key="frameBorderRight" value="128" type="int"/>
								<Property key="frameMarginTop" value="-166" type="int"/>
								<Property key="frameMarginBottom" value="-166" type="int"/>
								<Property key="frameMarginLeft" value="-55" type="int"/>
								<Property key="frameMarginRight" value="-55" type="int"/>
								<Property key="changeInterval" value="10" type="int"/>
								<Property key="maxWidth" value="500" type="int"/>
								<Property key="maxHeight" value="700" type="int"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="FrameInTransition" disable="false">
							<Properties>
								<Property key="duration" value="4.5" type="float"/>
								<Property key="blank" value="1.5" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="FrameOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="Zipper" interactable="true">
					<LayoutActions>
						<Action name="ZipperLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="column" value="12" type="int"/>
								<Property key="space" value="36" type="int"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="EdgeFlyInTransition" disable="false">
							<Properties>
								<Property key="duration" value="4.5" type="float"/>
								<Property key="blank" value="1.5" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="EdgeFlyOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="Scroll" interactable="true">
					<LayoutActions>
						<Action name="ScrollLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="hotspot_size" value="64" type="int"/>
								<Property key="hotspot_animation_interval_min" value="5" type="int"/>
								<Property key="hotspot_animation_interval_max" value="10" type="int"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="ScrollInTransition" disable="false">
							<Properties>
								<Property key="duration" value="4.5" type="float"/>
								<Property key="blank" value="1.5" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="ScrollOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="FlipCard" interactable="true">
					<LayoutActions>
						<Action name="FlipCardLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
								<Property key="splashTime" value="3" type="float"/>
								<Property key="row" value="4" type="int"/>
								<Property key="column" value="7" type="int"/>
								<Property key="spaceX" value="20" type="int"/>
								<Property key="spaceY" value="20" type="int"/>
								<Property key="animDelayMin" value="5" type="float"/>
								<Property key="animDelayMax" value="15" type="float"/>
								<Property key="animDuration" value="1" type="float"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="EmptyInTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="FadeOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
						<Subject message="/XTC/IntegrationBoard/DirectOpen">
							<Parameters>
								<Parameter key="uid" value="{{dummyboard_uid}}" type="_"/>
								<Parameter key="style" value="circular" type="string"/>
								<Parameter key="source" value="assloud://" type="string"/>
								<Parameter key="uri" value="{{content_uri}}" type="_"/>
								<Parameter key="position_x" value="{{dummyboard_position_x}}" type="_"/>
								<Parameter key="position_y" value="{{dummyboard_position_y}}" type="_"/>
								<Parameter key="uiSlot" value="{{dummyboard_uiSlot}}" type="_"/>
								<Parameter key="delay" value="0" type="float"/>
							</Parameters>
						</Subject>
					</Subjects>
				</LayerPattern>
				<LayerPattern name="Dummy" interactable="true">
					<LayoutActions>
						<Action name="DummyLayout" disable="false">
							<Properties>
								<Property key="duration" value="30" type="float"/>
							</Properties>
						</Action>
					</LayoutActions>
					<InActions>
						<Action name="DummyInTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</InActions>
					<OutActions>
						<Action name="DummyOutTransition" disable="false">
							<Properties>
								<Property key="duration" value="3" type="float"/>
							</Properties>
						</Action>
					</OutActions>
					<Subjects>
					</Subjects>
				</LayerPattern>
			</LayerPatterns>
		</Style>
	</Styles>
	<!-- 预创建的实例列表
        uid: 实例的唯一ID
        style: 使用的样式名
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
			<Subject message="/XTC/VisionLayout/Open">
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

### 配置层模板

#### 卷轴模式（Scroll）

在 catalog 中的 kvS 中，添加 Scroll_Image 字段，值为卷轴的背景图，图片地址位于包（bundle）中的附件文件夹（\_attachments）。

```json
{
    ...
    "kvS": {
        "LayerPattern": "Scroll",
        "TitleImage": "",
        "ProfileImage": "",
        "Scroll_Image": "b359b77a-fb45-4845-8455-27f57ddaeed8/_attachments/scroll.jpg"
    }
}
```

注意 LayerPattern 字段需要匹配到 xml 配置文件中的 LayerPattern。

```xml
<LayerPattern name="Scroll" interactable="true">
......
</LayerPattern>
```

完成以上两个步骤，已经可以显示卷轴图片了。如果需要配置热点。则需要在内容（Content）的元数据（Meta）文件中添加需要的字段。

```json
"kvS": {
    "XTC_VisionLayout_Hotspot_x": "100",
    "XTC_VisionLayout_Hotspot_y": "100"
}
```

以上两个值，分别代表了热点在大图中的 x 和 y 坐标，卷轴背景图的中心点为（0，0），左和下为负，右和上为正。

所有的内容（content），在卷轴布局中，均显示为一个热点。

#### 翻转卡片模式（FlipCard）

翻转卡片的版式具有一个过场阶段(Splash)，此阶段所有节点显示一张过场图片，此图片位于 themes 文件夹中，对应的格式为

```
flipcard.splash.{layerpath}-{index}.png
```

其中 layerpath 对应 catalog 中的 path 字段,index 对应节点的序号（从 1 开始）。其中 layerpath 中的"/"符号需要替换为"\_"。

例如 catalog 中的 path 为"/Demoshow"，此版式具有 3 行 x5 列个节点，那么每个节点对应的过场图片如下

```
flipcard.splash._Demoshow-1.png
...
flipcard.splash._Demoshow-15.png
```

#### 虚拟模式（Dummy）

虚拟布局用于挂载外部实现的布局，其组成为虚拟布局（DummyLayout），虚拟布局专用的虚拟入过渡（DummyInTransition）和虚拟出过渡（DummyOutTransition）。
注意：虚拟布局只能使用 DummyInTransition 和 DummyOutTransition。

配置方式可参考，LayerPattern.name 为 Dummy 的配置段。配置中只保留了持续时间的参数，其余参数需要在挂载的外部布局模块中配置。

### 配置标题图

TODO

### 配置简介图

TODO

## 消息订阅

- /XTC/VisionLayout/ToolBar/Popup

此消息将打开工具栏

| 参数 | 类型   | 说明       |
| ---- | ------ | ---------- |
| uid  | string | 实例的 uid |

- /XTC/VisionLayout/DummyLayout/OnInlay

当虚拟布局嵌入时

| 参数                      | 类型                  | 说明             |
| ------------------------- | --------------------- | ---------------- |
| layer                     | string                | 层的名称         |
| pattern                   | string                | 模式的名称       |
| virtual_resolution_width  | int                   | 虚拟分辨率的宽度 |
| virtual_resolution_height | int                   | 虚拟分辨率的高度 |
| uiSlot                    | UnityEngine.Transform | ui 的挂载槽      |

- /XTC/VisionLayout/DummyLayout/OnEnter

当虚拟布局显示状态进入时

| 参数     | 类型   | 说明           |
| -------- | ------ | -------------- |
| layer    | string | 层的名称       |
| pattern  | string | 模式的名称     |
| duration | float  | 显示的持续时间 |

- /XTC/VisionLayout/DummyLayout/OnExit

当虚拟布局显示状态退出时

| 参数    | 类型   | 说明       |
| ------- | ------ | ---------- |
| layer   | string | 层的名称   |
| pattern | string | 模式的名称 |

- /XTC/VisionLayout/DummyInTransition/OnEnter

当虚拟布局入变换状态进入时

| 参数     | 类型   | 说明             |
| -------- | ------ | ---------------- |
| layer    | string | 层的名称         |
| pattern  | string | 模式的名称       |
| duration | float  | 入变换的持续时间 |

- /XTC/VisionLayout/DummyInTransition/OnExit

当虚拟布局入变换状态退出时

| 参数    | 类型   | 说明       |
| ------- | ------ | ---------- |
| layer   | string | 层的名称   |
| pattern | string | 模式的名称 |

- /XTC/VisionLayout/DummyOutTransition/OnEnter

当虚拟布局出变换状态进入时

| 参数     | 类型   | 说明             |
| -------- | ------ | ---------------- |
| layer    | string | 层的名称         |
| pattern  | string | 模式的名称       |
| duration | float  | 出变换的持续时间 |

- /XTC/VisionLayout/DummyOutTransition/OnExit

当虚拟布局出变换状态退出时

| 参数    | 类型   | 说明       |
| ------- | ------ | ---------- |
| layer   | string | 层的名称   |
| pattern | string | 模式的名称 |

## 依赖插件

oelFSM

## 更新日志

### 1.0.5

[新增] 支持 Catalog 中的 Instance 字段过滤

### 0.18.0

[新增] 翻转卡片版式

### 0.15.1

[修正] 卷轴版式位于第一个时会抛出异常

### 0.15.0

[更新] 升级框架到 1.86

### 0.13.1

- 修正：

补全 LayerPattern.Subject 中缺失的 uiSlot 参数
LayerPattern.Subject 中的变量的类型更改为"\_"

### 0.13.1

- 修正：

补全 LayerPattern.Subject 中缺失的 uiSlot 参数
LayerPattern.Subject 中的变量的类型更改为"\_"

### 0.13.0

- 新增：

支持配置工具栏

### 0.12.0

- 更新：

Stacked 布局更改为分层配置

### 0.11.3

- 修正：

Dummy 消息缺少 layer 参数

### 0.11.2

- 修正：

Dummy 消息缺少 duration 参数

### 0.11.0

- 新增：

新增 Dummy 布局
