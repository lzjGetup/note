# 1.基本概念及API
1. ==ORM==(object relational mapping):**对象关系映射**
2. ==Resourses(apache)==:属于MyMbtis加载资源的工具类,可用于加载核心配置文件
3. ==SqlSessionFactory==:获取SqlSession构建者对象的工厂接口
4. ==SqlSession==:用于执行Sql,管理事务,接口代理

>==核心配置文件==
>==environments标签用于记录不同配置环境,default指定默认环境,id为对应的唯一标识,transactionManager.type属性表示使用JDBC的默认事务处理模式,mappers标签实现核心中引入映射配置文件==



```java
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE configuration  
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"  
        "http://mybatis.org/dtd/mybatis-3-config.dtd">  
  
<configuration>  
    <environments default="mysql">  
        <environment id="mysql">  
            <transactionManager type="JDBC"/>  
            <dataSource type="POOLED">  
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>  
                <property name="url" value="jdbc:mysql://localhost:3306/db1?useSSL=false"/>  
                <property name="username" value="root"/>  
                <property name="password" value="123456"/>  
            </dataSource>  
        </environment>  
    </environments>  
    <mappers>  
        <mapper resource="studentMapper.xml"/>  
    </mappers>  
</configuration>
```




>==2.studentMapper.xml映射配置文件的详细解释,**其中增删改查方法只是略有不同**==



```java
<?xml version="1.0" encoding="UTF-8" ?>  
<!--MyBatis的DTD约束-->  
<!DOCTYPE mapper  
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  
<!--mapper:核心根标签-->  
<!--namespace属性:名称空间-->  
<mapper namespace="StudentMapper" >  
<!--    select查询功能标签-->  
<!--    id属性:唯一标识-->  
<!--    resultType属性:指定结果映射对象类型-->  
<!--    parameterType属性:指定参数映射对象类型-->  
<!--     注意增删改操作需要进行事务的提交,才会将操作结果记录在数据库,在openSession()加入true,事务可以自动提交-->  
    <select id="selectAll" resultType="com.ling.Beans.Student">SELECT * from student;</select>  
    <insert id="insert" parameterType="com.ling.Beans.Student">insert into student values (#{id},#{name},#{age})</insert>  
    <update id="update" parameterType="com.ling.Beans.Student">  
        update student SET name=#{name},age=#{age} where id=#{id}    </update>  
    <delete id="delete" parameterType="java.lang.Integer">  
        delete from student where id=#{id}    </delete>  
</mapper>
```



>==3.以查询为例,创建class测试类的全过程(入门案例):==

>![[Pasted image 20230927140725.png]]


# 2.外部加载properties文件

```java
<properties resource="jdbc.properties"/>
```

# 3.为全类名取别名
==在配置文件里面添加如下即可==
```java
<typeAliases>  
    <typeAlias type="com.ling.Beans.Student" alias="student"/>  
</typeAliases>
```

# 4.动态sql语句
	|对于不同的查询条件,我们无法将sql写死,于是mybatis给予我们新的解决方案
```java
<select id="selectCondition"  resultType="student" parameterType="student">  
    select * from student    <where>  
        <if test="id !=null">  
            id=#{id}        </if>  
        <if test="name !=null">  
            and name=#{name}        </if>  
        <if test="age !=null">  
            and age=#{age}        </if>  
    </where>  
</select>
```
==**1**采用where和if标签即可实现多条件查询==

```java
<select id="selectByIds" resultType="student" parameterType="list">  
    select * from student    
    <where>  
        <foreach collection="list" open="id in(" close=")" item="id" separator=",">  
        #{id}       
		</foreach>  
    </where>  
</select>
```

==**2**采用foreach可以对多个相同字段进行查询,比如多个ID的学生信息==

```java
//声明sql语句的引用
<sql id="select*">select * from student</sql>
//语句中引用
<include refid="select*"></include>
```

==**3**采用sql,include标签可以在任意处sql语句中抽取相同部分,并插入使用==

