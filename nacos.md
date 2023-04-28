# nacos2.2 单机部署+mysql8
## 下载


~~~ 
wget -c https://github.com/alibaba/nacos/releases/download/2.2.2/nacos-server-2.2.2.tar.gz 
~~~ 
## 解压
~~~
tar -xvf nacos-server-$version.tar.gz
mv nacos /usr/local/
~~~
## 数据库
- 创建用户授权
~~~
#创建账户
create user 'nacos'@'%' identified by 'nacos';
#赋予权限
grant all privileges on *.* to 'nacos'@'%' with grant option;
#刷新
flush privileges;
~~~
- 创建数据库 导入sql
~~~
create database nacos_config;
use nacos_config
source /usr/local/nacos/conf/mysql_schem.sql
~~~
## 修改配置
- 修改conf目录下的application.properties文件。
~~~
spring.datasource.platform=mysql
db.num=1
 db.url.0=jdbc:mysql://127.0.0.1:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
 db.user.0=nacos
 db.password.0=nacos
nacos.core.auth.plugin.nacos.token.secret.key=SecretKey012345678901234567890123456789012345678901234567890123456789
nacos.core.auth.server.identity.key=test
nacos.core.auth.server.identity.value=test
nacos.core.auth.enabled=true

~~~
- 创建 cluster.conf 
#  启动
~~~
sh shutdown.sh
~~~

# 登陆

~~~
http://ip:8848/nacos/#/login
账户 nacos
密码 nacos
~~~



