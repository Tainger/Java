# html概念介绍

## 概念

1. Hyper Text Markup language 超文本标记语言
   1. 超文本：使用超链接方法，将各种不同的文字信息组织在一起的网状文本。
   2. 标记语言：由标签构成的语言，<标签名>如html,xml。标记语言不是编程语言
2. html是完成页面内容的展示

## 快速入门

1. 语法

   1. html文档的后缀名 .html 或者 .htm
      1. 围堵标签
      2. 开始标签和结束标签。如：<html></html>
      3. 自闭合标签：开始和结束标签在一起。如<br/>
      4. 标签可以嵌套：需要正确嵌套，不能你中有我，我中有你。 错误：<a><b></a><b/> 正确：<a><b></b></a>
      5. 在开始标签中可以定义属性。属性是由键值对构成的，值需要用引号（单双都可）引起来。
      6. html的标签不区分大小写，但是都建议使用小写。

2. 代码

   ```javascript
   <!DOCTYPE html>  //表示这是一个html文档类型,另一种是xml
   <html lang="en"> //表示html是采用哪种语言
   <head>
       <meta charset="UTF-8">  //html采用哪种编码方式
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>  //html标题
   </head>
   <body>
       
   </body>
   </html>
   ```

## 标签学习

1. 文件标签:构成html最基本的标签

   - html：html文档的根标签
   - head：头标签。用于指定html文档的一些属性。引入外部资源，<style></style>就是放在head标签的。
   - title：标题标签
   - body：一个浏览器除了导航栏下面都是body部分了

2. 文本标签

   - 注释<!-- -->

   - 换行标签<br>

   - 标题标签 <h1></h1>,随着字号增大而逐渐变小。

   - 段落标签<p></p>

   - 水平线标签</hr>

     - 
     - 
     - 
     - 
     - 属性
       - color：颜色
       - width：宽度
       - size：尺寸
       - align:对齐方式

   - 加粗标签<b></b>

   - 斜体标签<i></i>

   - ~~字体标签<font></font>设置字体的大小~~

     - 属性
       - color 
       - size
       - face

   - 属性定义

     - color

       ​	![image-20200530122441855](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200530122441855.png)

     - width

     ​          ![image-20200530122507312](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200530122507312.png)

   - 居中标签<center></center> 使元素在父元素中居中。

1. 图片标签
   - <img src=""></img>
   - 属性：
     - src图片的目录。./代表当前目录(./也可以省略)，../代表当前目录的上级目录
2. 列表标签
   - 有序列表
     - ol
     - li
   - 无序列表
     - ul
     - li
3. 链接标签
   - 定义一个超链接标签
     - 属性
       - href:指定访问资源的url
       - target：指定打开资源的方式
         - _self在自己的页面打开
         - _blank在一个新的界面开发

### 块标签

#### span标签

作用：文本内容在同一行进行展示，不会换行且没有任何的样式，便于css进行美化。称为行级标签。

#### div标签

作用：文本内容占同一行且没有任何的样式，便于css进行美化。称为块级标签。

### 语义化标签

作用：html5为了提高代码可读性，提供了一些标签。

举例：<header></header>

​           <footer></footer>

### 表格标签

作用：html初期作为布局和展示来使用

有水平拆分和垂直拆分

### 表单标签

- 概念：用于采集和收集用户的数据，用于和服务器进行交互
- form：用于定义一个表单，可以定义一个范围，可以代表采集一个用户的范围。
  - 属性：
    - action:指定采集数据的url
    - method：指定提交方式
      - 一共有七种方式，常用的有两种
        - Get
          - 请求参数会在地址栏中显示
          - 请求参数的长度是有限制的
        - Post
          - 请求参数不会在地址栏显示
          - 请求参数的大小没有限制
  - 表单中的数据要想提交，必须指定他的name属性
- 表单项标签
  - Input:可以通过type属性的值改变元素展示样式
  - select：下拉列表
  - textarea：文本域



 

### 标签属性

- h5的标签已经不支持属性，已经用css代替了。但是为了向下兼容其他版本但是还是会显示。

## 特殊字符

对于一些特殊字符，html页面是采用一些特殊编码进行转义。如果我们想要在文本显示多个空格，我们敲好几个空格但是只能显示一个空格。像一些版权特殊字符都要转义。

![image-20200530133358343](C:\Users\rocky\AppData\Roaming\Typora\typora-user-images\image-20200530133358343.png)

# 案例

## 公司简介



## 表格

## 旅游网站

## 分析

- 因为还没有学过css,使用table来进行布局

- 如果一行只有一个单元格，则使用

  ​	<tr><td></td></tr>

- 如果一行有多个单元格，则使用

  <tr><td><table></table></td></tr>

# 注册页面的实现

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <table align="center" margin-left="25%" border="1" width="50%"  cellspacing="0" cellpadding="10">
        <tr>
            <td>
                <label for="zhanghao">用户名</label>
            </td>
            <td>
                <input  type="text" placeholder="请输入账号：" name="zhanghao" id="zhanghao">
            </td>
        </tr>

        <tr>
            <td>
                密码
            </td>
            <td>
                <input type="password" placeholder="请输入密码：" name="password" >
            </td>
        </tr>

        <tr>
            <td>
                E-mail
            </td>
            <td>
                <input type="text" placeholder="请输入邮箱：" name="mail">
            </td>
        </tr>


        <tr>
            <td>
                姓名
            </td>
            <td>
                <input type="text" placeholder="请输入姓名：" name="name">
            </td>
        </tr>

        <tr>
            <td>
                手机号
            </td>
            <td>
                <input placeholder="请输入手机号：" name="phone">
            </td>
        </tr>

        <tr>
            <td>
                性别
            </td>
            <td>
               <input type="radio" name="sex" value="male">男
               <input type="radio" name="sex" value="female">女
            </td>
        </tr>

        <tr>
            <td>
                出生日期
            </td>
            <td>
               <input type="date" >
            </td>
        </tr>

        <tr>
            <td>
                <label for="active_code">验证码</label>
            </td>
            <td>
               <input type="text"  name="active_code" id ="active_code">
               <img src="image/jiangxuan_1.jpg" width="20px">
            </td>
        </tr>
    </table>
</body>
</html>
```

