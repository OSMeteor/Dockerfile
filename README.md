##### Dockerfile

### 阿里云Docker镜像库
[https://dev.aliyun.com/search.html?spm=5176.775974865.0.0.74Am4l](https://dev.aliyun.com/search.html?spm=5176.775974865.0.0.74Am4l)
docker run --iptables=false  -p 127.0.0.1:27017:27017 mongo /bin/bash
 netstat -lnp|grep 27017
 
docker kill some-mongo
docker rm some-mongo
docker run --name some-mongo  -d -p 127.0.0.1:27017:27017 --ip-forward=true -icc=true mongo
docker run --name some-mongo  -d -p 127.0.0.1:27017:27017   mongo
docker run -it --link some-mongo:mongo --rm mongo sh -c 'exec mongo "$MONGO_PORT_27017_TCP_ADDR:$MONGO_PORT_27017_TCP_PORT/test"'

docker exec -i some-mongo /bin/sh
docker run --name some-mongo  -d -p 0.0.0.0:27017:27017   mongo

#### dockerCMD 
[http://blog.csdn.net/wsscy2004/article/details/25878363](http://blog.csdn.net/wsscy2004/article/details/25878363)

*  docker attach bb2
*  docker exec -it bb2 /bin/sh  
*  
* docker logs <容器名orID> 2>&1 | grep '^User: ' | tail -n1
* docker ps
* docker ps -a为查看所有的容器，包括已经停止的。
* docker rm <容器名orID>
* docker stop <容器名orID>
* docker start <容器名orID>
* docker kill <容器名orID>
* docker images 
* 删除所有镜像
* docker rmi $(docker images | grep none | awk '{print $3}' | sort -r)
* 一个容器连接到另一个容器
* docker run -i -t --name sonar -d -link mmysql:db   tpires/sonar-server
sonar
* docker pull <镜像名:tag>
* 当需要把一台机器上的镜像迁移到另一台机器的时候，需要保存镜像与加载镜像。
* docker save busybox-1 > /home/save.tar
* docker load < /home/save.tar
* docker build -t <镜像名> <Dockerfile路径>
* docker build -t xx/gitlab .  如Dockerfile在当前路径：
* 后台运行(-d)、并暴露端口(-p)
* docker run -b -d -p 127.0.0.1:27017:27017 mongo
* db.copyDatabase("students","students","211.95.27.34")
 

### 防火墙相关
* chkconfig iptables on  
* chkconfig iptables off  
* CentOS 7.0默认使用的是firewall作为防火墙，这里改为iptables防火墙。
firewall：
systemctl start firewalld.service#启动firewall
systemctl stop firewalld.service#停止firewall
systemctl disable firewalld.service#禁止firewall开机启动

一、查看哪些端口被打开 netstat -anp
二、关闭端口号:iptables -A INPUT -p tcp --drop 端口号-j DROP
　　iptables -A OUTPUT -p tcp --dport 端口号-j DROP
三、打开端口号：iptables -A INPUT -ptcp --dport 端口号-j ACCEPT
四、以下是linux打开端口命令的使用方法。
　　nc -lp 23 &(打开23端口，即telnet)
　　netstat -an | grep 23 (查看是否打开23端口)
五、linux打开端口命令每一个打开的端口，都需要有相应的监听程序才可以 


vi /etc/sysconfig/iptables 
/etc/init.d/iptables stop #start 开启 #restart 重启 

ip  a docker0

iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 172.31.0.23:80

http://www.cnblogs.com/kreo/p/4368811.html

https://docs.docker.com/v1.8/articles/networking/

iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 27017 -j DNAT --to 192.168.42.1:27017
 iptables -I DOCKER -i ext_if ! -s 8.8.8.8 -j DROP



* brctl show // 网桥
* ip link show // 网络设备
* ip addr show // 网络设备ip地址
* cat /proc/sys/net/ipv4/ip_forward
* ip route
* ifconfig -a
* ip addr
* netstat -rn
* –userland-proxy


### 阿里云
docker kill some-mongo
docker rm some-mongo
* mongodb  
* db.serverStatus() 基本信息
* db.stats()
* db.serverStatus().locks  锁信息
* db.serverStatus().globalLock 全局锁信息
* db.serverStatus().mem 内存信息
* db.serverStatus().connections
* docker run --name osmeteor-mongo  -d -p 0.0.0.0:27017:27017   mongo
* docker run --name osmeteor-redis  -d -p 0.0.0.0:6379:6379   redis
* docker run --name osmeteor-nginx  -d -p 0.0.0.0:80:80   nginx
* [https://dev.aliyun.com/detail.html?spm=5176.1972343.2.2.caAsV2&repoId=1256](https://dev.aliyun.com/detail.html?spm=5176.1972343.2.2.caAsV2&repoId=1256)
* docker run --name osmeteor-rabbitmq  -d -p 0.0.0.0:15672:15672 -p 0.0.0.0:55672:55672   rabbitmq
* docker run -d -p 0.0.0.0:15672:15672 -p 0.0.0.0:55672:55672 --hostname my-rabbit --name osmeteor-rabbitmq -e RABBITMQ_DEFAULT_USER=osmeteor -e RABBITMQ_DEFAULT_PASS=p@ssw0rd rabbitmq:3-managemen

docker run -d --hostname osmeteor-rabbitmq --name some-rabbit -p 0.0.0.0:15672:15672 -p 0.0.0.0:55672:55672 rabbitmq:3-management

docker run -d -p 5672:5672 -p 15672:15672 -e RABBITMQ_NODENAME=rabbit -e RABBITMQ_SERVER_START_ARGS="-rabbit cluster_nodes {['rabbit@host1','rabbit@host2'],disc}" --name rabbitmq-server-cluster --net="host" $IMAGE




