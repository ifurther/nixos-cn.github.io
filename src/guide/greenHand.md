# 双系统安装

## Windows 系统上的准备

本节将介绍如何在已经安装了 Windows 系统的物理机上再安装 NixOS 。

### 关闭快速启动

若不关闭 Windows 的快速启动，可能会导致 NixOS 掉网卡。点击 “更改当前不可用配置” 以后会出现一个 UAC 窗口，点击允许以后，再取消 “启用快速启动（推荐）” 复选框。

![关闭快速启动](/images/GreenHand/TurnOffWindowsFastboot.jpg)

### 调整时间设置

由于 Windows 与 Linux 时间标准不同，从 Linux 切换回 Windows 会导致系统时间变更的问题。

在这里我们提供修改 Windows 设置，以让两种系统时间保持一致的的方法。

PowerShell 管理员权限运行：

```powershell
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

该命令向注册表添加了字段，下次重启生效。

### 制作引导盘

我们使用 [Ventoy](https://www.ventoy.net/cn/download.html) 制作引导盘，Ventoy
会将引导写入媒介，然后你可以间接选择引导你媒介中的镜像。这样的好处是你不用为了刻录整个驱动器，下次需要引导其他镜像时只需要把镜像拷贝到该驱动器即可。

下载[最简镜像](https://nixos.org/download.html#nix-more:~:text=without%20a%20desktop.-,Minimal%20ISO%20image,-The%20minimal%20installation)
（Minimal ISO image），我们不使用官方安装程序做演示，因为没有太多的自定义选项。下载完成后，拷贝至已经安装 Ventoy 的驱动器。

## 调整 BIOS 设置

### 关闭安全引导

在按下开机键，屏幕出现厂商品牌的时候，按住可以使你进入 BIOS 设置的按键，然后你会进入跟下图相同或类似的界面。

::: warning 厂商差异
具体情况以厂商主板为准。
不同厂商生产的机型进入 BIOS 设置的按键不相同，甚至界面也不会相同。
对于某些厂商（比如联想，宏碁），关闭安全启动需要为主板设置管理员密码，建议完成系统安装后立刻移除主板密码，以防止密码呗遗忘。
:::

![关闭安全引导](/images/GreenHand/DisableSecureBoot.png)

::: tip 安全引导
NixOS 已经支持安全引导，参见 [lanzaboote](https://github.com/nix-community/lanzaboote)
:::