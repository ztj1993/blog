# Windows 工作环境部署

## 文档说明
- 文档名称：Windows 工作环境部署
- 文档作者：Ztj
- 作者邮箱：ztj1993#gmail.com
- 创建日期：2019-06-21
- 更新日期：2019-09-24
- 文档状态：定版

## 基本说明
- 下载地址 http://msdn.itellyou.cn/
- 安装 windows 10 enterprise ltsc 2019
- 推荐的计算机名称：windows, pc, job
- 以下命令需要在 PowerShell 管理员模式下执行

## 激活系统
```
slmgr -ipk M7XTQ-FN8P6-TTKYV-9D4CC-J462D
slmgr -skms kms.03k.org
slmgr -ato
slmgr -dlv
```

## 初始配置
```
# 允许执行远程脚本
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Force
```

## Scoop
```
# 配置 Scoop 目录
$env:SCOOP='C:\UserScoopApps'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

# 安装 Scoop
iwr -useb get.scoop.sh | iex

# 安装工具
scoop install sudo
scoop install aria2
scoop install git
scoop install openssh
scoop install curl

# 添加 extras
scoop bucket add extras

# 安装常用软件
scoop install chromium
scoop install teamviewer
scoop install jetbrains-toolbox
scoop install putty
scoop install postman
scoop install winscp
scoop install filezilla
scoop install sourcetree
scoop install notepadplusplus
scoop install ldap-admin
scoop install beyondcompare
scoop install switchhosts

# 安装系统工具
scoop install rufus

# 安装 VC++ 运行库
scoop install vcredist

# 安装 java 环境
scoop bucket add java
scoop install oraclejdk

# 安装 python 环境
scoop install python

# 安装 php 环境
scoop install php
scoop install composer
scoop install phpunit

# 安装 go 环境
scoop install go
scoop install protobuf
```

## Choco
```
# 安装环境
$env:ChocolateyInstall="D:\ChocoApps"
iwr -useb https://chocolatey.org/install.ps1 | iex
```

## 应用配置
```
# 配置 composer 源
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
# 配置 ldap-admin 简体中文
aria2c https://raw.githubusercontent.com/ztj1993/files/master/ldap-admin-chinese-utf8-1.6.llf
```

## 安装 Store
- [下载地址](https://github.com/kkkgo/LTSC-Add-MicrosoftStore)
- 删除 PurchaseApp & Xbox
- 管理员执行 Add-Store.cmd

## 应用商店安装
- 安装 Microsoft To-Do

## 推荐目录结构
```
mkdir Backups
mkdir Codes
mkdir Data
mkdir Documents
mkdir Games
mkdir History
mkdir Shared
mkdir Softwares
mkdir Temps
```

## 常用命令
```
# 添加 VPN 客户端
iex(new-object net.webclient).downloadstring('https://dwz.cn/CxHFkLgw')

# 启用 Hyper-V, Containers
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
Enable-WindowsOptionalFeature -Online -FeatureName Containers

# 设置端口转发
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=7379 connectaddress=127.0.0.1 connectport=6379
# 删除端口转发
netsh interface portproxy del v4tov4 listenport=7379 listenaddress=0.0.0.0
# 查看端口转发
netsh interface portproxy show v4tov4
```

## 软件卸载

### Scoop
```
scoop uninstall scoop
```

### Choco
```
Remove-Item -Recurse -Force "$env:ChocolateyBinRoot" -WhatIf
Remove-Item -Recurse -Force "$env:ChocolateyToolsRoot" -WhatIf
[System.Environment]::SetEnvironmentVariable("ChocolateyBinRoot", $null, 'User')
[System.Environment]::SetEnvironmentVariable("ChocolateyToolsLocation", $null, 'User')
```
