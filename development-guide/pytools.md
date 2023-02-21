---
description: 'python工具箱 #开发指南'
---

# PyTools

python脚本编写的工具箱。

## vendor_meta

虚拟环境（Vendor）的Meta文件辅助工具。

| 参数 | 说明 |
| --- | --- |
| -x | 解开指定的meta.json为多个单独的配置文件 |
| -c | 将指定的文件夹中的多个独立的配置文件合并为一个meta.json |
| -y | 当输出路径存在时自动删除 |


用法：

* 将vendor的meta.json文件拆分为解码后的多个单独的配置文件。

用法：

```cmd
cd fmp-pytools
python vendor_meta -x {path_of_meta.json}
```

输出目录位于和meta.json同级目录的.meta文件夹，此文件夹存在时操作会退出，可使用-y参数自动删除.meta文件夹

* 将多个单独的配置文件合并为一个编码后的meta.json。

用法：

```cmd
cd fmp-pytools
python vendor_meta -c {path_of_.meta}
```

输出文件位于和.meta文件夹同级目录的meta.json，此文件存在时操作会退出，可使用-y参数自动删除meta.json

## bundle_meta

构建资源包的meta.json的工具。

| 参数 | 说明 |
| --- | --- |
| -d | 资源包的文件夹的绝对路径 |

用法：

```cmd
cd fmp-pytools
python bundle_meta -d {path_of_bundle}
```

输出文件位于资源包目录的meta.json，如果此文件存在，则会读取name、uuid、summary、labelS、tagS、summary_i18nS等属性，合并到输出文件中。如果没有存在的meta.json，则输出的文件的以上字段为空。

