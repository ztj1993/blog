# Windows 工作环境部署

## 文档说明
- 文档名称：Windows 工作环境部署
- 文档作者：Ztj
- 作者邮箱：ztj1993#gmail.com
- 创建日期：2019-06-21
- 更新日期：2019-10-08
- 文档状态：定版

## 基本说明
- 安装 windows 10 enterprise ltsc 2019
- 推荐的计算机名称：windows, pc, job
- 以下命令需要在 PowerShell 管理员模式下执行

## 下载安装系统
- 下载地址 http://msdn.itellyou.cn/
- Windows 10 Enterprise LTSC 2019 (x64)
- Office Professional Plus 2016 (x86 and x64)
- Visio Professional 2016 (x86 and x64)
- Project Professional 2016 (x86 and x64)

## 激活系统
```
$sys32="${env:windir}\system32"
$lic16="${env:ProgramFiles(x86)}\Microsoft Office\root\Licenses16"
$off16="${env:ProgramFiles(x86)}\Microsoft Office\Office16"

# 激活系统
cscript //nologo "${sys32}/slmgr.vbs" /ipk M7XTQ-FN8P6-TTKYV-9D4CC-J462D
cscript //nologo "${sys32}/slmgr.vbs" /skms kms.03k.org
cscript //nologo "${sys32}/slmgr.vbs" /ato
cscript //nologo "${sys32}/slmgr.vbs" /dlv

# 激活 Office 2016
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\ProPlusVL_KMS_Client-ppd.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\ProPlusVL_KMS_Client-ul.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\ProPlusVL_KMS_Client-ul-oob.xrm-ms"

cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\ProjectProVL_KMS_Client-ppd.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\ProjectProVL_KMS_Client-ul-oob.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\ProjectProVL_KMS_Client-ul.xrm-ms"

cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\VisioProVL_KMS_Client-ppd.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\VisioProVL_KMS_Client-ul-oob.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\VisioProVL_KMS_Client-ul.xrm-ms"

cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\client-issuance-bridge-office.xrm-ms
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\client-issuance-root.xrm-ms
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\client-issuance-root-bridge-test.xrm-ms
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\client-issuance-stil.xrm-ms
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\client-issuance-ul.xrm-ms
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\client-issuance-ul-oob.xrm-ms
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}\pkeyconfig-office.xrm-ms

cscript //nologo "${off16}\OSPP.VBS" /inpkey:XQNVK-8JYDB-WJ9W3-YJ8YR-WFG99
cscript //nologo "${off16}\OSPP.VBS" /inpkey:PD3PC-RHNGV-FXJ29-8JK7D-RJRJK
cscript //nologo "${off16}\OSPP.VBS" /inpkey:YG9NW-3K39V-2T3HJ-93F3Q-G83KT

cscript //nologo "${off16}\OSPP.VBS" /act
```

## 初始配置
```
# 允许执行远程脚本
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Force
```

## Scoop (用于安装便携软件)
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
start powershell "scoop install chromium; pause"
start powershell "scoop install jetbrains-toolbox; pause"
start powershell "scoop install putty; pause"
start powershell "scoop install postman; pause"
start powershell "scoop install winscp; pause"
start powershell "scoop install filezilla; pause"
start powershell "scoop install sourcetree; pause"
start powershell "scoop install notepadplusplus; pause"
start powershell "scoop install ldap-admin; pause"
start powershell "scoop install beyondcompare; pause"
start powershell "scoop install switchhosts; pause"

# 安装系统工具
start powershell "scoop install rufus; pause"

# 安装 VC++ 运行库
start powershell "scoop install vcredist; pause"

# 安装 python 环境
start powershell "scoop install python; pause"

# 安装 php 环境
start powershell "scoop install php; pause"
start powershell "scoop install composer; pause"
start powershell "scoop install phpunit; pause"

# 安装 go 环境
start powershell "scoop install go; pause"
start powershell "scoop install protobuf; pause"
```

## Choco (用于安装系统软件)
```
# 安装环境
$env:ChocolateyInstall="C:\ChocoApps"
iwr -useb https://chocolatey.org/install.ps1 | iex

# 安装远程控制
start powershell "choco install -y teamviewer; pause"

# 安装 VirtualBox(不兼容 Hyper-V)
start powershell "choco install -y virtualbox; pause"

# 安装 VMware Workstation(不兼容 Hyper-V)
start powershell "choco install -y vmwareworkstation; pause"

# 安装 Docker Toolbox
start powershell "choco install -y docker-toolbox; pause"

# 安装 JDK8
start powershell "choco install -y jdk8; pause"
```

## 其他软件
```
scoop bucket add ztj1993 https://github.com/ztj1993/scoop.git
scoop install BaiduPCS-Go
scoop install PicPick
scoop install Microsoft-To-Do
```

## 应用配置
```
# 配置 composer 源
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# 配置 ldap-admin 简体中文
aria2c https://raw.githubusercontent.com/ztj1993/files/master/ldap-admin-chinese-utf8-1.6.llf

# Notepad++ 简体中文
Settings -> Preferences... -> General -> Localization -> 中文简体
# Notepad++ Tab 转 空格
设置 -> 首选项... -> 语言 -> 制表符设置 -> 替换为空格(勾选)
```

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
mkdir Virtual
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
