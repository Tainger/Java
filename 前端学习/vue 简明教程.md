## vue 简明教程

​																																																			-- 后端程序猿

### Es6 语法

#### let声明变量

相对于var 声明变量， let声明的变量具有严格的作用域。

```javascript
{
	var a = 10;
	let b = 11;
}
console.log(a);
console.log(b);
```

### Vue 

#### mvvm思想

- M:  即 Model，模型， 包括数据和一些基本的操作。
- V： 即View， 视图模型， 页面渲染结果。
- VM： 即View-model， 模型与视图的双向操作（无需开发人员的干涉）

在mvvm 之前，开发人员从后端获取需要的数据模型，然后通过DOM操作Model渲染到View中的数据。而后当用户操作视图，我们还需要通过Dom获取VIew中的数据，然后同步到Model中。

而MVVM 中的 VM 要做的事情就是DOM操作完全封装起来，开发人员**不用再关心Model和View之间是如何相互影响的**。

##### Example:

![image-20201108094838892](/Users/rocky/Library/Application Support/typora-user-images/image-20201108094838892.png)

当model里的name 改变的时候，页面也随着改变

#### 插值表达式

在vm 和dom 元素相关联的情况下， 我们可以通过插值表达式对dom元素进行关联。

```javascript

```

##### 注： vm就相当于视图与模型的双向关联器

#### 双向绑定

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div id = "app">
        <input type="text" v-model = "num"></input>
        <h1> {{name}},你好帅 ,有{{num}} 为你点赞</h1>
        <button v-on:click = "num++">点责</button>
        <button v-on:click = "cancel()">取消</button>
    </div>

    <script src = "./node_modules/vue/dist/vue.js"></script>

    <script>
        // 1. vue声明式渲染，vm管控 id 为 app的dom元素。
      
        let vm = new Vue({
            el : '#app',
            data : {
                name : "张三",
                num : 1
            },
            methods: {
                cancel(){
                    this.num -- ;
                }
            },

        });
        //2.v-model 双向绑定， 模型变化， 视图变化，反之毅然。
    </script>
</body>
</html>
```

注： 模型改变，页面改变，反之毅然。

```
let vm = new Vue（{}）  声明式渲染
el: //绑定元素
data： //封装数据
method： 分装方法
```

#### 指令

##### 插值表达式

在vm 和dom 元素相关联的情况下， 我们可以通过插值表达式对dom元素进行关联。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div id = "app">
        <input type="text"> </input>
        <h1> {{name}},你好帅</h1>
    </div>

    <script src = "./node_modules/vue/dist/vue.js"></script>

    <script>
        // 1. vue声明式渲染，vm管控 id 为 app的dom元素。
        let vm = new Vue({
            el : '#app',
            data : {
                name : "张三"
            }

        });
    </script>
</body>
</html>
```

注：

- 该表达式支持js语法，可以调用**js内置函数**（必须有返回值）
- 表达式必须有返回结果。例如  1+1， 没有结果的返回值不允许使用。 如 let a = 1+1;
- 可以直接获取Vue实例中绑定元素中定义的数据和元素。
- 插值表达式只能放在标签体里面。（v-bind 可以在标签中绑定动态值）



##### v-text , v-html

v-text 会对所传入的字符串进行展示，假如你传的是html，会把html进行转义，把它作为字符串进行展示。

v-html会对传入的html，作为页面元素进行展示。

###### example

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <div id = "app">
        {{msg}} <br>
        <span v-html = "msg"></span> <br>

        <span v-text = "msg"></span> <br>
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>

    <script>
        new Vue({

            el : "#app",
            data : {
                msg : "<h1> 窝头 </h1>"
            },
            methods: {
                
            },
        })

    </script>
</body>
</html>
```

![image-20201108102750567](/Users/rocky/Library/Application Support/typora-user-images/image-20201108102750567.png)

**作用：** 解决{{}}插值表达式闪烁问题。

##### v-bind

单向绑定

在标签内显示vue实例中的数据。这个是单向绑定，vue实例中的数据改变，那么实例中的数据改变。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div id = "app">
        <a v-bind:href="href">超链接</a>

    </div>

    <script src="./node_modules/vue/dist/vue.js"></script>

    <script>
        new Vue({
            el : "#app",
            data : {
                style : "true",
                href : "http://www.baidu.com"
            },
            methods: {
                demo(){
                    return 1+1;
                }
            }
        })
    </script>
</body>
</html>
```

##### V-model 

双向绑定,用于表单自定义组件。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div id = "app">
        <input type="checkbox" v-model = "language"  value="java"> JAVA <br>
        <input type="checkbox"  v-model = "language" value="c++"> c++  <br>
        <input type="checkbox"  v-model = "language" value = "c">  c   <br>

        {{language.join(',')}}
    </div>

    <script src="./node_modules/vue/dist/vue.js"></script>

    <script>
        let vm = new Vue({
            el : "#app",
            data : {
                language : []
            },
            methods: {
                
            }
        })
    </script>
</body>
</html>
```

##### v-on

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div style="border: 1px red solid;">
        nima
        <div style="border: 2px blue solid;">
            woqu
        </div>
    </div>
    
    <br>

    <div style="border: 2px blue solid;">
        woqu
    </div>

    <div id = "app">
        <input v-model:value="num">
        <button v-on:click="commet">点赞</button>
        <button v-on:click="cancel">踩</button>
    </div>

    <script src="./node_modules/vue/dist/vue.js"></script>

    <script>

        let vm = new Vue({

            el : "#app",
            data : {
                num : 0
            },
            methods: {
                cancel(){
                    this.num-- ;
                },
                commet(){
                    this.num++ ;
                }
            },
        })

    </script>
</body>
</html>
```

###### 事件修饰符



###### 按键修饰符











##### v-for

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div id = "app">
        <ul>
            <!-- 1.显示user信息  v-for = “（index, item）in items” -->
            //遍历数组
            <li v-for = "(item, index) in users">

                当前索引 {{index}}  ===> {{item.name}}   =====> {{item.age}} ========> {{item.identity}}
                <br>
                <span v-for = "(v, k, i) in item">
                    name:{{v}} ====> age: {{k}} ======> index: {{i}}
                </span>
            </li>
            //遍历对象
            <!-- 3.  遍历对象
                    v-for = "value in object"
                    v-for = "(item, index) in object"
                    v-for = "(value, key, index) in object"
            -->
           
            <!--  4. 遍历增加索引提高渲染效率  -->
            <ul>
                <li v-for = "(item, index) in nums" ::key="index">
                    {{item}} ======> {{index}}
                </li>
            </ul>
        </ul>
    </div>


    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        
        let vm = new Vue({
            el : "#app",
            data : {
                users : [
                    {"name": "贾知远", "age": 20, "identity": "身份"},
                    {"name": "张三", "age": 21, "identity":"难顶"},
                    {"name": "李四", "age": 22, "identity":"错误"},
                ],
                nums : [5, 5, 6, 6, 6, 6, 2, 3, 4, 5, 6]
            },
            methods: {
                
            },
        })


    </script>
</body>
</html>
```

#### 计算属性和监听器

