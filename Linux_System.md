# [你应该知道的16个Linux服务器监控命令](http://roclinux.cn/?p=2549)
在使用Linux服务器的过程中，有16个命令可以帮助你全面了解你的服务器的运行状况。如果你能够很熟练地掌握这些命令，就离成为一名专业的Linux系统管理员不远啦！

至此，我们的命令行准备好了，下面就可以开始通过强大的命令来查看“到底服务器里发生了什么”：

* [01    - iostat       ]
* [02/03 - meminfo/free ]
* [04    - mpstat       ]
* [05    - netstat      ]
* [06    - nmon         ]
* [07    - pmap         ]
* [08/09 - ps/pstree    ]
* [10    - sar          ]
* [11    - strace       ]
* [12    - tcpdump      ]
* [13    - top          ]
* [14    - uptime       ]
* [15    - vmstat       ]
* [16    - wireshark    ]


### [05    - netstat      ]
netstat命令，是Linux系统管理员几乎每天都会用到的命令（它已经逐步在被ss命令取代），他可以显示很多有关网络方面的信息，例如socket使用情况、路由情况、网卡情况、协议情况、网络流量统计等等。

一些常用的netstat选项包括：
```
-a : 显示所有socke信息
-r : 显示路由信息
-i : 显示网卡借口统计
-s : 显示网络协议统计
```
### [07 – pmap]

pmap命令可以显示进程占用的内存量。

你可以通过pmap找到那个占用内存量最多的进程。
```
pmap PID
```

### [08/09 – ps/pstree]
ps和pstree在Linux系统里是一对好兄弟，它们都是用来列出处于运行状态的进程的列表的。

ps告诉我们每个进程使用的内存量以及所消耗的CPU时间。


# References
[sar访谈 - linux命令五分钟系列之二十九](http://roclinux.cn/?p=1647)

[Linux大棚](http://roclinux.cn)
