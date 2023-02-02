---
description: 集成面板
---

# XTC\_IntegrationBoard

* [0.13.0](../module-hub/xtc\_integrationboard@0.13.0.md)

集成面板可以将多个模块整合进一个面板中，用多个模块为一个内容提供多样的显示形态和交互体验。

## 术语约定

TODO

## 功能特性

* 对齐网格（Align Grid）

将视窗（Viewport）划分为N行M列的网格，在开启吸附功能后，在（x,y）坐标位置打开的集成面板会自动寻找最靠近的网格，并将最终打开的坐标位置设置为网格的中心的坐标位置（x', y'）。

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
  <!-- 交融检测
      mode: 模式，可选值为 circular, rectangle
  -->
  <!-- 样式列表
      name: 名称
      Style.AlignGrid: 对齐网格，将屏幕划分为n行xm列的网格，可控制面板吸附在最近的网格的中心位置
      Style.AlignGrid.visible: 是否可见
      Style.AlignGrid.row: 行数
      Style.AlignGrid.column: 列数
      Style.AlignGrid.stickH: 水平吸附
      Style.AlignGrid.stickV: 垂直吸附
      Style.TitleBarBackground: 首页标题栏背景
      Style.TitleBarBackground.image: 位于theme文件夹中的图片
      Style.TitleBarBackground.color: 图片的叠加颜色
      Style.TitleBarBackground.Border: 图片的九宫格边界
      Style.PanelBackground: 首页面板背景
      Style.PanelBackground.image: 位于theme文件夹中的图片
      Style.PanelBackground.color: 图片的叠加颜色
      Style.PanelBackground.Border: 图片的九宫格边界
      Style.LikeBackground: 点赞背景
      Style.LikeBackground.image: 位于theme文件夹中的图片
      Style.LikeBackground.color: 图片的叠加颜色
      Style.LikeBackground.Border: 图片的九宫格边界
      Style.TopicBackground: 标语背景
      Style.TopicBackground.image: 位于theme文件夹中的图片
      Style.TopicBackground.color: 图片的叠加颜色
      Style.TopicBackground.Border: 图片的九宫格边界
      Style.DescriptionBackground: 描述背景
      Style.DescriptionBackground.image: 位于theme文件夹中的图片
      Style.DescriptionBackground.color: 图片的叠加颜色
      Style.DescriptionBackground.Border: 图片的九宫格边界
      Style.TabBar: 标签栏
      Style.TabBar.space:  标签间的间隔
      Style.TabBar.Background: 标签栏背景
      Style.TabBar.TabButtons:  标签按钮列表
      Style.TabBar.TabButton.contentKey:  对应content的meta.json的kvS中的键，如果存在则显示。“_”表示不与content对应，始终显示。
      Style.CoverPicture.fitmode: 匹配模式，可选值为（none:使用原图大小，zoomout:比容器大时缩小为容器大小，zoomin:比容器小时放大为容器大小，zoom:同时使用zoomin和zoomout）
    -->
  <Styles>
    <Style name="rectangle" width="880" height="740">
      <AlignGrid row="1" column="1" stickH="true" stickV="true"/>
      <TitleBarBackground image="rectangle_titlebar_bg.png" color="#3333334C">
        <Border top="56" bottom="56" left="56" right="56"/>
      </TitleBarBackground>
      <PanelBackground image="rectangle_panel_bg.png" color="#272930CC">
        <Border top="56" bottom="56" left="56" right="56"/>
      </PanelBackground>
      <LikeBackground image="rectangle_button.png" color="#5B656F46">
        <Border top="16" bottom="16" left="16" right="16"/>
      </LikeBackground>
      <TopicBackground image="rectangle_button.png" color="#5B656F46">
        <Border top="16" bottom="16" left="16" right="16"/>
        <SwitchIcon image=""/>
      </TopicBackground>
      <DescriptionBackground image="rectangle_button.png" color="#5B656F46">
        <Border top="16" bottom="16" left="16" right="16"/>
      </DescriptionBackground>
      <TopicSwitchIcon image="rectangle_icon_switch.png" />
      <DescriptionSwitchIcon image="rectangle_icon_switch.png"/>
      <LikedIcon image="rectangle_icon_liked.png">
        <Anchor horizontal="left" vertical="center" marginH="12" marginV="0" width="20" height="20"/>
      </LikedIcon>
      <UnlikedIcon image="rectangle_icon_unliked.png">
        <Anchor horizontal="left" vertical="center" marginH="12" marginV="0" width="20" height="20"/>
      </UnlikedIcon>
      <SizeRange descriptionMaxHeight="110"/>
      <ImageToolBox image="rectangle_button.png" color="#5B656F88">
        <Border top="16" bottom="16" left="16" right="16"/>
        <Anchor horizontal="right" vertical="bottom" marginH="36" marginV="24" height="48"/>
        <ZoomInButton image="rectangle_imagetoolbox_zoomin.png" color="#FFFFFFFF">
          <Anchor height="36" width="36"/>
        </ZoomInButton>
        <ZoomOutButton image="rectangle_imagetoolbox_zoomout.png" color="#FFFFFFFF">
          <Anchor height="36" width="36"/>
        </ZoomOutButton>
        <BackButton image="rectangle_imagetoolbox_back.png" color="#FFFFFFFF">
          <Anchor height="36" width="36"/>
        </BackButton>
      </ImageToolBox>
      <PageSlots>
        <PageSlot page="media">
          <InlaySubject message="/XTC/MediaCenter/Inlay">
            <Parameters>
              <Parameter key="uid" value="{{uid}}" type="_"/>
              <Parameter key="style" value="default" type="string"/>
              <Parameter key="slot" value="{{page_slot}}" type="_"/>
            </Parameters>
          </InlaySubject>
          <RefreshSubject message="/XTC/MediaCenter/Refresh">
            <Parameters>
              <Parameter key="uid" value="{{uid}}" type="_"/>
              <Parameter key="source" value="assloud://" type="string"/>
              <Parameter key="uri" value="{{uri}}" type="_"/>
            </Parameters>
          </RefreshSubject>
        </PageSlot>
      </PageSlots>
      <TabBar space="24">
        <Background image="rectangle_tabbar_bg.png" color="#272930A0">
          <Border top="56" bottom="56" left="56" right="56"/>
        </Background>
        <CloseButton image="rectangle_tab_close.png" color="#FFFFFFFF">
          <Anchor width="44" height="44"/>
          <Subjects>
            <Subject message="/XTC/IntegrationBoard/DirectClose">
              <Parameters>
                <Parameter key="uid" value="{{uid}}" type="_"/>
                <Parameter key="delay" value="0" type="float"/>
              </Parameters>
            </Subject>
          </Subjects>
        </CloseButton>
        <TabButtons>
          <TabButton name="__home__" contentKey="_"
                     uncheckedIcon="rectangle_tab_profile_unchecked.png" uncheckedWidth="44" uncheckedHeight="44"
                     checkedIcon="rectangle_tab_profile_checked.png" checkedWidth="96" checkedHeight="44">
            <Subjects>
              <Subject message="/XTC/IntegrationBoard/ActivatePage">
                <Parameters>
                  <Parameter key="uid" value="{{uid}}" type="_"/>
                  <Parameter key="page" value="__home__" type="string"/>
                </Parameters>
              </Subject>
            </Subjects>
          </TabButton>
          <TabButton name="dossier" contentKey="dossier"
                     uncheckedIcon="rectangle_tab_dossier_unchecked.png" uncheckedWidth="44" uncheckedHeight="44"
                     checkedIcon="rectangle_tab_dossier_checked.png" checkedWidth="96" checkedHeight="44">
            <Subjects>
              <Subject message="/XTC/IntegrationBoard/ActivatePage">
                <Parameters>
                  <Parameter key="uid" value="{{uid}}" type="_"/>
                  <Parameter key="page" value="dossier" type="string"/>
                </Parameters>
              </Subject>
            </Subjects>
          </TabButton>
          <TabButton name="media" contentKey="MediaCenter"
                     uncheckedIcon="rectangle_tab_media_unchecked.png" uncheckedWidth="44" uncheckedHeight="44"
                     checkedIcon="rectangle_tab_media_checked.png" checkedWidth="96" checkedHeight="44">
            <Subjects>
              <Subject message="/XTC/IntegrationBoard/ActivatePage">
                <Parameters>
                  <Parameter key="uid" value="{{uid}}" type="_"/>
                  <Parameter key="page" value="media" type="string"/>
                </Parameters>
              </Subject>
            </Subjects>
          </TabButton>
          <TabButton name="search" contentKey="_"
                     uncheckedIcon="rectangle_tab_search_unchecked.png" uncheckedWidth="44" uncheckedHeight="44"
                     checkedIcon="rectangle_tab_search_checked.png" checkedWidth="96" checkedHeight="44">
            <Subjects>
              <Subject message="/XTC/IntegrationBoard/ActivatePage">
                <Parameters>
                  <Parameter key="uid" value="{{uid}}" type="_"/>
                  <Parameter key="page" value="search" type="string"/>
                </Parameters>
              </Subject>
            </Subjects>
          </TabButton>
        </TabButtons>
      </TabBar>
      <CoverPicture fitmode="zoom"/>
    </Style>
  </Styles>
  <!-- 预创建的实例列表
      uid: 实例的唯一ID
      style: 使用的样式名
    -->
  <Instances>
    <Instance uid="default" style="rectangle"/>
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
      <Subject message="/XTC/IntegrationBoard/Open">
        <Parameters>
          <Parameter key="uid" value="default" type="string"/>
          <Parameter key="source" value="assloud://" type="string"/>
          <Parameter key="uri" value="XTC.IntegrationBoard/1" type="string"/>
          <Parameter key="delay" value="0" type="float"/>
        </Parameters>
      </Subject>
    </Subjects>
  </Preload>
</MyConfig>
```

## 消息订阅

* /XTC/IntegrationBoard/ActivatePage

此消息将激活一个标签，打开对应的页面

| 参数   | 类型     | 说明                         |
| ---- | ------ | -------------------------- |
| uid  | string | 准备创建的实例的uid                |
| page | string | 要打开的页面的名称，对应TabButton.name |

* /XTC/IntegrationBoard/DirectOpen

此消息将首先创建一个集成面板，然后刷新内容并显示，最后对齐到网格。

| 参数          | 类型     | 说明                    |
| ----------- | ------ | --------------------- |
| uid         | string | 准备创建的实例的uid           |
| style       | string | 准备创建的实例的样式            |
| source      | string | 内容的源类型，可选项为assloud:// |
| uri         | string | 内容在源中的访问地址            |
| delay       | float  | 延时打开的时间，单位为秒          |
| position\_x | float  | 打开的位置的x坐标             |
| position\_y | float  | 打开的位置的y坐标             |

* /XTC/IntegrationBoard/DirectClose

此消息将关闭并销毁一个集成面板

| 参数    | 类型     | 说明           |
| ----- | ------ | ------------ |
| uid   | string | 准备创建的实例的uid  |
| delay | float  | 延时关闭的时间，单位为秒 |
|       |        |              |

## 依赖插件

oelMVCS

## 更新日志

### 0.9.0

* 新增：

支持视频循环，对应配置为：

```markup
<VideoLoop mode="none" visible="false"/>
```
