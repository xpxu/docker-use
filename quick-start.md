## QUICK-START

###1. push docker image to hub.docker.com
Refer to [Tag, push, and pull your image](https://docs.docker.com/mac/step_six/)

```cpp
//docker 登陆
docker login 
//6c615a225191 is target container id and xpxu/ubuntu_django is a repo created in hub.docker
docker tag 6c615a225191 xpxu/ubuntu_django 
//将6c615a225191推送到xpxu/ubuntu_django这个仓库
docker push xpxu/ubuntu_django 
```
