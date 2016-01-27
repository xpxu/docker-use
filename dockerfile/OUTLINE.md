Dockerfile关键字
================

FROM
----
基于哪个镜像

RUN
---
执行命令

MAINTAINER
----------
镜像创建者

CMD
---
container启动时执行的命令，但是一个Dockerfile中只能有一条CMD命令，多条则只执行最后一条CMD.CMD主要用于container时启动指定的服务，当docker run command的命令匹配到CMD command时，会替换CMD执行的命令

ENTRYPOINT
----------
container启动时执行的命令，但是一个Dockerfile中只能有一条ENTRYPOINT命令，如果多条，则只执行最后一条.ENTRYPOINT没有CMD的可替换特性

USER
----
使用哪个用户跑container

EXPOSE
------
container内部服务开启的端口。

ENV
---
用来设置环境变量

ADD/COPY
---
将文件<src>拷贝到container的文件系统对应的路径<dest>.拷贝到container中的文件和文件夹权限为0755,uid和gid为0.如果文件是可识别的压缩格式，则docker会帮忙解压缩
ADD 多了2个功能, 下载URL和解压.  其他都一样.如果你不希望压缩文件拷贝到container后会被解压的话, 那么使用COPY.如果需要自动下载URL并拷贝到container的话, 请使用ADD.

VOLUME
------
创建数据卷

WORKDIR
-------
切换目录用，可以多次切换(相当于cd命令)，对RUN,CMD,ENTRYPOINT生效

