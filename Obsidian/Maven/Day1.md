# Maven简介

1. *概述*

>![[Pasted image 20231001160029.png]]

2. *POM*

**POM 是 Project Object Model 的缩写，即项目对象模型。**

**pom.xml 就是 maven 的配置文件，用以描述项目的各种信息。**


3. *依赖*

>![[Pasted image 20231001160304.png]]

```java
//排除依赖
<exclusions>  
    <exclusion>
    //该标签可以排除依赖(不想使用别的模块带来的传递依赖)
```

```java
//可选依赖
<optional> true</optional>
//表明不想让外部引用知道内部的依赖
```



4. *生命周期(常用)*

>![[Pasted image 20231001160433.png]]

# Maven高级

## 分模块开发与设计
**在项目中,对于多个模块之间都需要共同使用的类,通常抽取该模块使用**

==首先,将模块下载到maven的个人仓库下,采用生命周期的install方法.其次,类比如下==
```java
<!--XX模块的依赖-->  
<dependency>  
    <groupId>com.ling</groupId>  
    <artifactId>myproject-mylen</artifactId>  
    <version>1.0.1</version>  
</dependency>
```


## 继承与聚合
*聚合*

==多模块相互依赖时,底部变动,导致上层也需要重构,这个时候需要聚合工程来处理==

>![[Pasted image 20231001164023.png]]

*继承*
>![[Pasted image 20231001200305.png]]
==作用==

1. 减少配置
2. 减少版本冲突

==注意==
1. 父工程的依赖,一般IDEA里面的Maven项目的子模块是直接默认全部继承的
2. 对于部分模块的特有的依赖,用`<dependencyManagement>`进行管理.


## 属性
```java
<properties>  
    <spring.version>6.0.9</spring.version>  
</properties>  
<dependencies>  
    <dependency>  
        <groupId>org.springframework</groupId>  
        <artifactId>spring-context</artifactId>  
        <version>${spring.version}</version>  
    </dependency>  
</dependencies>
```

**属性设置可以统一版本号**

## 多环境开发
>![[Pasted image 20231001204707.png]]

