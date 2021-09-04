# 排查cpu使用过高的方法

#### 模拟cpu占高比的环境
##### 编写高占比代码
```java

@RestController
@RequestMapping("/api/v1/device")
public class PostController {

    @GetMapping("get")
    public BaseModel testParam(){
        BaseModel baseModel = new BaseModel();
        baseModel.setBmpId(111L);
        while (true) {
            System.out.println(666);
        }
    }
}
```
##### 打包
```java
mvn clean package -Dmaven.test.skip=true
```

##### 上传linux 环境 并 运行

```java
 java -jar  stackoverflow-cn-1.0-SNAPSHOT.war
```
##### 查看占用cpu高的进程

```java
top
```

![image-20210905002521753](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905002521753.png)

##### 查看Pid 为4512中最耗cpu的子线程

```java
top -p 4512 -H
```

![image-20210905002810072](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905002810072.png)

##### 将最耗cpu线程的pid号转换为16进制

```java
print "%x \n" 4784
```

![image-20210905003203067](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905003203067.png)

##### 利用jstack 查看出问题的代码位置

```java
jstack 4512 | grep 12b0 -A 30
```

![image-20210905003455673](https://we-take-bucket.oss-cn-beijing.aliyuncs.com/imgimage-20210905003455673.png)

