# Dubbo 调用

## 一 Dubbo 快速入门

### 快速演示Dubbo的远程调用

dubbo引入









dubbo默认依赖

![image-20210908080352213](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210908080352213.png)

- javassit
- spring-context 依赖上下文

### 编写代码

#### 客户端需要对象

- ServiceConfig
- ProtocolConfig
- ApplicationConfig

#### 服务端需要的对象

- ReferenceConfig
- ApplicationConfig



#### demo1

没有配置注册中心,dubbo-server

```java
public class SimpleServer {

    public void openService(int port) {

        //服务配置
        ServiceConfig serviceConfig = new ServiceConfig();
        //设置服务接口
        serviceConfig.setInterface(UserService.class);
        //设置开放协议
        serviceConfig.setProtocol(new ProtocolConfig("dubbo", port));
        //设置一个空的注册中心
        serviceConfig.setRegistry(new RegistryConfig(RegistryConfig.NO_AVAILABLE));
        //设置服务当前的应用
        serviceConfig.setApplication(new ApplicationConfig("simple-app"));
        //设置服务实现对象
        serviceConfig.setRef(new UserServiceImpl());
        //暴露服务
        serviceConfig.export();

        System.out.println("服务已开启:" + port);
    }

    public static void main(String[] args) throws IOException {
        new SimpleServer().openService(20880);
        System.in.read();
    }
}
```

youngClient

```java
public class YoungClient {

    public UserService buildRemoteService(String remoteUrl) {
        ReferenceConfig<UserService> referenceConfig = new ReferenceConfig<>();
        referenceConfig.setInterface(UserService.class);
        referenceConfig.setUrl(remoteUrl);
        referenceConfig.setApplication(new ApplicationConfig("young-app"));
        return referenceConfig.get();
    }

    public static void main(String[] args) {
        YoungClient client = new YoungClient();
        UserService service = client.buildRemoteService("dubbo://127.0.0.1:20880/simple.dubbo.service.UserService");
        int user = service.getUser(100);
        System.out.println(user);
    }
}
```



#### 分布式配置中心

不能动态的增减服务，解藕 

