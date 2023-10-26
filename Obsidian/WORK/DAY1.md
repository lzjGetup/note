# 1.会话技术
>![[Pasted image 20231011111340.png]]

==每次http请求,服务器都会开启一个新的线程==

# 2.会话跟踪方案
1.  cookie(存储在浏览器,不安全)
2. Session(存储在服务器,无法跨域)
3. Jwt(json wed token)(企业主流令牌技术)

==JWT==
>![[Pasted image 20231011111918.png]]

# 3.MD5加密
*MD5是采用的加密方式*
[MD5加密](https://blog.csdn.net/Oliver_xpl/article/details/90214896)

# 4.Nginx反向代理负载均衡
==反向代理==

>![[Pasted image 20231011112617.png]]

==负载均衡==
>![[Pasted image 20231011112633.png]]


# 5.新增业务流程

## 5.1控制层

1. 在controller层定义方法
2. 根据Rest风格的请求方式在方法上加入注解
3. 加入swagger注解以便在文档中获得方法详细信息
4. 加入日志调试信息

*例如*
```java
@PostMapping  
@ApiOperation("新增员工")  
public Result save(@RequestBody EmployeeDTO employeeDTO) {  
    log.info("新增员工:{}", employeeDTO);  
    employeeService.save(employeeDTO);  
    return Result.success();  
}
```
==其中,XXDTO对象是实现数据在各个内部层次之间传递数据的载体==
## 5.2业务层

### 接口
**定义方法即可**
```java
void save(EmployeeDTO employeeDTO);
```

### 实现类
**1.实现方法和业务逻辑**
**2.调用持久层方法**

```java
@Override  
public void save(EmployeeDTO employeeDTO) {  
    Employee employee = new Employee();  
    //对象属性拷贝  
    BeanUtils.copyProperties(employeeDTO, employee);
    //调用持久层  
    employeeMapper.insert(employee);
}
```

==数据库存储对象为实体entity,DTO对象包含属性和实体对象包含属性不一样,因此,需要进行属性拷贝==


## 5.3持久层
==主要面向数据库,一般两种方式==

1. Mapper软件包下定义接口,基于注解实现

```java
//接口方法中加入注解
@Select("select * from employee where username = #{username}")  
Employee getByUsername(String username);
```

2. Resources.Mapper包下定义XML文件(Mybatis原始方式,针对复杂sql语句)

```java
//mybatis select标签等
<select id="pageQuery" resultType="com.sky.entity.Employee">  
    select * from employee
    <where>  
        <if test="name!=null and name!=''" >  
	        and name like concat('%',#{name},'%')
        </if>  
    </where>  
    order by create_time desc
</select>
```


# 6.自定义注解及常量
```java
import com.sky.enumeration.OperationType;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
/**  
 * 自定义注解,用于标识某方法需要进行功能字段自动填充处理  
 */  
@Target(ElementType.METHOD)  
@Retention(RetentionPolicy.RUNTIME)  
public @interface AutoFill {  
    //数据库操作类型UPDATE INSERT  
    OperationType value();  
}
```

```java
public enum OperationType{
	UPDATE,
	INSERT
}
```

==@Retention的作用是定义被它所注解的注解保留多久,三种策略==
1. SOURCE  被编译器忽略
2. CLASS  注解将会被保留在Class文件中，但在运行时并不会被JVM保留。这是默认行为，所有没有用Retention注解的注解，都会采用这种策略.
3. RUNTIME 保留至运行时。所以我们可以通过反射去获取注解信息。

**ElementType.METHOD**表明在方法上使用
**OperationType** 为自定义枚举类型

==此操作可以实现在业务代码运行时,通过反射获取到对应请求的对数据库的哪种操作,因此可以区别对待不同数据库操作,比如delete和insert操作==

# 7.常量类
==对于经常使用的基本类型,如String,int,通常在项目中定义常量类来存储==
```java
/**  
 * 状态常量，启用或者禁用  
 */  
public class StatusConstant {  
    //启用  
    public static final Integer ENABLE = 1;  
    //禁用  
    public static final Integer DISABLE = 0;  
}

/**  
 * 信息提示常量类  
 */  
public class MessageConstant {  
  
    public static final String ALREADY_EXISTS="已存在";  
    public static final String PASSWORD_ERROR = "密码错误";  
    public static final String ACCOUNT_NOT_FOUND = "账号不存在";
}
```

# 8.配置属性类
==作用:为yml配置文件提供配置属性名称==
*例如阿里云连接配置*
```java
@Component  
@ConfigurationProperties(prefix = "sky.alioss")  
@Data  
public class AliOssProperties {  
  
    private String endpoint;  
    private String accessKeyId;  
    private String accessKeySecret;  
    private String bucketName;  
  
}
```












