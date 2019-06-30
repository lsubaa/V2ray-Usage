# V2ray-Usage


---

## Project V 

Project V 是一个工具集合，它可以帮助你打造专属的基础通信网络。Project V 的核心工具称为V2Ray，其主要负责网络协议和功能的实现，与其它 Project V 通信。V2Ray 可以单独运行，也可以和其它工具配合，以提供简便的操作流程。

### 主要特性

* 多入口多出口: 一个 V2Ray 进程可并发支持多个入站和出站协议，每个协议可独立工作。
* 可定制化路由: 入站流量可按配置由不同的出口发出。轻松实现按区域或按域名分流，以达到最优的网络性能。
* 多协议支持: V2Ray 可同时开启多个协议支持，包括 Socks、HTTP、Shadowsocks、VMess 等。每个协议可单独设置传输载体，比如 TCP、mKCP、WebSocket 等。
* 隐蔽性: V2Ray 的节点可以伪装成正常的网站（HTTPS），将其流量与正常的网页流量混淆，以避开第三方干扰。
* 反向代理: 通用的反向代理支持，可实现内网穿透功能。
* 多平台支持: 原生支持所有常见平台，如 Windows、Mac OS、Linux，并已有第三方支持移动平台。

**详见[V2ray官网 over the Wall](https://www.v2ray.com)

## Linux 安装脚本

V2Ray 提供了一个在 Linux 中的自动化安装脚本。这个脚本会自动检测有没有安装过 V2Ray，如果没有，则进行完整的安装和配置；如果之前安装过 V2Ray，则只更新 V2Ray 二进制程序而不更新配置。

以下指令假设已在 su 环境下，如果不是，请先运行 sudo su。

运行下面的指令下载并安装 V2Ray。当 yum 或 apt-get 可用的情况下，此脚本会自动安装 unzip 和 daemon。这两个组件是安装 V2Ray 的必要组件。如果你使用的系统不支持 yum 或 apt-get，请自行安装 unzip 和 daemon

> bash <(curl -L -s https://install.direct/go.sh)

此脚本会自动安装以下文件：

* /usr/bin/v2ray/v2ray：V2Ray 程序；
* /usr/bin/v2ray/v2ctl：V2Ray 工具；
* /etc/v2ray/config.json：配置文件；
* /usr/bin/v2ray/geoip.dat：IP 数据文件
* /usr/bin/v2ray/geosite.dat：域名数据文件

此脚本会配置自动运行脚本。自动运行脚本会在系统重启之后，自动运行 V2Ray。目前自动运行脚本只支持带有 Systemd 的系统，以及 Debian / Ubuntu 全系列。

运行脚本位于系统的以下位置：

* /etc/systemd/system/v2ray.service: Systemd
* /etc/init.d/v2ray: SysV

脚本运行完成后，你需要：

1. 编辑 /etc/v2ray/config.json 文件来配置你需要的代理方式；
2. 运行 service v2ray start 来启动 V2Ray 进程；
3. 之后可以使用 service v2ray start|stop|status|reload|restart|force-reload 控制 V2Ray 的运行。

## go.sh 参数

go.sh 支持如下参数，可在手动安装时根据实际情况调整：

* -p 或 --proxy: 使用代理服务器来下载 V2Ray 的文件，格式与 curl 接受的参数一致，比如 "socks5://127.0.0.1:1080" 或 "http://127.0.0.1:3128"。
* -f 或 --force: 强制安装。在默认情况下，如果当前系统中已有最新版本的 V2Ray，go.sh 会在检测之后就退出。如果需要强制重装一遍，则需要指定该参数。
* --version: 指定需要安装的版本，比如 "v1.13"。默认值为最新版本。
* --local: 使用一个本地文件进行安装。如果你已经下载了某个版本的 V2Ray，则可通过这个参数指定一个文件路径来进行安装。

**示例：**

* 使用地址为 127.0.0.1:1080 的 SOCKS 代理下载并安装最新版本：./go.sh -p socks5://127.0.0.1:1080
* 安装本地的 v1.13 版本：./go.sh --version v1.13 --local /path/to/v2ray.zip

