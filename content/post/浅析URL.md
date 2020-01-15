---
title: "浅析URL"
date: 2020-01-16T00:34:31+08:00
draft: false
---

### IP：网际协议，全称 Internet Protocal。

主要有两个功能：标识主机或者网络和寻址。
约定了：

1. 如何定位一台设备。
2. 如何封装数据报文，以跟其他设备交流。

IP 分为内网和外网。

---

### 外网 IP

可在 ip138.com 可查看外网 IP，而重启路由器后，可能会重新分配一个外网 IP。

### 内网 IP

一般格式为 192.168.xxx.xxx，一般路由器 IP 为 192.168.1.1。

### 几个特殊的 IP

- 127.0.0.1 表示自己。
- localhost 通过 hosts 指定为自己。
- 0.0.0.0 不表示任何设备。

### hosts 文件

Windows 系统中，hosts 位于 C:\Windows\System32\drivers\etc\hosts 。在 macOS / Linux 系统中，hosts 位于 /etc/hosts。

### 端口 Port

一台机器可以提供不同服务。

- 要提供 HTTP 服务最好使用 80 端口。
- 要提供 HTTPS 服务最好使用 433 端口。
- 要提供 FTP 服务最好使用 21 端口。
- 一共有 65535 个端口。（基本上够用）

### 端口规则

- 0 到 1023 号端口是留给系统使用的，拥有了管理员权限后，才能使用 0-1023 号端口。
- 其他端口可以给普通用户使用。
- http-server 默认使用 8080 端口。
- 端口被占用，只能用另一个端口。

  #### IP 和端口缺一不可！

---

### 域名

域名可以说是一个 IP 地址的别称，为了便于记忆。

可以 ping 域名来查看 IP 地址。

- 一个域名可以对应不同的 IP（负载均衡），大公司常用，可防止一台机器扛不住。
- 一个 IP 可以对应不同域名（共享主机），小公司常用，公用服务器。

### 域名类型

- 顶级域名： .com
- 二级域名：baidu.com（俗称一级域名）
- 三级域名： www.baidu.com（俗称二级域名）

www.xxx.com 和 xxx.com 可能是同一家公司，也可能不是，而且 www 非常多余。

### DNS

DNS（Domain Name System）将域名和 IP 对应起来。

比如:

1. 当你输入 baidu.com 时，你的浏览器会向运营商提供的服务器询问 baidu.com 对应什么 IP
2. 运营商回复 IP 后，浏览器才会向相应 IP 的 80/433 端口发送请求。
3. 请求的内容即为 baidu.com 的首页。

#### 80 或 443 窗口

- 服务器默认使用 80 提供 http 服务。
- 服务器默认使用 443 提供 https 服务。
- 可在开发者工具里查看具体的端口。

### 路径

用于请求不同的页面，路径是没有后缀，在开发者工具 Network 中可查看。

例如：

https://developer.mozilla.org/zh-CN/docs/Learn/HTML
https://developer.mozilla.org/zh-CN/docs/Learn/CSS

### 查询参数

而同一页面，同一路径，也可以显示不同内容，主要取决于查询参数。

### 锚点

同一页面，同一查询结果，同一内容的不同位置。

例如：

https://developer.mozilla.org/zh-CN/docs/Web/CSS#参考书
https://developer.mozilla.org/zh-CN/docs/Web/CSS#教程

notes:

- 锚点看起来有中文，但实际不支持中文（通过编码识别）。
- 锚点无法在 Network 面板看到，因为锚点不会传给服务器。

### URL

完整的 URL 包括`[协议类型]://[访问资源需要的凭证信息]@[服务器地址]:[端口号]/[资源层级UNIX文件路径][文件名]?[查询参数]#[锚点]`

其中[访问凭证信息]、[端口号]、[查询参数]、[锚点]都属于选填项。

HTTPS 默认端口 443，HTTP 默认端口 80。
