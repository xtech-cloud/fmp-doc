---
description: 网格菜单
---

# XTC\_GridMenu

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
      Background.image: 背景图片
      Grid.colume: 网格布局的列数
      Grid.row: 网格布局的行数
      Cell.name: 单元格的名称
      Cell.columnStart: 单元格的开始列数
      Cell.columnEnd: 单元格的结束列数
      Cell.rowStart: 单元格的开始行数
      Cell.rowEnd: 单元格的结束行数
      Cell.Content.type: 单元格的内容类型，可选值为[RawImage, Button, SlicedImage, ClickArea]
      Cell.Content.ParameterS: 单元格的内容的类型的参数
      Cell.Content.SubjectS: 单元格的内容被激活后发布的主题列表
    -->
  <Styles>
    <Style name="default">
      <Background image="bg.jpg"/>
      <Grid column="96" row="54"/>
      <CellS>
        <Cell name="logo" columnStart="3" columnEnd="63" rowStart="2" rowEnd="4">
          <Content type="RawImage">
            <ParameterS>
              <Parameter key="image" value="logo.png" type="string"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="carousel" columnStart="3" columnEnd="63" rowStart="6" rowEnd="39">
        </Cell>
        <Cell name="carousel-click" columnStart="3" columnEnd="63" rowStart="6" rowEnd="39">
          <Content type="ClickArea">
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="入口1" columnStart="66" columnEnd="74" rowStart="6" rowEnd="21">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-1.png" type="string"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="入口2" columnStart="76" columnEnd="84" rowStart="6" rowEnd="21">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-1.png" type="string"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="入口3" columnStart="86" columnEnd="94" rowStart="6" rowEnd="21">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="入口4" columnStart="66" columnEnd="74" rowStart="24" rowEnd="39">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-1.png" type="string"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="入口5" columnStart="76" columnEnd="84" rowStart="24" rowEnd="39">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-1.png" type="string"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="入口6" columnStart="86" columnEnd="94" rowStart="24" rowEnd="39">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="资源栏" columnStart="3" columnEnd="94" rowStart="42" rowEnd="52">
          <Content type="SlicedImage">
            <ParameterS>
              <Parameter key="image" value="dock-bg.png" type="string"/>
              <Parameter key="border_left" value="64" type="int"/>
              <Parameter key="border_right" value="64" type="int"/>
              <Parameter key="border_top" value="64" type="int"/>
              <Parameter key="border_bottom" value="64" type="int"/>
            </ParameterS>
          </Content>
        </Cell>
        <Cell name="资源1" columnStart="6" columnEnd="13" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="资源2" columnStart="17" columnEnd="24" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="资源3" columnStart="28" columnEnd="35" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="资源4" columnStart="39" columnEnd="46" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="资源5" columnStart="50" columnEnd="57" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="资源6" columnStart="61" columnEnd="68" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="资源7" columnStart="72" columnEnd="79" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
        <Cell name="资源8" columnStart="83" columnEnd="90" rowStart="42" rowEnd="52">
          <Content type="Button">
            <ParameterS>
              <Parameter key="image" value="entry-2.png" type="string"/>
            </ParameterS>
            <SubjectS>
              <Subject message="/XTC/GridMenu/Hide">
                <Parameters>
                  <Parameter key="uid" value="default" type="string"/>
                </Parameters>
              </Subject>
            </SubjectS>
          </Content>
        </Cell>
      </CellS>
      <Debug active="true" lineColor="#FF0000FF" cellColor="#00FF0088" drawLine="true" drawCell="true"/>
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
      <Subject message="/XTC/GridMenu/Open">
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


## 依赖插件


## 更新日志

### 0.6.0

[更新] 升级框架到1.84
[新增] 新增ClickArea内容

### 0.5.1

* 删除：Carousel的相关代码


### 0.5.0

* 删除：Carousel内容
