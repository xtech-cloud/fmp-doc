---
description: 视觉布局
---

# XTC\_VisionLayout

## 术语约定

* 布局（Layout）

TODO

* 过渡（Transition）

TODO

* 主题（Theme）

TODO

## 功能特性

* 版式布局

TODO

* 进入效果

TODO

* 退出效果

TODO

* 标题定制

TODO

* 简介定制

TODO

* 控制面板

TODO



## 配置说明

配置的详细说明在模块包中的.xml文件中有详细标注，这里只列举一些常用功能的配置方法。

### 配置主题模板

#### 卷轴布局（Scroll）

在catalog中的kvS中，添加Scroll\_Image字段，值为卷轴的背景图，图片地址位于包中（bundle）。

```json
{
    ...
    "kvS": {
        "LayerPattern": "Scroll",
        "TitleImage": "",
        "ProfileImage": "",
        "Scroll_Image": "b359b77a-fb45-4845-8455-27f57ddaeed8/scroll.jpg"
    }
}
```

注意LayerPattern字段需要匹配到xml配置文件中的LayerPattern。

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

以上两个值，分别代表了热点在大图中的x和y坐标，卷轴背景图的中心点为（0，0），左和下为负，右和上为正。

所有的内容（content），在卷轴布局中，均显示为一个热点。

### 配置标题图

TODO

### 配置简介图

TODO



## 消息订阅

* /XTC/VisionLayout/ToolBar/Popup

此消息将打开工具栏

| 参数  | 类型     | 说明     |
| --- | ------ | ------ |
| uid | string | 实例的uid |

## 依赖插件&#x20;

oelMVCS

