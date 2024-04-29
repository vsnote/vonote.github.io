---
title: Windows 11 通过 Docker 安装 Windows XP
link: windows-11-install-windows-xp-via-docker
date: 2024-04-29 17:09:39
tags:
---

最近在网上看到一个 Git 项目 [dockur/windows](https://github.com/dockur/windows)，可以用 Docker 安装 原版的 Windows 系统，很久没折腾过系统了，想尝试一下。以下是整个安装的过程。

### 直接运行
文档里面有直接运行的脚本，但是安装有系统是固定的链接下载的，都是英文版本。
```bash
docker run -it --rm --name windows -p 8006:8006 --device=/dev/kvm --cap-add NET_ADMIN --stop-timeout 120 dockurr/windows
```
### 自定义运行
首先把需要安装的系统镜像下载下来，这里推荐 [Itellyou](https://next.itellyou.cn)，这里面基本上都是原版系统，不过需要安装迅雷才能下载。

然后把项目 clone 下来：
```
git clone https://github.com/dockur/windows.git
```

修改 compose.yml
```yml
services:
  windows:
    image: dockurr/windows
    container_name: windows
    environment:
      VERSION: "winxp"
    devices:
      - /dev/kvm
    cap_add:
      - NET_ADMIN
    ports:
      - 8006:8006
      - 3390:3389/tcp
      - 3390:3389/udp
    stop_grace_period: 2m
    restart: on-failure
    volumes:
      - /e/sys-image/winxp3.iso:/storage/custom.iso
      - ./data:/storage

```

最后执行命令：
```
docker compose up -d
```

正常的话就可以通过 [http://localhost:8006](http://localhost:8006) 来访问虚拟机了，不过浏览器对硬件的支持不是很好，作者建议通过 rdp 来访问。需要注意的是，我在 windows 和 macos 系统上都部署了，但是本机都不能通过 rdp 连接到 docker 里面的虚拟机，通过局域网是可以正常访问的。

![winxp](/images/winxp.png "winxp")

![win7](/images/win7.png "win7")
