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

**详见**
  * [V2ray官网，需要over the Wall才能看到](https://www.v2ray.com)
  * [v2ray-core](https://github.com/v2ray/v2ray-core/releases)
  * [V2Ray 配置指南](https://toutyrater.github.io)

**简易用法**

   **server(linux)**

```shell
   bash <(curl -L -s https://install.direct/go.sh)
   # 使用 service v2ray start|stop|status|reload|restart|force-reload 控制 V2Ray 的运行
```

 **client(macOS)**
 
  * [V2rayU](https://github.com/yanue/v2rayu)
  * [V2rayX](https://github.com/Cenmrev/V2RayX)
 
  **set** 
   * local Sock Por: 1081
   * local Http Port: 8001

---

## 下载安装

**平台支持**

**V2Ray 在以下平台中可用：**

* Windows 7 及之后版本（x86 / amd64）；
* Mac OS X 10.10 Yosemite 及之后版本（amd64）；
* Linux 2.6.23 及之后版本（x86 / amd64 / arm / arm64 / mips64 / mips）；
* 包括但不限于 Debian 7 / 8、Ubuntu 12.04 / 14.04 及后续版本、CentOS 6 / 7、Arch Linux；
* FreeBSD (x86 / amd64)；
* OpenBSD (x86 / amd64)；
* Dragonfly BSD (amd64)；

### 下载 V2Ray

预编译的压缩包可以在如下几个站点找到：

* Github Release: [github.com/v2ray/v2ray-core](https://github.com/v2ray/v2ray-core/releases)
* Github 分流: [github.com/v2ray/dist](https://github.com/v2ray/dist/)
* Homebrew: [github.com/v2ray/homebrew-v2ray](https://github.com/v2ray/homebrew-v2ray)
* Arch Linux: [packages/community/x86_64/v2ray/](https://www.archlinux.org/packages/community/x86_64/v2ray/)
* Snapcraft: [snapcraft.io/v2ray-core](https://snapcraft.io/v2ray-core)

压缩包均为 zip 格式，找到对应平台的压缩包，下载解压即可使用。

**验证安装包**

V2Ray 提供两种验证方式：

* 安装包 zip 文件的 SHA1 / SHA256 摘要，在每个安装包对应的.dgst文件中可以找到。
* 可运行程序（v2ray 或 v2ray.exe）的 gpg 签名，文件位于安装包中的 v2ray.sig 或 v2ray.exe.sig。签名公钥可以在代码库中找到。

**Windows 和 Mac OS 安装方式**

通过上述方式下载的压缩包，解压之后可看到 v2ray 或 v2ray.exe。直接运行即可。

---

## Linux 安装脚本

V2Ray 提供了一个在 Linux 中的自动化安装脚本。这个脚本会自动检测有没有安装过 V2Ray，如果没有，则进行完整的安装和配置；如果之前安装过 V2Ray，则只更新 V2Ray 二进制程序而不更新配置。

以下指令假设已在 su 环境下，如果不是，请先运行 sudo su。

运行下面的指令下载并安装 V2Ray。当 yum 或 apt-get 可用的情况下，此脚本会自动安装 unzip 和 daemon。这两个组件是安装 V2Ray 的必要组件。如果你使用的系统不支持 yum 或 apt-get，请自行安装 unzip 和 daemon

> bash <(curl -L -s https://install.direct/go.sh)

**此脚本会自动安装以下文件:**

* /usr/bin/v2ray/v2ray：V2Ray 程序；
* /usr/bin/v2ray/v2ctl：V2Ray 工具；
* /etc/v2ray/config.json：配置文件；
* /usr/bin/v2ray/geoip.dat：IP 数据文件
* /usr/bin/v2ray/geosite.dat：域名数据文件

此脚本会配置自动运行脚本。自动运行脚本会在系统重启之后，自动运行 V2Ray。目前自动运行脚本只支持带有 Systemd 的系统，以及 Debian / Ubuntu 全系列。

**运行脚本位于系统的以下位置:**

* /etc/systemd/system/v2ray.service: Systemd
* /etc/init.d/v2ray: SysV

**脚本运行完成后，你需要:**

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


## 命令行参数

### V2Ray

V2Ray 的程序文件的命令行参数如下：

> v2ray [-version] [-test] [-config=config.json] [-format=json]

**-version**

只输出当前版本然后退出，不运行 V2Ray 主程序。

**-test**

测试配置文件有效性，如果有问题则输出错误信息，不运行 V2Ray 主程序。

**-config**

配置文件路径，可选的形式如下:

* 本地路径，可以是一个绝对路径，或者相对路径。
* "stdin:": 表示将从标准输入读取配置文件内容，调用者必须在输入完毕后关闭标准输入流。
* 以http://或https://(均为小写)开头: V2Ray 将尝试从这个远程地址加载配置文件。

**-format**

配置文件格式，可选的值有：

* json: JSON 格式；
* pb 或 protobuf: Protobuf 格式；

> 当-config没有指定时，V2Ray 将先后尝试从以下路径加载config.json:

  >* 工作目录（Working Directory）
  >* 环境变量中v2ray.location.asset所指定的路径

### V2Ctl

V2Ctl 是一个集合，它有若干个子命令组成。全局的命令行形式如下：

> v2ctl <command> <options>

**command**

子命令，有以下选项:

* api: 调用 V2Ray 进程的远程控制指令。
* config: 从标准输入读取 JSON 格式的配置，然后从标准输出打印 Protobuf 格式的配置。
* cert: 生成 TLS 证书。
* fetch: 抓取远程文件。
* tlsping: (V2Ray 4.17+) 尝试进行 TLS 握手。
* verify: 验证文件是否由 Project V 官方签名。
* uuid: 输出一个随机的 UUID。

**V2Ctl Api**

> v2ctl api [--server=127.0.0.1:8080] <Service.Method> <Request>

调用 V2Ray 进程的远程控制指令。示例：

> v2ctl api --server=127.0.0.1:8080 LoggerService.RestartLogger ''

**V2Ctl Config**

> v2ctl config

此命令没有参数。它从标准输入读取 JSON 格式的配置，然后从标准输出打印 Protobuf 格式的配置。

**V2Ctl Cert**

> v2ctl cert [--ca] [--domain=v2ray.com] [--expire=240h] [--name="V2Ray Inc"] [--org="V2Ray Inc] [--json] [--file=v2ray]

生成一个 TLS 证书。

  **--ca**

如果指定此选项，将会生成一个 CA 证书。

  **--domain**

证书的 Alternative Name 项。该参数可以多次使用，来指定多个域名。比如--domain=v2ray.com --domain=v2ray.cool。

  **--expire**

证书有效期。格式为 Golang 的时间长度。

  **--name**

证书的 Command Name 项。

  **--org**

证书的 Orgnization 项。

  **--json**

将生成的证书以 V2Ray 支持的 JSON 格式输出到标准输出。默认开启。

  **--file**

将证书以 PEM 格式输出到文件。当指定 --file=a 时，将生成 a_cert.pem 和 a_key.pem 两个文件。

**V2Ctl Fetch**

> v2ctl fetch <url>

抓取指定的 URL 的内容并输出，只支持 HTTP 和 HTTPS。

**V2Ctl TlsPing**

> v2ctl tlsping <domain> --ip=[ip]

向指定的域名发起 TLS 握手。

  **domain**

目标域名

  **--ip**

此域名的 IP 地址。如果未指定此参数，V2Ctl 将使用系统的 DNS 进行域名解析。

**V2Ctl Verify**

> v2ctl verify [--sig=/path/to/sigfile] <filepath>

此命令用于验证一个文件是否由 Project V 官方签名。

  **--sig**

签名文件路径，默认值为待验证文件加入'.sig'后缀。

  **filepath**

待验证文件路径。

**V2Ctl UUID**

> v2ctl uuid

此命令没有参数。每次运行都会输出一个新的 UUID。

---

## 新手上路

在下载并安装了 V2Ray 之后，你需要对它进行一下配置。这里介绍一下简单的配置方式，只是为了演示，如需配置更复杂的功能，请参考后续的配置文件说明。

### 客户端

在你的 PC （或手机）中，你需要运行 V2Ray 并使用下面的配置：

```json
{
  "inbounds": [{
    "port": 1080,  // SOCKS 代理端口，在浏览器中需配置代理并指向这个端口
    "listen": "127.0.0.1",
    "protocol": "socks",
    "settings": {
      "udp": true
    }
  }],
  "outbounds": [{
    "protocol": "vmess",
    "settings": {
      "vnext": [{
        "address": "server", // 服务器地址，请修改为你自己的服务器 ip 或域名
        "port": 10086,  // 服务器端口
        "users": [{ "id": "b831381d-6324-4d53-ad4f-8cda48b30811" }]
      }]
    }
  },{
    "protocol": "freedom",
    "tag": "direct",
    "settings": {}
  }],
  "routing": {
    "domainStrategy": "IPOnDemand",
    "rules": [{
      "type": "field",
      "ip": ["geoip:private"],
      "outboundTag": "direct"
    }]
  }
}
```

上述配置唯一要改的地方就是你的服务器 IP，配置中已注明。上述配置会把除了局域网（比如访问路由器）之外的所有流量转发到你的服务器。

### 服务器

然后你需要一台防火墙外的服务器，来运行服务器端的 V2Ray。配置如下：

```json
{
  "inbounds": [{
    "port": 10086, // 服务器监听端口，必须和上面的一样
    "protocol": "vmess",
    "settings": {
      "clients": [{ "id": "b831381d-6324-4d53-ad4f-8cda48b30811" }]
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  }]
}
```

服务器的配置中需要确保 id 和端口与客户端一致，就可以正常连接了。

### 运行

* 在 Windows 和 macOS 中，配置文件通常是 V2Ray 同目录下的 config.json 文件。直接运行 v2ray 或 v2ray.exe 即可。
* 在 Linux 中，配置文件通常位于 /etc/v2ray/config.json 文件。运行 v2ray --config=/etc/v2ray/config.json，或使用 systemd 等工具把 V2Ray 作为服务在后台运行。


