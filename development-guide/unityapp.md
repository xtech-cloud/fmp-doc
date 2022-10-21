---
description: 'Unity应用程序 #开发指南'
---

# UnityApp

## 环境配置

### 配置虚拟环境

在link-vendor.bat的同级目录创建vendor文件夹，完成后运行link-vendor.bat。 运行一次程序，完成相关默认配置文件的创建。

### 配置升级

按需求修改vendor/Upgrade.xml文件。一个参考的例子如下

```xml
<?xml version="1.0"?>
<Schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Body>
        <Update strategy="auto">
            <FMP environment="develop" repository="http://localhost:9000/fmp.repository">
                <References>
                    <Reference org="XTC" module="Startkit" version="1.0.0"/>
                </References>
                <Plugins>
                    <Plugin name="EasyTouchPlugin" verison="5.0.17" />
                </Plugins>
            </FMP>
        </Update>
    </Body>
    <Header>
        <Option attribute="Update.strategy" values="升级策略，可选值为：skip, auto, manual" />
    </Header>
</Schema>
```

如果使用本地磁盘的仓库，可将repository的地址修改为本机的文件夹路径。例如 `D:/MyRepository`

### 配置引导

按需求修改vendor/Bootloader.xml文件。一个参考的例子如下

```xml
<Bootloader>
    <Steps>
        <Step length="1" tip="加载演示模块" module="XTC.FMP.MOD.Startkit.LIB.Unity"/>
    </Steps>
</Bootloader>
```

## 构建配置

### 添加衍生应用

1. 进入deploy文件夹
2. 复制branch文件夹为.branch
3. 在.branch中添加新的应用文件名，修改图标文件和license的key和secret。
4. 在.branch/deploy.json中添加新的衍生应用应用。

### 构建

先确保当前的git提交具有有效的tag

进入deploy目录,运行以下命令

```bash
python deploy.py
```

在deploy/\_output目录中得到打包的程序
