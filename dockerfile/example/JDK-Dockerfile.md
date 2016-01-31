注意以下几点
* 1. 环境变量no_proxy的使用.
* 2. pip环境变量的设置. More in [pip User Guide](https://pip.pypa.io/en/stable/user_guide/#environment-variables)
* 3. jdk的安装

```
FROM oraclelinux:6.6
MAINTAINER "xx@xx.com"
ENV http_proxy http://www-proxy.XX.com:80

// 使用no_proxy环境变量指定不使用代理的例外情况
ENV no_proxy localhost,127.0.0.1

// PIP相关环境变量设置
ENV PIP_INDEX_URL http://artifactory-slc.xx.com/artifactory/api/pypi/pypi-virtual/simple
ENV PIP_TRUSTED_HOST artifactory-slc.xx.com

//指定yum安装之后，执行一次yum -y clean all，清除缓存
RUN yum update ca-certificates; yum -y clean all

// rpm更新yum repo， 然后yum安装包
RUN rpm -ivh https://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum install -y python-setuptools redis tar less wget which nmap ipmitool sudo; yum -y clean all

// 安装jdk1.7
WORKDIR /usr/java
RUN yum install -y glibc.i686 libstdc++-4.4.7-11.el6.i686; yum -y clean all
RUN wget -nv --no-check-certificate --no-cookies --header 'Cookie: oraclelicense=accept-securebackup-cookie' http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-linux-i586.tar.gz -O - | tar xz
RUN ln -s /usr/java/jdk1.7.0_72/bin/java /usr/bin/java

EXPOSE 5000
CMD ["/usr/bin/xx"]
```
