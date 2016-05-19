shadowsocks
===========

[![PyPI version]][PyPI]
[![Build Status]][Travis CI]
[![Coverage Status]][Coverage]

A fast tunnel proxy that helps you bypass firewalls.

Server 服务端
------

### Install

Debian / Ubuntu:

    apt-get install python-pip
    pip install shadowsocks

CentOS 安装方法:

    yum install python-setuptools && easy_install pip
    pip install shadowsocks

(如果有权限问题，可能需要这样:)

    sudo yum install python-setuptools && sudo easy_install pip
    sudo pip install shadowsocks

Windows:

See [Install Server on Windows]

### 简单运行:

    ssserver -p 443 -k password -m aes-256-cfb

在后台运行:

    sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start

停止服务器:

    sudo ssserver -d stop

比较好的运行方式: 

创建文件:  `/etc/shadowsocks/config.json`

    mkdir /etc/shadowsocks
    touch /etc/shadowsocks/config.json
    vim /etc/shadowsocks/config.json

输入内容: 

    {
        "server_port":10086,
        "local_port":1080,
        "password":"******",
        "timeout":600,
        "method":"aes-256-cfb"
    }

vim 可以通过 `a` 命令从命令模式进入编辑模式。 输入完成后可以通过 `Esc` 键从编辑模式进入命令模式,然后输入 `:wq` 则保存退出.

此时, 控制台运行方式是: 

    ssserver -c /etc/shadowsocks/config.json

当然,不太友好, 让服务器在后台运行的命令是:

    ssserver -c /etc/shadowsocks/config.json -d start

-d 就是 daemon, 守护进程的意思. ssserver 程序会理解的。
对应的停止命令: 

    ssserver -c /etc/shadowsocks/config.json -d stop

相关的wiki在这里: [Configuration-via-Config-File](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File)

更多的客户端或其他信息, 请参考原版的: [Wiki]

如果想要自动启动，可以编辑 `/etc/rc.local` 文件，添加上面的启动脚本。

```
[root@aliyun ~]# cat /etc/rc.local 
#!/bin/sh
#
# This script will be executed *after* all the other init scripts.
# You can put your own initialization stuff in here if you don't
# want to do the full Sys V style init stuff.

touch /var/lock/subsys/local

# start tomcat7
/usr/local/tomcat7/bin/startup.sh

# start shadowsocks
/usr/bin/ssserver -c /etc/shadowsocks/config.json -d start
```

当然,如果不是root则需要使用 `sudo vim /etc/rc.local` 来编辑。然后保存。

如果有权限问题，比如 CentOS7，则可能需要执行才能自动启动

    sudo chmod +x /etc/rc.d/rc.local

另外, 如果开启了 iptables 或者 firewalld, 则需要启用某个端口。 或者简单粗暴地关闭防火墙。


查看有哪个IP在连接10086端口:

    netstat -nat|grep -i "10086"|grep ESTABLISHED|awk '{print $5}'|awk -F: '{print $1}'|awk '!a[$0]++'


查看连接访问日志:

    sudo less /var/log/shadowsocks.log

Check all the options via `-h`. You can also use a [Configuration] file
instead.

客户端(Client)
------

* [Windows] / [OS X]
* [Android] / [iOS]
* [OpenWRT]

Use GUI clients on your local PC/phones. Check the README of your client
for more information.

Documentation
-------------

You can find all the documentation in the [Wiki].

License
-------

Copyright 2015 clowwindy

Licensed under the Apache License, Version 2.0 (the "License"); you may
not use this file except in compliance with the License. You may obtain
a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
License for the specific language governing permissions and limitations
under the License.

Bugs and Issues
----------------

* [Troubleshooting]
* [Issue Tracker]
* [Mailing list]



[Android]:           https://github.com/shadowsocks/shadowsocks-android
[Build Status]:      https://img.shields.io/travis/shadowsocks/shadowsocks/master.svg?style=flat
[Configuration]:     https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File
[Coverage Status]:   https://jenkins.shadowvpn.org/result/shadowsocks
[Coverage]:          https://jenkins.shadowvpn.org/job/Shadowsocks/ws/PYENV/py34/label/linux/htmlcov/index.html
[Debian sid]:        https://packages.debian.org/unstable/python/shadowsocks
[iOS]:               https://github.com/shadowsocks/shadowsocks-iOS/wiki/Help
[Issue Tracker]:     https://github.com/shadowsocks/shadowsocks/issues?state=open
[Install Server on Windows]: https://github.com/shadowsocks/shadowsocks/wiki/Install-Shadowsocks-Server-on-Windows
[Mailing list]:      https://groups.google.com/group/shadowsocks
[OpenWRT]:           https://github.com/shadowsocks/openwrt-shadowsocks
[OS X]:              https://github.com/shadowsocks/shadowsocks-iOS/wiki/Shadowsocks-for-OSX-Help
[PyPI]:              https://pypi.python.org/pypi/shadowsocks
[PyPI version]:      https://img.shields.io/pypi/v/shadowsocks.svg?style=flat
[Travis CI]:         https://travis-ci.org/shadowsocks/shadowsocks
[Troubleshooting]:   https://github.com/shadowsocks/shadowsocks/wiki/Troubleshooting
[Wiki]:              https://github.com/shadowsocks/shadowsocks/wiki
[Windows]:           https://github.com/shadowsocks/shadowsocks-csharp
