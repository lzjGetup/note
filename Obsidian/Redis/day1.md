# 非关系型数据库
1. 键值型数据库
2. 文档型数据库
3. 图型数据库
>![[Pasted image 20231022101511.png]]

>![[Pasted image 20231022102430.png]]

# 简介
![[Pasted image 20231022103014.png]]

# 客户端
>![[Pasted image 20231022103719.png]]

# Jedis入门
>![[Pasted image 20231022110006.png]]
>![[Pasted image 20231022111549.png]]

# Jedis连接池

>![[Pasted image 20231022111823.png]]


# SpringDataRedis
## 入门
>![[Pasted image 20231022114611.png]]

## 设置序列化器
为SpringDataRedis设置序列化器,一是String序列化器,用于字符序列;二是json字符序列化器,用于java对象序列化.
```java
@Configuration  
public class RedisConfig {  
    @Bean  
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) throws UnknownHostException {  
        //创建Template  
        RedisTemplate<String, Object> redisTemplate = new RedisTemplate<>();  
        //设置连接工厂  
        redisTemplate.setConnectionFactory(redisConnectionFactory);  
        //设置序列化工具  
        GenericJackson2JsonRedisSerializer JsonRedisSerializer = new GenericJackson2JsonRedisSerializer();  
        //key和hashKey采用string序列化器  
        redisTemplate.setKeySerializer(RedisSerializer.string());  
        redisTemplate.setHashKeySerializer(RedisSerializer.string());  
        //value和hashValue采用json序列化  
        redisTemplate.setValueSerializer(JsonRedisSerializer);  
        redisTemplate.setHashValueSerializer(JsonRedisSerializer);  
        return redisTemplate;  
    }  
}
```

==需要注意的是,对于json自动序列化,其会添加对象类路径,造成内存浪费==
*如图*
>![[Pasted image 20231022144741.png]]

**"@class:xxx"**
属于json自动序列化带来的类路径,为此,我们需要手动书写序列化json数据

==改进序列化方案==
使用StringRedisTemplate+序列化工具,手动实现
```java
@SpringBootTest  
public class StringRedisTemplateTest {  
    @Autowired  
    private StringRedisTemplate stringRedisTemplate;  
    private static final ObjectMapper MAPPER=new ObjectMapper();  
      
    @Test  
    void testUser() throws JsonProcessingException {  
        //创建对象  
        User u=new User("ling",100);  
        //手动序列化  
        String json = MAPPER.writeValueAsString(u);  
        //写入数据  
        stringRedisTemplate.opsForValue().set("user:1",json);  
        //获取数据  
        String jsonUser = stringRedisTemplate.opsForValue().get("user:1"); 
        //手动反序列化  
        User user = MAPPER.readValue(jsonUser, User.class);  
        System.out.println(user);  
    }  
}
```


# 基于session登录
>![[Pasted image 20231022165410.png]]

```java
session.setAttribute();
//设置保存session信息;
```






