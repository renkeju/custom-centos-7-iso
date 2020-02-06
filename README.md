# 定制 Centos 7 ISO

此仓库允许使用必要的软件包创建自定义的CentOS 7 ISO

## 要求

为了使用此仓库，您需要具备以下条件：

 * 构建镜像使用的OS为 CentOS 7.x 发行版
 * 具有一定可用磁盘空间的正在运行的CentOS实例（物理或虚拟主机）
 * 当前实例可以访问互联网

## 设置

其中包括一个在CentOS实例中运行的`setup_env.sh`脚本。 这个脚本将安装创建自定义ISO所需的必要软件包。.

## 使用

下一个脚本是`create_iso`，它需要依序命令：

 1. fetch
 2. layout
 3. finish

### fetch

如果是以下情况，此命令将从指定的URL（默认值为Stanford）获取DVD ISO.

 * 没有可用的iso。

### layout

此命令将提取ISO并将其放置到磁盘上并复制任何在 `RPMS` 目录中的自定义rpms。

## finish

此命令将清除所有以前的ISO元数据，复制到 `./ks.cfg` 中的kickstart文件，修改启动菜单以添加kickstart文件，并在 `/data/centos-7-iso-layout` 中创建ISO。

您可以单独运行每个命令，也可以一起运行。

    ./create_iso fetch
    # create RPMs
    ./create_iso layout
    ./create_iso finish

或 `./create_iso fetch layout finish`.

由此产生的ISO将可以启动并安装干净的映像，以准备用于安装。

## 镜像默认设置

* Stock Kernel
* US Keyboard and Language
* Firewall enabled with SSH allowed
* Passwords are using SHA512
* Firstboot disabled
* SELinux is set to enabled
* Timezone is set to Asia/Shanghai
* Disk is LVM and create /home direrctory
* Default packages installed

   * @^minimal
   * @core
   * kexec-tools
   * ansible
