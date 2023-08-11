---
description: 翼形菜单
---

# XTC\_WingMenu

## 术语约定

* 门户（Portal）

翼形菜单的第一级目录是以竖直的条图呈现，这一节目录称之为门户。

* 导览式页面（Navigation）

门户展开后的面板中，显示文件夹结构的二级菜单，当二级菜单激活后，再显示此二级菜单包含的内容列表。

* 过滤式页面（Filter）

门户展开后的面板中，显示门户的所有内容列表，使用过滤菜单显示内容的子集。

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
      MiddlePanel: 中间展开形状的菜单的面板
      MiddlePanel.color: 面板颜色
      MiddlePanel.decal: 面板的贴花的图片
      EdgePanel: 两边展开形状的菜单的面板
      MiddlePanel.color: 面板颜色
      BundleCell: 资源包单元
      ContentCell: 资源内容单元
      EntryCell: 资源可执行入口
      Filter: 过滤栏
      Navigation.fontColor: 导览栏
      ContentDetail.Title: 内容详情的主标题
      ContentDetail.Label: 内容详情的标签
      ContentDetail.Caption: 内容详情的副标签
      ContentDetail.Topic: 内容详情的标语
      ContentDetail.Description: 内容详情的简介
      Entry.icon: 资源入口的图片
      Entry.text: 资源入口的文字
      Entry.kvKey: 资源入口的在meta中kvS的键，仅当对应的键在kvS中有值时，资源入口才会显示
      Entry.SubjectS: 资源入口被点击后发布的主题列表
    -->
  <Styles>
    <Style name="default">
      <MiddlePanel color="#FFFFFF77" decal="middlepanel-decal.png"/>
      <EdgePanel color="#FFFFFF77"/>
      <BundleCell fontSize="16" fontColor="#FFFFFFFF"/>
      <ContentCell fontSize="16" fontColor="#FFFFFFFF"/>
      <EntryCell fontSize="16" fontColor="#FFFFFFFF"/>
      <Filter fontSize="18" fontColor="#FFFFFFFF"/>
      <Navigation fontSize="18" fontColor="#FFFFFFFF"/>
      <ContentDetail>
        <Title fontSize="32" fontColor="#FFFFFFFF"/>
        <Label fontSize="18" fontColor="#FFC31EFF"/>
        <Caption fontSize="18" fontColor="#39EBFFFF"/>
        <Topic fontSize="24" fontColor="#FFFFFFFF"/>
        <Description fontSize="18" fontColor="#FFFFFFFF"/>
      </ContentDetail>
      <EntryS>
        <Entry icon="entry-image-64.png" text="图片" kvKey="">
          <SubjectS>
            <Subject message="/XTC/WingMenu/Open">
              <Parameters>
                <Parameter key="uid" value="default" type="string"/>
                <Parameter key="source" value="" type="string"/>
                <Parameter key="uri" value="" type="string"/>
                <Parameter key="delay" value="0" type="float"/>
              </Parameters>
            </Subject>
          </SubjectS>
        </Entry>
        <Entry icon="entry-video-64.png" text="视频" kvKey="Res.Video">
          <SubjectS>
            <Subject message="/XTC/VideoSee/Open">
              <Parameters>
                <Parameter key="uid" value="default" type="string"/>
                <Parameter key="source" value="assloud://" type="string"/>
                <Parameter key="uri" value="{{resource_uri}}" type="string"/>
                <Parameter key="delay" value="1" type="float"/>
              </Parameters>
            </Subject>
          </SubjectS>
        </Entry>
        <Entry icon="entry-app-64.png" text="微应用" kvKey="Res.Application">
          <SubjectS>
            <Subject message="/XTC/LuaEnv/Open">
              <Parameters>
                <Parameter key="uid" value="default" type="string"/>
                <Parameter key="source" value="assloud://" type="string"/>
                <Parameter key="uri" value="{{resource_uri}}" type="string"/>
                <Parameter key="delay" value="1" type="float"/>
              </Parameters>
            </Subject>
          </SubjectS>
        </Entry>
        <Entry icon="entry-model-64.png" text="模型" kvKey="">
          <SubjectS>
            <Subject message="/XTC/WingMenu/Open">
              <Parameters>
                <Parameter key="uid" value="default" type="string"/>
                <Parameter key="source" value="" type="string"/>
                <Parameter key="uri" value="" type="string"/>
                <Parameter key="delay" value="0" type="float"/>
              </Parameters>
            </Subject>
          </SubjectS>
        </Entry>
      </EntryS>
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
      <Subject message="/XTC/WingMenu/Open">
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

### 配置门户

菜单结构需要在catalog.json中进行配置。

在catalog.json中的sectionS数组中，添加以下内容

```json
{
  "name": "测试1",
  "path": "/Test1",
  "instanceS": [
    "default"
  ],
  "contentS": [
  ],
  "kvS": {
    "shape": "edge",
    "banner": "banner-1.png",
    "pagination":"navigation",
    "cover": "cover-1.png",
  }
}
```

name指定此门户的显示名称

path指定此门户的路径

kvS中的shape指定了该门户的形状，可选值为(middle, edge)，middle形状的门户打开时从中间展开，edge形状的门户打开时从两边展开。

kvS中的banner指定了该门户的条形图，该路径相对于themes目录中的模块名目录。

kvS中的pagination指定了该门户的页呈现形式，可选值为(navigation, filter)。navigation形式的页面，会打开二级菜单后打开内容列表，并在内容列表下方显示返回到二级菜单的按钮。而filter形式的页面，会显示所有的内容列表，内容列表下方的过滤栏用于过滤内容子集，

kvS.cover字段可配置门户展开时显示的封面图(600x600)，该路径相对于themes目录中的模块名目录，仅edge形状的门户有效

### 配置导览式页面

在catalog.json中的sectionS数组中，添加以下内容

```json
{
  "name": "1",
  "path": "/Test1/1",
  "instanceS": [
    "default"
  ],
  "contentS": [
      "2f0b906f-1861-4c49-a687-1784a14953c5/+",
      "b359b77a-fb45-4845-8455-27f57ddaeed8/1dfbca4d-3376-4076-ab57-fde7020330f1"
  ],
  "kvS": {
    "icon.source": "theme://",
    "icon.uri": "icon-1.png",
    "cover": "cover-1-1.png"
  }
}
```

导览式页面，一个section定义了一个导览菜单。

name指定此菜单的显示名称

path指定此菜单的路径，注意，路径中需要包含对应的门户的路径，例如`/Test1/1`表示在门户/Test1中的导览菜单1。

contentS指定菜单包含的内容列表

kvS中的icon.source指定此菜单的图片的来源，可选值为(assloud://, theme://)，assould://表示图片位于assets文件夹下，theme://表示图片位于themes文件夹下。

kvS中的icon.uri指定此菜单的图片在来源中的相对路径

kvS.cover字段可配置菜单打开时显示的封面图(600x600)，该路径相对于themes目录中的模块名目录，仅配置为edge和navigation的门户有效

导览式页面需要确保对应的门户的ksS.pagination的值是navigation

### 配置过滤式页面

在catalog.json中的sectionS数组中，添加以下内容

```json
{
      "name": "4",
      "path": "/Test2/4",
      "instanceS": [
        "default"
      ],
      "contentS": [
          "b359b77a-fb45-4845-8455-27f57ddaeed8/+"
      ],
      "kvS": {
      }
    },
```

导览式页面，一个section定义了一个过滤菜单。
name指定此菜单的显示名称
path指定此菜单的路径，注意，路径中需要包含对应的门户的路径，例如`/Test2/4`表示在门户/Test2中的过滤菜单4。
contentS指定菜单包含的内容列表

过滤式页面需要确保对应的门户的ksS.pagination的值是filter

## 消息订阅


## 依赖插件


## 更新日志

### 0.2.0 (2023/8/11)

- 支持配置右面版封面
