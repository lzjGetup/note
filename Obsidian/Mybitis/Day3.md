# Mybatis注解开发
==以select命令为例,展开详细步骤==
1. 创建Mapper接口,在接口中定义方法,在方法上方添加==@select==注解
2.在核心配置文件的mapper标签中,package属性中表明接口位置
*1*
```java
public interface StudentMapper {  
    @Select("select * from student")  
    public abstract List<Student>selectAll();  
}
```
*2*
```java
<mappers>  
    <package name="com.ling.Mapper"/>  
</mappers>
```

==其他语句同理==
```java
public interface StudentMapper {  
    @Select("select * from student")  
    public abstract List<Student>selectAll();  
  
    @Insert("insert into student values(#{id},#{name},#{age});")  
    public abstract int insert(Student stu);  
  
    @Update("update student set name=#{name},age=#{age} where id=#{id}")  
    public abstract int update(Student stu);  
  
    @Delete("delete from student where id=#{id}")  
    public int delete (Integer id);  
}
```

==**使用注解大大简化开发,不必再编写mapper映射文件**==

## 一对一查询注解
==简单环境==
```java
public class Card{
private Integer id;private String number;private Person p;
}
public class Person{
private Integer id;private String name;private Integer age;
}
//其中在数据库中card表pid字段外键依赖person表的主键
```
==配置接口==
```java
public interface PersonMapper {  
    @Select("select * from person where id=#{id}")  
    public abstract Person selectById(Integer id);  
}
//根据id一对一查询
```

```java
public interface CardMapper {  
    @Select("select * from card")  
    @Result(column = "id", property = "id")  
    @Result(column = "number", property = "number")  
    @Result(  
            property = "p",  
            javaType = Person.class,  
            column = "pid",  
            one = @One(select = "com.ling.Mapper.PersonMapper.selectById")  
    )  
    public abstract List<Card> selectAll();  
}
```
==其中各个属性表意如下==
![[Pasted image 20230929113700.png]]


## 一对多查询
==与一对一查询的大体格式相同,其中对于"多"的那方的引用数据类型,需要用many=@many格式==


```java
@Result(  
        property = "students",  
        javaType = List.class,  
        column = "id",  
        many = @Many(select = "com.ling.Mapper.StudentMapper.selectByCid")  
)
```
==需要注意的是,此处应该对引用数据类型里面的包含的对象设置关联方法, column = "id",是二者查询连接的关键==
```java
//一对多查询  
@Select("select * from student where cid=#{cid}")  
public abstract List<Student>selectByCid(Integer cid);
```

## 多对多查询
==类似于一对多查询,需要注意的点是,多对多查询需要通过中间表建立连接关系,不展开详细介绍==
[多对多](https://www.bilibili.com/video/BV1UB4y197vr?p=56&vd_source=c9f01c4138ffca623361215fe6c00336)

