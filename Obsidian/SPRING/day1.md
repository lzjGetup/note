# 1.

## IOC 控制反转

	|由ioc 容器解决创建对象的过程
---
# 2.
## DI依赖注入
	|在容器中建立bean与bean之间关系的过程
### 依赖注入四种方式
![[Pasted image 20230925152214.png]]
### 构造器注入
	|构造器注入中,name属性里面与目标类的构造方法里面的形参强耦合,用type属性可以修改成依赖类型识别
==如图==
![[Pasted image 20230925153716.png]]

	|或者使用index属性,确定注入的形参的位置
==如图==
![[Pasted image 20230925185126.png]]

### 自动装配
```java
//按照类型装配
<bean id="dao" class="com.ling.dao.impl.daoimpl" autowire="byType">
```
```java
//按照名字装配
<bean id="dao" class="com.ling.dao.impl.daoimpl" autowire="byName">
//注意:按照名字装配时,最好不要为一个对象配置两个bean
```
>自动装配注意点
![[Pasted image 20230925191741.png]]


## property属性
	|用于设置bean之间的依赖关系

	|引用数据类型注入
```java
<property>
1.数组
<array> </array>
2.列表
<list> </list>
3.set
<set> </set>
---------------以上内部均写 <value> </value>
4.map
<map>
<entry key="",value=""/>
</map>
</property>

```


---
# 3.

## bean
	|name可以设置别名,中间用逗号或空格隔开
	|scope可以设置bean是否为单列bean
#### bean的创建(实例工厂)
```java
<bean id="userFactory" class="com.itling.factory.UserDaoFactory"/>
//先创建工厂对象
<bean id="userDao" factory-method="getUserDao" factory -bean="userFactory"/>
//factory -bean指明用哪个工厂,factory-method指明用工厂的哪个方法构造对象
```
==可以改进成factoryBean的方法==
*如图*
![[Pasted image 20230925150145.png]]

#### bean的生命周期
![[Pasted image 20230925151704.png]]

---

## 4.加载property文件(例如jdbc文件)
*如图为jdbc.properties文件*
![[Pasted image 20230925194751.png]]
1. 开启context命名空间
**其中,xmlns:为xml文件配置namespace**
**灰色部分为新添加的部分**
>![[Pasted image 20230925195128.png]]

2. 使用context命名空间加载property文件
>![[Pasted image 20230925200127.png]]
==此处的location里面可以加载多个配置文件, ".property"可以一次加载所有配置文件==

3. 使用属性占位符号${}读取property文件中的属性
>![[Pasted image 20230925200022.png]]
