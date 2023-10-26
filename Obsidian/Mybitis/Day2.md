# 1.多表操作

## 1.1 一对一查询,封装
```java
<!--  
namespace:声明mapper文件位置  
resultMap:用于表示查询结果集如何存储转变成对象  
    id属性:对应select标签中的id  
    type属性:封装数据的目标对象  
id(resultMap内的标签):主键  
result:其他字段  
association:用于引用数据类型的注入  
    column:表示数据库中的字段  
    property:表示类中的属性  
    javaType:引用数据类型的java类名(一般用别名)  
-->  
<mapper namespace="com.ling.Table01.OneToOneMapper">  
<resultMap id="OneToOne" type="card">  
    <id column="cid" property="id"/>  
    <result column="number" property="number"/>
    //  improtant
    <association property="p" javaType="person">  
        <id column="pid" property="id"/>  
        <result column="name" property="name"/>  
        <result column="age" property="age"/>  
    </association>  
	//   improtant
</resultMap>  
<select id="selectAll" resultMap="OneToOne">  
    select c.id cid,number,pid,name,age from card c,person p where c.pid=p.id;</select>

```

>==注意点==:**核心MybatisConFig.xml文件中需要  1.加载jdbc.properties文件  2.为java对象设置别名  3.用Mappers标签声明mapper.xml文件的全路径.==重点在于association标签对应用数据类型的装配==**


## 1.2 一对多查询,封装(多对多类似)
```java
<resultMap id="oneToMany" type="classes">  
        <id column="cid" property="id"/>  
        <result column="cname" property="name"/>  
<!--        一对多,采用集合数据类型等装载对象-->  
<!--        property属性:属性名 ofType属性:集合里面的对象名-->  
        <collection property="students" ofType="student">  
            <id column="sid" property="id"/>  
            <result column="sname" property="name"/>  
            <result column="sage" property="age"/>  
        </collection>  
    </resultMap>
```

>==注意点==:**与一对多不同点在于resultMap 里面采用collecttion标签,==重点在于collection标签对集合数据类型的装配==**




