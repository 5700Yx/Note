# 基础编程

**包括**<br>
$
\qquad\begin{cases}
    \small Java常用工具类 \\
    \small Java集合框架 \\
    \small JDBC编程技术 \\
\end{cases}
$

## JDBC编程

- 同一个数据库**建立连接**
- 向数据库**发送语句**
- 从数据库**返回结果**

### JDBC数据库编程基本步骤

1. 将**驱动程序导入到工程**，程序中加载驱动

```java
    Class.forName("com.mysql.jdbc.Driver");
    // 高版本路径为 "com.mysql.cj.jdbc.Driver" ，无需手动调用
```

2. 创建来连接对象`Connection`

```java
    Connection connection = DriverManager.getConnection("jdbc:mysql://120.0.0.1:3306/support", "root", "password")
```

3. 在连接对象上创建命令对象`Statement`

```java
    Statement cmd = connection.createStatement();
```

4. 执行`SQL`语句

```java
    String sql = "SELECT * FROM user_table";
    ResultSet rs = cmd.executeQuery(sql);

    while(rs.next()) {
        // 每次循环读取一行数据
    }
```

5. 关闭连接

```java
    connection.close();
```

## XML

### XML基本概念

- XML指**可扩展标记语言**
- XML的设计宗旨是**传输数据**
- XML可用于**存储数据**
- XML可用于**交换数据**

1. 必须有声明语句
   - XML声明是XML文档的第一句，其格式如下
    ```xml
        <?xml version="1.0" encoding="utf-8"?>
    ```
2. XML文档有且只有一个根元素
   - 良好格式的XML文档必须有一个根元素，就是紧接着声明后面建立的第一个元素，其他元素都是这个根元素的子元素，根元素完全包括文档中其他所有的元素
3. 区分大小写
   - 在XML文档中，大小写存在区别，`A`和`a`是不同的标记
4. 所有的标记必须有相应的结束标记
   - 所有标记必须成对出现，有一个开始标记，就必须有一个结束标记，否则会被视为错误。
   - 所有标记必须正确嵌套
5. 属性值使用引号
   - 所有属性值必须用引号修饰（可以是单引号，也可以是双引号，推荐使用双引号），否则会被使为错误
6. 注释
    ```xml
            <!--> comment </!-->
    ```
    ```xml
            <!--
                comment
            -->
    ```

### 基于JDOM项目对XML编程

- 主要API
    ```java
        SAXBuilder.build(FileInputStream("*.xml")); //获取xml文件，返回Document实例
        Element.getChildren(); //获取该节点的所有子节点，返回List
        Element.getChild(); //获取指定子节点实例
        Element.getAtrribute(); //获取指定节点属性的value
        Element.getText(); //获取该节点的节点文本
        Document(new Element()); //新建xml文件文档
        Document.getRootNote(); //获取根节点。
        Element.addContent(Element); //添加子节点
        Element.setAttibute();添加节点属性
        Element.setText(); //添加该节点的文本值,
        xmloutPutter(Fommat.getPrettyFormat());
        xmlOutPutter.output(Document, FileOutPutStream);
        //输出xml文件，其中Document为xml文档对象，FileoutPutStream为文本输出流
    ```

# 网页编程

## HTML 文档的基本结构

```html
<!DOCTYPE html>
<html lang = "zh-CN">
    <head>
        <meta charset = "UTF-8">
        <title></title>
    </head>
    <body>
        <h1>Hello world!</h1>
    </body>
</html>
```

`<!DOCTYPE html>` 文档类型声明，必须位于文档第一行

`<html>` 根元素，包裹整个页面

`<head>` 头部，其中信息（编码、标题、引入的 `CSS` ），不直接显示

`<title>` 页面标题，仅显示在浏览器标签页上

`<body>` 主体

`<meta charset = "UTF-8">` 声明字符编码

## 超链接 `a`

```html
<a href = "https://github.com/dashboard" target = "_blank">Github Dashboard</a>
<!--跳转到外部网址-->

<a href="#section2">跳转至第二节</a>
<!--跳转到页内锚点，即本页指定位置#id -->
```

`href` 指定目标地址，是超链接的核心属性

`target = "_blank"` 在新标签页中打开，避免用户离开本站

## 列表

```html
<ul>
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
</ul>
<!--无序列表-->

<ol>
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
</ol>
<!--有序列表-->
```

## 页面区域

- div：**块级容器**

    独占一行，用于**把页面分为页头、主体、页脚等区域**，本身没有任何默认样式

    ```html
    <div id = "header">页头区域</div>
    <div id = "main">
        <p>主体内容</p>
    </div>
    <div id = "footer">页脚区域</div>
    ```

- span：**行内容器**
  
    不独占一行，用于包裹一句话中的数个关键字，以便 `CSS` 为其设置样式

    ```html
    <p>span 标签可以用于修改关键字的样式，如
        <span class = "highlight">高光</span>
    </p>
    ```

## 表格

## 表单

**用户向服务器提交数据的唯一入口**

```html
<form action = "RegisterServlet" method = "post">
    用户名：<input type = "text" name = "username">
    <input type = "submit" value = "提交">
</form>
```

- 要提交的**所有控件必须写在 `form` 容器内**，不在其中的容器不会被提交
- 一个页面中可以有多个 `form` ，但每次只提交一个

### 常用表单控件

| 控件 | 写法 | 说明 |
| -- | -- | -- |
| 文本框 | `<input type="text" name="username">` | 单行文字输入 |
| 密码框 | `<input type="password" name="pwd">` | 输入内容掩码显示为圆点 |
| 单选按钮 | `<input type="radio" name="gender" value="male">` | name相同才算同一组，才能互斥 |
| 复选框   | `<input type="checkbox" name="hobby" value="read">` | 可多选；同name的值以数组提交 |
| 下拉列表 | `<select name="province"><option>...</option>` | 选项写在option中，省空间 |
| 文本域   | `<textarea name="intro" rows="4"></textarea>` | 多行文本，用于简介、备注 |
| 隐藏域   | `<input type="hidden" name="source" value="campus">` | 用户看不到，但会随表单提交 |
| 提交按钮 | `<input type="submit" value="提交注册">` | 点击后发送整个表单 |

## CSS

- $CSS$指层叠样式表$(Cascading Style Sheets)$
- $CSS$描述类如何在屏幕、纸张或其他媒体上显示$HTML$元素
- $CSS$用于定义网页的样式，包括针对不同设备和屏幕尺寸的设计和布局
- $CSS$的作用就是给$HTML$、页面标签添加各种样式、定义网页的显示效果

### CSS的书写方式

- $CSS$的书写方式有三种
  1. 行内样式：在某个特定的标签里采用`style`属性，范围只针对此标签
  2. 内嵌样式（内联样式）：在界面的`head`标签里采用`<style>`标签，范围针对此页面
  3. 外链样式：引入外部样式表$CSS$文件
     1. **采用`<link>`标签**
     2. **采用`import`引用**

### CSS的基本选择器

- $CSS$选择器：指定$CSS$要作用的标签，标签的名称就是选择器（即选择指定容器）
- $CSS$的选择器分为基本选择器和扩展选择器
  - 基本选择器
    - 标签选择器：针对一类标签
    - $ID$选择器：针对一个特定的标签实验
    ```css
        #title{ border:3px }
    ```
    - 类选择器：针对想要的所有标签使用
    ```css
        .title{ width:800px; }
    ```
    ```html
        <h3 class="title">Title</h3>
    ```
    - 通用选择器（通配符）：针对所有的标签都适用
  - 扩展选择器

### 盒子模型

- 包括`div`、`span`、`a`，图片、表单元素一律视为文本而非盒子
- 盒子中有$5$个主要属性
  - `width`
  - `height`
  - `padding`
  - `border`
  - `margin`

## JavaScript

- `HTML`中的`JavaScript`脚本代码必须位于`<sciprt>`与`</script>`标签中
- 也可以存放在`.js`文件，嵌入到文档中
    ```javascript
        <scrtpt src = "javascript.js">
        </script>
    ```

### JavaScript基本语法

#### 变量定义

- **只包含字母、数字、下划线**
- **以字母开头**
- **不能使用`JavaScript`的保留字**
- **区分大小写**
- **变量需要声明，不指定类型**
    ```javascript
        var num = 10;
        var str = "JavaScript";
    ```

#### 定义函数

- 在`JavaScript`中**定义函数需要使用`function`关键字，无返回类型**
  - 仅通过如`window.alert()`、`document.write()`等方法输出
    ```javascript
        <srcipt language = "JavaScript">
            function func() {
                // 函数体
            }
        </script>
    ```

## JQuery

- `JQuery`库包含以下内容
  - `HTML`元素选取
  - `HTML`元素操作
  - `CSS`操作
  - `HTML`事件函数
  - `JavaScript`特效和动画
  - `HTML`、`DOM`遍历和修改

### JQuery安装

- `$(document).ready()`用于确保在执行任何脚本之前，`DOM`已经完全加载完毕
    ```HTML
        <!DOCTYPE html>
        <html lang = "en">
            <head>
                <meta cahrset = "UTF-8">
                <title>Document</title>
                <!-- 引入 JQuery -->
                <script src = "https://code.jquery.com/jquery-3.6.0.min.js"></script>
            </head>
            <body>
                <script>
                    $(document).ready(function(){
                        alert("Ready!");
                    });
                </script>
            </body>
    ```

### JQuery语法

- **基础语法**：`$(selector).action()`
    ```javascript
        $(this).hide();     // 隐藏当前元素
        $("p").hide();      // 隐藏所有 <p> 元素
        $("p.text").hide(); // 隐藏所有 class="test" 的元素
        $("#text").hide();      // 隐藏 id="test" 的元素
    ```
---

- **元素选择器**
  - `JQuery`**元素选择器**基于元素名选取元素
  - 如`$("p")`为在页面中选取所有`<p>`元素
  ```html
    <script>
        $(document).ready(function(){
            $("button").click(function(){ //为 button 指定点击事件
                $("p").hide(); //隐藏所有 <p> 元素
            });
        });
    </script>
  ```
- **#id选择器**
  - `JQuery`**#id选择器**通过`HTML`元素的`id`属性选取指定的元素
  ```html
    <script>
        $(document).ready(function(){
            $("#button1").click(function(){
                alert("Button1");
            });
            $("#button2").click(function(){
                alert("Button2");
            });
        });
    </script>
  ```
- **.class选择器**
  - `JQuery`**.class选择器**通过指定的`class`查找元素
  ```html
    <script>
        $(document).ready(function(){
            $(".test").hide();
        });
    </script>
  ```
### JQuery事件

- 常见`JQuery`事件

|鼠标事件|键盘事件|表单事件|文档/窗口事件|
|--|--|--|--|
|click|keypress|submit|load|
|dblclick|keydown|change|resize|
|mouseenter|keyup|focus|scroll|
|mouseleave||blur|unload|
|hover||||

### JQuery获取内容和属性

- `text()`：设置或返回所选元素的文本文件
- `html()`：设置或返回所选元素的内容（包括`HTML`标签）
- `val()`：设置或返回表单字段的值

## Ajax

- `Ajax(Asynchronous JavaScript and XML)`是一种在**无需重新加载整个页面的情况下，能够更新部分页面的技术集合**

### XMLHttpRequest

`XMLHttpRequest`对象是`JavaScript`中的一个内置对象，用于**在浏览器中发布异步`HTTP`请求**。它允许`Web`应用程序在不重新加载整个界面的情况下与服务器交换数据。这意味着**可以在后台加载和检索数据，从而实现动态更新页面内容的功能**

- 发送`get`请求
    ```javascript
        var xhr = new XMLHttpRequest();
        xhr.open('GET', 'http://example.com/data', true); //第三个参数表示是否异步发送
        xhr.send(null);
        xhr.onload = function() {
            if (xhr.status >= 200 && xhr.status <= 300) {
                console.log(xhr.responseText);
            } else {
                console.error(xhr.statusText);
            }
        }
    ```
- 状态码
  - `XMLHttpRequest`对象有一个名为`readyState`的属性，它表示请求、响应过程中的不同步骤，共有$5$个状态值
    - `0 (UNSENT)`：尚未调用`open()`方法
    - `1 (OPENED)`：已经调用了`open()`方法，但是没有调用`send()`方法
    - `2 (HEADERS_RECIVED)`：已经调用了`send()`方法，接收到所有响应头，正在下载响应体
    - `3 (LOADING)`：正在下载响应体
    - `4 (DONE)`：请求完成，响应已经准备好
- 响应处理<br>
$\qquad$一旦请求完成并且`readyState`达到$4$，可以通过监听`onload`事件赖处理响应数据
- `XMLHttpRequest`对象提供了属性响应数据：
  - `responsText`：包含响应的文本形式
  - `responseXML`：如果响应是`XML`文档，则包含`XML`文档对象
  - `responseType`：指定响应的数据类型，如`arraybuffer`、`blob`、`document`、`json`、`text`
  - `respons`：根据`responseType`属性，包含响应数据
    ```javascript
        xhr.onreadystatechange = function() {
            if (xhr.readyState === 4 && xhr.status === 200) {
                console.log(xhr.responseText);
                // 输出字符串形式的 JSON 文本
                // 解析 JSON 数据
                var data = JSON.parse(xhr.requestText);
                console.log(data);
                // 输出解析后的 JS 对象/数组，可在看控制台展开查看属性
            }
        }
    ```
## Bootstrap

# 框架编程