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

# 框架编程
