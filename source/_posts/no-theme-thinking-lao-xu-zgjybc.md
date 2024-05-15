---
title: 无主题 | 思码老徐
date: '2023-08-01 15:25:22'
updated: '2024-05-15 12:02:53'
permalink: /post/no-theme-thinking-lao-xu-zgjybc.html
comments: true
toc: true
---

# 无主题 | 思码老徐

---

* [https://www.xuchengen.cn/category/wuzhuti](https://www.xuchengen.cn/category/wuzhuti)
* Scoop 是一个 Win­dows 包管理工具，类似于 De­bian 的 apt、ma­cOS 的 homebrew。它由开源社区驱动，体验可能是是目前所有 Win­dows 包管理工具中最好的。对开发者来说，包管理器能非常方便的部署开发环境，比如 Python 、Node.js 。而对于像博主这样的普通的计算机使用者来说，可以方便的安装一些常用软件，尤其是开源软件，免去了手动去官网下载的繁琐步骤，而且后续对软件进行升级只需要输入一行命令，非常便捷。
* 2023-08-01 15:25:16

---

## 前言

Scoop 是一个 Win­dows 包管理工具，类似于 De­bian 的 apt、ma­cOS 的 homebrew。它由开源社区驱动，体验可能是是目前所有 Win­dows 包管理工具中最好的。对开发者来说，包管理器能非常方便的部署开发环境，比如 Python 、Node.js 。而对于像博主这样的普通的计算机使用者来说，可以方便的安装一些常用软件，尤其是开源软件，免去了手动去官网下载的繁琐步骤，而且后续对软件进行升级只需要输入一行命令，非常便捷。

## 环境要求

* Windows 7 SP1 + / Windows Server 2008+
* PowerShell 5（或更高版本，包括 PowerShell Core）和 .NET Framework 4.5（或更高版本）
* Windows 用户名为英文（Windows 用户环境变量中路径值不支持中文字符）
* 正常、快速的访问 GitHub 并下载资源

## 安装 Scoop

Scoop 默认使用普通用户权限，其本体和安装的软件默认会放在 %USERPROFILE%\scoop(即 C:\Users\用户名\scoop)，使用管理员权限进行全局安装 (-g) 的软件在 C:\ProgramData\scoop。如果有自定安装路径的需求，那么要提前设置好环境变量，否则后续再改不是一件容易的事情。

* 打开 PowerShell
* 设置用户安装路径

```
$env:SCOOP='C:\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')
```

* 设置全局安装路径（需要管理员权限）

```
$env:SCOOP_GLOBAL='D:\Scoop_Global'
[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')
```

* 设置允许 PowerShell 执行本地脚本

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

* 安装 Scoop

```
iwr -useb get.scoop.sh | iex
```

* 没安装过 Git 则需要安装。

```
scoop install git
```

## 基础使用

最基础的使用方法和其它包管理器类似，这里就不做赘述了，直接上命令列表：

* ​`scoop search <app>`​ – 搜索软件
* ​`scoop install <app>`​ – 安装软件
* ​`scoop info <app>`​ – 查看软件详细信息
* ​`scoop list`​ – 查看已安装软件
* ​`scoop uninstall <app>`​ – 卸载软件，`-p`​删除配置文件。
* ​`scoop update`​ – 更新 scoop 本体和软件列表
* ​`scoop update <app>`​ – 更新指定软件
* ​`scoop update *`​ – 更新所有已安装的软件
* ​`scoop checkup`​ – 检查 scoop 的问题并给出解决问题的建议
* ​`scoop help`​ – 查看命令列表
* ​`scoop help <command>`​ – 查看命令帮助说明

## 进阶使用

### 添加 bucket

所有的包管理器都会有相应的软件仓库 ，而 bucket 就是 Scoop 中的软件仓库。细心的你可能会发现 `scoop`​ 翻译为中文是 “舀”，而 `bucket`​ 是 “水桶”，所以安装软件可以理解为从水桶里舀水，似乎很形象的说。

Scoop 默认软件仓库（main bucket）软件数量是有限的，但是可以进行额外的添加。通过 `scoop bucket known`​ 命令可以查看官方认可的 bucket：

```
$ scoop bucket known
main
extras
versions
nightlies
nirsoft
php
nerd-fonts
nonportable
java
games
jetbrains
```

以上官方认可的 bucket 可以通过下面这个命令直接添加：

```
scoop bucket add <bucketname>
```

extras 涵盖了大部分因为种种原因不能被收录进主仓库的常用软件，这个是强推荐添加的。

```
scoop bucket add extras
```

比如博主经常会使用到的写盘工具 Ru­fus 就在 `extras`​ 这个仓库中。

```
scoop install rufus
```

nerd-fonts 包含了美化终端时会用到的 Pow­er­line 字体

```
scoop bucket add nerd-fonts
```

当添加 `nerd-fonts`​ 仓库后可以通过以下命令搜索到所有的字体：

```
scoop search "-NF"
```

安装字体需要使用管理员权限：

```
sudo scoop install FiraCode-NF
```

#### 第三方 bucket

添加第三方 bucket

```
scoop bucket add <bucketname> https://github.com/xxx/xxx
```

从第三方 bucket 中安装软件

```
scoop install <bucketname>/<app>
```

### 清理安装包缓存

Scoop 会保留下载的安装包，对于卸载后又想再安装的情况，不需要重复下载。但长期累积会占用大量的磁盘空间，如果用不到就成了垃圾。这时可以使用 `scoop cache`​ 命令来清理。

* ​`scoop cache show`​ – 显示安装包缓存
* ​`scoop cache rm <app>`​ – 删除指定应用的安装包缓存
* ​`scoop cache rm *`​ – 删除所有的安装包缓存

如果你不希望安装和更新软件时保留安装包缓存，可以加上 `-k`​ 或 `--no-cache`​ 选项来禁用缓存：

* ​`scoop install -k <app>`​
* ​`scoop update -k *`​

### 删除旧版本软件

当软件被更新后 Scoop 还会保留软件的旧版本，更新软件后可以通过 `scoop cleanup`​ 命令进行删除。

* ​`scoop cleanup <app>`​ – 删除指定软件的旧版本
* ​`scoop cleanup *`​ – 删除所有软件的旧版本

与安装软件一样，删除旧版本软件的同时也可以清理安装包缓存，同样是加上 `-k`​ 选项。

* ​`scoop cleanup -k <app>`​ – 删除指定软件的旧版本并清除安装包缓存
* ​`scoop cleanup -k *`​ – 删除所有软件的旧版本并清除安装包缓存

### 全局安装

全局安装就是给系统中的所有用户都安装，且环境变量是系统变量，对于需要设置系统变量的一些软件就需要全局安装，比如 Node.js、Python ，否则某些情况会出现无法找到命令的问题。

使用 `scoop install <app>`​ 命令加上 `-g`​ 或 `--global`​ 选项可对软件进行全局安装，全局安装需要管理员权限，所以需要提前以管理员权限运行的 Pow­er­Shell 。更简单的方式是先安装 `sudo`​，然后用 `sudo`​ 命令来提权执行：

```
scoop install sudo
sudo scoop install -g <app>
```

> 达成在 Win­dows 上使用`sudo`​的成就

使用 `scoop list`​ 命令查看已装软件时，全局安装的软件末尾会有 `*global*`​ 标志。

```
➜ scoop list
Installed apps:

  7zip 19.00
  adb 30.0.0
  aria2 1.35.0-1
  busybox 3466-g53c09d0e1
  CascadiaCode-NF 2.1.0 [nerd-fonts]
  colortool 1904.29002
  dark 3.11.2 *global*
  ffmpeg 4.2.3
  figlet 1.0-go
  FiraCode-NF 2.1.0 [nerd-fonts]
  git 2.26.2.windows.1 *global*
  innounp 0.49
  iperf3 3.1.3
  lessmsi 1.6.91 *global*
  lxrunoffline 3.4.1 [extras]
  nano 4.9-4
  neofetch 7.0.0
  nodejs-lts 12.17.0 *global*
  python 3.8.3 *global*
  rclone 1.52.0
  rufus 3.10 [extras]
  screentogif 2.24.2 [extras]
  sudo 0.2020.01.26
```

此外对于全局软件的更新和卸载等其它操作，都需要加上 `-g`​ 选项：

* ​`sudo scoop update -g *`​ – 更新所有软件（且包含全局软件）
* ​`sudo scoop uninstall -g <app>`​ – 卸载全局软件
* ​`sudo scoop uninstall -gp <app>`​ – 卸载全局软件（并删除配置文件）
* ​`sudo scoop cleanup -g *`​ – 删除所有全局软件的旧版本
* ​`sudo scoop cleanup -gk *`​ – 删除所有全局软件的旧版本（并清除安装包包缓存）

### 代理设置

Scoop 默认使用的是系统代理，如果你想手动指定代理，可以输入下面的命令。需要注意的是只支持 http 协议。

```
scoop config proxy localhost:1080
```

> 设置完可以通过`scoop config proxy`​查看。

如果你想取消代理，那么输入下面的命令，这将会恢复使用系统代理。

```
scoop config rm proxy
```

### 开启多线程下载

使用 Scoop 安装 Aria2 后，Scoop 会自动调用 Aria2 进行多线程加速下载。

```
scoop install aria2
```

使用 `scoop config`​ 命令可以对 Aria2 进行设置，比如 `scoop config aria2-enabled false`​ 可以禁止调用 Aria2 下载。以下是与 Aria2 有关的设置选项：

* ​`aria2-enabled`​: 开启 Aria2 下载，默认`true`​
* ​`aria2-retry-wait`​: 重试等待秒数，默认`2`​
* ​`aria2-split`​: 单任务最大连接数，默认`5`​
* ​`aria2-max-connection-per-server`​: 单服务器最大连接数，默认`5`​ ，最大`16`​
* ​`aria2-min-split-size`​: 最小文件分片大小，默认`5M`​

博主在这里推荐以下优化设置，单任务最大连接数设置为 `32`​，单服务器最大连接数设置为 `16`​，最小文件分片大小设置为 `1M`​

```
scoop config aria2-split 32
scoop config aria2-max-connection-per-server 16
scoop config aria2-min-split-size 1M
```

## 常用命令总结

看到这里一定有很多小伙伴已经懵逼了，最后总结一波 Scoop 在日常使用中的常用命令：

```
# 更新 scoop 及软件包列表
scoop update

## 安装软件 ##
# 非全局安装（并禁止安装包缓存）
scoop install -k <app>
# 全局安装（并禁止安装包缓存）
sudo scoop install -gk <app>

## 卸载软件 ##
# 卸载非全局软件（并删除配置文件）
scoop uninstall -p <app>
# 卸载全局软件（并删除配置文件）
sudo scoop uninstall -gp <app>

## 更新软件 ##
# 更新所有非全局软件（并禁止安装包缓存）
scoop update -k *
# 更新所有软件（并禁止安装包缓存）
sudo scoop update -gk *

## 垃圾清理 ##
# 删除所有旧版本非全局软件（并删除软件包缓存）
scoop cleanup -k *
# 删除所有旧版本软件（并删除软件包缓存）
sudo scoop cleanup -gk *
# 清除软件包缓存
scoop cache rm *
```

## 尾巴

Scoop 的使用方法和功能远不止上面提及的这些，但作为一个普通用户也只会用到一些基本的命令和功能。纵观全网也很少有人把基础功能都说明白，这也是在 2022 年谷歌随便一搜一大把 Scoop 教程和笔记文章的情况下博主依然写这样一篇更加全面教程的原因。希望这篇教程对你有所帮助。

> Trojan是啥？Trojan就是Trojan呀，用了都说好，大家都在用，用了都说爽。不废话上链接。

```
https://raw.githubusercontent.com/Xuchengen/static/master/gwf/trojan_install.sh
```

该脚本为一键部署脚本，自动安装Nginx、Trojan、Let’s证书、伪装站点。同时附赠BBR以及服务器参数优化脚本。

> 我们都知道Jetbrains全家桶作为生产力开发工具的重要性，用好了955用不好那就活该996。这篇文章主要记录一下Jetbrains系列开发工具在各平台用户路径下的配置位置，然后针对性的调优，比如破解。

## Windows平台

```
Syntax
%APPDATA%\JetBrains\&lt;product&gt;&lt;version&gt;

Example
C:\Users\JohnS\AppData\Roaming\JetBrains\IntelliJIdea2022.1
```

## Linux平台

```
Syntax
~/.config/JetBrains/&lt;product&gt;&lt;version&gt;

Example
~/.config/JetBrains/IntelliJIdea2022.1
```

## MacOS

```
Syntax
~/Library/Application Support/JetBrains/&lt;product&gt;&lt;version&gt;

Example
~/Library/Application Support/JetBrains/IntelliJIdea2022.1
```

## Jetbrains官方原话

> Do not change JVM options in the default file, because it is replaced when IntelliJ IDEA is updated. Moreover, in case of macOS, editing this file violates the application signature.
>
> 不要更改默认文件中的 JVM 选项，因为它会在 IntelliJ IDEA 更新时被替换。此外，对于 macOS，编辑此文件会违反应用程序签名。

> Trojan是个好东西！！！最近使用我北京机房的服务器资源白嫖了一台甲骨文云服务器，之前用家宽一直申请不成功然后在自己的服务器上搭建一个Trojan立马就申请成功（引起极度舒适），全仰仗Trojan提供的网络服务。博主废话就不多说直接贴代码。

## 一键脚本

```
#ContOS Yum 安装 
wget yum -y install wget

#Debian Ubuntu 安装 
wget apt-get install wget
```

```
wget -N --no-check-certificate -q -O trojan_install.sh "https://raw.githubusercontent.com/V2RaySSR/Trojan/master/trojan_install.sh" && chmod +x trojan_install.sh && bash trojan_install.sh
```

## 三部曲脚本

```
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan1.sh" && chmod +x trojan1.sh && ./trojan1.sh
```

```
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan2.sh" && chmod +x trojan2.sh && ./trojan2.sh
```

```
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan3.sh" && chmod +x trojan3.sh && ./trojan3.sh
```

至于证书的问题我觉得可以考虑自签然后客户端忽略证书验证。

自从Mac book pro坏了之后我又重新windows阵营，windows系统给人的感觉就是皮实耐操软件生态丰富。windows10系统对开发者也非常的友好，再不济我们可以使用虚拟机。今天在这儿分享一个Office 2019增强版转VOL并激活的脚本。

## Office 2019增强版转VOL并激活脚本

```
:: 修复乱码问题
CHCP 65001
title office2019 retail转换vol版
:: 判断安装目录
if exist "%ProgramFiles%\Microsoft Office\Office16\ospp.vbs" cd /d "%ProgramFiles%\Microsoft Office\Office16"
if exist "%ProgramFiles(x86)%\Microsoft Office\Office16\ospp.vbs" cd /d "%ProgramFiles(x86)%\Microsoft Office\Office16"

cls

echo 正在重置Office2019零售激活...

cscript ospp.vbs /rearm

echo 正在安装 KMS 许可证...
for /f %%x in ('dir /b ..\root\Licenses16\ProPlus2019VL_kms*.xrm-ms') do cscript ospp.vbs /inslic:"..\root\Licenses16\%%x" &gt;nul

echo 正在安装 MAK 许可证...
for /f %%x in ('dir /b ..\root\Licenses16\ProPlus2019VL_mak*.xrm-ms') do cscript ospp.vbs /inslic:"..\root\Licenses16\%%x" &gt;nul

echo 正在安装 KMS 密钥...
cscript ospp.vbs /inpkey:NMMKJ-6RK4F-KMJVX-8D9MJ-6MWKP

echo 正在设置 KMS 服务器...
cscript ospp.vbs /sethst:kms.03k.org

echo 正在联系KMS服务器...
cscript ospp.vbs /act

echo 转化完成，按任意键退出！

pause &gt;nul

exit
```

这个脚本中有使用第三方的激活服务器`kms.03k.org`​，如果这个服务器不能激活你的电脑或者Office你也可以使用老徐搭的激活服务器`xuchengen.cn`​。

> 面试官经常会问初始容量为1000的HashMap，依次存放1000个元素会不会触发扩容？首先1000这个数不满足2的次幂，与之接近且符合2次幂的数为1024，1024乘以0.75等于768，触发扩容阈值为768所以会触发扩容。计算一个数是2的多少次幂我们用科学计算器来算，毕竟人肉逻辑机还是挺慢的。

## 2的多少次方等于1024

传统计算器：计算器依次按`1024 ÷ 2`​ 然后按`=`​直到结果为1，在这个过程中累计按了多少次`=`​则是2的多少次幂数，这里的结果是2的10次幂为1024。

科学计算器：计算器依次按`(1000 log) ÷ (2 log) =`​ 计算结果显示的就是2的多次次幂数，这里的结果是2的10次幂为1024。

> 关于Linux我比较提倡的学习方法是在使用中学习总结。最近在我的腾讯云服务器部署了套DzzOffice开源网盘系统，因为系统盘只有40G数据盘200G挂载给了/data目录，已经没有多余的磁盘挂载给/var/www目录我想在未来的某一天系统盘肯定不够用从而导致其他的问题，思索了好一会儿想到了创建软连接的方法来解决这个问题。

系统盘：40G

数据盘：200G

网站根目录：/var/www（实际占用系统盘）

解决办法：将网站根目录备份到数据盘/data/var/www目录然后删除/var/www目录，最后创建软连接指向到/data/var/www。

```
ln -s /data/var/www /var/www
```

> 以一台Linux服务器为例。这台Linux包括一颗`Intel(R) Xeon(R) CPU E3-1230 v2 @ 3.30GHz`​ CPU, 单颗CPU包括 4 个 cpu core, 使用超线程包含8个逻辑cpu core。
>
> 下面让我们通过Linux的命令来查找对应的参数，看看是否符合官方的介绍, 主要是查看`/proc/cpuinfo`​的信息获得。

## 查看 CPU 的型号

```
cat /proc/cpuinfo | grep 'model name' | sort | uniq
```

输出:

```
model name      : Intel(R) Xeon(R) CPU E3-1230 V2 @ 3.30GHz
```

## 查看 CPU 颗数

实际Server中插槽上的CPU个数, 物理cpu数量，可以数不重复的 `physical id`​个数。

```
cat /proc/cpuinfo | grep 'physical id' | sort | uniq | wc -l
```

输出:

```
1
```

## 查看 CPU 核数

一颗CPU上面能处理数据的芯片组的数量。

```
cat /proc/cpuinfo |grep "cores"|uniq|awk '{print $4}'
```

输出:

```
4
```

## 逻辑 CPU 核数

一般情况，我们认为一颗cpu可以有多核，加上intel的超线程技术(HT), 可以在逻辑上把一个物理线程模拟出两个线程来使用，使得单个核心用起来像两个核一样，以充分发挥CPU的性能，

逻辑CPU数量=物理cpu数量 x cpu cores 这个规格值 x 2(如果支持并开启超线程)。

top命令查询出来的就是逻辑CPU的数量。

```
cat /proc/cpuinfo |grep "processor"|wc -l
```

输出:

```
8
```

## 参考资料

[https://stackoverflow.com/questions/6481005/how-to-obtain-the-number-of-cpus-cores-in-linux-from-the-command-line](https://stackoverflow.com/questions/6481005/how-to-obtain-the-number-of-cpus-cores-in-linux-from-the-command-line)

[https://blog.csdn.net/dba_waterbin/article/details/8644626](https://blog.csdn.net/dba_waterbin/article/details/8644626)

[https://www.zhihu.com/question/28472793](https://www.zhihu.com/question/28472793)

> 在HTTP和RPC的选择上，可能有些人是迷惑的，主要是因为有些RPC框架配置复杂，如果走HTTP也能完成同样的功能，那么为什么要选择RPC，而不是更容易上手的HTTP来实现了。
>
> 本篇主要阐述HTTP和RPC的异同，让大家更容易根据自己的实际情况选择更适合的方案。

## 传输协议

RPC，可以基于TCP协议，也可以基于HTTP协议

HTTP，基于HTTP协议

## 传输效率

RPC，使用自定义的TCP协议，可以让请求报文体积更小，或者使用HTTP2协议，也可以很好的减少报文的体积，提高传输效率。

HTTP，如果是基于HTTP1.1的协议，请求中会包含很多无用的内容，如果是基于HTTP2.0，那么简单的封装以下是可以作为一个RPC来使用的，这时标准RPC框架更多的是服务治理。

## 性能消耗

> 主要在于序列化和反序列化的耗时

RPC，可以基于thrift实现高效的二进制传输。

HTTP，大部分是通过json来实现的，字节大小和序列化耗时都比thrift要更消耗性能。

## 负载均衡

RPC，基本都自带了负载均衡策略。

HTTP，需要配置Nginx，HAProxy来实现。

## 服务治理

> 下游服务新增、重启、下线时如何不影响上游调用者

RPC，能做到自动通知，不影响上游。

HTTP，需要事先通知，修改Nginx/HAProxy配置。

## 总结

RPC主要用于公司内部的服务调用，性能消耗低，传输效率高，服务治理方便。

HTTP主要用于对外的异构环境，浏览器接口调用，APP接口调用，第三方接口调用等。

> 最近升级了最新版本的Mac微信客户端，然后就遇到了如题所示的故障，其主要原因是我安装了微信助手插件。如果你也遇到相同的问题请使用如下办法解决（貌似重启电脑以后还要重新执行一次）。

​![](assets/wechat-20230801152521-mike13c.jpg)​

## 终端命令行

```
sudo codesign --sign - --force --deep /Applications/WeChat.app
```

```
sudo spctl --master-disabley
```

在访达应用程序中找到微信客户端右键显示简介勾选覆盖恶意软件保护

​![](assets/wechat2-20230801152521-w5o0oy4.jpg)​

### 文章导航

[← 早期文章](https://www.xuchengen.cn/category/wuzhuti/page/2)
