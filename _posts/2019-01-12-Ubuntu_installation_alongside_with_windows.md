---
layout:     post
title:      Ubuntu 双系统安装那些事儿
subtitle:   Win10 下 UEFI 环境安装 Ubuntu 18.04 双系统
date:       2019-01-12
author:     Chen HE
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - IT
---

安装Ubuntu之前，默认大家都已经在自己的计算机上安装了windows系统，那么下面开始讲一下详细安装流程。

#### 安装前准备工作

##### 确认主板BIOS是UEFI模式 

首先确认下你的主板的BIOS是UEFI模式，例如 Asus X99-E WS/USB 3.1 主板的BIOS默认就是UEFI模式。

##### 安装顺序

如果大家希望使用双系统引导机制，那么最重要的一点就是先安装Windows，而后再安装Linux。这一安装次序非常严格，千万不能弄混。在严格遵循以上次序之后，Linux安装程序会替我们完成Windows系统的处理工作、设定分区大小并在引导加载程序当中提供选项，允许我们在启动时选择进入Windows环境。如果大家先安装Linux而后安装Windows，那么微软的这套产品会直接忽略Linux，而且完全不知道该如何调整分区大小，甚至会直接利用自己的引导加载程序将Linux的给覆盖掉。在这种情况下，如果大家还是希望启动Linux系统，则需要首先修复遭到破坏的Linux系统引导加载程序。

##### 制作启动盘

我是使用U盘的方式来安装Ubuntu系统的，因此主要介绍这种方式。首先需要准备好一个4G以上的空U盘。在[Ubuntu官网](https://www.ubuntu.com/download)下载Ubuntu 18.04LTS的ISO安装文件。按照官网步骤下载[Rufus](https://rufus.akeo.ie/)。并使用上一步中下载好的ISO文件制作启动U盘。这一步可以参考参考[How to create a bootable USB stick on Windows](https://www.ubuntu.com/download/desktop/create-a-usb-stick-on-windows)

![制作启动盘](https://github.com/he-chen-95/chen-image-host/raw/master/2019/rafus.jpg)

近几年新发布的计算机的磁盘分区类型一般都是GPT，系统引导类型选择UEFI。其优点可自行百度。以前磁盘分区类型还有MBR，系统引导类型为BIOS或UEFI。注意ubuntu只有64位版本支持uefi+GPT。

##### 释放磁盘空间

在安装系统之前，需要事先释放一部分磁盘空间留给Ubuntu系统。在Win10系统中，我们可以通过鼠标右键计算机—>管理—->磁盘管理—->选中盘符右键—->压缩卷 。压缩出最少50G(建议)的空间出来，不要分配盘符，直接让其处于空闲或未分配状态即可。

![磁盘分区](https://github.com/he-chen-95/chen-image-host/raw/master/2019/disk-patrition-1.JPG)

从图中可以看到我有两个磁盘（磁盘0是128GB的SSD硬盘，磁盘1是1TB的机械硬盘）。我们需要清空一个主分区（非C盘），然后右键选择”删除卷”释放磁盘空间，接着这些空间会变成绿色的可用空间。我在磁盘1上释放了约500GB空间留给Ubuntu系统。

##### 禁用Windows的 Fast Startup

###### 方法1

进入控制面板->电源，找到 Fast Startup，禁用掉。

![禁用快速启动-01](https://github.com/he-chen-95/chen-image-host/raw/master/2019/disable-fast-boot-01.jpg)
![禁用快速启动-02](https://github.com/he-chen-95/chen-image-host/raw/master/2019/disable-fast-boot-02.JPG)
![禁用快速启动-03](https://github.com/he-chen-95/chen-image-host/raw/master/2019/disable-fast-boot-03.JPG)

注： “快速启动”是Windows 8时代引进的新特性，建议关闭该特性的原因是，“快速启动”会影响Grub开机引导过程，可能出现无法载入Ubuntu的状况，最后选择“保存修改”。

###### 方法2

进入 UEFI BIOS 界面，点击 Boot 菜单，找打 Fast Boot, 改为 Disabled。不同品牌的电脑BIOS设置不同，请自行百度。一般进入BIOS的方法是在开机界面按ESC。重启电脑进到Setup里面，然后在Boot 或者是Security 等大选项下找到 Secure Boot（安全启动），然后Enter 会出来一个 Enable 和 Disable 的选项，选到 Disable 那就关闭了安全启动了。保存你的设定然后再重启！重启电脑，进入BIOS，关闭Windows系统的快速启动（Fast Boot）选项，即设置为Disable状态。BIOS中设置U盘为第一启动项，保存并重启

##### 关闭主板的 SRT（Intel Smart Response Technology)

进入 UEFI BIOS 界面，点击 Advanced菜单，找到 Intel Rapid Storage Technology, 点击进去，如果你没有RAID模式的磁盘，这个RST一般是灰色的，没有启用

##### 禁用主板的 Secure Boot

如果你想要装Windows和 Linux 双操作系统，那么必须要禁用主板的 Secure Boot ，因为主板内置的公钥只有一个，就是微软的，因为微软影响力大。更具体信息请参考：[反Secure Boot垄断：兼谈如何在Windows 8电脑上安装Linux - 阮一峰](http://link.zhihu.com/?target=http%3A//www.ruanyifeng.com/blog/2013/01/secure_boot.html)。

Ubuntu 已经买了这个证书，所以微软的这个公钥，也能允许Ubuntu安装在主板上。看到这里，你会问，那岂不是不用禁用 Secure Boot 了？不尽然，在Ubuntu 下安装 GTX 1080 的 Nvidia 驱动的时候，会警告 UEFI Secure Boot is not compatible with the use of third-party drivers. 如果没有禁用Secure Boot, 安装了显卡驱动后，开机，输入密码时，会进不去系统，屏幕会闪一下，有回到了登录界面，死循环 。具体步骤请参考：[How to Disable or Enable Secure Boot on Your Computer via ASUS UEFI BIOS Utility](http://link.zhihu.com/?target=http%3A//www.technorms.com/45538/disable-enable-secure-boot-asus-motherboard-uefi-bios-utility)。

进入 UEFI BIOS界面，选择 Boot->Secure Boot-> Key Management -> Save Secure Boot Keys，插入U盘，备份key到这个U盘，会有四个文件, PK, KEK, DB 和DBX 写入到U盘。删除 Platform Key. 选择 Delete PK，点击OK确认删除。删除后回到上一级菜单，可以看到 Secure Boot 已经变成 disabled 了。

#### 安装Ubuntu系统

##### 设置BIOS为U盘启动

将制作好的启动U盘插在电脑上，重启电脑，进入BIOS启动顺序选择项。移动光标选择USB选项按回车即为U盘启动。系统启动后，选择”Try ubuntu“，进入试用Ubuntu界面。双击左上角的"Install Ubuntu 18.04LTS"，打开安装界面。（安装过程比较简单，根据提示输入一些信息即可）

##### Ubuntu桌面版分区策略

进入安装类型页面，不要选择"与其它系统共存"那一项，而选择最后那个“其它选项（创建自己的分区）”。使用之前预留的空闲区域来安装ubuntu系统，继续。

选中“空闲”区域，点击左下角的加号创建分区，若创建错了就点减号删除。下面每一步依次点击空闲分区-->新建分区(加号)来挂载分区。

```分区策略
/efi，系统分区：逻辑分区，空间起始位置，用于：efi系统分区。包含系统内核和系统启动所需的文件，实现双系统的关键所在，建议256M。

/，根目录分区：逻辑分区，空间起始位置，用于：EXT4日志文件系统。存储系统文件。ubuntu系统程序安装的区域，包括日后的程序更新，安装软件等都会占用这个分区的空间。

swap，交换分区：逻辑分区，空间起始位置，用于：交换分区。空间大小建议是物理内存的2倍，无挂载点。当物理内存（RAM）不足时，可以取出这部分当做虚拟内存使用。

/home，用户数据分区：逻辑分区，空间起始位置，用于：EXT4日志文件系统，home目录，存放用户数据的空间。
```

![引导设置](https://github.com/he-chen-95/Chen-Image-Host/raw/master/2019/UEFI-patrition.png)

核心步骤，“安装启动引导器的设备：”，找到类型为efi的设备，如图：/dev/sda7。然后在安装启动引导器的设置，选择上面对应的设备。它的作用和boot引导分区一样，但是boot引导是默认grub引导的，而efi显然是UEFI引导的。不要按照那些老教程去选boot引导分区，也就是最后你的挂载点里没有“注意:/boot”这一项，否则你就没办法UEFI启动两个系统了。

![磁盘分区策略-02](https://github.com/he-chen-95/chen-image-host/raw/master/2019/disk-partition-2.JPG)

我的磁盘分区策略如上图所示，我将Ubuntu单独安装在机械硬盘上。磁盘1磁盘分区1是EFI系统分区（主分区），负责引导ubuntu系统启动。磁盘1磁盘分区1是交换（swap）分区（逻辑分区）, 建议大小是电脑RAM大小的两倍。磁盘1磁盘分区3(逻辑分区)是用于挂载/home目录。磁盘1磁盘分区4(逻辑分区)是用于挂载/根目录.

下一步确认分区信息，继续走：安装成功后，会提示重启（记得拔掉U盘）。 重启后记得进入BIOS改回UEFI Security Boot On模式，也就是重新开启Security Boot。 启动顺序里面应该有一个Windows manager 和一个Ubuntu，可以顺带调一下启动顺序。然后再重启你应该就可以看到选择系统的启动引导界面了。 如果开机直接进入了Win10系统，大概是因为BIOS上开了快速启动，重启默认进入Windows系统。 你可以关闭BIOS的快速启动，也可以不关闭。如果想进入ubnutu则开机秒按F12,进入系统选择菜单，选择Ubuntu选项，如果显示如下画面，则表明大功告成！这样，两块硬盘就分别安装了独立的操作系统，具体进入哪个，由UEFI BIOS里的启动优先级来决定。你想默认启动Windows，那就把Windows那块硬盘拖动到第一的位置，如果你想默认启动Ubuntu，那就把Ubuntu那块硬盘拖动到第一的位置。

#### Linux分区基础知识

Linux的发展日新月异，老旧的Linux文档很可能会对读者认识Linux产生误导。Ubuntu已经取消了用hd和sd区分不同类型的硬盘的机制，取而代之的，用sda统一代表电脑中的第一块硬盘。在Linux下，/dev/sdaX中的数字X的编号是有限的，最大的分区编号是16。因此，主分区和扩展分区编号占用1～4，逻辑分区占用5～16。即 使你的硬盘中只有一个主分区(如，/dev/sda1)和一个扩展分区(/dev/sda2)，剩下的两个主分区编号： /dev/sda3,dev/sda4也不会分配给逻辑分区。第一个逻辑分区一定是从/dev/sda5开始编号的。

需要将/home目录单独挂载的原因，此目录下的/home/user目录存放了大量用户的个人文件和资料。所以如果独立挂载/home，即使遇到Ubuntu无故身亡的尴尬局面，也可以立刻重装系统。/home分区在每次重装系统市的时候不要格式化其中数据，之后再将/home/目录挂载到根目录/下，可以读取到之前的用户数据。

将/var和/tmp独立分区的教程通常是面向服务器的。因为高负载的服务器通常会产生很 多日志文件、临时文件，这些文件经常改变，因此把/var，/tmp独立出来有利于提高服务器性能。

关于Ubuntu系统分区的一些建议，您还可以参考Ubuntu社区的文章[advice and strategy on partitioning a Linux system](https://help.ubuntu.com/community/DiskSpace)

#### 安装Linux与Windows 10双系统的优点

文件共享：Linux还允许我们轻松访问自己的Windows文件，我们也能够在Linux桌面系统的文件管理器当中查看Windows分区，从而更为轻松地浏览并查看Windows文件。相比之下，Windows系统不提供便捷的Linux文件系统访问机制。大部分Linux发行版采用ext4文件系统，因此大家如果打算通过Windows查看Linux文件系统，可能得借力于支持ext4文件系统的第三方工具。
