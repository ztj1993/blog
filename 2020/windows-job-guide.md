# Windows 公司工作环境指南

## 前言
阅读本文前，可以先阅读：
[Windows 工作环境部署](../2019/windows-work-environment.md)

昨天，我上传了
[scoop-index](https://github.com/ztj1993/scoop-index)
项目，完成了工作环境的固定，可以实现 
运维，Docker，前端，Android，Python，PHP，Go
等常见开发环境的构建。

我在以前写的文章中提到，公司应当准备两种环境供员工使用，分别为：
- 分散型团队方案：scoop
- 公司集中化办公：KVM

[scoop-index](https://github.com/ztj1993/scoop-index)
项目就是为分散型团队构建的解决方案。

## 主要构建
- scoop 官方库并关闭了 buckets 更新
- 嵌入了 main, extras, java, jetbrains, php 等清单库

由于关闭了 buckets 更新，因此可以保证每个成员安装的环境版本为一致的。
同时每个成员已经下的软件 cache 可以共用。

## 软件中文包解决
我使用了多种中文包的尝试，包括 fork jetbrains 清单库添加中文包，
但这种解决方案会有更新等问题，只应用了三个月后放弃。

现在，我随着
[scoop-index](https://github.com/ztj1993/scoop-index)
推出了新的
[scoop-chinese](https://github.com/ztj1993/scoop-chinese)
解决方案，这个解决方案虽然是过度型产品，但要比以前的好用的多。

未来抽出时间，也会推出新的解决方案，以彻底解决中文汉化问题。

## 结尾
此工作环境，主要解决了小型团队开发环境一致性问题，欢迎交流。
