---
description: '守护程序 #部署指南'
---

# DaemonApp

## WSL

使用fmp-cli构建，将XTC.Repository.zip拷贝到fmp-daemon/apps目录下

```
|- fmp-daemon
  |- apps
    |- XTC.Repository
      |- appsettings.json
      |- *.dll
      |- ...
  |- cers
    |- xtc.crt
    |- xtc.key
```

修改XTC.Repository/application.json的端口为28000和29000(ssl)

重启fmp-daemon容器


