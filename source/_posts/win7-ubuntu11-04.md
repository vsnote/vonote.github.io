---
title: 最简单的win7+Ubuntu11.04双系统安装方法
link: win7-ubuntu11-04
tags:
  - ubuntu
  - win7
  - 教程
  - 系统
  - 系统技巧
id: '29'
categories:
  - - 笔记
date: 2012-11-17 20:06:01
---

也许是最近过的比较平静，看着WIN7有点烦躁，那颗折腾的心又出来了，于是下了个[UBUNTU11.10的最新版](http://61.234.240.71/data1/iso/c38165dbc82d5cd09ab07ffc4b2259e9/ubuntu-11.10-desktop-i386.iso)，折腾吧！小白~ 我原来是有装了个WIN8开发者预览版的。因为也玩了段时间了，所以就干脆删除了，用来放UBUNTU11.10，有30个G，虽然小了点，但玩玩也够了。 接下来再下载[EASYBCD2.1](http://software-files-a.cnet.com/s/software/12/30/36/68/EasyBCD%202.1.2.exe?token=1324666693_b95d5a5af9af7a82581c0dc74ddc0435&lop=link&ptype=3001&ontid=2094&siteId=4&edId=3&spi=f563c43494653bb43ccacba5e7284a20&pid=12303668&psid=10556865&&fileName=EasyBCD+2.1.2.exe),这个用来装双系统，简直就是神器！很方便，更简单。 下载后直接下一步安装，然后打开这个工具。 [![步骤一](http://vsnote.test/wp-content/uploads/2012/11/82635f026e061d9551348a747bf40ad163d9cafc.jpg "依次按照图中标注的设置")](http://vsnote.test/wp-content/uploads/2012/11/82635f026e061d9551348a747bf40ad163d9cafc.jpg) 依次按照上面图片中的步骤设置好 [![步骤二](http://vsnote.test/wp-content/uploads/2012/11/2222222.jpg "还是接着设置")](http://vsnote.test/wp-content/uploads/2012/11/2222222.jpg) 点击上图上的那个按钮会打开一个配置文件，复制下面这段代码

title Install Ubuntu 11.10
root (hd0,0)
kernel (hd0,0)/vmlinuz boot=casper iso-scan/filename=/ubuntu-11.10-desktop-i386.iso ro quiet splash
locale=zh\_CN.UTF-8
initrd (hd0,0)/initrd.lz

ubuntu-11.10-desktop-i386.iso 这个是你下载的镜像文件名，放在C盘下面！ 接着就把ubuntu 11.10用压缩工具或者虚拟光驱打开，把casper目录里的vmlinuz和initrd.lz两个文件复制到C盘的根目录下面。 之后就重启，进入Install Ubuntu 11.10这个开机选项。 进入LIVECD之后不要先急着安装，找到终端，然后输入这条命令：sudo umount -l /isodevice（卸载掉挂载的硬盘，不然安装的时候无法安装）。 接下来就可以双击安装UBUNTU11.10了，中间有会弹出来一个对话框，点是就行了。然后分区的时候点高级选项。 分区步骤： 1、先删除掉那个要放UBUNTU的分区。 2、在刚删除的那个分区中添加挂载点。 交换分区200M /home 10g 剩下的就给了 / 之后就填写一些基本信息就可以装完了。 大功告成了！