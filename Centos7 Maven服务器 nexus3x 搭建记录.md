安装环境：
--------------
>
>操作系统：centos7 64位。
>
>JDK：jdk1.8 64位
>
>nexus：nexus3.0.0
>

下载
--------------
`
官网：
https://www.sonatype.com/download-oss-sonatype
`

`
wget https://sonatype-download.global.ssl.fastly.net/nexus/3/nexus-3.4.0-02-unix.tar.gz
`

解压
--------------

```
mkdir /usr/local/nexus

tar -zxvf nexus-3.4.0-02-unix.tar.gz  -C /usr/local/nexus/

ls
    nexus-3.4.0-02
    sonatype-work
    (一个 nexus 服务，一个私有库目录)
```


配置
--------------

```
cd nexus-3.4.0-02/
```

配置启动用户

`vi bin/nexus.rc `
> 
> \# 增加下面部分，为了开机启动环境配置  
> \# 这个主要为了后面使用，不需要使用root用户启动服务  
> run_as_user="root"
> 
> JAVA_HOME=/usr/java/jdk1.8.0_131
> 
> NEXUS_HOME=/usr/local/nexus/nexus-3.4.0-02 
> 

配置端口和目录,可以默认不修改

`vi etc/nexus-default.properties`

> application-port=8083 
>
> application-host=0.0.0.0

开机启动
--------------
>vim /lib/systemd/system/nexus.service  


    [Unit]  
    Description=nexus  
    After=network.target  
      
    [Service]  
    Type=forking  
    ExecStart=/usr/local/nexus/nexus-3.4.0-02/bin/nexus start  
    ExecReload=/usr/local/nexus/nexus-3.4.0-02/bin/nexus reload  
    ExecStop=/usr/local/nexus/nexus-3.4.0-02/bin/nexus stop  
    PrivateTmp=true  
      
    [Install]    
    WantedBy=multi-user.target  

设置开机启动

    systemctl enable nexus.service   
防火墙设置
--------------
    vi /etc/sysconfig/iptables
    添加：
    -A INPUT -m state --state NEW -m tcp -p tcp --dport 8081 -j ACCEPT
    保存退出后
    systemctl restart iptables.service #重启防火墙使配置生效

或者关闭防火墙

    systemctl stop firewalld.service #停止firewall
    systemctl disable firewalld.service #禁止firewall开机启动


使用
--------------

1、使用admin/admin123 登录

2、创建用户 设置->Security->Users->Create user

3、使用创建好的用户登录。

4、创建maven仓库

>maven仓库几种类型:

> * hosted，本地仓库，通常我们会部署自己的构件到这一类型的仓库。比如公司的第二方库。
  * proxy，代理仓库，它们被用来代理远程的公共仓库，如maven中央仓库。
  * group，仓库组，用来合并多个hosted/proxy仓库，当你的项目希望在多个repository使用资源时就不需要多次引用了，只需要引用一个group即可。





















