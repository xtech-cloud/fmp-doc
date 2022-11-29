---
description: 资源云
---

# Assloud

Assloud为Asset Cloud的复合词，即资源云。

Assloud意在提供一个由标准化、规范化的工作流生成的可用于FMP解决方案的内容聚合平台。

## 功能特性（Features）

TODO

## 架构设计（Architecture Design）

assloud主要由包、内容、资源三个层级组成。它们的结构如下所示：

```
|- bundle-x
   |- content-x
      |- meta.json
      |- icon.png
      |- cover.png
      |- ...
   |- _resources
      |- a.x2i
      |- b.xpd
      |- c.xsa
      |- ... 
```



### 资源（Resources）

资源为一个可执行的内容文件，可能的形态为一个视频、一个文档、一个模型、一个微应用等等。

资源是一个最小的运行单位。

### 内容（Content）

内容通过引用资源的方式，提供多种形态的展示形式。

内容是一个最小的显示单位。

内容具有一个元文件meta.json，包含了一个内容的所有数据信息，结构如下：

```json
{
    "name": "大熊猫",
    "kvS": {
    },
    "alias": "大熊猫",
    "title": "大熊猫",
    "caption": "Ailuropoda melanoleuca",
    "label": "食肉目;熊科",
    "topic": "中国国宝",
    "description": "体型肥硕似熊、丰腴富态，头圆尾短，体色为黑白两色，脸颊圆，有很大的“黑眼圈”。",
    "alias_i18nS": {
    },
    "title_i18nS": {
    },
    "caption_i18nS": {
    },
    "label_i18nS": {
    },
    "topic_i18nS": {
    },
    "description_i18nS": {
    },
    "labelS": [
    ],
    "tagS": [
    ],
    "foreign_bundle_uuid": "b359b77a-fb45-4845-8455-27f57ddaeed8",
    "AttachmentS": [
        {
            "path": "cover.png",
            "hash": "7065ccf10aeed15ac5b0665e1c946b26",
            "Size": 874272,
            "Url": ""
        }
    ],
    "Uuid": "c56217f6-555d-4e11-8b23-db260160c8b7"
}
```

| 字段                    | 类型                  | 说明                  |
| --------------------- | ------------------- | ------------------- |
| name                  | string              | 内容的名称，同时也是存储时使用的路径名 |
| alias                 | string              | 别名，用于生成搜索需要的首字母     |
| title                 | string              | 主标题                 |
| caption               | string              | 副标题                 |
| label                 | string              | 用于显示的标签，以分号分隔       |
| topic                 | string              | 标语                  |
| description           | string              | 描述                  |
| alias\_i18nS          | map\<string,string> | 别名的多国语言字典           |
| title\_i18nS          | map\<string,string> | 主标题的多国语言字典          |
| caption\_i18nS        | map\<string,string> | 副标题的多国语言字典          |
| topic\_i18nS          | map\<string,string> | 标语的多国语言字典           |
| description\_i18nS    | map\<string,string> | 描述的多国语言字典           |
| labelS                | list\<string>       | 用于检索的预设标签的列表        |
| tagS                  | list\<string>       | 用于检索的自定义标签的列表       |
| AttachmentS           | list\<object>       | 附件文件的列表             |
| Uuid                  | string              | 内容的唯一ID             |
| foreign\_bundle\_uuid | string              | 所在的包的唯一ID           |

内容也可以包含多个附件文件，这些包含的附件文件，定义在AttachmentS字段中，存储时位于内容的路径下。



### 包（Bundle）

多个内容和资源组成一个包。

包是一个最小的发布单位。

包具有一个元文件meta.json，包含了一个包的所有数据信息，结构如下：

```json
{
    "name": "XTC.Demo.1",
    "summary": "测试数据1",
    "labelS": [
    ],
    "tagS": [
    ],
    "resourceS": [
    ],
    "summary_i18nS": {
    },
    "foreign_content_uuidS": [
        "9fd295ef-5a0e-4607-b247-04f0fb43be97",
        "4c3970f2-381d-464d-9988-7fb8a5b2fa25",
        "6fa05de9-750f-4450-a8db-e8337e48699b",
        "c56217f6-555d-4e11-8b23-db260160c8b7",
        "bab32059-7a7b-4150-b83e-1b38567375b8",
        "1dfbca4d-3376-4076-ab57-fde7020330f1",
        "b2fbd138-3706-4920-b474-01d8f6c5a5a3"
    ],
    "Uuid": "b359b77a-fb45-4845-8455-27f57ddaeed8"
}
```

| 字段                      | 类型                  | 说明                  |
| ----------------------- | ------------------- | ------------------- |
| name                    | string              | 内容的名称，同时也是存储时使用的路径名 |
| summary                 | string              | 包的简介                |
| summary\_i18nS          | map\<string,string> | 包的简介的多国语言字典         |
| labelS                  | list\<string>       | 用于检索的预设标签的列表        |
| tagS                    | list\<string>       | 用于检索的自定义标签的列表       |
| resourceS               | list\<object>       | 资源文件的列表             |
| Uuid                    | string              | 包的唯一ID              |
| foreign\_content\_uuidS | list\<string>       | 包含的内容的唯一ID的列表       |





###



### &#x20;