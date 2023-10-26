# AOP
1. 概念: 面向切面编程,编程范式及思想
2. 作用:无侵入式编程,不改动源码的情况下,增添功能

>![[Pasted image 20230929221750.png]]

## AOP 详细步骤
1. *核心配置类中加入`@EnableAspectJAutoProxy`*,*开启切面自动代理*
2. *创建通知类,如下*
```java
@Component  
@Aspect  
public class MyAdvice {  
    @Pointcut("execution(void com.ling.dao.BookDao.update())")  
    public void pt(){}  
      
    @Before("pt()")  
    public void fn(){  
        System.out.println(System.currentTimeMillis());  
    }  
}
```
==`@Component`为自动装配为bean,`@Aspect `,为声明切面,pt()方法表明切入点,` @Pointcut("execution()")`为固定格式,声明切入点位置,`@Before,@After,@Around`为前置,后置,环绕方法,环绕常用==


## AOP切入点表达式
1. 标准表达式
>![[Pasted image 20230930131715.png]]

2. 通配符
>![[Pasted image 20230930132550.png]]

3. 注意事项
>![[Pasted image 20230930133152.png]]

## AOP通知类型
![[Pasted image 20230930140555.png]]
```java
Signature signature = pjt.getSignature();  
Class type = signature.getDeclaringType();  
String name = signature.getName();
```


==注意其中ProceedingJoinPoint为原始方法在代理方法内的切入点,原始方法有返回值的,需要接收并返回,类型为object==

==getSignature()方法返回对象可以获取对应类的具体信息==
 

>![[Pasted image 20230930141210.png]]

# Spring事务

1. *添加事务管理*
>![[Pasted image 20230930151318.png]]

2.  *Spring核心配置文件中加入*`@EnableTransactionManagement`

3. *设置事务管理器*
>![[Pasted image 20230930151847.png]]

### 事务角色

>![[Pasted image 20230930160326.png]]
==对于业务层调用数据层产生的事务,默认为事务管理员和事务协调员处于同一事务绑定,倘若想要某个事务协调员行为无论事务管理员成功与否,都将执行,那么可以采用`@Transactional(propagation = Propagation.REQUIRES_NEW)`==

*具体细节*
>![[Pasted image 20230930162308.png]]




