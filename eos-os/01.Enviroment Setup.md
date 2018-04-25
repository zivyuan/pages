# EOS 系统搭建

## EOS系统核心组成部分

* nodeos：EOS 系统的核心进程，也就是所谓的“节点”。运行时可以配置插件
* cleos：本地的命令行工具，通过命令行与真人用户交互，并与节点（nodeos）的 REST 接口通信。是用户或者开发者与节点进程交互的桥梁。
* keosd：本地钱包工具。非节点用户存储钱包的进程，可以管理多个含有私钥的钱包并加密。

### 搭建计划
1. 测试环境安装。安装用于运行 EOS 节点核心程序的操作系统
2. 核心系统安装。EOS 核心组件，nodeos、cleos、keosd
3. 本地部署方案测试。服务可用性测试、钱包测试、测试网络运行测试
4. 将本地方案部署到线上，使 EOS 节点可以通过外部网络访问
5. 节点可用性测试，启动测试网络
6. 基于测试网络构建测试用 DAPP
7. 发布节点

## Step 1
###测试环境安装

官方的系统环境建议：

1. Amazon 2017.09 and higher
2. Centos 7
3. Fedora 25 and higher (Fedora 27 recommended)
4. Mint 18
5. Ubuntu 16.04 (Ubuntu 16.10 recommended)
6. MacOS Darwin 10.12 and higher (MacOS 10.13.x recommended)

根据实际情况选择 Centos 7 作为运行 EOS 节点的操作系统。选择 Centos 7 有两个原因，一是因为平常使用的 Mac，但实际生产环境肯定不会用 Mac 系统的；第二是 Centos 作为一款开源的服务器操作系统得到广泛的应用，其可靠性毋庸置疑，相关资源也丰富。

![](https://www.centos.org/images/logo_small.png)

#### 下载 Centos 7
[Centos Download Page](https://www.centos.org/download/)

为了保持系统纯净，这里下载 [Minimal ISO](http://ftp.yz.yamagata-u.ac.jp/pub/linux/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1708.iso) 版本。

#### 安装 Centos 7
安装系统使用了著名的虚拟机软件 [Virtual Box](https://www.virtualbox.org/wiki/VirtualBox)

![](https://www.virtualbox.org/graphics/vbox_logo2_gradient.png)

【 Centos 安装截图】

*注意*

由于 Centos 默认的网络设置是不会自动开机加载的，所以系统启动后的第一件事情是打开网络自动配置设置。

配置方法：

    cd /etc/sysconfig/network-scripts/

在目录里找到类似 `ifcfg-en??` 的文件，比如我这里是 `ifcfg-enp0s3`

    vi ifcfg-enp0s3

在文件里找到行：`ONBOOT=no` 并修改为 `ONBOOT=yes`，然后再保存并加载网络配置

    service network restart


#### 安装必要软件
由于使用的是 Mini 版系统，一些必要的软件是没有的，比如 git。可以通过 yum 来安装：

    yum install -y git

至此 EOS 运行的基础环境就搭建完成了。
