卸载已经安装svn：
---------------
```
//检查svn安装
rpm -qa subversion

//卸载
yum remove subversion
```

检查yum是否有最新版的安装版本：
----------
`yum list | grep subversion`

新增SVN源
----------
```
vi /etc/yum.repos.d/wandisco-svn.repo

//添加内容：
[WandiscoSVN]
name=Wandisco SVN Repo
baseurl=http://opensource.wandisco.com/centos/7/svn-1.8/RPMS
enabled=1
gpgcheck=0

//测试配置是否可用：
yum list | grep subversion

```

开始安装
------------------
```
    yum clean all

    yum install subversion
```
