数据卷/VOLUME
=============

含义
----
>一个数据卷是一个特别指定的目录，该目录利用容器的UFS文件系统可以为容器提供一些稳定的特性或者数据共享。数据卷可以在多个容器之间共享。
创建数据卷，只要在docker run命令后面跟上-v参数即可创建一个数据卷，当然你也可以跟多个-v参数来创建多个数据卷，当创建好带有数据卷的容器后，你就可以在其他容器中通过--volumes-froms参数来挂载该数据卷了，而不管该容器是否运行。你也可以在Dockerfile中通过VOLUME指令来增加一个或者多个数据卷。

应用场景
--------
>如果你有一些数据想在多个容器间共享，或者想在一些临时性的容器中使用该数据，那么最好的方案就是你创建一个数据卷容器，然后从该临时性的容器中挂载该数据卷容器的数据。例如如下操作：

    #启动一个Volume_Container容器，包含两个数据卷
    docker run -v /var/volume1 -v /var/volume2 -name Volume_Container ubuntu14.04  linux_command
    #创建App_Container容器，挂载Volume_Container容器中的数据卷
    docker run -t -i -rm -volumes-from Volume_Container -name App_Container ubuntu14.04  linux_command
    #或者再创建一个容器，挂载App_Container中从Volume_Container挂载的数据卷
    docker run -t -i -rm -volumes-from App_Container -name LastApp_Container ubuntu14.04  linux_command

>在一个终端内创建数据卷容器，并在数据卷目录内写入测试文件， 另打开一个容器，挂载上一个数据卷容器的数据卷，查看测试文件。即使你删除了刚开始的第一个数据卷容器或者中间层的数据卷容器，只要有其他容器使用数据卷，数据卷都不会被删除的。

>你也可以把一个本地主机的目录当做数据卷挂载在容器上，同样是在docker run后面跟-v参数，不过-v后面跟的不再是单独的目录了，他是[host-dir]:[container-dir]:[rw|ro]这样格式的，host-dir是一个绝对路径的地址，如果host-dir不存在，则docker会创建一个新的数据卷，如果host-dir存在，但是指向的是一个不存在的目录，则docker也会创建该目录，然后使用该目录做数据源。例如：

    docker run -i -t -v /tmp:/mnt ubuntu/14.04:14.04 /bin/bash


>你不能使用docker export、save、cp等命令来备份数据卷的内容，因为数据卷是存在于镜像之外的，但是总会有变通方法的，如下：

    # 创建一个新容器，挂载数据卷容器，同时挂载一个本地目录，然后把远程数据卷容器的数据卷通过备份命令备份到映射的本地目录里面。 
    docker run -rm --volumes-from DATA -v $(pwd):/backup busybox tar cvf /backup/backup.tar /data



