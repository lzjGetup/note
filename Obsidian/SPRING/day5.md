# SpringMVC

## 快速入门
1. ==导入SpringMVC和Servlet的坐标==
```java
<!--springMVC的依赖-->  
<dependency>  
    <groupId>org.springframework</groupId>  
    <artifactId>spring-webmvc</artifactId>  
    <version>6.0.9</version>  
</dependency>  
<!--servlet的依赖-->  
<dependency>  
    <groupId>javax.servlet</groupId>  
    <artifactId>javax.servlet-api</artifactId>  
    <version>3.1.0</version>  
    <scope>provided</scope>  
</dependency>
```

2. ==创建SpringMVC控制类,平替Servlet功能==
*`@RequestMapping`表明请求路径,倘若出现不同控制有同名方法,则可以把注解放在配置类上*



>![[Pasted image 20231001124948.png]]

3. ==初始化springMVC环境==

>![[Pasted image 20231001125156.png]]

4. ==初始化servlet容器,加载springmvc环境,并设置springmvc技术处理的请求==

>![[Pasted image 20231001125410.png]]


## 避免
==对于Spring项目,SpringMVC负责controller层,我们需要避免Spring配置类扫描controller层的bean==
*其中,excludeFilters属性表明需要过滤的包,type表示按照那种类型过滤,==FilterType.ANNOTATION==表示按照注解类型过滤,classes表示按照那种注解过滤*
>![[Pasted image 20231001131719.png]]

## GET,POST传递参数

1. 请求变量名和形参相同时,直接传参即可.引用数据类型,方法会创建引用数据类型的对象.引用数据类型里面有引用数据类型的,用`use.name`类似形式传递.
2. 请求变量名和形参不同时,用`@RequestParam("name")`形式绑定参数即可.

==JSON数据传递转换成对象==
`@EnableWebMvc`开启JSON数据转换
`@RequestBody`可以实现请求JSON数据里面信息传递给形参

>![[Pasted image 20231002102134.png]]


# RUST风格

==概述==
>![[Pasted image 20231002105555.png]]


==模式==
>![[Pasted image 20231002105625.png]]







