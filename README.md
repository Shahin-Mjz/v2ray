# Deploy a `V2Ray` Proxy on a `VPS`
最好用的 V2Ray 一键安装脚本 &amp; 管理脚本

### 安装或卸载
使用 root 用户输入下面命令安装或卸载
```
bash <(curl -s -L https://git.io/v2ray.sh)
```
** 如果上面链接失效了,可以使用下面的方法 **
```
git clone https://github.com/heweiye/v2ray -b master
cd v2ray
chmod +x install.sh
./install.sh local
```

### 功能特点
- 支持 V2Ray 多数传输协议
- 支持 WebSocket + TLS / HTTP/2
- 支持 动态端口 (WebSocket + TLS，Socks5， HTTP/2 除外)
- 支持 屏蔽广告
- 支持 配置 Shadowsocks
- 支持 下载客户端配置文件 (不用 Xshell 也可以下载)
- 客户端配置文件同时支持 SOCKS 和 HTTP
- 支持 生成 V2Ray 配置二维码链接 (仅适用部分客户端)
- 支持 生成 V2Ray 配置信息链接
- 支持 生成 Shadowsocks 配置二维码链接
- 支持修改 V2Ray 传输协议
- 支持修改 V2Ray 端口
- 支持修改 动态端口
- 支持修改 用户ID
- 支持修改 TLS 域名
- 支持修改 Shadowsocks 端口
- 支持修改 Shadowsocks 密码
- 支持修改 Shadowsocks 加密协议
- 自动启用 BBR 优化 (如果内核支持)
- 集成可选安装 BBR (by teddysun.com)
- 集成可选安装 锐速 (by moeclub.org)
- 一键 查看运行状态 / 查看配置信息 / 启动 / 停止 / 重启 / 更新 / 卸载 / 等等…
- 人性化向导 & 纯净安装 & 卸载彻底

哈哈哈..我故意要写够 23 条的。说着当然，脚本肯定都会有如上所说的功能。

### 快速管理
```
v2ray info 查看 V2Ray 配置信息
v2ray config 修改 V2Ray 配置
v2ray link 生成 V2Ray 配置文件链接
v2ray infolink 生成 V2Ray 配置信息链接
v2ray qr 生成 V2Ray 配置二维码链接
v2ray ss 修改 Shadowsocks 配置
v2ray ssinfo 查看 Shadowsocks 配置信息
v2ray ssqr 生成 Shadowsocks 配置二维码链接
v2ray status 查看 V2Ray 运行状态
v2ray start 启动 V2Ray
v2ray stop 停止 V2Ray
v2ray restart 重启 V2Ray
v2ray log 查看 V2Ray 运行日志
v2ray update 更新 V2Ray
v2ray update.sh 更新 V2Ray 管理脚本
v2ray uninstall 卸载 V2Ray
```

### 配置文件路径
```
V2Ray 配置文件路径：/etc/v2ray/config.json
Caddy 配置文件路径：/etc/caddy/Caddyfile
脚本配置文件路径: /etc/v2ray/233blog_v2ray_backup.conf
```

**警告，请不要修改脚本配置文件，免得出错。。**
如果你不是有特别的需求，也不要修改 V2Ray 配置文件
不过也没事，若你实在想要瞎折腾，出错了的话，你就卸载，然后重装，再出错 ，再卸载，再重装，重复到自己不再想折腾为止。。

### WS+TLS / HTTP2
如果你使用了这两个协议，那么就会使用了脚本自带的 Caddy 集成
不管如何，不建议直接去更改 Caddy 的配置：/etc/caddy/Caddyfile
如果你需要配置其他网站相关，请将网站的配置文件放到 /etc/caddy/sites 目录下，然后重启 Caddy 进程即可，脚本默认生成的 Caddy 的配置会加载 /etc/caddy/sites 这个目录下的所有配置文件。
所以，请将你的网站配置文件放到 /etc/caddy/sites 目录下，完完全全不需要去更改 /etc/caddy/Caddyfile
记得重启 Caddy 进程：service caddy restart

### Caddy 插件相关
本脚本集成了 Caddy，但不集成任何 Caddy 插件，如果你需要安装某些 Caddy 插件，你可以使用官方的 Caddy 安装脚本来一键安装。
本人的脚本集成的 Caddy 的安装路径，跟 Caddy 官方的安装脚本是一致的。所以可以直接安装，不会有任何问题

举个例子，安装包含 http.filebrowser 插件的 Caddy，执行如下命令即可

```
curl https://getcaddy.com | bash -s personal http.filebrowser
```

你可以在 https://caddyserver.com/download 找到 Caddy 更多插件和安装命令。

### 备注
V2Ray 客户端配置文件 SOCKS 监听端口为 2333， HTTP 监听端口为 6666
可能某些 V2Ray 客户端的选项或描述略有不同，但事实上，此脚本显示的 V2Ray 配置信息已经足够详细，由于客户端的不同，请对号入座。

### 使用Cloudflare中转V2Ray流量
担心 IP 被墙？或者不想 IP 被墙？是的！使用 Cloudflare 来中转 V2Ray 的 WebSocket 流量就行！由于使用了 Cloudflare 中转，所以墙根本不知道背后的 IP 是多少，你可以愉快的玩耍了~

提醒
如果你不是使用 移动宽带 的用户，那么使用 Cloudflare 中转的速度相对来说是比较慢的，这个是因为线路的问题，无解。
警告警告警告
该教程目前写得比较简陋，以后应该会增加详细图文教程
V2Ray 的 WS + TLS 不是神话，如果你没学会走路就不要急着跑
大佬。。。你如果是从来没接触过 V2Ray 的人一上来就开玩 WS + TLS
你真的不怕摔跤吗
你有解析过域名吗，知道什么是 A 记录吗，会修改 NS 吗。。
如果不懂，那就先补上这些知识再往下看
如果实在想玩 WS + TLS，请认认真真看教程
教程真的写得比较简陋，如果实在折腾不成功，那也很正常的，改天再来
或者直接放弃

准备
一个域名，建议使用免费域名
确保域名已经可以在 Cloudflare 正常使用。
在 Cloudflare 的 Overview 选项卡可以查看域名状态，请确保为激活状态，即是： Status: Active
怎么 SSH 连接上被墙的 IP ? Xshell 在属性那里可以设置代理，或者你可以在一台没有被墙的境外 VPS 使用 iptables 转发数据到被墙的机器上，此处不细说了。

添加域名解析
在 DNS 选项卡那边添加一个 A 记录的域名解析，假设你的域名是 233blog.com，并且想要使用 www.233blog.com 作为翻墙的域名
那么在 DNS 那里配置，Name 写 www，IPv4 address 写你的 VPS IP，务必把云朵点灰，然后选择 Add Record 来添加解析记录即可
(如果你已经添加域名解析，请务必把云朵点灰，即是 DNS only)

OK，确保操作没有问题的话，继续

安装 V2Ray
如果你已经使用本人提供的 V2Ray 一键安装脚本并安装了 V2Ray，那就直接输入 v2ray config 修改传输协议为 WebSocket + TLS

如果你并没有使用本站提供的 V2Ray 一键安装脚本来安装 V2Ray
那么现在开始使用吧，最好用的 V2Ray 安装脚本，保证你满意
使用 root 用户输入下面命令安装或卸载
```
bash <(curl -s -L https://git.io/v2ray.sh)
```

如果提示 curl: command not found ，那是因为你的小鸡没装 Curl
ubuntu/debian 系统安装 Curl 方法: apt-get update -y && apt-get install curl -y
centos 系统安装 Curl 方法: yum update -y && yum install curl -y
安装好 curl 之后就能安装脚本了

之后选择安装，传输协议选择 WebSocket + TLS (即是选择 4 )，V2Ray 端口随便，不要是 80 和 443 即可，然后输入你的域名，域名解析 Y ，自动配置 TLS 也是 Y ，其他就默认吧，一路回车。等待安装完成
如果你的域名没有正确解析，安装会失败，解析相关看上面的 添加域名解析

安装完成后会展示 V2Ray 的配置信息，并且会询问是否生成二维码等，不用管它，直接回车

然后输入 v2ray status 查看一下运行状态，请确保 V2Ray 和 Caddy 都在运行

如果没有问题的话，继续

设置 Crypto 和 开启中转
确保 Cloudflare 的 Crypto 选项卡的 SSL 为 Full
并且请确保 SSL 选项卡有显示 Universal SSL Status Active Certificate 这样的字眼，如果你的 SSL 选项卡没有显示这个，不要急，只是在申请证书，24 小时内可以搞定。

然后在 DNS 选项卡那里，把刚才点灰的那个云朵图标，点亮它，一定要点亮一定要点亮一定要点亮

云朵图标务必为橙色状态，即是 DNS and HTTP proxy(CDN)

V2Ray 配置信息
很好，现在接下来配置客户端使用
输入 v2ray info 即可查看 V2Ray 的配置，如果你有使用某些 V2Ray 客户端，可以根据给出的配置的信息来配置使用了。赶紧测试吧
