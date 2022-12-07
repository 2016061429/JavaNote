# JAVA基础笔记

## 类和对象

###  类和对象的概念 

- 对象主要指现实生活中客观存在的实体，在Java语言中对象体现为内存空间中的一块存储区域。 

- 类简单来就是“分类” ，是对具有相同特征和行为的多个对象共性的抽象描 述，在Java语言中体现为一种引用数据类型，里面包含了描述特征/属性 的成员变量以及描述行为的成员方法。 

- 类是用于构建对象的模板，对象的数据结构由定义它的类来决定。 

### 类的定义

```java
class Person {	//类名
    String name;	//类体:数据类型 成员变量名 = 初始值; 
}
```

注意： 当成员变量由多个单词组成时，通常要求从第二个单词起每个单词的首 字母大写 。 

### 对象的创建

```java
new Person();
//当一个类定义完毕后，可以使用new关键字来创建该类的对象，这个过程叫做类的实例化。
//创建对象的本质就是在内存空间的堆区申请一块存储区域， 用于存放该对象独有特征信息。
```

###  引用的定义 

 基本概念:

1. 使用引用数据类型定义的变量叫做引用型变量，简称为"引用" 。 
2. 引用变量主要用于记录对象在堆区中的内存地址信息，便于下次访问。  

```java
Person p = new Person();
p.name = "zhangsan";
System.out.println(p.name);
```

### 实际案例

```Java
public class Person {
    String name;
    int age;
    
    // 自定义成员方法实现将姓名(年龄)修改为参数指定数值的行为
	// String s = "guanyu";
    void setName(String s) {
        name = s;
    }
    void setAge(int i) {
        age = i;
    }
    
    // 自定义成员方法实现姓名(年龄)数值的获取并返回的行为
    String getName() {
        return name;
    }
    int getAge() {
        return age;
    }
}
```

### 成员变量初始值

![Image text](https://github.com/2016061429/JavaNote/tree/main/JavaSE/picture/image-20221202202443291.png)


### 成员方法

```java
class Person {
	void show() {
		System.out.println("XXX");
	}
}
```

### 返回值类型的详解

- 返回值主要指从方法体内返回到方法体外的数据内容。 
- 返回值类型主要指返回值的数据类型，可以是基本数据类型，也可以是 引用数据类型。 
- 当返回的数据内容是66时，则返回值类型写 int 即可 
- 在方法体中使用return关键字可以返回具体的数据内容并结束当前方法。 
- 当返回的数据内容是66时，则方法体中写 return 66; 即可 
- 当该方法不需要返回任何数据内容时，则返回值类型写void即可。 

### 形参列表的详解 

- 形式参数主要用于将方法体外的数据内容带入到方法体内部。 
- 形式参数列表主要指多个形式参数组成的列表，语法格式如下： 数据类型 形参变量名1, 数据类型 形参变量名2, ...  
- 当带入的数据内容是"hello"时，则形参列表写 String s 即可 
- 当带入的数据内容是66和"hello"时，则形参列表写 int i, String s 即可 
- 若该方法不需要带入任何数据内容时，则形参列表位置啥也不写即可。 

### 方法体的详解 （待补充）



## 方法和封装 

### 构造方法

#### 构造方法基本概念

 构造方法名与类名完全相同并且没有返回值类型，连void都不许有。 

```java
class 类名 {
	类名(形参列表) {
		//构造方法体;
	}
}
```

#### 默认构造方法

- 当一个类中没有定义任何构造方法时，编译器会自动添加一个无参空构 造构造方法，叫做默认/缺省构造方法，如：Person(){} 
- 若类中出现了构造方法，则编译器不再提供任何形式的构造方法。  

####  构造方法的作用

- 使用new关键字创建对象时会自动调用构造方法实现成员变量初始化工作。  

#### 实际案例

编程实现Point类的定义并向Point类添加构造方法 

- Point() 默认创建原点对象 
- Point(int i, int j) 根据参数创建点对象  

```java
public class Point {
    int x;
    int y;
    
    // 自定义无参构造方法
    Point() {}
    // 自定义有参构造方法
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    void show() {
        System.out.println("横坐标是：" + x + "，纵坐标是：" + y);
    }

	public static void main(String[] args) {
    	// 1.使用无参方式构造对象并打印特征
    	Point p1 = new Point();
    	p1.show();
    
    	// 2.使用有参方式构造对象并打印特征
    	Point p2 = new Point(3, 5);
    	p1.show();   
	}
}
```

### 方法重载 

#### 方法重载的概念 

- 若方法名称相同，参数列表不同，这样的方法之间构成重载关系 (Overload)。  

#### 重载的体现形式 

- 方法重载的主要形式体现在：参数的个数不同、参数的类型不同、参数的顺序不同，与返回值类型和形参变量名无关，但建议返回值类型最好相同。
- 判断方法能否构成重载的核心：调用方法时能否加以区分。

#### 重载的实际意义 

- 方法重载的实际意义在于调用者只需要记住一个方法名就可以调用各种 不同的版本，来实现各种不同的功能。 
- 如：java.io.PrintStream类中的println方法。 

### this关键字 

#### this的基本概念 

- 若在构造方法中出现了this关键字，则代表当前正在构造的对象。
- 若在成员方法中出现了this关键字，则代表当前正在调用的对象。
- this关键字本质上就是当前类类型的引用变量。 

#### 工作原理

- 在构造方法中和成员方法中访问成员变量时，编译器会加上this.的前缀， 而this.相当于汉语中"我的"，当不同的对象调用同一个方法时，由于调用 方法的对象不同导致this关键字不同，从而this.方式访问的结果也就随之 不同。 

#### 使用方式

- 当局部变量名与成员变量名相同时，在方法体中会优先使用局部变量(就 近原则)，若希望使用成员变量，则需要在成员变量的前面加上this.的前 缀，明确要求该变量是成员变量（重中之重）。 
- this关键字除了可以通过this.的方式调用成员变量和成员方法外，还可以 作为方法的返回值（重点）。
- 在构造方法的第一行可以使用this()的方式来调用本类中的其它构造方法 。  

#### 注意事项 

- 引用类型变量用于存放对象的地址，可以给引用类型赋值为null，表示不 指向任何对象。 
- 当某个引用类型变量为null时无法对对象实施访问（因为它没有指向任何 对象）。此时，如果通过引用访问成员变量或调用方法，会产生 NullPointerException 异常。  

#### 实际案例

编程实现为Point类添加重载的成员方法： 

- up() – 实现纵坐标减1的功能。 
- up(int dy) – 实现纵坐标减去参数指定数值的功能。

测试重载方法的调用规则 

```java
public class Point {
    int x;
    int y;

    // 自定义无参构造方法
    Point() {}
    // 自定义有参构造方法
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    void show() {
        System.out.println("横坐标是：" + x + "，纵坐标是：" + y);
    }
    void up() {
        y--;
    }
    void up(int y) {
        this.y -= y;
    }

    public static void main(String[] args) {

        Point p1 = new Point();
        p1.show();

        Point p2 = new Point(3,5);
        p2.show();

        p2.up();
        p2.show();
        p2.up(2);
        p2.show();
    }
}
```

### 封装

#### 封装的概念

- 通常情况下可以在测试类给成员变量赋值一些合法但不合理的数值，无 论是编译阶段还是运行阶段都不会报错或者给出提示，此时与现实生活 不符。
- 为了避免上述错误的发生，就需要对成员变量进行密封包装处理，来隐 藏成员变量的细节以及保证成员变量数值的合理性，该机制就叫做封装。  

#### 封装的实现流程

- 私有化成员变量，使用private关键字修饰。
- 提供公有的get和set方法，并在方法体中进行合理值的判断。
- 在构造方法中调用set方法进行合理值的判断。  

```java
public class Student {
	
	// 1.私有化成员变量，使用private关键字修饰
	// private关键字修饰表示私有的含义，也就是该成员变量只能在当前类的内部使用
	private int id;       // 用于描述学号的成员变量
	private String name;  // 用于描述姓名的成员变量 
	
	// 3.在公有的构造方法中调用set方法进行合理值的判断
	public Student() {}
	public Student(int id, String name) {
		//this.id = id;
		//this.name = name;
		setId(id);
		setName(name);
	}
	
	// 2.提供公有的get和set方法，并在方法体中进行合理值的判断
	// 使用public关键字修饰表示公有的含义，也就是该方法可以在任意位置使用
	public int getId() {
		return id;
	}
	public void setId(int id) {
		if(id > 0) {
			this.id = id;
		} else {
			System.out.println("学号不合理哦！！！");
		}
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	
	// 自定义成员方法实现特征的打印
	// 什么修饰符都没有叫做默认的访问权限，级别介于private和public之间
	public void show() {
		//System.out.println("我是" + name + "，我的学号是" + id);
		System.out.println("我是" + getName() + "，我的学号是" + getId());
	}
}
```

#### JavaBean的概念 

1. JavaBean是一种Java语言写成的可重用组件，其它Java 类可以通过反射机 制发现和操作这些JavaBean 的属性。 
2. JavaBean本质上就是符合以下标准的Java类： 
   - 类是公共的 
   - 有一个无参的公共的构造器
   - 有属性，且有对应的get、set方法  

## static关键字和继承 

### static关键字 

#### 基本概念 

- 使用static关键字修饰成员变量表示静态的含义，此时成员变量由对象层级提升为类层级，也就是整个类只有一份并被所有对象共享，该成员变 量随着类的加载准备就绪，与是否创建对象无关。
- static关键字修饰的成员可以使用引用的方式访问，但推荐类名的方式。 

#### 使用方式 

- 在非静态成员方法中既能访问非静态的成员又能访问静态的成员。 (成员：成员变量 + 成员方法， 静态成员被所有对象共享) 
- 在静态成员方法中只能访问静态成员不能访问非静态成员。 (成员：成员变量 + 成员方法， 因为此时可能还没有创建对象)  
- 在以后的开发中只有隶属于类层级并被所有对象共享的内容才可以使用 static关键字修饰。(不能滥用static关键字)  

#### 构造块和静态代码块

- 构造块：在类体中直接使用{}括起来的代码块。
- 每创建一个对象都会执行一次构造块。
- 静态代码块：使用static关键字修饰的构造块。
- 静态代码块随着类加载时执行一次。  

#### 实际案例

```java

```



#### 单例设计模式的概念

- 在某些特殊场合中，一个类对外提供且只提供一个对象时，这样的类叫 做单例类，而设计单例的流程和思想叫做单例设计模式。  

单例设计模式的实现流程

- 私有化构造方法，使用private关键字修饰。
- 声明本类类型的引用指向本类类型的对象，并使用private static关键字共 同修饰。
- 提供公有的get方法负责将对象返回出去，并使用public static关键字共同 修饰。  

#### 单例设计模式的实现方式  

- 单例设计模式的实现方式有两种：饿汉式 和 懒汉式，在以后的开发中推 荐饿汉式。  



### 继承

#### 继承的概念

- 当多个类之间有相同的特征和行为时，可以将相同的内容提取出来组成 一个公共类，让多个类吸收公共类中已有特征和行为而在多个类型只需 要编写自己独有特征和行为的机制，叫做继承。  
-  在Java语言中使用extends(扩展)关键字来表示继承关系。 
-  使用继承提高了代码的复用性，可维护性及扩展性，是多态的前提条件。  

```Java
public class Worker extends Person{} // 表示Worker类继承自Person类
//其中Person类叫做超类、父类、基类。
//其中Worker类叫做派生类、子类、孩子类。
```

#### 继承的特点

- 子类不能继承父类的构造方法和私有方法，但私有成员变量可以被继承 只是不能直接访问。
- 无论使用何种方式构造子类的对象时都会自动调用父类的无参构造方法， 来初始化从父类中继承的成员变量，相当于在构造方法的第一行增加代 码super()的效果。  
- 使用继承必须满足逻辑关系：子类 is a 父类，也就是不能滥用继承。
- Java语言中只支持单继承不支持多继承，也就是说一个子类只能有一个父 类，但一个父类可以有多个子类。 

#### 方法重写的概念

- 从父类中继承下来的方法不满足子类的需求时，就需要在子类中重新写 一个和父类一样的方法来覆盖从父类中继承下来的版本，该方式就叫做 方法的重写（Override）。  

#### 方法重写的原则

- 要求方法名相同、参数列表相同以及返回值类型相同，从Java5开始允许 返回子类类型。
- 要求方法的访问权限不能变小，可以相同或者变大。
- 要求方法不能抛出更大的异常(异常机制)。  

#### 实际案例

- 编程实现Animal类的封装，特征有：名字和毛色，要求提供打印所有特 征的方法。
- 编程实现Dog类的封装并继承自Animal类，该类的特征有：牙齿数量，要 求提供打印所有特征的方法。
- 编程实现DogTest类，在main方法中分别使用无参和有参方式构造Dog类 型对象并打印特征。  

```java
// Animal类
public class Animal {
    private String name;
    private String color;

    public Animal() {}
    public Animal(String name, String color) {
        setName(name);
        setColor(color);
    }

    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getColor() {
        return color;
    }
    public void setColor(String color) {
        this.color = color;
    }

    public void show() {
        // sout 回车   生成打印的语句
        System.out.println("名字：" + getName() + ", 颜色：" + getColor());
    }
}

// Dog类
public class Dog extends Animal{
    private int tooth;
    public Dog() {
        super(); // 表示调用父类的无参构造方法  自动保存
    }
    public Dog(String name, String color, int tooth) {
        super(name, color); // 表示调用父类的有参构造方法
        setTooth(tooth);
    }

    public int getTooth() {
        return tooth;
    }
    public void setTooth(int tooth) {
        if (tooth > 0) {
            this.tooth = tooth;
        } else {
            System.out.println("牙齿数量不合理哦！！！");
        }
    }

    @Override
    public void show() {
        super.show();
        System.out.println("牙齿数量是：" + getTooth());
    }
}

// DogTest
public class DogTest {
    public static void main(String[] args) {
        // 1.使用无参方式构造Dog类型的对象并打印特征
        Dog d1 = new Dog();
        d1.show(); // null null 0

        // 2.使用有参方式构造Dog类型的对象并打印特征
        Dog d2 = new Dog("旺财", "白色", 10);
        d2.show(); // 旺财 白色  10
    }
}
```

#### 构造块与静态代码块（笔试要点）

- 先执行父类的静态代码块，再执行子类的静态代码块。
- 执行父类的构造块，执行父类的构造方法体。
- 执行子类的构造块，执行子类的构造方法体。  

### 访问控制  

#### 常用的访问控制符 

![image-20221204032039671]([picture\](https://github.com/2016061429/JavaNote/tree/main/JavaSE/picture/)image-20221204032039671.png)

#### 注意事项

- public修饰的成员可以在任意位置使用。
- private修饰的成员只能在本类内部使用。
- 通常情况下，成员方法都使用public关键字修饰，成员变量都使用private 关键字修饰。  

#### 包的定义

- 在定义一个类时，除了定义类的名称一般还要指定一个包名，格式如下： 
  - package 包名;  
  - package 包名1.包名2.包名3...包名n; 
- 为了实现项目管理、解决命名冲突以及权限控制的效果。  



### final关键字 

#### 基本概念

- final本意为"最终的、不可改变的"，可以修饰类、成员方法以及成员变量。  

#### 使用方式

- final关键字修饰类体现在该类不能被继承。
  - 主要用于防止滥用继承，如：java.lang.String类等。
- final关键字修饰成员方法体现在该方法不能被重写但可以被继承。
  - 主要用于防止不经意间造成重写，如：java.text.Dateformat类中format方法等。
- final关键字修饰成员变量体现在该变量必须初始化且不能改变。 
  - 主要用于防止不经意间造成改变，如：java.lang.Thread类中MAX_PRIORITY等。  

#### 常量的概念（找个例子）

- 在以后的开发中很少单独使用final关键字来修饰成员变量，通常使用 public static final关键字共同修饰成员变量来表达常量的含义，常量的命 名规范要求是所有字母都要大写，不同的单词之间采用下划线连。 
- public static final double PI = 3.14 



### 多态 

#### 多态的语法格式 

#### 案例题目（看一下讲解）

- 编程实现Shape类的封装，特征有：横纵坐标，要求提供打印所有特征的 方法。
- 编程实现Rect类的封装并继承自Shape类，特征有：长度和宽度。
- 编程实现ShapeRectTest类，在main方法中分别创建Shape和Rect类型对 象并打印特征。  

```java
// Shape
public class Shape {
    private int x;
    private int y;

    public Shape() {
    }

    public Shape(int x, int y) {
        setX(x);
        setY(y);
    }

    public int getX() {
        return x;
    }

    public void setX(int x) {
        this.x = x;
    }

    public int getY() {
        return y;
    }

    public void setY(int y) {
        this.y = y;
    }

    public void show() {
        System.out.println("横坐标：" + getX() + "，纵坐标：" + getY());
    }

    // 自定义静态方法
    public static void test() {
        System.out.println("Shape类中的静态方法！");
    }
}

// Rect
public class Rect extends Shape {
    private int len;
    private int wid;

    public Rect() {
    }

    public Rect(int x, int y, int len, int wid) {
        super(x, y);
        setLen(len);
        setWid(wid);
    }

    public int getLen() {
        return len;
    }

    public void setLen(int len) {
        if(len > 0) {
            this.len = len;
        } else {
            System.out.println("长度不合理哦！！！");
        }
    }

    public int getWid() {
        return wid;
    }

    public void setWid(int wid) {
        if (wid > 0) {
            this.wid = wid;
        } else {
            System.out.println("宽度不合理哦！！！");
        }
    }

    @Override
    public void show() {
        super.show();
        System.out.println("长度是：" + getLen() + "，宽度是：" + getWid());
    }

    // 自定义静态方法
    //@Override Error: 历史原因、不是真正意义上的重写
    public static void test() {
        System.out.println("---Rect类中的静态方法！");
    }
}

// Test
public class ShapeRectTest {

    public static void main(String[] args) {

        // 1.声明Shape类型的引用指向Shape类型的对象并打印特征
        Shape s1 = new Shape(1, 2);
        // 当Rect类中没有重写show方法时，下面调用Shape类中的show方法
        // 当Rect类中重写show方法后，下面调用Shape类中的show方法
        s1.show(); // 1 2

        // 使用ctrl+d快捷键可以复制当前行
        System.out.println("------------------------------------");
        // 2.声明Rect类型的引用指向Rect类型的对象并打印特征
        Rect r1 = new Rect(3, 4, 5, 6);
        // 当Rect类中没有重写show方法时，下面调用Shape类中的show方法
        // 当Rect类中重写show方法后，下面调用Rect类中的show方法
        r1.show(); // 3 4 5 6

        // 使用alt+shift+上下方向键  可以移动代码
        System.out.println("------------------------------------");
        // 3.声明Shape类型的引用指向Rect类型的对象并打印特征
        // 相当于从Rect类型到Shape类型的转换  也就是子类到父类的转换   小到大的转换  自动类型转换
        Shape sr = new Rect(7, 8, 9, 10);
        // 当Rect类中没有重写show方法时，下面调用Shape类中的show方法
        // 当Rect类中重写show方法后，下面的代码在编译阶段调用Shape类的方法，在运行阶段调用Rect类中的show方法
        sr.show(); // 7 8 9 10

        System.out.println("------------------------------------");
        // 4.测试Shape类型的引用能否直接调用父类和子类独有的方法呢？？？
        int ia = sr.getX();
        System.out.println("获取到的横坐标是：" + ia); // 7
        //sr.getLen();  error  Shape类中找不到getLen方法，也就是还在Shape类中查找

        // 调用静态方法
        sr.test(); // 提示：不建议使用引用.的方式访问
        Shape.test(); // 推荐使用类名.的方式访问

        System.out.println("------------------------------------");
        // 5.使用父类类型的引用调用子类独有方法的方式
        // 相当于从Shape类型到Rect类型的转换，也就是父类到子类的转换  大到小的转换   强制类型转换
        int ib = ((Rect) sr).getLen();
        System.out.println("获取到的长度是：" + ib); // 9

        // 希望将Shape类型转换为String类型  强制类型转换要求必须拥有父子类关系
        //String str1 = (String)sr;  Error
        // 希望将Shape类型强制转换为Circle类型，下面没有报错
        //Circle c1 = (Circle)sr; // 编译ok，但运行阶段发生  ClassCastException类型转换异常

        // 在强制类型转换之前应该使用instanceof进行类型的判断
        // 判断sr指向堆区内存中的对象是否为Circle类型，若是则返回true，否则返回false
        if(sr instanceof Circle) {
            System.out.println("可以放心地转换了！");
            Circle c1 = (Circle)sr;
        } else {
            System.out.println("强转有风险，操作需谨慎！");
        }
    }
}

```

#### 多态的特点 

- 当父类类型的引用指向子类类型的对象时，父类类型的引用可以直接调 用父类独有的方法。 
- 当父类类型的引用指向子类类型的对象时，父类类型的引用不可以直接 调用子类独有的方法。 
- 对于父子类都有的非静态方法来说，编译阶段调用父类版本，运行阶段 调用子类重写的版本（动态绑定）。
- 对于父子类都有的静态方法来说，编译和运行阶段都调用父类版本。  

#### 引用数据类型之间的转换

- 引用数据类型之间的转换方式有两种：自动类型转换和强制类型转换。
- 自动类型转换主要指小类型向大类型的转换，也就是子类转为父类，也叫做向上转型。
- 强制类型转换主要指大类型向小类型的转换，也就是父类转为子类，也 叫做向下转型或显式类型转换。 
- 引用数据类型之间的转换必须发生在父子类之间，否则编译报错。  
- 若强转的目标类型并不是该引用真正指向的数据类型时则编译通过，运行阶段发生类型转换异常。
- 为了避免上述错误的发生，应该在强转之前进行判断，格式如下： 
  - if(引用变量 instanceof 数据类型)  
  - 判断引用变量指向的对象是否为后面的数据类型 

#### 多态的实际意义

- 多态的实际意义在于屏蔽不同子类的差异性实现通用的编程带来不同的 效果。  



### 抽象类 

#### 抽象方法的概念

- 抽象方法主要指不能具体实现的方法并且使用abstract关键字修饰，也就 是没有方法体。
- 抽象类主要指不能具体实例化的类并且使用abstract关键字修饰，也就是 不能创建对象。  
- 具体格式如下： 

```java
//访问权限 abstract 返回值类型 方法名(形参列表);  
public abstract void cry();  
```

#### 抽象类和抽象方法的关系 

- 抽象类中可以有成员变量、构造方法、成员方法；
- 抽象类中可以没有抽象方法，也可以有抽象方法；
- 拥有抽象方法的类必须是抽象类，因此真正意义上的抽象类应该是具有 抽象方法并且使用abstract关键字修饰的类。 

#### 抽象类的实际意义 

- 抽象类的实际意义不在于创建对象而在于被继承。
- 当一个类继承抽象类后必须重写抽象方法，否则该类也变成抽象类，也就是抽象类对子类具有强制性和规范性，因此叫做模板设计模式。 

开发经验分享 

- 在以后的开发中推荐使用多态的格式，此时父类类型引用直接调用的所 有方法一定是父类中拥有的方法，若以后更换子类时，只需要将new关键 字后面的子类类型修改而其它地方无需改变就可以立即生效，从而提高 了代码的可维护性和可扩展型。
- 该方式的缺点就是：父类引用不能直接调用子类独有的方法，若调用则 需要强制类型转换。 

####  抽象类的应用 ()

- 银行有 定期账户和活期账户。继承自 账户类。账户类中： 

```java
public class Account{
	private double money;
	public double getLixi(){}
}
```

```java
public /*final*/ abstract class Account {
    private int money;

    public Account() {
    }

    public Account(int money) {
        setMoney(money);
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        if (money >= 0) {
            this.money = money;
        } else {
            System.out.println("金额不合理哦！！！");
        }
    }

    // 自定义抽象方法实现计算利息并返回的功能描述
    public abstract double getLixi();
    // private 和 abstract 关键字不能共同修饰一个方法
    //private abstract double getLixi();
    // final 和 abstract 关键字不能共同修饰一个方法
    //public final abstract double getLixi();
    // static 和 abstract 关键字不能共同修饰一个方法
    //public static abstract double getLixi();
}

//
public abstract class AbstractTest {
    private int cnt;

    public AbstractTest() {
    }

    public AbstractTest(int cnt) {
        setCnt(cnt);
    }

    public int getCnt() {
        return cnt;
    }

    public void setCnt(int cnt) {
        this.cnt = cnt;
    }

    // 自定义抽象方法
    public abstract void show();

    public static void main(String[] args) {

        // 声明该类类型的引用指向该类类型的对象
        //AbstractTest at = new AbstractTest();
        //System.out.println("at.cnt = " + at.cnt); // 0
    }
}
```



### 接口

#### 接口的基本概念

- 接口就是一种比抽象类还抽象的类，体现在所有方法都为抽象方法。
- 定义类的关键字是class，而定义接口的关键字是interface。
- 如： 金属接口 货币接口 黄金类  

练习题目 

- 编程实现Runner接口，提供一个描述奔跑行为的抽象方法。
- 编程实现Hunter接口继承Runner接口，并提供一个描述捕猎行为的抽象 方法。 
- 编程实现Man类实现Hunter接口并重写抽象方法，在main方法中使用多 态方式测试。  

```java
// Runner
public interface Runner {
    // 自定义抽象方法描述奔跑的行为
    public abstract void run();
}

// Hunter
// 接口只能继承接口，不能继承类
public interface Hunter extends Runner {
    // 自定义成员方法描述捕猎的行为
    public abstract void hunt();

    // 将两个默认方法中重复的代码可以提取出来打包成一个方法在下面的两个方法中分别调用即可
    private void show() {
        System.out.println("在以后的开发中尽量减少重复的代码，也就是减少代码的冗余！");
    }
    // 增加一个抽象方法
    //public abstract void show1();
    // 增加非抽象方法
    public default void show1() {
        show();
        //System.out.println("在以后的开发中尽量减少重复的代码，也就是减少代码的冗余！");
        System.out.println("show1方法中：这里仅仅是接口中的默认功能，实现类可以自由选择是否重写！");
    }

    // 增加非抽象方法
    public default void show2() {
        show();
        //System.out.println("在以后的开发中尽量减少重复的代码，也就是减少代码的冗余！");
        System.out.println("show2方法中：这里仅仅是接口中的默认功能，实现类可以自由选择是否重写！");
    }

    // 增加静态方法 隶属于类层级，也就是接口层级
    public static void test() {
        System.out.println("这里是静态方法，可以直接通过接口名.的方式调用，省略对象的创建");
    }
}

// Man
public class Man implements Hunter {
    @Override
    public void hunt() {
        System.out.println("正在追赶一直小白兔...");
    }

    @Override
    public void run() {
        System.out.println("正在被一直大熊追赶，玩命奔跑中...");
    }

    @Override
    public void show1() {
        System.out.println("为了给你几分薄面，我决定重写一下！");
    }

    public static void main(String[] args) {

        // 1.声明接口类型的引用指向实现类的对象，形成了多态
        Runner runner = new Man();
        runner.run();

        Hunter hunter = new Man();
        hunter.hunt();

        System.out.println("-----------------------------------------");
        // 2.可以使用接口名称.的方式调用接口中的静态方法
        Hunter.test();
    }
}
```

#### 类和接口之间的关系 

![image-20221204164227026](picture\image-20221204164227026.png)

#### 抽象类和接口的主要区别（笔试题）

- 定义抽象类的关键字是abstract class，而定义接口的关键字是interface。 
- 继承抽象类的关键字是extends，而实现接口的关键字是implements。
- 继承抽象类支持单继承，而实现接口支持多实现。
- 抽象类中可以有构造方法，而接口中不可以有构造方法。
- 抽象类中可以有成员变量，而接口中只可以有常量。 
- 抽象类中可以有成员方法，而接口中只可以有抽象方法。 
- 抽象类中增加方法时子类可以不用重写，而接口中增加方法时实现类需 要重写（Java8以前的版本）。
- 从Java8开始增加新特性，接口中允许出现非抽象方法和静态方法，但非 抽象方法需要使用default关键字修饰。
- 从Java9开始增加新特性，接口中允许出现私有方法。  



##  特殊类 

### 内部类（熟悉）

#### 静态内部类的格式 

```java
访问修饰符 class 外部类的类名 {
	访问修饰符 static class 内部类的类名 {
		内部类的类体;
	} 
} 
```

#### 匿名内部类的语法格式（重点）

- 接口/父类类型 引用变量名 = new 接口/父类类型() { 方法的重写 };  

枚举

注解

#### 常见的预制注解 

![image-20221204165027918](picture\image-20221204165027918.png)

![image-20221204165045675](picture\image-20221204165045675.png)

## 常用类的概述和使用 

### 常用的包（熟悉） 

- java.lang包 - 该包是Java语言的核心包，并且该包中的所有内容由Java虚拟机自动导入。 如：System类、String类、...  
- java.util包 - 该包是Java语言的工具包，里面提供了大量工具类以及集合类等。 如：Scanner类、Random类、List集合、... 
- java.io包 - 该包是Java语言中的输入输出包，里面提供了大量读写文件相关的类等。 如：FileInputStream类、FileOutputStream类、... 
- java.net包 - 该包是Java语言中的网络包，里面提供了大量网络编程相关的类等。 如：ServerSocket类、Socket类、... 
- java.sql 包 - 该包是Java语言中的数据包，里面提供了大量操作数据库的类和接口等。 如：DriverManager类、Connection接口、… ... ... 
- Java程序员在编程时可以使用大量类库，因此Java编程时需要记的很多，对编程能力本身要求不是 特别的高。  



### Object类的概述（重点） 

基本概念

- java.lang.Object类是Java语言中类层次结构的根类，也就是说任何一个类都是该类的直接或者间接子类。 
- 如果定义一个Java类时没有使用extends关键字声明其父类，则其父类为 java.lang.Object 类。 
- Object类定义了“对象”的基本行为, 被子类默认继承。 

常用的方法  

![image-20221207154636249](picture\image-20221207154636249.png)

案例题目： 

- 编程实现Student类的封装，特征：学号(id)和姓名，要求提供打印所有特征的方法。 
- 编程实现StudentTest类，在main方法中使用有参方式构造两个Student类型的对象并打印特征。 

题目扩展:  

- 如何实现以姓名作为基准判断两个对象是否相等？以及以学号和姓名同时作为基准判断两个对象是 否相等？ 

```java
// Studnt
public class Student extends Object {
    private int id; // 用于描述学号的成员变量
    private String name; // 用于描述姓名的成员变量

    public Student() {
    }

    public Student(int id, String name) {
        setId(id);
        setName(name);
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        if (id > 0) {
            this.id = id;
        } else {
            System.out.println("学号不合理哦！！！");
        }
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return id == student.id &&
                Objects.equals(name, student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}

// Test
public class StudentTest {

    public static void main(String[] args) {

        // 1.使用有参方式构造Student类型的两个对象并判断是否相等
        Student s1 = new Student(1001, "zhangfei");
        //Student s2 = new Student(1002, "guanyu");
        Student s2 = new Student(1001, "zhangfei");
        //Student s2 = s1;  // 表示s2和s1都指向了同一个对象，地址相同了
        // 下面调用从Object类中继承下来的equals方法，该方法默认比较两个对象的地址，可以查看源码验证
        // 当Student类中重写equals方法后，则调用重写以后的版本，比较内容
        //boolean b1 = s1.equals(s2);
        //Student s3 = null;
        //boolean b1 = s1.equals(s3);
        //Student s3 = s1;
        boolean b1 = s1.equals(s2);
        System.out.println("b1 = " + b1); // false true
        System.out.println(s1 == s2); // 比较地址  false

        System.out.println("----------------------------------------------------------");
        // 下面调用从Object类中继承下来的hashCode方法，获取调用对象的哈希码值(内存地址的编号)
        // 当Student类中重写hashCode方法后，则调用重写以后的版本
        int ia = s1.hashCode();
        int ib = s2.hashCode();
        System.out.println("ia = " + ia);
        System.out.println("ib = " + ib);

        System.out.println("----------------------------------------------------------");
        // 下面调用从Object类中继承下来的toString方法，获取调用对象的字符串形式：包名.类名@哈希码值的十六进制
        // 当Student类中重写toString方法后，则调用重写以后的版本：Student[id = 1001, name = zhangfei]
        String str1 = s1.toString();
        System.out.println("str1 = " + str1); // com.lagou.task11.Student@55d
        System.out.println(s1); // 当打印一个引用变量时会自动调用toString方法
        String str2 = "hello" + s1;
        System.out.println("str2 = " + str2);
    }
}
```



###  包装类 

包装类的概念

- 通常情况下基本数据类型的变量不是对象，为了满足万物皆对象的理念就需要对基本数据类型的变 量进行打包封装处理变成对象，而负责将这些变量声明为成员变量进行对象化处理的相关类，叫做包装 类。 如： 

  ```java
  Person p = new Person(); 
  int num = 10; 
  ```

 包装类的分类 

![image-20221207155656635](picture\image-20221207155656635.png) 



#### Integer类的概述 

基本概念： java.lang.Integer类内部包装了一个int类型的变量作为成员变量，主要用于实现对int类型的包装并 提供int类型到String类之间的转换等方法。

常用的常量

 ![image-20221207160028705](picture\image-20221207160028705.png)

常用方法

![image-20221207160128236](picture\image-20221207160128236.png)

装箱和拆箱的概念

- 在Java5发布之前使用包装类对象进行运算时，需要较为繁琐的“拆箱”和“装箱”操作；即运算前先将 包装类对象拆分为基本类型数据，运算后再将结果封装成包装类对象。 从Java5开始增加了自动拆箱和自动装箱的功能。 

自动装箱池 

- 在Integer类的内部提供了自动装箱池技术，将-128到127之间的整数已经装箱完毕，当程序中使用 该范围之间的整数时，无需装箱直接取用自动装箱池中的对象即可，从而提高效率。  



#### Double类的概述 

基本概念

- java.lang.Double类型内部包装了一个double类型的变量作为成员变量，主要用于实现对double 类型的包装并提供double类型到String类之间的转换等方法。 

常用的常量

![image-20221207161829958](picture\image-20221207161829958.png) 

 常用的方法  

![image-20221207162043319](picture\image-20221207162043319.png)



#### Boolean类的概述 

-  java.lang.Boolean类型内部包装了一个boolean类型的变量作为成员变量，主要用于实现对 boolean类型的包装并提供boolean类型到String类之间的转换等方法。 

#### Character类的概述   

-  java.lang.Character类型内部包装了一个char类型的变量作为成员变量，主要用于实现对char类型 的包装并提供字符类别的判断和转换等方法。 

#### 包装类（Wrapper）的使用总结 

- 基本数据类型转换为对应包装类的方式 调用包装类的构造方法或静态方法即可 
- 获取包装类对象中基本数据类型变量数值的方式 调用包装类中的xxxValue方法即可 
- 字符串转换为基本数据类型的方式 调用包装类中的parseXxx方法即可  



### 数学处理类（熟悉） 

#### Math类的概述  

基本概念

-  java.lang.Math类主要用于提供执行数学运算的方法，如：对数，平方根。 

####  BigDecimal类的概述 

基本概念 

- 由于float类型和double类型在运算时可能会有误差，若希望实现精确运算则借助 java.math.BigDecimal类型加以描述。 

#### BigInteger类的概述  

基本概念 

- 若希望表示比long类型范围还大的整数数据，则需要借助java.math.BigInteger类型描述。  



## String类的概述和使用 

String类的概念（重点） 

- java.lang.String类用于描述字符串，Java程序中所有的字符串字面值都可以使用该类的对象加以描 述，如："abc"。 
- 该类由final关键字修饰，表示该类不能被继承。 
- 从jdk1.9开始该类的底层不使用char[]来存储数据，而是改成 byte[]加上编码标记，从而节约了一 些空间。 
- 该类描述的字符串内容是个常量不可更改，因此可以被共享使用。 

```java
//如：
 String str1 = “abc”; - 其中"abc"这个字符串是个常量不可改变。 
 str1 = “123”; - 将“123”字符串的地址赋值给变量str1。
 - 改变str1的指向并没有改变指向的内容
```

常量池的概念（原理） 

- 由于String类型描述的字符串内容是常量不可改变，因此Java虚拟机将首次出现的字符串放入常量 池中，若后续代码中出现了相同字符串内容则直接使用池中已有的字符串对象而无需申请内存及创建对 象，从而提高了性能。 

常用的构造方法（练熟、记住） 

![image-20221207164614201](picture\image-20221207164614201.png)

常用的成员方法（练熟、记住）  

<img src="picture\image-20221207164946946.png" alt="image-20221207164946946" style="zoom:80%;" />

案例题目 判断字符串“上海自来水来自海上”是否为回文并打印，所谓回文是指一个字符序列无论从左向右读 还是从右向左读都是相同的句子。 

```java
public class StringJudgeTest {

    public static void main(String[] args) {

        // 1.创建字符串对象并打印
        String str1 = new String("上海自来水来自海上");
        System.out.println("str1 = " + str1); // 上海自来水来自海上   9
        // 2.判断该字符串内容是否为回文并打印
        for (int i = 0; i < str1.length()/2; i++) {
            if (str1.charAt(i) != str1.charAt(str1.length()-i-1)) {  // 0和8   1和7  2和6  3和5
                System.out.println(str1 + "不是回文！");
                return;  // 仅仅是用于实现方法的结束
            }
        }
        System.out.println(str1 + "是回文！");
    }
}
```

![image-20221207165801291](picture\image-20221207165801291.png)

案例题目 编程实现字符串之间大小的比较并打印。 

```java
// compareTo	compareToIgnoreCase
public class StringCompareTest {
    public static void main(String[] args) {

        // 1.构造String类型的对象并打印
        String str1 = new String("hello");
        System.out.println("str1 = " + str1); // hello

        // 2.使用构造好的对象与其它字符串对象之间比较大小并打印
        System.out.println(str1.compareTo("world"));  // 'h' - 'w' => 104 - 119 => -15
        System.out.println(str1.compareTo("haha"));   // 'e' - 'a' => 101 - 97  => 4
        System.out.println(str1.compareTo("hehe"));   // 'l' - 'h' => 108 - 104 => 4
        System.out.println(str1.compareTo("heihei")); // 'l' - 'i' => 108 - 105 => 3
        System.out.println(str1.compareTo("helloworld")); // 长度： 5 - 10 => -5
        System.out.println(str1.compareToIgnoreCase("HELLO")); // 0
    }
}
```

![image-20221207170818423](picture\image-20221207170818423.png)

案例题目 编程实现上述方法的使用。 

![image-20221207170940054](picture\image-20221207170940054.png)

案例题目 提示用户从键盘输入用户名和密码信息，若输入”admin”和”123456”则提示“登录成功，欢迎使 用”，否则提示“用户名或密码错误，您还有n次机会”，若用户输入三次后依然错误则提示“账户已 冻结，请联系客服人员！”   

![image-20221207171004766](picture\image-20221207171004766.png)

 案例题目 编写通用的代码可以查询字符串"Good Good Study, Day Day Up!"中所有"Day"出现的索引位置并 打印出来。  

![image-20221207171039727](picture\image-20221207171039727.png)

 案例题目 提示用户从键盘输入一个字符串和一个字符，输出该字符(不含)后面的所有子字符串。  

#### 正则表达式

- 正则表达式本质就是一个“规则字符串”，可以用于对字符串数据的格式进行验证，以及匹配、查 找、替换等操作。该字符串通常使用^运算符作为开头标志，使用$运算符作为结尾标志，当然也可以省 略。 

 正则表达式的规则 

![image-20221207171305769](picture\image-20221207171305769.png)

![image-20221207171335578](picture\image-20221207171335578.png)

## 可变字符串类和日期相关类 (待整理)

可变字符串类 

Java8之前的日期相关类 

Java8中的日期相关类 



## 集合类库 

### 集合的概述

集合的由来  

- 当需要在Java程序中记录单个数据内容时，则声明一个变量。
- 当需要在Java程序中记录多个类型相同的数据内容时，声明一个一维数组。
- 当需要在Java程序中记录多个类型不同的数据内容时，则创建一个对象。
- 当需要在Java程序中记录多个类型相同的对象数据时，创建一个对象数组。
- 当需要在Java程序中记录多个类型不同的对象数据时，则准备一个集合。

集合的框架结构 

- Java中集合框架顶层框架是：java.util.Collection集合 和 java.util.Map集合。  
- 其中Collection集合中存取元素的基本单位是：单个元素。 
- 其中Map集合中存取元素的基本单位是：单对元素。  

### Collection集合 （重点）

基本概念

-  java.util.Collection接口是List接口、Queue 接口以及Set接口的父接口，因此该接口里定义的方法 既可用于操作List集合，也可用于操作Queue集合和Set集合。 

常用的方法（练熟、记住）  

![image-20221207174042199](picture\image-20221207174042199.png)

```java

```



### Iterator接口（重点）  

基本概念

- java.util.Iterator接口主要用于描述迭代器对象，可以遍历Collection集合中的所有元素。 
- java.util.Collection接口继承Iterator接口，因此所有实现Collection接口的实现类都可以使用该迭 代器对象。 

常用的方法

![image-20221207175302504](picture\image-20221207175302504.png)

 案例题目： 如何使用迭代器实现toString方法的打印效果？ 

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;
import java.util.Iterator;

public class CollectionPrintTest {

    public static void main(String[] args) {

        // 1.准备一个Collection集合并放入元素后打印
        Collection c1 = new ArrayList();
        c1.add("one");
        c1.add(2);
        c1.add(new Person("zhangfei", 30));
        // 遍历方式一： 自动调用toString方法   String类型的整体
        System.out.println("c1 = " + c1); // [one, 2, Person{name='zhangfei', age=30}]

        System.out.println("------------------------------------------------");
        // 2.遍历方式二：使用迭代器来遍历集合中的所有元素  更加灵活
        // 2.1 获取当前集合中的迭代器对象
        Iterator iterator1 = c1.iterator();
        while (iterator1.hasNext()) {
            System.out.println("获取到的元素是：" + iterator1.next());
        }

        System.out.println("------------------------------------------------");
        // 由于上个循环已经使得迭代器走到了最后，因此需要重置迭代器
        iterator1 = c1.iterator();
        // 3.使用迭代器来模拟toString方法的打印效果
        StringBuilder sb1 = new StringBuilder();
        sb1.append("[");
        while (iterator1.hasNext()) {
            Object obj = iterator1.next();
            // 当获取的元素是最后一个元素时，则拼接元素加中括号
            if (!iterator1.hasNext()) {
                sb1.append(obj).append("]");
            } else {
                // 否则拼接元素加逗号加空格
                sb1.append(obj).append(",").append(" ");
            }
        }
        // [one, 2, Person{name='zhangfei', age=30}]
        System.out.println("c1 = " + sb1);

        System.out.println("------------------------------------------------");
        // 4.不断地去获取集合中的元素并判断，当元素值为"one"时则删除该元素
        iterator1 = c1.iterator();
        while (iterator1.hasNext()) {
            Object obj = iterator1.next();
            if("one".equals(obj)) {
                iterator1.remove();  //使用迭代器的remove方法删除元素没问题
                //c1.remove(obj); // 使用集合的remove方法编译ok，运行发生ConcurrentModificationException并发修改异常
            }
        }
        System.out.println("删除后集合中的元素有：" + c1); // [2, Person{name='zhangfei', age=30}]

        System.out.println("------------------------------------------------");
        // 5.使用 for each结构实现集合和数组中元素的遍历  代码简单且方法灵活
        // 由调试源码可知：该方式确实是迭代器的简化版
        for (Object obj : c1) {
            System.out.println("取出来的元素是：" + obj);
        }

        int[] arr = new int[] {11, 22, 33, 44, 55};
        for (int i : arr) {
            System.out.println("i = " + i);
            i = 66; // 修改局部变量i的数值，并不是修改数组中元素的数值
        }
        System.out.println("数组中的元素有：" + Arrays.toString(arr));

    }
}
```



### for each循环（重点） 

基本概念 

- Java5推出了增强型for循环语句，可以应用数组和集合的遍历。 
- 是经典迭代的“简化版”。 

语法格式

```java
for(元素类型 变量名 : 数组/集合名称) {
 	循环体;
}
```

执行流程

-   不断地从数组/集合中取出一个元素赋值给变量名并执行循环体，直到取完所有元素为止。 



### List集合（重中之重） 

基本概念

- java.util.List集合是Collection集合的子集合，该集合中允许有重复的元素并且有先后放入次序。 
- 该集合的主要实现类有：ArrayList类、LinkedList类、Stack类、Vector类。 
- 其中ArrayList类的底层是采用动态数组进行数据管理的，支持下标访问，增删元素不方便。 
- 其中LinkedList类的底层是采用双向链表进行数据管理的，访问不方便，增删元素方便。 
- 可以认为ArrayList和LinkedList的方法在逻辑上完全一样，只是在性能上有一定的差别，ArrayList 更适合于随 机访问而LinkedList更适合于插入和删除；在性能要求不是特别苛刻的情形下可以忽略这个差别。 
- 其中Stack类的底层是采用动态数组进行数据管理的，该类主要用于描述一种具有后进先出特征的 数据结构，叫做栈(last in first out LIFO)。 
- 其中Vector类的底层是采用动态数组进行数据管理的，该类与ArrayList类相比属于线程安全的 类，效率比较低，以后开发中基本不用。 

常用的方法  

![image-20221207220347082](picture\image-20221207220347082.png)

案例题目 

- 准备一个Stack集合，将数据11、22、33、44、55依次入栈并打印，然后查看栈顶元素并打印， 然后将栈中所有数据依次出栈并打印。 再准备一个Stack对象，将数据从第一个栈中取出来放入第二个栈中，然后再从第二个栈中取出并 打印。  

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class ListTest {

    public static void main(String[] args) {

        // 1.声明一个List接口类型的引用指向ArrayList类型的对象，形成了多态
        // 由源码可知：当new对象时并没有申请数组的内存空间
        List lt1 = new ArrayList();
        // 2.向集合中添加元素并打印
        // 由源码可知：当调用add方法添加元素时会给数组申请长度为10的一维数组，扩容原理是：原始长度的1.5倍
        lt1.add("one");
        System.out.println("lt1 = " + lt1); // [one]

        System.out.println("----------------------------------------------------");
        // 2.声明一个List接口类型的引用指向LinkedList类型的对象，形成了多态
        List lt2 = new LinkedList();
        lt2.add("one");
        System.out.println("lt2 = " + lt2); // [one]
    }
}
```

### Queue集合（重点） 

基本概念

- java.util.Queue集合是Collection集合的子集合，与List集合属于平级关系。 
- 该集合的主要用于描述具有先进先出特征的数据结构，叫做队列(first in first out FIFO)。 
- 该集合的主要实现类是LinkedList类，因为该类在增删方面比较有优势。  

常用的方法 

![image-20221207220827908](picture\image-20221207220827908.png)

案例题目：准备一个Queue集合，将数据11、22、33、44、55依次入队并打印，然后查看队首元素并打印， 然后将队列中所有数据依次出队并打印 

```java
public class QueueTest {

    public static void main(String[] args) {

        // 1.准备一个Queue集合并打印
        Queue queue = new LinkedList();
        System.out.println("队列中的元素有：" + queue); // [啥也没有]

        System.out.println("----------------------------------------------------------");
        // 2.将数据11、22、33、44、55依次入队并打印
        for (int i = 1; i <= 5; i++) {
            boolean b1 = queue.offer(i * 11);
            //System.out.println("b1 = " + b1);
            System.out.println("队列中的元素有：" + queue); // 11 22 33 44 55
        }

        System.out.println("----------------------------------------------------------");
        // 3.然后查看队首元素并打印
        System.out.println("对首元素是：" + queue.peek()); // 11

        System.out.println("----------------------------------------------------------");
        // 4.然后将队列中所有数据依次出队并打印
        int len = queue.size();
        for (int i = 1; i <= len; i++) {
            System.out.println("出队的元素是：" + queue.poll()); // 11 22 33 44 55
        }

        System.out.println("----------------------------------------------------------");
        // 5.查看队列中最终的元素
        System.out.println("队列中的元素有：" + queue); // [啥也没有]
    }
}
```



### 泛型机制（熟悉）  

基本概念 

- 通常情况下集合中可以存放不同类型的对象，是因为将所有对象都看做Object类型放入的，因此 从集合中取出元素时也是Object类型，为了表达该元素真实的数据类型，则需要强制类型转换， 而强制类型转换可能会引发类型转换异常。 
- 为了避免上述错误的发生，从Java5开始增加泛型机制，也就是在集合名称的右侧使用<数据类型> 的方式来明确要求该集合中可以存放的元素类型，若放入其它类型的元素则编译报错。 
- 泛型只在编译时期有效，在运行时期不区分是什么类型。 

### Set集合（熟悉） 

基本概念 

- java.util.Set集合是Collection集合的子集合，与List集合平级。 
- 该集合中元素没有先后放入次序，且不允许重复。 
- 该集合的主要实现类是：HashSet类 和 TreeSet类以及LinkedHashSet类。 
- 其中HashSet类的底层是采用哈希表进行数据管理的。 
- 其中TreeSet类的底层是采用红黑树进行数据管理的。 
- 其中LinkedHashSet类与HashSet类的不同之处在于内部维护了一个双向链表，链表中记录了元 素的迭代顺序，也就是元素插入集合中的先后顺序，因此便于迭代。  

### Map集合（重点） 

基本概念

-  java.util.Map集合中存取元素的基本单位是：单对元素，其中类型参数如下： 

  K - 此映射所维护的键(Key)的类型，相当于目录。 

  V - 映射值(Value)的类型，相当于内容。 

-  该集合中key是不允许重复的，而且一个key只能对应一个value。  
-  该集合的主要实现类有：HashMap类、TreeMap类、LinkedHashMap类、Hashtable类、 Properties类。 
-  其中HashMap类的底层是采用哈希表进行数据管理的。 
-  其中TreeMap类的底层是采用红黑树进行数据管理的。
-  其中LinkedHashMap类与HashMap类的不同之处在于内部维护了一个双向链表，链表中记录了 元素的迭代顺序，也就是元素插入集合中的先后顺序，因此便于迭代。  
-  其中Hashtable类是古老的Map实现类，与HashMap类相比属于线程安全的类，且不允许null作 为key或者value的数值。
-  其中Properties类是Hashtable类的子类，该对象用于处理属性文件，key和value都是String类 型的。   
-  Map集合是面向查询优化的数据结构, 在大数据量情况下有着优良的查询性能。 
-  经常用于根据key检索value的业务场景。 

常用的方法

![image-20221207232735104](picture\image-20221207232735104.png)

元素放入HashMap集合的原理  

- 使用元素的key调用hashCode方法获取对应的哈希码值，再由某种哈希算法计算在数组中的索引 位置。 
- 若该位置没有元素，则将该键值对直接放入即可。 
- 若该位置有元素，则使用key与已有元素依次比较哈希值，若哈希值不相同，则将该元素直接放 入。 
- 若key与已有元素的哈希值相同，则使用key调用equals方法与已有元素依次比较。 
- 若相等则将对应的value修改，否则将键值对直接放入即可。 

```java
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class MapTest {

    public static void main(String[] args) {

        // 1.准备一个Map集合并打印
        Map<String, String> m1 = new HashMap<>();
        // 自动调用toString方法，默认打印格式为：{key1=value1, key2=value2, ...}
        System.out.println("m1 = " + m1); // {啥也没有}

        // 2.向集合中添加元素并打印
        String str1 = m1.put("1", "one");
        System.out.println("原来的value数值为：" + str1); // null
        System.out.println("m1 = " + m1); // {1=one}

        str1 = m1.put("2", "two");
        System.out.println("原来的value数值为：" + str1); // null
        System.out.println("m1 = " + m1); // {1=one, 2=two}

        str1 = m1.put("3", "three");
        System.out.println("原来的value数值为：" + str1); // null
        System.out.println("m1 = " + m1); // {1=one, 2=two, 3=three}
        // 实现了修改的功能
        str1 = m1.put("1", "eleven");
        System.out.println("原来的value数值为：" + str1); // one
        System.out.println("m1 = " + m1); // {1=eleven, 2=two, 3=three}

        System.out.println("-------------------------------------------------------------");
        // 3.实现集合中元素的查找操作
        boolean b1 = m1.containsKey("11");
        System.out.println("b1 = " + b1); // false
        b1 = m1.containsKey("1");
        System.out.println("b1 = " + b1); // true

        b1 = m1.containsValue("one");
        System.out.println("b1 = " + b1); // false
        b1 = m1.containsValue("eleven");
        System.out.println("b1 = " + b1); // true

        String str2 = m1.get("5");
        System.out.println("str2 = " + str2); // null
        str2 = m1.get("3");
        System.out.println("str2 = " + str2); // three

        System.out.println("-------------------------------------------------------------");
        // 4.实现集合中元素的删除操作
        str2 = m1.remove("1");
        System.out.println("被删除的value是：" + str2); // eleven
        System.out.println("m1 = " + m1); // {2=two, 3=three}

        System.out.println("-------------------------------------------------------------");
        // 5.获取Map集合中所有的key并组成Set视图
        Set<String> s1 = m1.keySet();
        // 遍历所有的key
        for (String ts : s1) {
            System.out.println(ts + "=" + m1.get(ts));
        }

        System.out.println("-------------------------------------------------------------");
        // 6.获取Map集合中所有的Value并组成Collection视图
        Collection<String> co = m1.values();
        for (String ts : co) {
            System.out.println("ts = " + ts);
        }

        System.out.println("-------------------------------------------------------------");
        // 7.获取Map集合中所有的键值对并组成Set视图
        Set<Map.Entry<String, String>> entries = m1.entrySet();
        for (Map.Entry<String, String> me : entries) {
            System.out.println(me);
        }
    }
}
```



### Collections类 

基本概念

- java.util.Collections类主要提供了对集合操作或者返回集合的静态方法。 

常用方法

![image-20221207233024304](picture\image-20221207233024304.png)

```java
import com.lagou.task10.StaticOuter;

import java.util.*;

public class CollectionsTest {

    public static void main(String[] args) {

        // 1.准备一个集合并初始化
        List<Integer> lt1 = Arrays.asList(10, 30, 20, 50, 45);
        // 2.实现集合中元素的各种操作
        System.out.println("集合中的最大值是：" + Collections.max(lt1)); // 50
        System.out.println("集合中的最小值是：" + Collections.min(lt1)); // 10

        // 实现集合中元素的反转
        Collections.reverse(lt1);
        System.out.println("lt1 = " + lt1); // [45, 50, 20, 30, 10]
        // 实现两个元素的交换
        Collections.swap(lt1, 0, 4);
        System.out.println("交换后：lt1 = " + lt1); // [10, 50, 20, 30, 45]
        // 实现元素的排序
        Collections.sort(lt1);
        System.out.println("排序后：lt1 = " + lt1); // [10, 20, 30, 45, 50]
        // 随机置换
        Collections.shuffle(lt1);
        System.out.println("随机置换后：lt1 = " + lt1); // [30, 10, 45, 20, 50] 随机
        // 实现集合间元素的拷贝
        //List<Integer> lt2 = new ArrayList<>(20);
        List<Integer> lt2 = Arrays.asList(new Integer[10]);
        System.out.println("lt1的大小是：" + lt1.size());
        System.out.println("lt2的大小是：" + lt2.size());
        // 表示将lt1中的元素拷贝到lt2中
        Collections.copy(lt2, lt1);
        System.out.println("lt2 = " + lt2);
    }
}
```



## 异常机制和File类 

### 异常机制（重点） 

基本概念 

- 异常就是"不正常"的含义，在Java语言中主要指程序执行中发生的不正常情况。 
- java.lang.Throwable类是Java语言中错误(Error)和异常(Exception)的超类。 
- 其中Error类主要用于描述Java虚拟机无法解决的严重错误，通常无法编码解决，如：JVM挂掉了 等。 
- 其中Exception类主要用于描述因编程错误或偶然外在因素导致的轻微错误，通常可以编码解决， 如：0作为除数等。 
