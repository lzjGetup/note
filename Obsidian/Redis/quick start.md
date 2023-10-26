# redis入门
## 启动服务
**以连接主机为例**
*进入redis安装目录,输入命令启动redis服务*
```cmd
redis-server.exe redis.windows.conf
```

*启动redis客户端服务*
```cmd
redis-cli.exe
```
==添加具体主机端口命令==
```cmd
redis-cli.exe -h localhost -p 6379 -a 你的密码
```
==其中,6379为redis端口号,ctrl+c命令可以终止redis服务,exit可以退出当前连接客户端,在redis.windows.conf里面可以修改密码,具体字段是#requirepass==

## 数据类型
==redis存储的是key-value结构的数据,其中key是字符串类型,value有五种常用数据类型==
1. string
2. hash(like JAVA hashMap)
3. list
4. set
5. sorted set / zset

### 各种数据类型的特点
>![[Pasted image 20231014111850.png]]


## 常用命令
==字符命令==
>![[Pasted image 20231014134838.png]]

==哈希命令==
>![[Pasted image 20231014140023.png]]

==列表操作==
>![[Pasted image 20231014141643.png]]

==集合操作==
![[Pasted image 20231014142229.png]]

==有序集合==
>![[Pasted image 20231014143457.png]]



==通用命令==
>![[Pasted image 20231014144110.png]]









