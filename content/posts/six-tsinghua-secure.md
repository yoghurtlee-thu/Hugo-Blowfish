---
title: 关于你清奇怪的校园网
date: 2024-04-29T20:29:00
summary: 旋转大脑.webp
tags:
  - 折腾
  - 博客
category: 计算机
featureimage: 
series: 
series_order: 
slug: six-tsinghua-secure
draft: false
---
好的，众所周知，我一向对你清的校园网颇有微词。不仅是封端口，而且还有 AP 隔离（简单来说同一个局域网的设备无法通信），造成我的 Localsend 都没办法用（这也是我换 iPhone 的原因之一）。

但是！就是在今天，事情发生了奇怪的转机。

## 起因：为了一碟醋做了一锅饺子

这件事的起因其实很简单，就是我是一个坚定的本地音乐主义者。我会用我所有可能的手段，包括但不限于免费的音乐网站，通过听歌白嫖一些流媒体的限时 VIP 下载之后把文件逆加密以及抓取 B 站视频转成 mp3 等方式获取 `.mp3` 和 `.flac` 格式的文件存到本地听。关于我的本地音乐之旅，我未来会专门写一篇文章详细介绍（`画大饼.webp`）。

然而，这样下载的文件大都没有元数据。作为一个强迫症，我是无法接受的。

之前在 Windows 和 Android 上有一款宝藏软件—— [音乐标签](https://www.cnblogs.com/vinlxc/p/11347744.html)。这款软件可以从国内的 QQ 音乐、网易云等自动刮削元数据，而且还免费，除了好就是好。然而我现在是 Apple 全家桶用户，于是就没有于是了。

这段时间我尝试了许多方法，包括但不限于寻找各种各样的替代软件，尝试打包 GitHub 上面的一些源码，使用兼容层运行这个软件，为此我还装了 Java，Python 的各种库，Wine 以及我死活不愿意装的 Rosetta。然而并没有什么用。

于是我采用了奇葩的方法，就是使用我的 Android 备用机进行刮削，然后传回电脑。至于为什么不用备用电脑？我当然用过，但是启动不如手机方便。

好，问题来了：怎么传文件呢？

由于是备用机，不可能一直登录 VX/QQ，Edge drop 的稳定性又太过铀溴，跨平台传文件的终极方案 localsend 又用不了，让我头痛欲裂。

## 伟大的孙哥

众所周知，在折腾这方面，小氯解决不了的问题，就会请教光荣而伟大的孙哥。

今天我和孙哥约饭的时候，就问起这个问题，结果孙哥诧异地表示你清校园网根本没有什么 AP 隔离。

![黑人问号.webp|301](https://chlorinedemo.s3.bitiful.net/emoji/EMJ-confused.webp)

于是我回去按照孙哥教的方法测试了一下。用 Python 写个小代码：

```Python
import http.server
import socketserver
import socket

# 定义端口，随便写一个空闲的就行
PORT = 31000

# 创建请求处理程序
Handler = http.server.SimpleHTTPRequestHandler

# 获取本地IP地址
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.connect(("8.8.8.8", 80))
ip_address = s.getsockname()[0]
s.close()

# 创建服务器
with socketserver.TCPServer(("", PORT), Handler) as httpd:
    print(f"服务器在 {ip_address}:{PORT} 上运行")
    httpd.serve_forever()

```

这会把当前的根目录暴露出去。

然后我拿起手机访问了 IP，结果访问上了。

啊？！

那既然如此，我可就要用 Localsend 了。

## 小氯不等式

在 MacBook 和 Android 上安好 Localsend。在设置——高级设置中把端口改成刚才测试的 `31000`。

然后在发送页面，不出意外是看不到目标设备的。

此时，我们只需要点击收藏夹，将目标设备的 IP 和端口手动填入，收藏后就可以直接传文件了。

![](https://chlorinedemo.s3.bitiful.net/emoji/EMJ-confused.webp)

好好好，跨世纪的发现，小氯不等式：发现不了设备≠不能传文件。

甚至 Localsend 默认的端口也可以用！也就是说，我曾经错过了无数与 Localsend 并肩作战的机会（`大哭.webp`）。

## 后记

于是我至少暂时找到了一个音乐元数据的解决方案。

此外，既然校园网只会封端口但是没有 AP 隔离，那么，

> NAS，启动！
