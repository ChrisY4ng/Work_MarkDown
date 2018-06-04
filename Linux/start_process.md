# 启动过程

启动过程分为5个阶段：

1. 内核的引导
2. 运行init
3. 系统初始化
4. 建立终端
5. 用户登录系统

init程序类型：

- SysV：init, CentOS 5之前，配置文件:/etc/inittab
- Upstart:init,CentOS 6,配置文件：/etc/inittab、/etc/init/*.conf
- Systemed:init,CentOS 7,配置文件：/usr/lib/systemd/system、/etc/systemd/system

## 内核的引导

- 打开计算机电源，
- BIOS开机自检，按照BIOS中设置的启动设备来启动，
- 操作系统接管硬件，读入/boot 目录下的内核文件。

## 运行INIT

init进程是系统所有进程的起点。init程序首先读取配置文件/ect/inittab。init进程的一大任务是启动守护进程（“daemon”，开机需要启动）。
Linux包含7个运行级别，不同运行级别启动的程序不同。启动时根据不同的运行级别，确定要运行那些程序。

linux运行级别：

- 运行级别0：系统停机。系统默认运行级别不能为0，否则不能正常启动。
- 运行级别1：单用户工作状态。root权限，用于系统维护，不能远程登录。
- 运行级别2：多用户状态（没有NFS）。
- 运行级别3：完全的多用户状态（包含NFS）。登录后进入控制台命令行模式。
- 运行级别4：保留，系统未使用。
- 运行级别5：X11控制台，登录后进入图形GUI模式。
- 运行级别6：系统正常关闭并重启。系统默认运行级别不能为0，否则不能正常启动。

## 系统初始化

完成激活交换分区、检查磁盘、加载硬件模块、其他一些需要优先执行的任务。

    si::sysinit:/etc/rc.d/rc.sysinit -->运行/etc/rc.d/rc.sysinit脚本

## 建立终端

init会打开6个终端，以便用户登录。

    inittab中的一下6行就定义了6个终端：
    1:2345:respawn:/sbin/mingetty tty1
    2:2345:respawn:/sbin/mingetty tty2
    3:2345:respawn:/sbin/mingetty tty3
    4:2345:respawn:/sbin/mingetty tty4
    5:2345:respawn:/sbin/mingetty tty5
    6:2345:respawn:/sbin/mingetty tty6

运行级别2、3、4、5 都将以respawn方式运行mingetty程序，mingetty能打开终端、设置模式。

## 用户登录

一般包含三种登录方式：

1. 命令行登录
2. ssh登录
3. 图形界面登录

## Linux关机

正确关机流程：sync>shutdown/reboot/halt
man shutdown 查看帮助文档。

    sync 将数据由内存同步到硬盘中。
    shutdown 关机指令
    shutdown -h 10 '10分钟后关机' 10分钟后关机，并显示此消息
    shutdown -h now 立刻关机
    shutdown -h +10 10分钟后关机
    shutdown -h 20:00 指定时间20:00关机
    shutdown -r now 立刻重启
    shutdown -r +10 10分钟后重启
    reboot 重启===shutdown -r now / init 6
    halt 关机===shutdown -h now / poweroff / init 0