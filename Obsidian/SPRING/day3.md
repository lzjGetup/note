# 1.Spring整合Mybatis
==传统mybatis,采用xml配置文件的方式进行配置,spring整合mybatis方法更加简单易懂==
*步骤*
1. ==pom文件导入相关依赖==
```java
<!--mybitis的依赖-->  
        <dependency>  
            <groupId>org.mybatis</groupId>  
            <artifactId>mybatis</artifactId>  
            <version>3.5.11</version>  
        </dependency>  
<!--spring-Mybatis整合-->  
        <dependency>  
            <groupId>org.mybatis</groupId>  
            <artifactId>mybatis-spring</artifactId>  
            <version>3.0.2</version>  
        </dependency>
<!--jdbc的依赖-->  
<dependency>  
    <groupId>org.springframework</groupId>  
    <artifactId>spring-jdbc</artifactId>  
    <version>5.3.29</version>  
</dependency>
```

2. ==spring核心配置类文件加入inport语句导入(类比管理第三方bean)==

>![[Pasted image 20230929214429.png]]
==@value对属性注入==
![[Pasted image 20230929214659.png]]
==@bean管理第三方bean,分别对应原始sqlSession工厂方法,Mapper映射文件==

>![[Pasted image 20230929214723.png]]


# 2.Spring整合JUnit
1. 指定专用的类运行器
2. 指定配置类
>![[Pasted image 20230929220055.png]]



