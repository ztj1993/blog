# Ubuntu 工作环境部署

## Ubuntu
- 文档名称：Ubuntu 工作环境部署
- 文档作者：Ztj
- 作者邮箱：ztj1993#gmail.com
- 创建日期：2019-09-30
- 更新日期：2019-10-29
- 文档状态：定版

## 基本说明
- 安装 Ubuntu Desktop 18.04
- 推荐的计算机名称：my-ubuntu-job

## 基本配置
```
# 替换源
wget https://raw.githubusercontent.com/ztj1993/shell/master/apt-aliyun-mirror.sh
chmod +x ./apt-aliyun-mirror.sh && sudo ./apt-aliyun-mirror.sh && rm -rf ./apt-aliyun-mirror.sh

# 更新系统
DEBIAN_FRONTEND=noninteractive sudo apt-get -y upgrade

# 免密码
echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$(whoami)

# 关闭盖子不休眠
sudo sed -i "s/^#HandleLidSwitch=suspend/HandleLidSwitch=ignore/" /etc/systemd/logind.conf

# 基础软件
sudo apt-get install -y curl wget git vim htop terminator

# l2tp vpn
sudo apt-get install -y network-manager-l2tp-gnome
sudo service xl2tpd stop
sudo update-rc.d xl2tpd disable
```

## 远程控制
```
wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb
sudo dpkg -i teamviewer_amd64.deb
sudo apt-get -f install
```
