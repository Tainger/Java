# 自定义Mybatis框架

#### 链接数据源的信息

```xml
<dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?characterEncoding=utf-8&amp;
                useSSL=false&amp;serverTimezone=Hongkong"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
</dataSource>
```

有了数据库的信息，就能创建Connection对象。

#### 映射配置信息

```xml
<mappers>
        <mapper resource="com/itheima/dao/UserDao.xml"></mapper>
</mappers>
```

有了它，就能读取sql语言的配置信息。

#### sql语句与方法的映射信息

```xml
<mapper namespace="com.itheima.dao.UserDao">
    <select id="findAll" resultType="com.itheima.dao.entity.User">
        select * from user;
    </select>
</mapper>
```

有了它就有了执行sql语句，就可以获取PreapareStatement

#### 读取以上三个配置文件的技术 

用到的技术是解析xml的技术，此处用的就是解析dom4j的技术

#### 接口代理



#### 实现思路

-  

