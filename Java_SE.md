# 基础语法

## new关键字

用于实例化对象，如
        
        arr = new int[10];
        String str = new String("Java Program");
        
new关键字所实例化的对象都存储在堆中<br>
而基本数据类型(int, char, double, boolean)，对象引用等，则存储在栈中，如

        int i = 10;
        double n = 3.14;


栈中保存：基本类型值、对象引用、方法调用信息<br>
堆中保存：对象实例、数组、字符串常量池(String Pool)<br>
关键规则：对象本身永远在堆中，栈中只存引用

---
|特性|栈(Stack)|堆(Heap)|
|--|--|--|
|**存储内容**|存储基本类型变量、对象引用(指针)|存储所有对象实例(包括new创建的字符串)|
|**生命周期**|生命周期短暂，仅限当前方法的作用域|生命周期较长，可能被多个线程共享|
|**内存分配速度**|快速(仅移动栈顶指针)|较慢(需内存分配和 GC 管理)|
|**线程安全性**|线程私有(每个线程有自己的栈)|线程共享|
|**空间大小**|较小(默认几 MB，可配置)|较大(占 JVM 内存的大部分)|
---

## 数组

  数组中的元素是指存储在连续内存空间中获得的一组数据集合。  
  
  声明数组变量：

      int[] arr;
      String[] names;
      double[] scores;

  实例化数组（为数组分配存储空间，要求空间连续）

      arr = new int[100];
      double[] D_arr = new double[20];

### 通过下标或索引访问元素

      arr[i++];
      /*
        i++先调用再自增
        如：
        for(int i = 0;i <= 20;i++){
          if(i % 2 == 0)
            arr[n++] = i;
        }
      */

  数组作为形参

      public static void displayArray(int[] arr){
        System.out.print(Arrays.toString(arr));
      }

#### 统计3到max之间的所有素数

      public static int countPrime(int max) {
          int count = 0;
          for(int n = 3;n <= max;n+=2){
              if(isPrimary(n))
                  count++;
          }
          return count;
      }
      public static int[] getPrime(int max) {
          int[] arr = new int[countPrime(max)];
          int count = 0;
          for(int n = 3;n <= max;n += 2){
              if(isPrimary(n)){
                  arr[count++] = n;
              }
          }
          return arr;
      }
      public static boolean isPrimary(int n) {
          boolean flag = true;
          for(int i = 2;i < n;i++) {
              if (n % i == 0) {
                  flag = false;
                  break;
              }
          }
          return flag;
      }
      public static void displayArray(int[] arr){
            for(int o:arr){
                System.out.println(o);
            }
      }

      public static void main(String[] args){
          displayArray(getPrime(100));
      }

数组声明时，不能设置长度，因为前面声明的变量并不是数组实例，而是实例的一个引用地址，关于数组的长度机器元素的个数是由后方的数组实例决定的。

#### 函数递归调用

        public static int getMax(int[] arr){
            int max = 0;
            for(int o : arr){
                if(o > max){
                    max = o;
                }
            }
            return max;
        }

        public static int getMax(int[] arr , int n){
            if(n == 0) return arr[0];
            else{
                int max = 0;
                for(int i = 0;i < n - 1;i++){
                    max = max>arr[i]?max:arr[i];
                }
                return max;
            }
        }

        public static void main(String[] args){
            int[] arr = {4,32,2,1,-1,9};
            System.out.println(getMax(arr));
            System.out.println(getMax(arr , arr.length));
        }
    
    重载：在某个类中，有两个及以上方法名相同，形参不同

#### 二分查找

        public static void sortArray(int[] arr){
            for(int i = 0;i < arr.length;i++){
                int min = i;
                for(int j = i + 1;j < arr.length;j++){
                    if(arr[j]<arr[min]) min = j;
                }
                if(min != i){
                    int temp = arr[min]; arr[min] = arr[i]; arr[i] = temp;
                }
            }
        }

        public static int findElement(int[] arr , int x){
            int index = -1;
            int begin = 0,end = arr.length;
            while(begin <= end){
                int mid = (begin + end)/2;
                if(arr[mid] == x){
                    index = mid; break;
                }else if(arr[mid] > x)
                    end = mid - 1;
                else
                    begin = mid + 1;
            }
            return index;
        }

        public static void main(String[] args){
            int[] arr = {4,32,2,1,-1,9,10,10};
            int x = -1;
            sortArray(arr);
            System.out.println(Arrays.toString(arr));
            System.out.println(findElement(arr , x));
        }

#### 二维数组

        public static void main(String[] args){
            int[][] arr = new int[10][5];
            System.out.println(arr.length);
                //输出结果为 10
            System。out。println(arr[0].length);
                //输出结果为 5
            //二维数组每个元素都是一个一维数组
        }

# 类与对象

面向过程编程：主要通过多个函数实现功能<br>
面向对象编程(oop)：主要通过各种类实现功能

    属性：对象具有的各种特征；
        每个对象的每个属性都有特定值。

    方法：对象执行的操作。

    对象：用来描述客观事物的一个实体，由一组属性和方法构成。

    对象同时具有属性和方法两项特性；
    对象的属性和方法通常被封装在一起，共同体现对象的特征；

    类是模板，定义对象将会拥有的特征(属性)和行为(方法)

定义一个类

        public class Student {
            //定义属性
            private String ID;
            private String Name;
            private String major;
            //定义方法
            public void setInfo(String ID, String Name, String major){
                this.ID = ID;
                this.Name = Name;
                this.major = major;
            }
            public void getInfo(){
                return ID + "---" + Name + "---" + major;
            }
        }

通常在不同java文件内，如在同一个类中，则直接通过

        public class Test {
            public static void main(String[] args){
                Cource c1 = new Cource();
                c1.ID = 1;
            }
        }
        
        class Cource{
            String ID;
        }

调用这个类(类的调用需要生成对象，即通过 new 关键字生成实例)

        public class Test{
            public static void main(String[] args){

                Student s1 = new Student();
                //为s1分配空间；返回首地址赋值给s1
                //s1为对象(object),new Student()为实例(instance)
                s1.setInfo(2025001,"A","软件工程");
                System.out.println(s1.getInfo());
                
                Student s2 = s1;
                //将s1的首地址赋值给s2
            }
        } 

构造函数

        public class Test {
            public static void main(String[] args){
                Student s1 = new Student(1,"A");
                //在实例化的过程中对属性进行赋值
                //在对象实例化过程中，系统自动调用相应的构造函数
            }
        }

---

        public class Student {
            int ID;
            String Name;

            public Student(){
                //无形式参数的构造函数，如果没有手动添加构造函数，系统默认调用此构造函数，若已经创建了构造函数，系统将不在分配缺省的构造函数
            }

            public Student(int ID, String Name){
                this.ID = ID;
                this.Name = Name;
                //构造函数可以重载（overload），可以同时存在多个同名但是形式参数不同的构造函数
            }
        }

属性构造器函数

        public class Test {
            public static void main(String[] args){
                Student s1 = new Student();
                s1.setID(1);
                s1.setName(A);
                System.out.println(s1);
                //此处输出结果为 Name:A ID:1 系统会自动调用 toString 函数
            }
        }
---
        public class Student {
            private int ID;
            private String Name;

            public void setID(int ID){
                this.ID = ID;
            }
            
            public int getID(){
                return this.ID;
            }
            
            public void setName(String Name){
                this.Name = Name;
            }
            
            public String getName(){
                return this.Name;
            }
            
            //toString()函数，在System.out.println()中，即使不使用此函数返回字符串，系统也会自动调用
            public String toString(){
                return "Name:" + this.Name + "\nID:" + this.ID;
            }
        }

## 静态

### 静态 static

        public class StaticClass {
            public int x; 
            //实例属性
            public static int y; 
            //类属性：所有对象共享一个副本，实例化时不初始化
            public StaticClass(){
                x++;y++;
            }
            public void display(){
                System.out.println(x + "," + y)
            }
            public static void main(String[] args){
                StaticClass o1 = new StaticClass();
                o1.display();
                StaticClass o2 = new StaticClass();
                o2.display();
                StaticClass.y = 10;
                o2.display();
            }
        }
---
        输出结果：
        1,1
        1,2
        1,10

### 静态函数

在JVM加载类之后，类中静态函数就分配入口地址，可以通过类名直接调用(也可以通过对象调用，不推荐)。类函数不依赖实例；
        
        Math.sqrt(20);
        
        //静态函数中不能调用非静态变量、方法、类
        //当静态函数中调用非静态类时，会因为尚未赋值而报错

动态函数：实例函数，通过实例才能调用该函数

### 静态语句块

        public class A {
            static {
                System.out.println("static");
            }

            public static void main (String[] agrs) {    
            }
        }

        // 此时，即使main方法中为空体，仍会执行一次静态语句块中的语句
        //静态语句块在程序中只会执行一次

### final 关键字

final关键字可以用于变量、方法和类。使用final关键字的主要目的是创建不可变的对象或防止被继承或覆盖。

### final变量

当final关键字用于变量时，这意味着一旦变量被赋值后，它的值就不能再被改变。如果是基本数据类型的变量，则其数值不可变；如果是引用类型的变量，则其引用不可变，但是对象的内容可以改变。例如：

        final int AGE = 30;
        AGE = 35; // 编译错误，不能再次赋值

对于类的成员变量，如果使用final修饰，则必须在声明时或在构造器中进行初始化。

### final方法

当final修饰一个方法时，这个方法不能被子类重写。例如：

        public class Parent {
            public final void show() {
                System.out.println("这是一个final方法。");
            }
        }

        public class Child extends Parent {
            // 以下尝试重写final方法将导致编译错误
            public void show() {
                System.out.println("尝试重写final方法。");
            }
        }

### final类

使用final关键字修饰的类不能被继承。例如，String类就是一个final类。声明一个类为final后，所有的方法都隐式地被视为final方法。

        public final class MyFinalClass {
            // 类定义
        }

        // 以下尝试继承final类将导致编译错误
        public class MySubClass extends MyFinalClass {
            // 类定义
        }

### final关键字的优势

提高性能：JVM和Java应用都会缓存final变量。

线程安全：final变量在多线程环境下可以安全共享，无需额外同步开销。

final关键字还可以用于优化方法、变量和类。

### 注意事项

final变量必须在声明时或构造器中初始化。

final方法不能被子类覆盖。

final类不能被继承。

在匿名类中，所有变量都必须是final变量。

final和static经常一起使用来创建常量。

## 继承

提高代码复用性

        public class A {
            private int x;
            public int y;
            protected int z;
            private void fun1(){}
            public void fun2(){}
            protect void fun3(){}
        }

        public class B extends A {
        }

        //通过 extends A 实现继承，A为父类，B为子类
        //此时通过 B 类中的对象，可以调用 A 类中的属性和方法，但是仍然受访问权限限制

---
### 子类从父类继承什么?

父类(基类，super类)<br>
子类(派生类)

子类从父类继承public和preotected成员(属性和方法)，private和defaul成员则不可以被继承<br>
但是可以访问default成员

### 继承下构造函数

当子类实例化时，系统自动将父类先实例化，先自动调用父类相应的构造函数，然后是子类本身的构造函数

        public class Person {
            private String Name;
            private int Age;
            public Person (){}
            public Person (String Name, int Age){
                this.Name = Name;
                this.Age = Age;
            }
            public String getName(){
                return Name;
            }
            public int getAge(){
                return Age;
            }
            public void setName(String Name){
                this.Name = Name;
            }
            public vod setAge(int Age){
                this.Age = Age
            }
        }
---

        public class Student extend Person {
            private int ID;
            piblic Student(){}
            public Student(String Name, int Age, int ID){
                super(Name,Age);
                //当子类实例化时，调用父类的构造函数，向父类传入对应成员
                //规定super()需为子类构造函数中第一行可执行语句，才能实现先调用父类构造函数时能顺利传入对应成员
                this.ID = ID;
            }
        }

### 方法的重写

当子类对父类的方法不满意时，可以对方法进行重写

        @Override
        public String toString() {
            //通过 super 关键字可以调用父类的方法
            return super.toString() + id + "---" + Name;
        }
        /*
            1.子类重写的方法必须和父类被重写的方法具有相同的方法名称、参数列表
            2.子类重写的方法的返回值类型不能大于父类被重写的方法的返回值类型
             (1)返回值是基本数据类型时，必须和父类的返回值类型相同
             (2)返回值是引用数据类型时(类类型)，子类重写方法返回的类型应该是父类被重写方法返回的类型或者其子类。(小于等于)
            3.子类重写的方法使用的访问权限不能小于父类被重写的方法的访问权限
                注意：子类不能重写父类中声明为private权限的方法
            4.子类方法抛出的异常不能大于父类被重写方法的异常

            注意：
                子类与父类中同名同参数的方法必须同时声明为非static的(即为重写)，或者同时声明为static的(不是重写)。
                因为static方法是属于类的，子类无法覆盖父类的方法
        */

多态:   存在多个标签相同但是实现不同的方法

## 抽象类与抽象函数

抽象类中只提供方法的声明，不提供方法的实现<br>
其中定义的抽象函数(虚函数)需要被继承到子类中实现

        public abstract class Shape {
            public abstract double getArea();
            //抽象函数用abstract修饰，只有方法的声明，不包含其实现(即没有方法体)
            public void displayArea() {
                System.out.println("Area:" + getArea());
            }
        }
---
        public class Circle extends Shape {
            double r;
            public Circle(double r) {
                this.r = r;
            }
            @Override
            public double getArea(double r) {
                return Math.PI*r*r;
            }
        }
---
        public class Test {
            public static void main(String[] args) {
                Shape shape = new Circle(5);
                System.out.println(shape.getArea());
                dispplayArea();
            }
        }

抽象类不能被实例化，只能作为基类(父类)通过它的子类进行实例化<br>
父类对象可以指向任何一个子类的实例，但是只能调用自己固有的方法

## 接口

        /*
            接口体：
            接口体中，只提供方法的声明，不允许提供方法的实现

            接口也可以通过 extends 关键字声明接口间的继承
            由于接口中的方法和常量都是 public 的，因此子接口将继承父接口中所有常量和方法
        */
        interface Constant {
            final int MAX = 100;
        }

        interface Computable extends Constant {
            int f(int x);
            public abstract int g(int x, int y);
        }

        //类使用 implement 关键字实现接口，如果这个类的父类实现了某个接口，那么这个类就不需要再次显式声明自己实现这个接口
        //如果这个接口中存在抽象方法，那么这个类要么是抽象类，要么实现全部抽象方法

        class A implements Computable{
            public int f(int x){
                return x * x;
            }
            public int g(int x, int y){
                return x + y;
            }
        }

        class B implements Computable{
            public int f(int x){
                return x * x * x;
            }
            public int g(int x, int y){
                return x * y;
            }
        }

        public class Test {
            public static void main(String[] args) {
                A a = new A();
                B b = new B();
                System.out.println(a.MAX);
                System.out.println(a.f(10) + " " + a.g(12, 6));
                System.out.println(b.MAX);
                System.out.println(b.f(10) + " " + b.g(29, 2));
            }
        }

        /*
            输出结果:

                100
                100 18
                100
                1000 58
                
        */
---
        //使用关键字 instanceof 可以判断某个类是否为另一个类的子类

        if(A instanceof B) {
            System.out.println("A是B的子类");
        } else {
            System.out.println("A不是B的子类");
        }


# 字符串

        String s1, s2, s3;
        s1 = "Hello World";
        s2 = new String();
        s3 = new String("Hello World");
        /*
            其中，s1与s3虽然值相等，但是地址不同
            '==':比较字符串地址
            'equals':比较字符串内容
        */
        System.out.println(s1 == s2);
        //false
        System.out.println(s1.equals(s2));
        //true

---

## 字符串常用方法

|方法|说明|示例|
|--|--|--|
|length()|获取长度|"abc".length() → 3|
|charAt(int)|获取指定位置的字符|"Java".charAt(1) → 'a'|
|substring(int, int)|截取子串|"Hello".substring(1,3) → "el"|
|indexOf(String)|查找子串位置|"apple".indexOf("p") → 1|
|equals(Object)|内容比较(区分大小写)|"java".equals("Java") → false|
|equalsIgnoreCase()|忽略大小写比较|"java".equalsIgnoreCase("Java") → true|
|toUpperCase()/toLowerCase()|转换大小写|"Hello".toLowerCase() → "hello"|
|trim()|去除首尾空格|" Java ".trim() → "Java"|
|replace(old, new)|替换字符/字符串|"abcd".replace("bc", "x") → "axd"|
|split(regex)|按正则分割字符串|"a,b,c".split(",") → ["a","b","c"]|
---

### 解析

        String str1 = "100", str2 = "3.14";
        int i = Integer.parseInt(str1);
        double d = Double.parseDouble(str2);
        //将字符串解析为整型或浮点型的类型

## 字符串拼接

### String

        String str_a, str_b, str1 = "Hello", str2 = "World";
        str_a = str1 + str2;
        str_b = str1.concat(str2);

### StringBuilder

        StringBuilder stringBuilder = new StringBuilder("Hello");
        stringBuilder.append("World");
        
### StringBuffer

        StringBuffer stringBuffer = new StringBuffer("Hello");
        stringBuffer.append("World");

---
|特性|String|StringBuffer|StringBuilder|
|--|--|--|--|
|**可变性**|不可变(Immutable)|可变(Mutable)|可变(Mutable)|
|**线程安全**|线程安全(但不需要加锁)|线程安全(所有方法是同步的)|非线程安全|
|**性能**|在频繁修改时性能较差|性能较好，但由于同步机制性能稍差|性能最佳|
|**适用场景**|不需要修改的字符串操作|多线程环境中的字符串拼接与修改|单线程环境中的字符串拼接与修改|
|**操作时是否生成新对象**|是|否|否|
---

# 界面编程

## Swing 核心类与组件

Swing 的类均以 J 开头(如 JFrame,JPanel)，位于 javax.swing 包中。以下是最常用的类和组件：

### 顶层容器

#### JFrame：主窗口容器，用于承载其他组件

        JFrame frame = new JFrame("窗口标题");
        frame.setSize(400, 300); // 设置窗口大小
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); // 关闭时退出程序
        frame.setVisible(true); // 显示窗口

#### JDialog：对话框窗口，用于弹出临时界面

        JDialog dialog = new JDialog(frame, "提示", true); // 模态对话框
        dialog.add(new JLabel("这是一个对话框"));

#### JWindow：无标题栏、窗口管理按钮等的容器

        JWindow window = new JWindow();
        window.setSize(800, 600);
        JLabel label = new JLabel("Hello World");
        window.add(label);
        label.setBounds(0, 0, 800, 600);
        window.setLocationRelativeTo(null);
        window.setVisible(true);

### 中间容器

#### JPanel：通用面板，用于组合其他组件或自定义绘制

        JPanel panel = new JPanel();
        panel.setBackground(Color.WHITE); // 设置背景颜色

#### JScrollPane：为组件（如表格、文本域）添加滚动条

        JTextArea textArea = new JTextArea(10, 30);
        JScrollPane scrollPane = new JScrollPane(textArea);

#### JTabbedPane：为组件添加选项卡

        JTabbedPane tabbedPane = new JTabbedPane();
        JPanel panel1 = new JPanel();
        panel1.add(new JLabel("Text1"));
        JPanel panel2 = new JPanel();
        panel2.add(new JLabel("Text2"));
        tabbedPane.addTab("Tab 1", null, panel1, null);
        tabbedPane.addTab("Tab 2", null, panel2, null);
        //参数列表[title, icon, component, tip]

#### JSplitPane：分割面板

#### JMenuBar菜单条 & JMenu菜单

        JMenuBar menuBar = new JMenuBar();
        JMenu menu1 = new JMenu("menu1");
        JMenu menu2 = new JMenu("menu2");
        menuBar.add(menu1);
        menuBar.add(menu2);

### 基础组件

#### JButton：按钮

        JButton button = new JButton("点击我");
        button.setToolTipText("这是一个按钮"); // 悬停提示
        button.setEnabel(ture);// 设置按钮是否可用

#### JLabel：标签，显示文本或图标

        JLabel label = new JLabel("用户名:");
        label.setIcon(new ImageIcon("icon.png")); // 设置图标

#### JTextField：单行文本框

        JTextField textField = new JTextField(20); // 20列宽度

#### JTextArea：多行文本区域

        JTextArea textArea = new JTextArea(5, 20); // 5行20列

#### JCheckBox复选框 & JRadioButton单选按钮

        JCheckBox checkBox = new JCheckBox("同意协议");
        checkBox.setSelected(false);

        JRadioButton radioButton1 = new JRadioButton("选项1");
        JRadioButton radioButton2 = new JRadioButton("选项2");
        ButtonGroup group = new ButtonGroup(); // 单选按钮分组
        group.add(radioButton1);
        group.add(radioButton2);
        //通过 radioButton.isSelected() 返回值判断是否选中

#### JComboBox：下拉框

        String[] items = {"选项1", "选项2"};
        JComboBox<String> comboBox = new JComboBox<>(items);
        combox.addItem("选项3");
        combox.setEditable(true);// 设置为可编辑

#### JTable：表格组件

        String[][] data = {{"1", "张三"}, {"2", "李四"}};
        String[] columns = {"ID", "姓名"};
        JTable table = new JTable(data, columns);

---

        //通过 javax.swing.table.DefaultTableModel 中的 TableModel 刷新表格
        table.setModel(new DefaultTableModel(data, columns));

#### JMenuItem：菜单项

        JMenuBar menuBar = new JMenuBar();
        JMenu menu = new Jmenu("menu");
        JMenuItem item1 = new JMenuItem("item1");
        JMenuItem item2 = new JMenuItem("item2");
        menu.add(item1);
        menu.add(item2);
        menuBar.add(menu);

## 布局管理器(Layout Manager)

Swing 使用布局管理器自动排列组件，确保界面在不同分辨率下适配。

### 常用布局

#### FlowLayout(流式布局)

        JPanel panel = new JPanel(new FlowLayout(FlowLayout.LEFT)); // 左对齐
        panel.add(button1);
        panel.add(button2);
        //FlowLayout.LEFT为枚举体
        //LEFT、CENTER、RIGHT、LEADING、TRAILING分别对应整型0~4

#### BorderLayout(边界布局，JFrame 默认布局 缺省布局)

        frame.add(new JButton("North"), BorderLayout.NORTH);
        frame.add(new JButton("Center"), BorderLayout.CENTER);

#### GridLayout(网格布局)

        JPanel panel = new JPanel(new GridLayout(2, 3, 10, 20)); 
        // 2行3列，水平间距10px，垂直间距20px
        panel.add(new JButton("1"));
        panel.add(new JButton("2"));

#### GridBagLayout(灵活网格布局)

        JPanel panel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        // 设置组件外部间距（上、左、下、右）
        gbc.insets = new Insets(10, 10, 10, 10); // 上下左右各10px间距
        gbc.gridx = 0; gbc.gridy = 0;
        panel.add(new JButton("Button1"), gbc);
        gbc.gridx = 1; gbc.gridy = 1;
        panel.add(new JButton("Button2"), gbc);

### 自定义布局(基于坐标绝对定位)

        panel.setLayout(null); // 禁用布局管理器
        button.setBounds(10, 10, 100, 30); // x, y, width, height
        panel.add(button);

## 事件处理(Event Handling)

Swing 基于监听器模式实现事件响应。

事件源: Swing 组件都是事件源(Jbutton, JMenuItem, JTextField, JFrame, ...)

事件(消息): Event 

构建一个监听类并实例化，然后向事件源注册，成为该事件源的监听器

### 常见事件类型

#### ActionListener：按钮点击、菜单项选择

        button.addActionListener(e -> {
            System.out.println("按钮被点击了！");
        });

#### MouseListener：鼠标点击、进入、离开

        panel.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                System.out.println("鼠标点击位置：" + e.getX() + ", " + e.getY());
            }
            public void mouseEntered(MouseEvent e) {
                //鼠标进入该区域时执行此处代码
            }
            public void mouseExited(MouseEvent e) {
                //鼠标离开该区域时执行此处代码
            }
        });

#### KeyListener：键盘输入

        textField.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                if (e.getKeyCode() == KeyEvent.VK_ENTER) {
                    System.out.println("按下了回车键");
                }
            }
        });
        /*
            getKeyChar(): 返回这个事件中和键相关的字符(char)

            getKeyCode(): 返回这个事件中和键相关的整数键(int)

            keyPressed(e: KeyEvent) -->在源组件上按下一个键后被调用

            KeyReleased(e: KeyEvent) -->在源组件上释放一个键后被调用

            KeyTyped(e: KeyEvent) -->在源组件上按下一个键然后释放该键后被调用

            按键常量

            VK_HOME    Home键      VK_CONTROL     控制键
            VK_END     End键       VK_SHIFT       shift键
            VK_PGUP    page up键   VK_BACK_SPACE  退格键
            VK_PGDN    page down键 VK_CAPS_LOCK   大小写锁定键
            VK_UP      上箭头      VK_NUM_LOCK    小键盘锁定键
            VK_DOWN    下箭头      VK_ENTER       回车键
            VK_LEFT    左箭头      VK_UNDEFINED   未知键
            VK_RIGHT   右箭头      VK_F1--VK_F12  F1 -- F12
            VK_ESCAPE  Esc键       VK_0 --VK_9    0 --- 9
            VK_TAB     Tab键       VK_A --VK_Z    A----Z
        */


### 事件适配器类

如 MouseAdapter、KeyAdapter，避免实现接口中所有方法。

## 自定义绘制

通过重写 paintComponent 方法实现自定义图形:

        JPanel panel = new JPanel() {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                g.setColor(Color.RED);
                g.drawRect(50, 50, 100, 100); // 绘制红色矩形
            }
        };

## 界面设计流程

### 1.声明或定义所需控件

        private JLabel jlabel = new JLabel("Text");

### 2.在构造函数中进行布局，放置相关组件(也可以在main方法中布局)

        import javax.swing.*;
        import java.awt.*;
        import java.awt.event.ActionEvent;
        import java.awt.event.ActionListener;

        public class FRAME extends JFrame implement ActionListener {
            //通过继承JFrame直接生成JFrame容器
            JButton button；
            public FRAME() {
                //获取当前JFrame的内容面板
                JPanel jpanel = (JPanel)this.getContentPane();
                jpanel.setLayout(new GridLayout(1,1));
                button = new JButton("BUTTON");
                jpanel.add(button);
                this.setSize(400,300);
                this.setLocation(0,0);
                this.setVisible(true);
                this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
                this.addActionListener(this);
            }
            @Override
            public void actionPerformed(ActionEvent e){
                if(e.getSource() == button) {
                    System.out.println("按钮被点击");
                }
            }
            //在main方法中调用构造函数
            public static void main(String[] args) {
                new FRAME();
            }
        }

# 数据库

## JDBC开发技术

### MySQL

`sql`

        create database if not exists database_name character set utf8mb4
        -- 创建名为 database_name 的数据库(如果不存在)，编码形式为 utf8mb4

        show databases;
        -- 查看所有数据库
        
        use database_name;
        -- 打开名为 database_name 的数据库

        create table if not exists students(
            id varchar(20) not null primary key,
            name varchar(30) not null,
            inyear int
        );
        /*  
            创建名为 students 的数据表
            其中 not null 要求内容非空
            primary key 主键要求此项不能重复
        */

        insert into studnts(id,name,inyear) value ('2024001','甲',2024);
        insert into studnts(id,name,inyear) value ('2024002','甲',2024);
        insert into studnts(id,name,inyear) value ('2024003','甲',2024);
        -- 向 students 数据表中插入元素

        delete from student where id = '2024003';
        -- 删除 id 为 '2024003' 的元素

        update students set name = '乙' where id = '2024002';
        -- 更新 id 为 '2024002' 的元素中 name 项目

        delete from students;
        -- 删除 students 数据表

### JDBC

        import java.sql.*;

        public class DB {
            public static void main(String[] args) throws ClassNotFoundException, SQLException {
                //加载驱动
                String driver = "com.mysql.jdbc.Driver";
                class.forName(driver);
                //连接至MySQL
                String url = "jdbc:mysql://localhost:3306/mydatabase", user = "root", pwd = "root";
                Connection connection = DriverMannager.getConnection(url, user, pwd);
                //创建命令对象
                Statement cmd = connection.createStatement();//返回为 int 类型数据
                String sql = "select * from students";
                ResaultSet rs = md.executeQuery(sql); //结果集
                //读取内容
                while(rs.next()) {
                    String id = getString("id");
                    String name = getString("name");
                    int inYear = getInt("inYear");
                    System.out.println(id + "--" + name + "--" + inYear);
                }
                connection.close();
                //关闭连接
            }
        }

# 异常处理

## 异常(Exception)

异常:在程序运行中，除了语法错误以外产生的无法继续运行的错误节点<br>
如:<br>
算术异常 被零除, 数据库异常 SQLException , I/O流异常 IOException ,<br>
越界异常 IndexOutOfBoundsException , 空指针异常 NullPointerException ,<br>
自定义异常 等等<br>
其中，Exception 为所有异常的父类

异常处理:

        try {
            //正常情况下需要执行的代码，当出现异常时，系统将自动抛出一个异常实例
        } catch(Exception e) {
            //如果出现异常，并且捕获到该异常，则执行 catch 块中的异常处理代码
            //允许存在多个 catch 块处理 try 块中不同异常，但要求异常类型由小到大
        } finally {
            //始终执行的代码
        }

---

        public static void main(String[] args) throws Exception {
            //声明异常，将异常实例传递到方法外层处理
        }

# 左移位运算符

在 Java 中，<< 是左移位运算符。让我详细解释这个操作符的含义和在 HashMap 中的应用。

左移位运算符 (<<) 详解
基本概念
语法：value << n

作用：将 value 的二进制表示向左移动 n 位，右侧用 0 填充

效果：相当于乘以 2 的 n 次方 (value × 2ⁿ)

示例说明

```java
int var = 1 << 4;  // 1 左移 4 位
```
二进制计算过程：

```text
1 的二进制: 0000 0000 0000 0000 0000 0000 0000 0001
左移 4 位:  0000 0000 0000 0000 0000 0000 0001 0000
结果: 16 (十进制)
```

等价计算：

```java
1 << 4 = 1 × 2⁴ = 1 × 16 = 16
```