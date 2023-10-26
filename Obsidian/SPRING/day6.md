# SSM整合
## 异常处理
>![[Pasted image 20231002205107.png]]
==一般规定:所有异常都抛到表现层进行处理,且大多采用AOP思想,并且也自定义异常和为不同自定义异常编码.样例如下==


```java
@RestControllerAdvice  
public class Test { 
	//捕获所有异常类
    @ExceptionHandler(Exception.class)  
    public void solveException(Exception e){  
        System.out.println("solve Exception>>>");  
    }  
}
```

## 放行资源请求

*对于,SpringMVC项目,加载页面的请求会被当成是,post或其他请求,这时我们需要放行,HTML,CSS资源的访问*

>![[Pasted image 20231003094753.png]]


