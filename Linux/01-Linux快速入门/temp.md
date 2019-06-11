## 系统服务管理

service iptables status # 查看防火墙状态
service iptables stop/start/restart

chkconfig iptables on/off   # 配置防火墙开机启动/关闭

service --status-all    # 查看系统所有后台服务进程
service sshd status     # 查看指定的后台服务进程状态

service sshd stop/start/restart

chkconfig httpd on/off  # 让httpd服务开机启动/关闭

centOS7命令：
CentOS 7.0中一个最主要的改变，就是切换到了systemd。它用于替代红帽企业版Linux前任版本中的SysV和Upstart，对系统和服务进行管理。systemd兼容SysV和Linux标准组的启动脚本。

Systemd是一个Linux操作系统下的系统和服务管理器。它被设计成向后兼容SysV启动脚本，并提供了大量的特性，如开机时平行启动系统服务，按需启动守护进程，支持系统状态快照，或者基于依赖的服务控制逻辑。

先前的使用SysV初始化或Upstart的红帽企业版Linux版本中，使用位于/etc/rc.d/init.d/目录中的bash初始化脚本进行管理。而在RHEL 7/CentOS 7中，这些启动脚本被服务单元取代了。服务单元以.service文件扩展结束，提供了与初始化脚本同样的用途。要查看、启动、停止、重启、启用或者禁用系统服务，你要使用systemctl来代替旧的service命令。

注：为了向后兼容，旧的service命令在CentOS 7中仍然可用，它会重定向所有命令到新的systemctl工具。

使用systemctl来启动/停止/重启服务

要启动一个服务，你需要使用如下命令：

# systemctl start httpd.service
这会启动httpd服务，就我们而言，Apache HTTP服务器。

要停掉它，需要以root身份使用该命令：

# systemctl stop httpd.service

要重启，你可以使用restart选项，如果服务在运行中，它将重启服务；如果服务不在运行中，它将会启动。你也可以使用try-start选项，它只会在服务已经在运行中的时候重启服务。同时，reload选项你也可以有，它会重新加载配置文件。

# systemctl restart httpd.service

# systemctl try-restart httpd.service

# systemctl reload httpd.service

我们例子中的命令看起来会像下面这样：

检查服务状态

要检查服务状态，你可以使用status选项，看这里：

# systemctl status httpd.service

输出结果就像这样：

它会告诉你运行中的服务的方方面面。

使用启用/禁用服务来控制开机启动

你也可以使用enable/disable选项来控制一个服务是否开机启动，命令如下：

# systemctl enable httpd.service

# systemctl disable httpd.service

CentOS（Community Enterprise Operating System，中文意思是：社区企业操作系统）是Linux发行版之一，它是来自于Red Hat Enterprise Linux依照开放源代码规定释出的源代码所编译而成。由于出自同样的源代码，因此有些要求高度稳定性的服务器以CentOS替代商业版的Red Hat Enterprise Linux使用。两者的不同，在于CentOS并不包含封闭源代码软件。

CentOS 是一个基于Red Hat Linux 提供的可自由使用源代码的企业级Linux发行版本。每个版本的 CentOS都会获得十年的支持（通过安全更新方式）。新版本的 CentOS 大约每两年发行一次，而每个版本的 CentOS 会定期（大概每六个月）更新一次，以便支持新的硬件。这样，建立一个安全、低维护、稳定、高预测性、高重复性的 Linux 环境。[1]  CentOS是Community Enterprise Operating System的缩写。

CentOS 是RHEL（Red Hat Enterprise Linux）源代码再编译的产物，而且在RHEL的基础上修正了不少已知的 Bug ，相对于其他 Linux 发行版，其稳定性值得信赖。