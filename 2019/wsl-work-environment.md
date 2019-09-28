# Windows for linux 工作环境部署

## 文档说明
- 文档名称：Windows Subsystem for Linux 工作环境部署
- 文档作者：Ztj
- 作者邮箱：ztj1993#gmail.com
- 创建日期：2019-06-18
- 更新日期：2019-09-28
- 文档状态：定版

## 基础说明
- 使用 Ubuntu 18 系统
- 使用 WSL 1 (注意)
- 以下命令需要在 PowerShell 管理员模式下执行

## 启用 Windows-Subsystem-Linux
```
# 启用 Windows-Subsystem-Linux
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

## 下载 Ubuntu 18
```
aria2c https://aka.ms/wsl-ubuntu-1804 --out=Ubuntu1804.appx

# 其他下方式
# Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1804 -OutFile Ubuntu1804.appx -UseBasicParsing
```

## 安装 Ubuntu 18
```
# 自动安装
Add-AppxPackage .\Ubuntu1804.appx

# 手动安装
# Expand-Archive .\Ubuntu1804.appx C:\Ubuntu1804
```

## 第一次启动
```
# 管理员模式启动 Ubuntu 18.04
# 设置用户名和密码
```

## 配置 Ubuntu 18
```
# 更新系统
wget https://raw.githubusercontent.com/ztj1993/shell/master/apt-aliyun-mirror.sh
chmod +x apt-aliyun-mirror.sh
sudo ./apt-aliyun-mirror.sh

# Ubuntu 初始化
wget https://raw.githubusercontent.com/ztj1993/shell/master/wsl-ubuntu-init.sh
chmod +x wsl-ubuntu-init.sh
sudo ./wsl-ubuntu-init.sh

# 允许 root 登录
wget https://raw.githubusercontent.com/ztj1993/shell/master/ssh-allow-root.sh
chmod +x ssh-allow-root.sh
sudo ./ssh-allow-root.sh

# 本地 ssh 代理(ssh to socks to http)
wget https://raw.githubusercontent.com/ztj1993/shell/master/ssh-proxy.sh
chmod +x ssh-proxy.sh
sudo ./ssh-proxy.sh

# Web 开发环境(nginx apache mysql php redis mongodb)
wget https://raw.githubusercontent.com/ztj1993/shell/master/apt-web-dev.sh
chmod +x apt-web-dev.sh
sudo ./apt-web-dev.sh

# Python 开发环境
wget https://raw.githubusercontent.com/ztj1993/shell/master/apt-python.sh
chmod +x apt-python.sh
sudo ./apt-python.sh
```
