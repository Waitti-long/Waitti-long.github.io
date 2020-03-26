# MySQL8 简单操作

**先说明版本问题：在使用mysql的时候如果发现任何的登陆不上去，用户名密码错误，请先检查mysql版本，5.7和8实在是差太多了**

Linux下如何安装mysql8(默认会安装mysql5.7)

```sh
wget https://dev.mysql.com/get/mysql-apt-config_0.8.10-1_all.deb # 下载mysql8配置包
sudo dpkg -i mysql-apt-config_0.8.10-1_all.deb # 配置时会有选项，选mysql8就行
sudo apt-get update
sudo apt-get upgrade # 有必要的话
# 如果update出现问题，执行以下两行，这是一个签名问题
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 8C718D3B5072E1F5
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 58712A2291FA4AD5
```

时区

```sql
# 仅修改当前会话的时区，停止会话失效
# 东八区
set time_zone = '+8:00';
 
# 修改全局的时区配置
set global time_zone = '+8:00';
flush privileges; # 刷新缓存
```

密码

```sql
ALTER USER "root"@"localhost" IDENTIFIED  BY "新密码";
```

JDBC的URL配置

* 上海时间（东八区）
* 使用Unicode
* utf-8编码
* 使用SSL

```
jdbc:mysql://localhost:3306/数据库名?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf8&useSSL=true
```

