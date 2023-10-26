# 1.Spring注解开发(组件扫描)

```java
//该注释可以实现注解开发,自动配置及注入
@component
<context:component-scan base-package="XXX"/>
//以上可以开启组件扫描
//XXX里面填写需要扫描的package
```

```java
@component
//可以由三个效果相同的替代
@Service
//用于业务层
@Repository
//用于数据层
@Controller
//用于表现层
```

# 2.Spring全注解开发

## 2.1配置bean
```java
//需要配置的bean上添加注解
@Component  
public class DaoImpl implements Dao{  
    @Override  
    public void run() {  
        System.out.println("dao running>>>>>>>>>>");  
    }  
}
```

## 2.2创建配置类

```java
//第一个注解表明该类为配置类,替代XML配置方式
//第二个注解表示为扫描范围,括号里面指定范围
@Configuration  
@ComponentScan("com.ling.spring6.Dao")  
public class conFig{  
}
```

## 2.3生命周期方法

```java
@PostConstruct
//用于构造方法后,对应init()方法
@PreDestroy  
//用于销毁bean前,对应destory()方法
@Scope
//用于设置是否为单例
```

## 2.4依赖注入
```java
@Autowired
//可以实现引用类型的依赖注入,底层为暴力反射,可以不使用setter方法
@Qualifier("xxx")
//配合以上使用,可以解决容器中有多个相同类型bean的时候,可以指定需要使用的bean,具体为在括号里面取实现类的别名
@Value("")
//实现基本类型注入
@PropertySource("XXX")
//实现外部加载配置文件,常用于conFig.class文件上,可以以大括号的方式一次多加载
```

## 2.5管理第三方bean
```java
//1.首先为第三方bean创建方法,返回值为第三方对象
//2.其次,在其头部使用 @bean 注解
@bean()
//3.最后,使用 @import 添加在主SpringConfig class文件首部
@import({jdbcConfig.class})
```

## 2.6第三方bean的依赖
```java
//普通类型,创建成员变量,用 @value() 注入
@Value("com.mysql.jdbc.Diver")  
private String diver;
//引用类型,在 bean 定义方法内,给出形参即可
```
==如图==
>![[Pasted image 20230926205805.png]]

## 2.7测试注意点
==对于以下测试,基于全注解开发时,getBean()方法里面填写接口==
```java
@Test  
public void Test(){  
    ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);  
    BookDao bean = context.getBean(BookDao.class);  
    bean.save();  
}
```

