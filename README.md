# fcn-deb

本项目用于打包fcn为可被Debian/Armbian/Ubuntu等Linux发行版系统直接安装的deb软件包，且在原有的fcn基础上，加入了兼容系统服务的管理脚本，极大的提高的软件的易用性。

## 服务管理

软件包在安装完毕之后，默认将fcn服务设为开机自启。可以手动切换 `fcn` 服务的开机自启状态。

1. 将fcn服务设为开机自启，操作如下：

`sudo systemctl enable fcn.service`

2. 将fcn服务取消开机自启，操作如下：

`sudo systemctl disable fcn.service`

3. 启动/停止/重启/查看状态，操作如下：

`sudo systemctl start fcn.service`、 `sudo systemctl stop fcn.service`、 `sudo systemctl restart fcn.service`、 `sudo systemctl status fcn.service`

4. 默认配置文件目录： `/etc/fcn`

其中 `fcn.conf` 为服务端默认配置文件，可以配置多个服务端配置文件，注意统一文件扩展名为 `.conf` 。

5. 日志查看：

使用命令 `journalctl -xe | grep fcn` 来查看并过滤由fcn产生的日志。

## 如何构建

在开始构建deb软件包之前请务必安装 `fakeroot` 工具(推荐)，或切换到root管理员身份操作

首先将本项目克隆到本地环境当中(注意在打包前删除项目目录下的.git文件夹，README.md以及LICENSE文件，以免将不必要的文件打包到安装包当中!)，根据需要自行从网上下载对应版本的fcn预编译发布应用包，并将其解压到本地目录当中，然后将可执行程序 `fcn` 复制到 `fcn-deb/usr/sbin/` 目录下(注意赋予可执行权限). 最后切换到fcn-deb所在的目录下，执行 `fakeroot dpkg-deb -b fcn-deb fcn-3.9-arm64.deb` (注意这里的架构请依据实际情况加以修改) 或切换到root管理员身份执行 `dpkg-deb -b fcn-deb fcn-3.9-arm64.deb` . 稍等片刻即可生成最终的deb安装包文件。
