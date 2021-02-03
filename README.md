## 设计模式的重要性

软件工程中，设计模式（design pattern）是对软件设计中普遍存在（反复出现）的各种问题，所提出的解决方案。这个术语是由埃里希·伽玛（Erich Gamma）等人在 1990 年代从建筑设计领域引入到计算机科学的

设计模式在软件中哪里？面向对象(oo)=>功能模块[设计模式+算法(数据结构)]=>框架[使用到多种设计模式]=> 架构 [服务器集群]

 如果项目开发完后，原来程序员离职，你接手维护该项目怎么办? **(维护性[可读性、规范性])**

目前程序员门槛越来越高，一线 IT 公司(大厂)，都会问你在实际项目中**使用过什么设计模式，怎样使用的，解决了什么问题。**

## 设计模式的目的

编写软件过程中，程序员面临着来自 耦合性，内聚性以及可维护性，可扩展性，重用性，灵活性 等多方面的挑战，设计模式是为了让程序(软件)，具有更好

1. 代码重用性 (即：相同功能的代码，不用多次编写)

2. 可读性 (即：编程规范性,  便于其他程序员的阅读和理解)

3. 可扩展性 (即：当需要增加新的功能时，非常的方便，称为可维护)

4. 可靠性 (即：当我们增加新的功能后，对原来的功能没有影响)

5. 使程序呈现高内聚，低耦合的特性分享金句：

设计模式包含了面向对象的精髓，“懂了设计模式，你就懂了面向对象分析和设计（OOA/D）的精要”

## 设计模式七大原则

设计模式原则，其实就是程序员在编程时，应当遵守的原则，也是各种设计模式的基础(即：设计模式为什么这样设计的依据)

1. 单一职责原则

2. 接口隔离原则

3. 依赖倒转(倒置)原则

4. 里氏替换原则

5. 开闭原则

6. 迪米特法则

7. 合成复用原则

设计的核心思想

1. 找出应用中可能需要变化之处，把它们独立出来，不要和那些不需要变化的代码混在一起。

2. 针对接口编程，而不是针对实现编程。

3. 为了交互对象之间的松耦合设计而努力

### 单一职责原则

1. 基本介绍

   对类来说的，即一个类应该只负责一项职责。如类 A 负责两个不同职责：职责 1，职责 2。当职责 1 需求变更而改变 A 时，可能造成职责 2 执行错误，所以需要将类A 的粒度分解为 A1，A2

2. 单一职责原则注意事项和细节

   1) 降低类的复杂度，一个类只负责一项职责。

   2) 提高类的可读性，可维护性

   3) 降低变更引起的风险

   4) 通常情况下，我们应当遵守单一职责原则，**只有逻辑足够简单，才可以在代码级违反单一职责原则；只有类中方法数量足够少，可以在方法级别保持单一职责原则**

下代码为类级别保持单一职责原则

```java
//方案2的分析
//1.遵守单一职责原则
//2.但是这样做的改动很大，即将类分解，同时修改客户端
//3.改进:直接修改Vehicle类，改动的代码会比较少=>方案三
class RoadVehicle{
    public void run(String vehicle){
        System.out.println(vehicle+"公路运行");
    }
}
class AirVehicle{
    public void run(String vehicle){
        System.out.println(vehicle+"天空运行");
    }
}
class WaterVehicle{
    public void run(String vehicle){
        System.out.println(vehicle+"水中运行");
    }
}
```



下代码为方法级别保持单一职责原则

```java
//方式3的分析
//1.这种修改方法没有对原来的类做大的修改，只是增加方法
//2.这里虽然没有在类这个级别上遵守单一职责原则,但是在方法级别上，仍然是遵守单一职责
class Vehicle2{
    public void run(String vehicle){
        System.out.println(vehicle+"在公路上运行");
    }

    public void runAir(String vehicle){
        System.out.println(vehicle+"在天空运行");
    }

    public void runWater(String vehicle){
        System.out.println(vehicle+"在水中运行");
    }
}
```



### 接口隔离原则

1. 基本介绍

   客户端不应该依赖它不需要的接口，即一个类对另一个类的依赖应该建立在**最小的接口上**

2. 不使用接口隔离原则

<center><img src="https://img-blog.csdnimg.cn/20210203153113651.png" /></center>

1) 类 A 通过接口 Interface1 依赖类 B，类 C 通过接口 Interface1 依赖类 D，如果接口 Interface1 对于类 A 和类 C来说不是最小接口，那么类 B 和类 D 必须去实现他们不需要的方法。

2) 按隔离原则应当这样处理：

将接口 Interface1 拆分为独立的几个接口(这里我们拆分成 3 个接口)，类 A 和类 C 分别与他们需要的接口建立依赖关系。也就是采用接口隔离原则

```java
interface Interface1{
    void operation1();
    void operation2();
    void operation3();
    void operation4();
    void operation5();
}
```



3. 应传统方法的问题和使用接口隔离原则改进

<center><img src="https://img-blog.csdnimg.cn/2021020315321582.png" /></center>

 

1) 类 A 通过接口 Interface1 依赖类 B，类 C 通过接口 Interface1 依赖类 D，如果接口 Interface1 对于类 A 和类 C来说不是最小接口，那么类 B 和类 D 必须去实现他们不需要的方法

2) 将接口 Interface1 拆分为独立的几个接口，类 A 和类 C 分别与他们需要的接口建立依赖关系。也就是采用接口隔离原则

3) 接口 Interface1 中出现的方法，根据实际情况拆分为三个接口

```java
// 接 口 1
interface Interface1 {
    void operation1();
}

// 接 口 2
interface Interface2 {
    void operation2();
    void operation3();
}

// 接 口 3
interface Interface3 {
    void operation4();
    void operation5();
}
```



### 依赖倒转原则

1. 基本介绍

   依赖倒转原则(Dependence Inversion Principle)是指：

   1) **高层模块不应该依赖低层模块，二者都应该依赖其抽象**

   2) **抽象不应该依赖细节，细节应该依赖抽象**

   3) 依赖倒转(倒置)的中心思想是面向接口编程

2. 依赖倒转原则是基于这样的设计理念：

   相对于细节的多变性，抽象的东西要稳定的多。以抽象为基础搭建的架构比以细节为基础的架构要稳定的多。在 java 中，抽象指的是接口或抽象类，细节就是具体的实现类

3. 使用接口或抽象类的目的是**制定好规范**，而不涉及任何具体的操作，把展现细节的任务交给他们的实现类去完成

4. 注意细节

   1) 低层模块尽量都要有抽象类或接口，或者两者都有，程序稳定性更好.

   2) 变量的声明类型尽量是抽象类或接口, 这样我们的变量引用和实际对象间，就

   ​    存在一个缓冲层，利于程序扩展和优化

   3) 继承时遵循里氏替换原则

```java
//定义接口
interface IReceiver {
    public String getInfo();
}

class Email implements IReceiver {
    public String getInfo() {
        return "电子邮件信息: hello,world";
    }
}

//增加微信
class WeiXin implements IReceiver {
    public String getInfo() {
        return "微信信息: hello,ok";
    }
}

class Person {
    //这里我们是对接口的依赖
    public void receive(IReceiver receiver ) { 
        System.out.println(receiver.getInfo());
    }
}

```



### 里氏替换原则

1. OO 中的继承性的思考和说明

   1) 继承包含这样一层含义：父类中凡是已经实现好的方法，实际上是在设定规范			和契约，虽然它不强制要求所有的子类必须遵循这些契约，但是如果子类对这些已经实现的方法任意修改，就会对整个继承体系造成破坏。

   2) 继承在给程序设计带来便利的同时，也带来了弊端。**比如使用继承会给程序带来侵入性，程序的可移植性降低， 增加对象间的耦合性，如果一个类被其他的类所继承，则当这个类需要修改时，必须考虑到所有的子类，并且父类修改后，所有涉及到子类的功能都有可能产生故障**

   3) 问题提出：在编程中，如何正确的使用继承? => 里氏替换原则

2. 基本介绍

   1) 里氏替换原则(Liskov Substitution Principle)在 1988 年，由麻省理工学院的以为姓里的女士提出的。

   2) 如果对每个类型为 T1 的对象 o1，都有类型为 T2 的对象 o2，使得以 T1 定义的所有程序 P 在所有的对象 o1 都代换成 o2 时，程序 P 的行为没有发生变化，那么类型 T2 是类型 T1 的子类型。换句话说，所有引用基类的地方必须能透明地使用其子类的对象。

   3) 在使用继承时，遵循里氏替换原则，**在子类中尽量不要重写父类的方法**

   4) 里氏替换原则告诉我们，继承实际上让两个类耦合性增强了，在适当的情况下，可以通过`聚合，组合，依赖 `来解决问题。.

3. 使用场景

   如果子类不能完整地实现父类的方法，或者父类的某些方法在子类中发生重写或者重载，则建议断开父子继承关系，采用`依赖、聚集、组合`等关系代替继承。如果非要继承，那么当重载的时候就一定要使子类方法的参数一定要大于或等于父类的参数。此时父类称为基类，子类拥有父类的全部属性和方法。并且:

   - 有子类出现的地方父类未必就可以出现

   - 父类出现的地方子类就可以出现

<center><img src="https://img-blog.csdnimg.cn/20210203153246881.png" /></center>

(左上是依赖，左下是聚合，右上是组合)

3. 代码实例

   1) 我们发现原来运行正常的相减功能发生了错误。原因就是类 B 无意中重写了父类的方法，造成原有功能出现错误。在实际编程中，我们常常会通过重写父类的方法完成新的功能，这样写起来虽然简单，但整个继承体系的复用性会比较差。特别是运行多态比较频繁的时候

    

   2) 通用的做法是：原来的父类和子类都继承一个更通俗的基类，原有的继承关系去掉，采用依赖，聚合，组合等关系代替.

   3) 改进方案

<center><img src="https://img-blog.csdnimg.cn/20210203153315516.png" /></center>

 

```java
// A 类
class A extends Base {
    // 返回两个数的差
    public int func1(int num1, int num2) { 
        return num1 - num2;
    }
}

// B 类继承了 A(原先是继承A类，现在进行改进)

// 增加了一个新功能：完成两个数相加,然后和 9 求和
class B extends Base {
    //如果 B 需要使用 A 类的方法,使用组合关系
    private A a = new A();

    //这里，重写了 A 类的方法,  可能是无意识
    public int func1(int a, int b) {
        return a + b;
    }

    public int func2(int a, int b) { 
        return func1(a, b) + 9;
    }

    //我们仍然想使用 A 的方法
    public int func3(int a, int b) { 
        return this.a.func1(a, b);
    }
}
```



### 开闭原则(具体实现与依赖倒转原则相似)

1. 基本介绍

   1) 开闭原则（Open Closed Principle）是编程中最基础、最重要的设计原则

   2) 一个软件实体如类，模块和函数应该对扩展开放(对提供方)，对修改关闭(对使		

     用方)。用抽象构建框架，用实现扩展细节。

   3) 当软件需要变化时，尽量通过扩展软件实体的行为来实现变化，而不是通过修	

     改已有的代码来实现变化。

   4) 编程中遵循其它原则，以及使用设计模式的目的就是遵循开闭原则。

2. 不使用开闭原则(具体代码看代码文件夹)

   <center><img src="https://img-blog.csdnimg.cn/20210203153338331.png" /></center>

   1) 优点是比较好理解，简单易操作。

   2) 缺点是违反了设计模式的 ocp 原则，即对扩展开放(提供方)，对修改关闭(使用方)。即当我们给类增加新功能的时候，尽量不修改代码，或者尽可能少修改代码.

   3) 比如我们这时要新增加一个图形种类 三角形，我们需要做如下修改，修改的地方较多

   4) 代码演示，

   

3. 使用ocp原则进行修改

   思路：把创建 Shape 类做成抽象类，并提供一个抽象的 draw 方法，让子类去实现即可，这样我们有新的图形种类时，只需要让新的图形类继承 Shape，并实现 draw 方法即可，使用方的代码就不需要修  -> 满足了开闭原则

   ```java
   //这是一个用于绘图的类 [使用方]  新增图形时不用此处修改
   class GraphicEditor {
       //接收Shape对象，调用draw方法
       public void drawShape(Shape s) {
           s.draw();
       }
   }
   
   //Shape类，基类
   abstract class Shape {
       int m_type;
   
       public abstract void draw();//抽象方法
   }
   
   //提供方,新增图形只要继承抽象类或者基类就可以了
   class Rectangle extends Shape {
       Rectangle() {
           super.m_type = 1;
       }
   
       @Override
       public void draw() {
           // TODO Auto-generated method stub
           System.out.println(" 绘制矩形 ");
       }
   }
   ```

   

### 迪米特法则	

1. 基本介绍

   1) 一个对象应该对其他对象保持最少的了解

   2) 类与类关系越密切，耦合度越大

   3) 迪米特法则(Demeter Principle)又叫**最少知道原则**，即一个类对自己依赖的类知道的越少越好。也就是说，对于被依赖的类不管多么复杂，都尽量将逻辑封装	在类的内部。**对外除了提供的 public 方法，不对外泄露任何信息**	

   4) 迪米特法则还有个更简单的定义：**只与直接的朋友通信**

   5) **直接的朋友**：每个对象都会与其他对象有耦合关系，只要两个对象之间有耦合关系，我们就说这两个对象之间是朋友关系。耦合的方式很多，依赖，关联， 组合，聚合等。其中，**我们称出现成员变量，方法参数，方法返回值中的类为直接的朋友，而出现在局部变量中的类不是直接的朋友。也就是说，陌生的类最好不要以局部变量的形式出现在类的内部。**

2. 迪米特法则注意事项和细节

   1) 迪米特法则的核心是降低类之间的耦合

   2) 但是注意：由于每个类都减少了不必要的依赖，因此迪米特法则只是要求降低类间(对象间)耦合关系， 并不是要求完全没有依赖关系

3. 代码分析

   ```java
   class class SchoolManager{
       //该方法完成输出学校总部和学院员工信息(id)
       void printAllEmployee(CollegeManager sub) {
   
           //分析问题
           //1. 这里的 CollegeEmployee 不是  SchoolManager的直接朋友
           //2. CollegeEmployee 是以局部变量方式出现在 SchoolManager
           //3. 违反了 迪米特法则 
   
           //获取到学院员工
           List<CollegeEmployee> list1 = sub.getAllEmployee();
           System.out.println("------------学院员工------------");
           for (CollegeEmployee e : list1) {
               System.out.println(e.getId());
           }
           ...........
       }
   }
   ```

   

   1) 前面设计的问题在于 SchoolManager 中，CollegeEmployee 类并不是 SchoolManager 类的直接朋友 (分析)

   2) 按照迪米特法则，应该避免类中出现这样非直接朋友关系的耦合

   3) 对代码按照迪米特法则 进行改进.,将涉及CollegeEmployee的代码封装到CollegeManager类中,因为CollegeManager类中其他方法出现了CollegeEmployee,是直接朋友。

   ```java
   class CollegeManager {
       //输出学院员工的信息
       public void printEmployee() {
           //获取到学院员工
           List<CollegeEmployee> list1 = getAllEmployee();
           System.out.println("------------学院员工------------");
           for (CollegeEmployee e : list1) {
               System.out.println(e.getId());
           }
       }
   }
   
   class SchoolManager{
       void printAllEmployee(CollegeManager sub) {
           //1. 将输出学院的员工方法，封装到CollegeManager
           sub.printEmployee();
           ..............
       }
   }
   
   
   ```

   

### 合成复用原则

基本介绍：原则是尽量使用合成/聚合的方式，而不是使用继承

<br/>



## 类之间的六大关系

 依赖、泛化（继承）、实现、关联、聚合与组合。

### 依赖

只要是在类中用到了对方，那么他们之间就存在依赖关系。如果没有对方，连编绎都通过不了。

1) 类中用到了对方

2) 如果是类的成员属性

3) 如果是方法的返回类型

4) 是方法接收的参数类型

5) 方法中使用到

<center><img src="https://img-blog.csdnimg.cn/20210203153404264.png" /></center>

### 泛化(继承)

 泛化关系实际上就是继承关系，他是依赖关系的特例

1) 泛化关系实际上就是继承关系

2) 如果 A 类继承了 B 类，我们就说 A 和 B 存在泛化关系

<center><img src="https://img-blog.csdnimg.cn/20210203153436295.png" /></center>

### 实现

实现关系实际上就是 A 类实现 B 接口，他是依赖关系的特例

<center><img src="https://img-blog.csdnimg.cn/2021020315350431.png" /></center>

### 关联

关联关系实际上就是类与类之间的联系，他是依赖关系的特例

关联具有**导航性**：即双向关系或单向关系

关联具有**多重性**：

<center><img src="https://img-blog.csdnimg.cn/20210203153531478.png" /></center>

### 聚合

聚合关系（Aggregation）**表示的是整体和部分的关系，整体与部分可以分开**。聚合关系是关联关系的特例，**所以他具有关联的导航性与多重性**。

如：一台电脑由键盘(keyboard)、显示器(monitor)，鼠标等组成；组成电脑的各个配件是可以从电脑上分离出来的，使用带空心菱形的实线来表示：

<center><img src="https://img-blog.csdnimg.cn/20210203153557847.png" /></center>

### 组合

组合关系：**也是整体与部分的关系，但是整体与部分不可以分开。**

再看一个案例：在程序中我们定义实体：Person 与 IDCard、Head, 那么 Head 和 

Person 就是 组合，IDCard 和Person 就是聚合。

```java
public class Person{ 
    private IDCard card;
    private Head head = new Head();
}
public class IDCard{} 
public class Head{}
```

但是如果在程序中 Person 实体中定义了对 IDCard 进行级联删除，即删除 Person 时连同 IDCard 一起删除，那么 IDCard  和 Person 就是组合了.

<center><img src="https://img-blog.csdnimg.cn/20210203153628688.png" /></center>

<br/>



## 设计模式总览

设计模式分为三种类型，共 23 种 

1. 创建型模式：单例模式、抽象工厂模式、原型模式、建造者模式、工厂模式。

2. 结构型模式：适配器模式、桥接模式、装饰模式、组合模式、外观模式、享元模式、代理模式。

3. 行为型模式：模版方法模式、命令模式、访问者模式、迭代器模式、观察者模式中介者模式、备忘录模式、解释器模式（Interpreter 模式）、状态模式、策略模   式、职责链模式(责任链模式)。	 

<br/>



## 创建型模式

创建型模式：单例模式、抽象工厂模式、原型模式、建造者模式、工厂模式。

### 单例模式

所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能存在一个对象实例， 并且该类只提供一个取得其对象实例的方法(静态方法)。

比如 Hibernate 的 SessionFactory，它充当数据存储源的代理，并负责创建Session 对象。SessionFactory并不是轻量级的，一般情况下，一个项目通常只需要一个SessionFactory 就够，这是就会使用到单例模式。

**注意事项和和使用场景：**

1. 单例模式保证了 系统内存中该类只存在一个对象，节省了系统资源，**对于一些需要频繁创建销毁的对象，使用单例模式可以提高系统性能**

2. 当想实例化一个单例类的时候，必须要记住使用相应的获取对象的方法，而不是使用 new

3. 单例模式使用的场景：
   - **需要频繁的进行创建和销毁的对象**
   - **创建对象时耗时过多或耗费资源过多(即：重量级对象)，但又经常用到的对象**
   - **工具类对象**
   - **频繁访问数据库或文件的对象(比如数据源、session 工厂等)**
4. 具体应用:**JDK的java.lang.Runtime就用到了饿汉式**

单例模式有八种方式：

1. `饿汉式(静态常量)`
2. `饿汉式（静态代码块）`
3.  懒汉式(线程不安全)

4.  懒汉式(线程安全，同步方法)

5.  懒汉式(线程安全，同步代码块)

6. ` 双重检查`
7. ` 静态内部类`
8.  `枚举`	(与其他相比可以防止反序列化)

#### 饿汉式（静态常量）

1. 构造器私有化 (防止 new )

2. 类的内部创建对象

3. 向外暴露一个静态的公共方法。getInstance

优缺点说明：

1. 优点：**这种写法比较简单，就是在类装载的时候就完成实例化。避免了线程同步问题。**

2. 缺点：在类装载的时候就完成实例化，没有达到 Lazy Loading 的效果。如果从始至终从未使用过这个实例，**则会造成内存的浪费**
3. 这种方式基于 classloder 机制避免了多线程的同步问题，不过，instance 在类装载时就实例化，在单例模式中大多数都是调用 getInstance 方法， 但是导致类装载的原因有很多种，因此不能确定有其他的方式（或者其他的静态方法）导致类装载，这时候初始化 instance 就没有达到 lazy loading 的效果

4. 结论：**这种单例模式可用，可能造成内存浪费**

 ```java
//饿汉式(静态变量)
class Singleton {
    //1. 构造器私有化, 外部能new
    private Singleton() {}

    //2.本类内部创建对象实例
    private final static Singleton instance = new Singleton();

    //3. 提供一个公有的静态方法，返回实例对象
    public static Singleton getInstance() {
        return instance;
    }
}
 ```



####  饿汉式（静态代码块）

1. 这种方式和上面的方式其实类似，只不过将类实例化的过程放在了静态代码块中，也是在类装载的时候，就执行静态代码块中的代码，初始化类的实例。优缺点和上面是一样的。

2. 结论：**这种单例模式可用，但是可能造成内存浪费**

```java
//饿汉式(静态代码块)
class Singleton {
    //1. 构造器私有化, 外部能new
    private Singleton() {}

    //2.本类内部创建对象实例
    private  static Singleton instance;

    static { // 在静态代码块中，创建单例对象
        instance = new Singleton();
    }

    //3. 提供一个公有的静态方法，返回实例对象
    public static Singleton getInstance() {
        return instance;
    }
}
```



#### 懒汉式(线程不安全)

1. 起到了 Lazy Loading 的效果，但是只能在单线程下使用。

2. 如果在多线程下，一个线程进入了 if (singleton == null)判断语句块，还未来得及往下执行，另一个线程也通过了这个判断语句，**这时便会产生多个实例**。所以在多线程环境下不可使用这种方式

3. 结论：**在实际开发中，不要使用这种方式.**

```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    //提供一个静态的公有方法，当使用到该方法时，才去创建 instance
    //即懒汉式
    public static Singleton getInstance() {
        if(instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```



#### 懒汉式(线程安全，同步方法)

1. 解决了线程安全问题

2. 效率太低了，每个线程在想获得类的实例时候，执行 getInstance()方法都要进行同步。而其实这个方法只执行一次实例化代码就够了，后面的想获得该类实例，直接 return 就行了。**方法进行同步效率太低**

3, 结论：**在实际开发中，不推荐使用这种方式**

```java
// 懒汉式(线程安全，同步方法)
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    //提供一个静态的公有方法，加入同步处理的代码，解决线程安全问题
    //即懒汉式
    public static synchronized Singleton getInstance() {
        if(instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```



#### 懒汉式(线程安全，同步代码块)

不仅用到了同步，效率低，而且还可能创建多个实例。就是个废物。(但改进成双重检查锁式比较常用)

结论:**不推荐使用**

```java
// 懒汉式(线程安全，同步方法)
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    //提供一个静态的公有方法，加入同步处理的代码，解决线程安全问题
    //即懒汉式
    public static Singleton getInstance() {
        if(instance == null) {
            synchronized(Singleton.class){
                instance = new Singleton();
            }
        }
        return instance;
    }
```



#### 双重检查锁式

1. Double-Check 概念是多线程开发中常使用到的，如代码中所示，我们进行了两次 if (singleton == null)检查，这样就可以**保证线程安全**了。

2. 这样，实例化代码只用执行一次，后面再次访问时，判断 if (singleton == null)，直接 return 实例化对象，**也避免的反复进行方法同步.**

3. 线程安全；**延迟加载；效率较高**

4. 结论：**在实际开发中，推荐使用这种单例设计模式**

`volitle`能保证可见性，也就是说只要一个线程对共享变量修改了，其他线程都能立即看到。当一个共享变量被volatile修饰时，它会保证修改的值会立即被更新到主存，当有其他线程需要读取时，它会去内存中读取新值。有序性也是一定程度的，但也并不能完全保证。因此还有个synchronized关键字。synchronized是啥，是排他锁、同步锁，也就是说同一时刻只会有一个线程获得锁，其他的都在等待锁的释放。所,synchronized就保证了有序性和原子性。因此此程序保证了可见性，原子性和有序性，就满足了并发访问。

```java
// 双重检查锁式
class Singleton {
    //volitle能保证可见性
    private static volatile Singleton instance;

    private Singleton() {}

    //提供一个静态的公有方法，加入双重检查代码，解决线程安全问题, 同时解决懒加载问题
    //同时保证了效率, 推荐使用
    public static synchronized Singleton getInstance() {
        if(instance == null) {
            //synchronized保证了有序性和原子性
            synchronized (Singleton.class) {
                if(instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```



#### 静态内部类式

1. 这种方式采用了类装载的机制来保证初始化实例时只有一个线程。

2. 静态内部类方式在 Singleton 类被装载时并不会立即实例化，而是在需要实例化时，调用 getInstance 方法，才会装载 SingletonInstance 类，从而完成 Singleton 的实例化。

3. 类的静态属性只会在第一次加载类的时候初始化，所以在这里，**JVM 帮助我们保证了线程的安全性，在类进行初始化时，别的线程是无法进入的。**

4. 优点：**避免了线程不安全，利用静态内部类特点实现延迟加载，效率高**

5. 结论：**推荐使用.**

```java
// 静态内部类完成， 推荐使用
class Singleton {
    private static Singleton instance;

    //构造器私有化
    private Singleton() {}

    //写一个静态内部类,该类中有一个静态属性 Singleton
    private static class SingletonInstance {
        private static final Singleton INSTANCE = new Singleton(); 
    }

    //提供一个静态的公有方法，直接返回SingletonInstance.INSTANCE
    public static Singleton getInstance() {
        return SingletonInstance.INSTANCE;
    }
}
```



#### 枚举式

1. 这借助 JDK1.5 中添加的枚举来实现单例模式。**不仅能避免多线程同步问题，而且还能防止反序列化重新创建新的对象。**

2. 这种方式是 Effective Java 作者 Josh Bloch  提倡的方式

3. 结论：**推荐使用**

```java
//使用枚举，可以实现单例, 推荐
enum Singleton {
    INSTANCE; 
    public void sayOK() {
        System.out.println("ok~");
    }
}

```

<br/>



### 工厂模式

[【设计模式】简单工厂、工厂方法与抽象工厂的区别](https://blog.csdn.net/jerry11112/article/details/80618420)

1. 工厂模式的意义

   将实例化对象的代码提取出来，放到一个类中统一管理和维护，达到和主项目的依赖

   关系的解耦。从而提高项目的扩展和维护性。

2. 三种工厂模式 (简单工厂模式、工厂方法模式、抽象工厂模式)

3. **设计模式的依赖抽象原则**

 

小结:

1. 创建对象实例时，不要直接 new 类, 而是把这个 new 类的动作放在一个工厂的方法中，并返回。有的书上说， 变量不要直接持有具体类的引用。

2. 不要让类继承具体类，而是继承抽象类或者是实现 interface(接口)

3. 不要覆盖基类中已经实现的方法。

**三个工厂都是各有利弊，简单工厂违反了最基本的原则，工厂方法与抽象工厂完美的解决了简单工厂的弊端！工厂方法的工厂个数过多，导致系统庞大，抽象工厂增加新的产品族很方便,但是增加新的产品会违反开闭原则！**

<br/>



#### 简单工厂模式

1. 简单工厂模式是属于创建型模式，是工厂模式的一种。简单工厂模式是由一个工厂对象决定创建出哪一种产品类的实例。**简单工厂模式是工厂模式家族中最简单实用的模式**

2. 简单工厂模式：**定义了一个创建对象的类，由这个类来封装实例化对象的行为(代码)**

3. 在软件开发中，**当我们会用到大量的创建某种、某类或者某批对象时，就会使用到工厂模式.**

不使用工厂模式:

<center><img src="https://img-blog.csdnimg.cn/20210203153728100.png" /></center>

1. 优点是比较好理解，简单易操作。

2. 缺点是违反了设计模式的 ocp 原则，即对扩展开放，对修改关闭。即当我们给类增加新功能的时候，尽量不修改代码，或者尽可能少修改代码.

3. 比如我们这时要新增加一个 Pizza 的种类(Pepper 披萨)，我们需要做如下修改. 如果我们增加一个 Pizza 类，只要是订购 Pizza 的代码都需要修改.

4. 改进的思路分析

   分析：修改代码可以接受，但是如果我们在其它的地方也有创建 Pizza 的代码，就意味着，也需要修改，而创建 Pizza的代码，往往有多处。

   思路：**把创建 Pizza 对象封装到一个类中，这样我们有新的 Pizza 种类时，只需要修改该类就可，其它有创建到 Pizza**

对象的代码就不需要修改了.-> 简单工厂模式

使用简单工厂模式 

简单工厂模式的设计方案: 定义一个可以实例化 Pizaa 对象的类，封装创建对象的代码。

<center><img src="https://img-blog.csdnimg.cn/20210203153759111.png" /></center>

(代码看代码文件夹，此处过于简单就不放入代码)

<br/>



#### 工厂方法模式

披萨项目新的需求：客户在点披萨时，可以点不同口味的披萨，比如 北京的奶酪 pizza、北京的胡椒 pizza 或者是伦敦的奶酪 pizza、伦敦的胡椒 pizza。

方案:

1. 工厂方法模式设计方案：将披萨项目的实例化功能抽象成抽象方法，在不同的口味点餐子类中具体实现。

2. 工厂方法模式：**定义了一个创建对象的抽象方法，由子类决定要实例化的类。工厂方法模式将对象的实例化推迟到子类。**

优点:

1. 工厂方法用来创建客户所需要的产品，同时隐藏了哪种具体产品类将被实例化的细节，用户只需要要关注工厂，不需要关注创建的细节！从客户端代码就可以看出！只知道对应的工厂就好！

2. **在增加修改新的运算类的时候不用修改代码，只需要增加对应的工厂就好，完全符合开放——封闭性原则！**

3. 创建对象的细节完全封装在具体的工厂内部，而且有了抽象的工厂类，所有的具体工厂都继承了自己的父类！完美的体现了多态性！

缺点：

1. 在增加新的产品（对应UML图的算法）时，**也必须增加新的工厂类，会带来额外的开销**

2. **抽象层的加入使得理解程度加大**

```java
//伦敦奶酪披萨
public class LDCheesePizza extends OrderPizza {
    @Override
    Pizza createPizza() {
        return new LDCheesePizza();
    }
}
//伦敦胡椒披萨
public class LDPepperPizza extends OrderPizza {
    @Override
    Pizza createPizza() {
        return new LDCheesePizza();
    }
}
//北京奶酪披萨
public class BJChessPizza extends OrderPizza {
    @Override
    Pizza createPizza() {......}
}

//北京胡椒披萨
public class BJPepperPizza extends OrderPizza {
    @Override
    Pizza createPizza() {......}
}
```

<br/>



#### 抽象工厂模式

1. 抽象工厂模式：定义了一个 interface 用于创建相关或有依赖关系的对象簇，而无需指明具体的类

2. 抽象工厂模式可以将简单工厂模式和工厂方法模式进行整合。

3. 从设计层面看，抽象工厂模式就是对简单工厂模式的改进(或者称为进一步的抽象)。

4. 将工厂抽象成两层，AbsFactory(抽象工厂) 和 具体实现的工厂子类。程序员可以根据创建对象类型使用对应的工厂子类。这样将单个的简单工厂类变成了工厂簇，更利于代码的维护和扩展。

**增加一个披萨族（产品族）很简单，而增加一个新的披萨（产品）就会非常复杂！**例如，我要是增加纽约胡椒披萨，纽约奶酪披萨，那么我就可以直接增加了，工厂顺便增加一个纽约工厂，这样完美了的利用好了开放封闭的原则！棒极了！但是我要是增加一个新的披萨，比如是牛肉披萨，那么它就要同时增加招加北京，伦敦，纽约披萨，同时还需要修改factory，违反了开放封闭的原则！

<center><img src="https://img-blog.csdnimg.cn/20210203153832110.png" /></center>

```java
interface AbsFactory {
    Pizza createCherryPizza();
    Pizza createPepperPizza();
}
public class LDFactory implements AbsFactory {
    @Override
    public Pizza createCherryPizza() {
        return  new LDCheesePizza();
    }

    @Override
    public Pizza createPepperPizza(){
        return new LDPepperPizza();
    }

}

public class BJFactory implements AbsFactory {
    ........
}
```

<br/>



### 原型模式

基本介绍:

1. 原型模式(Prototype 模式)是指：用原型实例指定创建对象的种类，并且通过拷贝这些原型，创建新的对象

2.  原型模式是一种创建型设计模式，允许一个对象再创建另外一个可定制的对象，无需知道如何创建的细节

3. 工作原理是:通过将一个原型对象传给那个要发动创建的对象，这个要发动创建的对象通过请求原型对象拷贝它们自己来实施创建，即 对象.clone()

4. 形象的理解：孙大圣拔出猴毛， 变出其它孙大圣

<center><img src="https://img-blog.csdnimg.cn/20210203153857876.png" /></center>

- Prototype : 原型类，声明一个克隆自己的接口

- ConcretePrototype: 具体的原型类,  实现一个克隆自己的操作

- Client: 让一个原型对象克隆自己，从而创建一个新的对象(属性一样）

```java
public class Sheep implements Cloneable {
    //克隆该实例，使用默认的clone方法来完成(浅拷贝)
    @Override
    protected Object clone() {
        Sheep sheep = null;
        try {
            sheep = (Sheep) super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return sheep;
    }
}
```



#### 深入讨论-浅拷贝和深拷贝

浅拷贝的介绍

1.  对于数据类型是基本数据类型的成员变量，浅拷贝会直接进行值传递，也就是将该属性值复制一份给新的对象。

2. 对于数据类型是引用数据类型的成员变量，比如说成员变量是某个数组、某个类的对象等，那么浅拷贝会进行引用传递，也就是只是将该成员变量的引用值（内存地址）复制一份给新的对象。因为实际上两个对象的该成员变量都指向同一个实例。在这种情况下，在一个对象中修改该成员变量会影响到另一个对象的该成员变量值。

3. 前面我们克隆羊就是浅拷贝

4. 浅拷贝是使用默认的 clone()方法来实现

   sheep = (Sheep) super.clone();

深拷贝的介绍

1. 复制对象的**所有基本数据类型的成员变量值**

2. **为所有引用数据类型的成员变量申请存储空间，并复制每个引用数据类型成员变量所引用的对象，直到该对象可达的所有对象。也就是说，对象进行深拷贝要对整个对象(包括对象的引用类型)进行拷贝**

3. 深拷贝实现方式 1：**重写 clone 方法来实现深拷贝**
4. 深拷贝实现方式 2：**通过对象序列化实现深拷贝(推荐)**

```java
public class DeepCloneableTarget implements Cloneable {
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

public class DeepProtoType implements Cloneable{
    public String name; //String 属性
    public DeepCloneableTarget deepCloneableTarget;// 引用类型
    //深拷贝 - 方式 1 使用clone 方法
    @Override
    protected Object clone() throws CloneNotSupportedException {
        Object deep = null;
        //这里完成对基本数据类型(属性)和String的克隆
        deep = super.clone();
        //对引用类型的属性，进行单独处理
        DeepProtoType deepProtoType = (DeepProtoType)deep;
        deepProtoType.deepCloneableTarget  = (DeepCloneableTarget)deepCloneableTarget.clone();
        return deepProtoType;
    }
}
```



```java
public class DeepCloneableTarget implements Serializable{}
public class DeepProtoType implements Serializable,{
    public String name; //String 属性
    public DeepCloneableTarget deepCloneableTarget;// 引用类型
    //深拷贝 - 方式2 通过对象的序列化实现 (推荐)
    public Object deepClone() {
        //创建流对象
        ByteArrayOutputStream bos = null;
        ObjectOutputStream oos = null;
        ByteArrayInputStream bis = null;
        ObjectInputStream ois = null;
        try {
            //序列化
            bos = new ByteArrayOutputStream();
            oos = new ObjectOutputStream(bos);
            oos.writeObject(this); //当前这个对象以对象流的方式输出

            //反序列化
            bis = new ByteArrayInputStream(bos.toByteArray());
            ois = new ObjectInputStream(bis);
            DeepProtoType copyObj = (DeepProtoType)ois.readObject();
            return copyObj;
        } catch (Exception e) {
        }finally{}  
    } 
}
```



#### 原型模式的注意事项和细节

1.  **创建新的对象比较复杂时，可以利用原型模式简化对象的创建过程**，同时也能够提高效率

2. 不用重新初始化对象，而是动态地获得对象运行时的状态

3. 如果原始对象发生变化(增加或者减少属性)，其它克隆对象的也会发生相应的变化，无需修改代码	

4. 在实现深克隆的时候可能需要比较复杂的代码

5.  缺点：**需要为每一个类配备一个克隆方法**，这对全新的类来说不是很难，但对已有的类进行改造时，需要修改其源代码，违背了 ocp 原则，这点请注意.

<br/>



### 建造者模式

1. 需要建房子：这一过程为打桩、砌墙、封顶

2. 房子有各种各样的，比如普通房，高楼，别墅，各种房子的过程虽然一样，但是要求不要相同的.

####  传统建造者

抽象建造者和指挥者在同一个类中

```java
public abstract class AbstractHouse {
    //打地基
    public abstract void buildBasic();
    //砌墙
    public abstract void buildWalls();
    //封顶
    public abstract void roofed();

    public void build() {
        buildBasic();
        buildWalls();
        roofed();
    }
}
```



1. 优点是比较好理解，简单易操作。

2. 设计的程序结构，过于简单，没有设计缓存层对象，程序的扩展和维护不好. 也就是说，这种设计方案，**把产品(即：房子) 和 创建产品的过程(即：建房子流程) 封装在一起，耦合性增强了。**

3. 解决方案：将产品和产品建造过程解耦  => 建造者模式.

#### 建造者模式基本介绍

 基本介绍

1. 建造者模式（Builder Pattern） 又叫生成器模式，是一种对象构建模式。它可以将复杂对象的建造过程抽象出来（抽象类别），使这个抽象过程的不同实现方法可以构造出不同表现（属性）的对象。

2. 建造者模式 是一步一步创建一个复杂的对象，它允许用户只通过指定复杂对象的类型和内容就可以构建它们， **用户不需要知道内部的具体构建细节。**

建造者模式的四个角色

1. `Product（产品角色）`： 一个具体的产品对象。

2. `Builder（抽象建造者）`： 创建一个 Product 对象的各个部件指定的 接口/抽象类。

3. `ConcreteBuilder（具体建造者）`： 实现接口，构建和装配各个部件。

4.  `Director（指挥者）`： 构建一个使用 Builder 接口的对象。它主要是用于创建一个复杂的对象。它主要有两个作用，一是：**隔离了客户与对象的生产过程**，二是：**负责控制产品对象的生产过程**。

#### 建造者模式原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203153933434.png" /></center>

#### 建造者模式解决盖房需求应用实例 

1. 需要建房子：这一过程为打桩、砌墙、封顶。不管是普通房子也好，别墅也好都需要经历这些过程，下面我们使用建造者模式(Builder Pattern)来完成

2. 思路分析图解(类图

<center><img src="https://img-blog.csdnimg.cn/20210203153959778.png" /></center>

```java
// 抽象的建造者
public abstract class HouseBuilder {
    protected House house = new House();
    //将建造的流程写好, 抽象的方法
    public abstract void buildBasic();
    public abstract void buildWalls();
    public abstract void roofed();
    //建造房子好， 将产品(房子) 返回
    public House buildHouse() {
        return house;
    }
}
```



```java
public class HighBuilding extends HouseBuilder {
    @Override
    public void buildBasic() {
        house.setBaise("100");
    }

    @Override
    public void buildWalls() {
        house.setWall("20");
    }

    @Override
    public void roofed() {
        house.setRoofed("高楼透明屋顶透明");
    }
}
public class CommonBuilding extends HouseBuilder{.....差不多}
```



```java
//指挥者，这里去指定制作流程，返回产品
public class HouseDirector {
    HouseBuilder houseBuilder = null;
    //构造器传入 houseBuilder
    public HouseDirector(HouseBuilder houseBuilder) {
        this.houseBuilder = houseBuilder;
    }

    //通过setter 传入 houseBuilder
    public void setHouseBuilder(HouseBuilder houseBuilder) {
        this.houseBuilder = houseBuilder;
    }

    //如何处理建造房子的流程，交给指挥者
    public House constructHouse() {
        houseBuilder.buildBasic();
        houseBuilder.buildWalls();
        houseBuilder.roofed();
        return houseBuilder.buildHouse();
    }
}
```



#### JDK中StringBuilder的源码分析

<center><img src="https://img-blog.csdnimg.cn/20210203154156291.png" /></center>

1. Appendable 接口定义了多个 append 方法(抽象方法), 即 Appendable 为抽象建造者, 	定义了抽象方法

2. AbstractStringBuilder  实现了  Appendable  接口方法，这里的  AbstractStringBuilder 已经是建造者，只是不能实例化

3. StringBuilder 即充当了指挥者角色，同时充当了具体的建造者，建造方法的实现是由 AbstractStringBuilder 完成 , 而 StringBuilder 继承了 AbstractStringBuilder

#### 建造者模式的注意事项和细节

1. **客户端(使用程序)不必知道产品内部组成的细节，将产品本身与产品的创建过程解耦**，使得相同的创建过程可以创建不同的产品对象

2. 每一个具体建造者都相对独立，而与其他的具体建造者无关，**因此可以很方便地替换具体建造者或增加新的具体建造者**， 用户使用不同的具体建造者即可得到不同的产品对象

3. 可以更加精细地控制产品的创建过程 。**将复杂产品的创建步骤分解在不同的方法中，使得创建过程更加清晰**， 也更方便使用程序来控制创建过程

4. **增加新的具体建造者无须修改原有类库的代码，指挥者类针对抽象建造者类编程，系统扩展方便，** 符合“开闭原则”

5. **建造者模式所创建的产品一般具有较多的共同点，其组成部分相似**，如果产品之间的差异性很大，则不适合使用建造者模式，因此其使用范围受到一定的限制。

6. **如果产品的内部变化复杂**，可能会导致需要定义很多具体建造者类来实现这种变化，导致系统变得很庞大，因此在这种情况下，要考虑是否选择建造者模式.

7. 抽象工厂模式 VS 建造者模式

   **抽象工厂模式实现对产品家族的创建**，一个产品家族是这样的一系列产品：具有不同分类维度的产品组合，**采用抽象工厂模式不需要关心构建过程，只关心什么产品由什么工厂生产即可。而建造者模式则是要求按照指定的蓝图建造产品，它的主要目的是通过组装零配件而产生一个新产品**



## 结构型模式

结构型模式：适配器模式、桥接模式、装饰模式、组合模式、外观模式、享元模式、代理模式。

### 适配器模式

#### 基本介绍

1. 适配器模式(Adapter Pattern)将某个类的接口转换成客户端期望的另一个接口表示，主的目的是兼容性，让原本因接口不匹配不能一起工作的两个类可以协同工作。其别名为包装器(Wrapper)

2. 适配器模式属于结构型模式

3.  主要分为三类：`类适配器模式`、`对象适配器模式`、`接口适配器模式`

 

####  工作原理

1. 适配器模式：将一个类的接口转换成另一种接口.让原本接口不兼容的类可以兼容

2. 从用户的角度看不到被适配者，是解耦的

3. 用户调用适配器转化出来的目标接口方法，适配器再调用被适配者的相关接口方法

4. 用户收到反馈结果，感觉只是和目标接口交互，如图



#### 类适配器模式

基本介绍：Adapter 类，通过继承 src 类，实现 dst  类接口，完成 src->dst 的适配。

以生活中充电器的例子来讲解适配器，充电器本身相当于 Adapter，220V 交流电相当于 src (即被适配者)，我们的目 dst(即 目标)是 5V 直流电

<center><img src="https://img-blog.csdnimg.cn/20210203154226618.png" /></center>

```java
//适配器类
public class VoltageAdapter extends Voltage220V implements IVoltage5V {
    @Override
    public int output5V() {
        // TODO Auto-generated method stub
        //获取到220V电压
        int srcV = output220V();  //调用父类的方法获取电压
        int dstV = srcV / 44 ; //转成 5v
        return dstV;
    }
}
```

类适配器模式注意事项和细节

1.  **Java 是单继承机制**，所以类适配器需要继承 src 类这一点算是一个缺点, 因为这要求 dst 必须是接口，有一定局限性;

2. **src 类的方法在 Adapter 中都会暴露出来**，也增加了使用的成本。

3. 由于其继承了 src 类，所以它可以根据需求重写 src 类的方法，**使得 Adapter 的灵活性增强了。**



#### 对象适配器模式(聚合)

基本介绍：基本思路和类的适配器模式相同，只是将 Adapter 类作修改，不是继承 src 类，而是**持有 src 类的实例**，以解决兼容性的问题。 即：持有 src 类，实现 dst  类接口，完成 src->dst 的适配

根据“合成复用原则”，在系统中尽量**使用关联关系（聚合）来替代继承关系。**

对象适配器模式是适配器模式常用的一种

<center><img src="https://img-blog.csdnimg.cn/20210203154249827.png" /></center>

```java
//适配器类
public class VoltageAdapter  implements IVoltage5V {
    private Voltage220V voltage220V; // 关联关系-聚合

    //通过构造器，传入一个 Voltage220V 实例
    public VoltageAdapter(Voltage220V voltage220v) {
        this.voltage220V = voltage220v;
    }

    @Override
    public int output5V() {
        int dst = 0;
        if(null != voltage220V) {
            int src = voltage220V.output220V();//获取220V 电压
            System.out.println("使用对象适配器，进行适配~~");
            dst = src / 44;
            System.out.println("适配完成，输出的电压为=" + dst);
        }
        return dst;
    }
}

```



对象适配器模式注意事项和细节

1. 对象适配器和类适配器其实算是同一种思想，只不过实现方式不同。**根据合成复用原则**，使用组合替代继承， 所以它解决了类适配器必须继承 src 的局限性问题，也不再要求 dst必须是接口。

2. 使用成本更低，更灵活。



#### 接口适配器模式

1. 一些书籍称为：**适配器模式(**Default Adapter Pattern)或**缺省适配器模式**。

2.  核心思路：当不需要全部实现接口提供的方法时，可先设计一个抽象类实现接口，并为该接口中每个方法提供一个默认实现（空方法），那么该抽象类的子类可有选择地	覆盖父类的某些方法来实现需求

3. 适用于一个接口不想使用其所有的方法的情况。

 

应用实例

1. Android 中的属性动画 ValueAnimator 类可以通addListener(AnimatorListener listener)方法添加监听器， 那么常规写法如右：

2.  有时候我们不想实现 Animator.AnimatorListener 接口的全部方法，我们只想监听 onAnimationStart，我们会如下写

<center><img src="https://img-blog.csdnimg.cn/20210203154326770.png" /></center>

<center><img src="https://img-blog.csdnimg.cn/20210203154351806.png" /></center>

**适配器模式在 SpringMVC 框架应用的源码剖析**

1. SpringMvc 中的 HandlerAdapter, 就使用了适配器模式

2. SpringMVC 处理请求的流程回顾

3. 使用 HandlerAdapter 的原因分析:

可以看到处理器的类型不同，有多重实现方式，那么调用方式就不是确定的，如果需要直接调用 Controller 方法，需要调用的时候就得不断是使用 if else 来进行判断是哪一种子类然后执行。那么如果后面要扩展 Controller， 就得修改原来的代码，这样违背了 OCP 原则。

<center><img src="https://img-blog.csdnimg.cn/20210203154426610.png" /></center>

<center><img src="https://img-blog.csdnimg.cn/20210203154450840.png" /></center>

#### 适配器模式的注意事项和细节

1. 三种命名方式，是根据 src 是以怎样的形式给到 Adapter（在 Adapter 里的形式）来命名的。

2. 类适配器：以类给到，在 Adapter 里，就是将 src 当做类，继承对象适配器：以对象给到，在 Adapter 里，将 src 作为一个对象，持有接口适配器：以接口给到，在 Adapter 里，将 src 作为一个接口，实现

3. Adapter 模式最大的作用还是**将原本不兼容的接口融合在一起工作**。

4. 实际开发中，**实现起来不拘泥于我们讲解的三种经典形式**



### 桥接模式

现在对不同手机类型的不同品牌实现操作编程(比如:开机、关机、上网，打电话等)

<center><img src="https://img-blog.csdnimg.cn/20210203154518827.png" /></center>

<center><img src="https://img-blog.csdnimg.cn/20210203154545316.png" /></center>



#### 传统方案解决手机操作问题分析

1. **扩展性问题(类爆炸)**，如果我们再增加手机的样式(旋转式)，就需要增加各个品牌手机的类，同样如果我们增加一个手机品牌，也要在各个手机样式类下增加。

2. **违反了单一职责原则**，当我们增加手机样式时，要同时增加所有品牌的手机，这样增加了代码维护成本.

3. 解决方案-使用桥接模式



#### 桥接模式(Bridge)-基本介绍

基本介绍

1. 桥接模式(Bridge 模式)是指：将实现与抽象放在两个不同的类层次中，使两个层次可以独立改变。

2. 是一种结构型设计模式

3. Bridge 模式基于类的最小设计原则，通过使用封装、聚合及继承等行为让不同的类承担不同的职责。它的主要特点是**把抽象(Abstraction)与行为实现(Implementation)分离开来，从而可以保持各部分的独立性以及应对他们的功能扩展**

<center><img src="https://img-blog.csdnimg.cn/20210203154608660.png" /></center>



#### 桥接模式

1.  Client 类：桥接模式的调用者

2. 抽象类(Abstraction) :维护了 Implementor / 即它的实现类 ConcreteImplementorA.., 二者是聚合关系, Abstraction



#### 原理类图

充当桥接类

1. RefinedAbstraction :  是 Abstraction  抽象类的子类

2. Implementor :  行为实现类的接口

3. ConcreteImplementorA /B ：行为的具体实现类

4. 从 UML 图：这里的抽象类和接口是聚合的关系，其实调用和被调用关系



#### 桥接模式解决手机操作问题 

使用桥接模式改进传统方式，让程序具有搞好的扩展性，利用程序维护

总结就是:**抽象类聚合了接口，并且子类对方法进行了重写**(符合里氏转换原则)

(视情况而定，可以没有抽象类和子类，就一个class实现,具体分析DriverManager,本质是分离抽象和实现)

<center><img src="https://img-blog.csdnimg.cn/2021020315463375.png" /></center>

```java
public abstract class Phone {
    //组合品牌
    private Brand brand;

    //构造器
    public Phone(Brand brand) {
        super();
        this.brand = brand;
    }
    protected void open() {
        this.brand.open();
    }
    //省略close和call方法,视情况调用   
}

public class UpRightPhone extends Phone {
    //构造器
    public UpRightPhone(Brand brand) {
        super(brand);
    }

    public void open() {
        super.open();
        System.out.println(" 直立样式手机 ");
    }
    //省略close和call方法,视情况重写
}
```



桥接模式在 JDBC 的源码剖析

桥接模式在 JDBC 的源码剖析

1. Jdbc 的 Driver 接口，如果从桥接模式来看，Driver 就是一个接口，下面可以有 MySQL 的 Driver，Oracle 的Driver，这些就可以当做实现接口类

2. 代码分析+Debug 源码

<center><img src="https://img-blog.csdnimg.cn/20210203154703246.png" /></center>



#### 桥接模式的注意事项和细节

1. **实现了抽象和实现部分的分离，从而极大的提供了系统的灵活性**，让抽象部分和实现部分独立开来，这有助于系统进行分层设计，从而产生更好的结构化系统。

2.  对于系统的高层部分，只需要知道抽象部分和实现部分的接口就可以了，其它的部分由具体业务来完成。

3. **桥接模式替代多层继承方案**，可以减少子类的个数，降低系统的管理和维护成本。

4. 桥接模式的引入**增加了系统的理解和设计难度**，由于聚合关联关系建立在抽象层，要求开发者针对抽象进行设计和编程

5. 桥接模式要求正确识别出系统中两个独立变化的维度(抽象、和实现)，因此**其使用范围有一定的局限性**，即需要有这样的应用场景。

6. **注意桥接模式和抽象工厂模式以及装饰者模式的不同(装饰者模式的不同看下文)**

对于那些不希望使用继承或因为多层次继承导致系统类的个数急剧增加的系统，桥接模式尤为适用.



#### 常见的应用场景:

1. JDBC 驱动程序

2. 银行转账系统

   转账分类: 网上转账，柜台转账，AMT 转账

   转账用户类型：普通用户，银卡用户，金卡用户..

3. 消息管理

   消息类型：即时消息，延时消息

   消息分类：手机短信，邮件消息，QQ 消息...



### 装饰者模式

装饰者模式用于解决需要新建大量的类

#### 星巴克咖啡订单项目（咖啡馆）： 

1.  咖啡种类/单品咖啡：Espresso(意大利浓咖啡)、ShortBlack、LongBlack(美式咖啡)、Decaf(无因咖啡)

2. 调料：Milk、Soy(豆浆)、Chocolate

3. 要求在扩展新的咖啡种类时，具有良好的扩展性、改动方便、维护方便

4. 使用 OO 的来计算不同种类咖啡的费用:  客户可以点单品咖啡，也可以单品咖啡+调料组合。

问题：这样设计，会有很多类，当我们增加一个单品咖啡，或者一个新的调料，类的数量就会倍增，就会出现类爆炸

<center><img src="https://img-blog.csdnimg.cn/20210203154731577.png" /></center>

#### 方案 2-解决星巴克咖啡订单(好点)

1. 前面分析到方案 1 因为咖啡单品+调料组合会造成类的倍增，因此可以做改进，将调料内置到 Drink 类，这样就不会造成类数量过多。从而提高项目的维护性(如图)

<center><img src="https://img-blog.csdnimg.cn/20210203154754485.png" /></center>

说明: milk,soy,chocolate 可以设计为 Boolean,表示是否要添加相应的调料.

 

#### 方案 2-解决星巴克咖啡订单问题分析

1. 方案 2 可以控制类的数量，不至于造成很多的类

2. 在增加或者删除调料种类时，代码的维护量很大

3. 考虑到用户可以添加多份 调料时，可以将 hasMilk 返回一个对应 int

4. 考虑使用 装饰者 模式



#### 装饰者模式定义

1. 装饰者模式：动态的将新功能附加到对象上。在对象功能扩展方面，**它比继承更有弹性，装饰者模式也体现了开闭原则(ocp)**

2. 这里提到的动态的将新功能附加到对象和 ocp 原则，在后面的应用实例上会以代码的形式体现，请同学们注意体会。



#### 装饰者模式原理

1. 装饰者模式就像打包一个快递

   主体：比如：陶瓷、衣服 (Component) //  被装饰者

   包装：比如：报纸填充、塑料泡沫、纸板、木板(Decorator)

2.  **Component** 主体：比如类似前面的 Drink

3. **ConcreteComponent** 和 **Decorator**

   ConcreteComponent：具体的主体， 比如前面的各个单品咖啡

4. Decorator: 装饰者，比如各调料.

在如图的 Component 与 ConcreteComponent 之间，如果 ConcreteComponent 类很多,还可以设计一个缓冲层，将共有的部分提取出来，抽象层一个类。

<center><img src="https://img-blog.csdnimg.cn/20210203154828586.png" /></center>

#### 装饰者模式解决星巴克咖啡订单

<center><img src="https://img-blog.csdnimg.cn/20210203154852431.png" /></center>

#### 装饰者模式下的订单：2 份巧克力+一份牛奶的 LongBlack

<center><img src="https://img-blog.csdnimg.cn/20210203154918574.png" /></center>

```java
public abstract class Drink {
    public String des; // 描述
    private float price = 0.0f;
    public String getDes() {
        return des;
    }
    public void setDes(String des) {
        this.des = des;
    }
    public float getPrice() {
        return price;
    }
    public void setPrice(float price) {
        this.price = price;
    }

    //计算费用的抽象方法
    //子类来实现
    public abstract float cost();

}
//抽象主体
public  abstract class Coffee  extends Drink {
    @Override
    public float cost() {
        // TODO Auto-generated method stub
        return super.getPrice();
    }
}
//具体主体
public class LongBlack extends Coffee {
    public LongBlack() {
        setDes(" longblack ");
        setPrice(5.0f);
    }
}
//抽象装饰
public abstract  class Decorator extends Drink {
    private Drink obj;

    public Decorator(Drink obj) { //聚合
        this.obj = obj;
    }

    @Override
    public float cost() {
        // getPrice 自己价格
        return super.getPrice() + obj.cost();
    }

    @Override
    public String getDes() {
        // obj.getDes() 输出被装饰者的信息
        return des + " " + getPrice() + " && " + obj.getDes();
    }
}
//具体装饰
public class Milk extends Decorator {
    public Milk(Drink obj) {
        super(obj);
        setDes(" 牛奶 ");
        setPrice(2.0f); 
    }
}
```



#### 装饰者模式在 JDK 应用的源码分析

Java 的 IO 结构，FilterInputStream 就是一个装饰者

<center><img src="https://img-blog.csdnimg.cn/20210203154951748.png" /></center>

1. InputStream  是抽象类,  类似我们前面讲的 Drink

2. FileInputStream 是 InputStream  子类，类似我们前面的 DeCaf, LongBlack

3. FilterInputStream 是 InputStream 子类：类似我们前面 的 Decorator 修饰者

4. DataInputStream  是 FilterInputStream  子类，具体的修饰者，类似前面的 Milk, Soy 等

5. FilterInputStream 类  有 protected volatile InputStream in;  即含被装饰者

6. 分析得出在 jdk 的 io 体系中，就是使用装饰者模式



#### 装饰者模式和桥接模式的不同

1. 桥接模式中所说的分离，其实是指将结构与实现分离（当结构和实现有可能发生变化时）或属性与基于属性的行为进行分离；而装饰者只是对基于属性的行为进行封闭成独立的类。

2. 桥接中的行为是横向的行为，行为彼此之间无关联；而装饰者模式中的行为具有可叠加性，其表现出来的结果是一个整体，一个各个行为组合后的一个结果。



#### 装饰者模式和享元模式的不同

装饰者模式用于解决需要新建大量的类。而享元模式是用于解决需要创建大量类似的对象



### 组合模式

#### 看一个学校院系展示需求

编写程序展示一个学校院系结构：需求是这样，要在一个页面中展示出学校的院系组成，一个学校有多个学院， 一个学院有多个系。如图：

<center><img src="https://img-blog.csdnimg.cn/20210203155021774.png" /></center>

传统方案解决学校院系展示

<center><img src="https://img-blog.csdnimg.cn/2021020315504753.png" /></center>

#### 传统方案解决学校院系展示存在的问题分析

1.  将学院看做是学校的子类，系是学院的子类，这样实际上是站在组织大小来进行分层次的

2. 实际上我们的要求是 ：在一个页面中展示出学校的院系组成，一个学校有多个学院，一个学院有多个系， 因此这种方案，不能很好实现的管理的操作，比如对学院、系的添加，删除，遍历等

解决方案：把学校、院、系都看做是组织结构，他们之间没有继承的关系，而是一个树形结构，可以更好的实现管理操作。 => 组合模式



#### 组合模式基本介绍

1. 组合模式（Composite Pattern），又叫**部分整体模式**，它创建了对象组的树形结构，将对象组合成树状结构以表示“**整体-部分**”的层次关系。

2. 组合模式依据树形结构来组合对象，用来表示部分以及整体层次。

3.  这种类型的设计模式属于结构型模式。

4. 组合模式使得用户对单个对象和组合对象的访问具有一致性，即：组合能让客户以一致的方式处理个别对象以及组合对象

#### 组合模式原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203155116502.png" /></center>

对原理结构图的说明-即(组合模式的角色及职责)

1. **Component** :这是组合中对象声明接口，在适当情况下，实现所有类共有的接口默认行为,用于访问和管理Component 子部件, Component  可以是抽象类或者接口

2. **Leaf** : 在组合中表示叶子节点，叶子节点没有子节点

3. **Composite** :非叶子节点，  用于存储子部件，  在 Component 接口中实现 子部件的相关操作，比如增加(add), 删除。



#### 组合模式解决学校院系展示的 应用实例

应用实例要求

1. 编写程序展示一个学校院系结构：需求是这样，要在一个页面中展示出学校的院系组成，一个学校有多个学院， 一个学院有多个系。

2. 思路分析和图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203155149216.png" /></center>

```java
public abstract class OrganizationComponent {
    private String name; // 名字
    private String des; // 说明

    //之所以不使用abstract，是因为有些子类不需要实现此类方法，
    //默认实现，如果没有重写,调用会报错
    protected  void add(OrganizationComponent organizationComponent) {
        //默认实现
        throw new UnsupportedOperationException();
    }

    protected  void remove(OrganizationComponent organizationComponent) {
        throw new UnsupportedOperationException();
    }

    //构造器
    public OrganizationComponent(String name, String des) {
        super();
        this.name = name;
        this.des = des;
    }
    //省略set,get方法
    //方法print, 做成抽象的, 子类都需要实现
    protected abstract void print();
}
```

```java
//University 就是 Composite , 可以管理College
public class University extends OrganizationComponent {
    //List 中 存放的College 
    List<OrganizationComponent> organizationComponents = new ArrayList<OrganizationComponent>();

    // 构造器
    public University(String name, String des) {
        super(name, des);
    }

    // 重写add
    @Override
    protected void add(OrganizationComponent organizationComponent) {
        organizationComponents.add(organizationComponent);
    }

    // 重写remove
    @Override
    protected void remove(OrganizationComponent organizationComponent) {
        organizationComponents.remove(organizationComponent);
    }

    // print方法，就是输出University 包含的学院
    @Override
    protected void print() {.....}
}

}
//College
public class College extends OrganizationComponent {
    .......与University 差不多
}
//Department 
public class Department extends OrganizationComponent {
    //没有集合
    public Department(String name, String des) {
        super(name, des);

    }
    //add , remove 就不用写了，因为他是叶子节点
    @Override
    protected void print() {......}

}
```



#### 组合模式在 JDK 集合的源码分析

1. Java 的集合类-HashMap 就使用了组合模式

2. 代码分析+Debug 源码

<center><img src="https://img-blog.csdnimg.cn/20210203155223112.png" /></center>

 

<center><img src="https://img-blog.csdnimg.cn/20210203155245721.png" /></center>

 

#### 组合模式的注意事项和细节

1. **简化客户端操作**。客户端只需要面对一致的对象而不用考虑整体部分或者节点叶子的问题。

2. **具有较强的扩展性**。当我们要更改组合对象时，我们只需要调整内部的层次关系，客户端不用做出任何改动.

3. **方便创建出复杂的层次结构**。**客户端不用理会组合里面的组成细节**，容易添加节点或者叶子从而创建出复杂的树形结构

4. **需要遍历组织机构，或者处理的对象具有树形结构时, 非常适合使用组合模式.**

5. **要求较高的抽象性，如果节点和叶子有很多差异性的话，比如很多方法和属性都不一样，不适合使用组合模式**



### 外观模式

#### 影院管理项目

组建一个家庭影院：

DVD 播放器、投影仪、自动屏幕、环绕立体声、爆米花机,要求完成使用家庭影院的功能，其过程为： 直接用遥控器：统筹各设备开关

开爆米花机放 下 屏 幕 开 投 影 仪 开音响开 DVD，选 dvd

去拿爆米花调 暗 灯 光 播放

观影结束后，关闭各种设备

#### 传统方式解决影院管理

<center><img src="https://img-blog.csdnimg.cn/20210203155313184.png" /></center>

#### 传统方式解决影院管理问题分析

1.  在 ClientTest 的 main 方法中，创建各个子系统的对象，并直接去调用子系统(对象)相关方法，会造成调用过程混乱，没有清晰的过程

2. 不利于在 ClientTest 中，去维护对子系统的操作

3. 解决思路：定义一个高层接口，给子系统中的一组接口提供一个一致的界面(比如在高层接口提供四个方法ready, play, pause, end )，用来访问子系统中的一群接口

4. 也就是说 就是通过定义一个一致的接口(界面类)，用以屏蔽内部子系统的细节，使得调用端只需跟这个接口发生调用，而无需关心这个子系统的内部细节 => 外观模式

#### 外观模式基本介绍

1.  外观模式（Facade），也叫“**过程模式**"：外观模式为子系统中的一组接口提供一个一致的界面，此模式定义了一个高层接口，这个接口使得这一子系统更加容易使用

2. **外观模式通过定义一个一致的接口，用以屏蔽内部子系统的细节，使得调用端只需跟这个接口发生调用，而无需关心这个子系统的内部细节**

外观模式原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203155342964.png" /></center>

对类图说明(分类外观模式的角色)

1. 外观类(**Facade**): 为调用端提供统一的调用接口, 外观类知道哪些子系统负责处理请求,从而将调用端的请求代理给适当子系统对象

2. 调用者(Client): 外观接口的调用者

3. 子系统的集合：指模块或者子系统，处理 Facade 对象指派的任务，他是功能的实际提供者



#### 外观模式解决影院管理

**传统方式解决影院管理说明**

1. 外观模式可以理解为转换一群接口，客户只要调用一个接口，而不用调用多个接口才能达到目的。比如：在 pc 上安装软件的时候经常有一键安装选项（省去选择安装目录、安装的组件等等），还有就是手机的重启功能（把关机和启动合为一个操作）。

2. 外观模式就是解决多个复杂接口带来的使用困难，起到简化用户操作的作用

<center><img src="https://img-blog.csdnimg.cn/2021020315540920.png“ /></center>

#### 外观模式应用实例

<center><img src="https://img-blog.csdnimg.cn/20210203155432207.png"/></center>

```java
public class Screen {
    //使用饿汉式
    private static Screen instance = new Screen();
    public static Screen getInstance() {
        return instance;
    }
    private Screen(){}
    public void up() {
        System.out.println(" Screen up ");
    }
    public void down() {
        System.out.println(" Screen down ");
    }
}
Popcorn,Projector,等类与Screen类似,只有一些方法不同
```



```java
//外观类
public class HomeTheaterFacade {
    //定义各个子系统对象
    private TheaterLight theaterLight=null;
    private Screen screen=null;
    .........
        //构造器
        public HomeTheaterFacade() {
        super();
        this.theaterLight = TheaterLight.getInstance();
        this.screen = Screen.getInstance();
        .......
    }

    //操作分成 4 步
    public void ready() {
        popcorn.on();
        screen.down();
        .........
    }

    public void play() {
        dVDPlayer.play();
    }

    public void pause() {
        dVDPlayer.pause();
    }

    public void end() {
        theaterLight.bright();
        screen.up();
        .........
    }
}
```



#### 外观模式在 MyBatis 框架应用的源码分析

1. **MyBatis** 中的 **Configuration** 去创建 **MetaObject** 对象使用到外观模式

2. 代码分析+**Debug** 源码+示意图

<center><img src="https://img-blog.csdnimg.cn/20210203155743786.png" /></center>

对源码中使用到的外观模式的角色类图

<center><img src="https://img-blog.csdnimg.cn/20210203155809665.png" /></center>



#### 外观模式的注意事项和细节

1. 外观模式对外屏蔽了子系统的细节，因此**外观模式降低了客户端对子系统使用的复杂性**

2. **外观模式对客户端与子系统的耦合关系 - 解耦**，让子系统内部的模块更易维护和扩展
3. 通过合理的使用外观模式，可以帮我们更好的**划分访问的层次**
4. **当系统需要进行分层设计时，可以考虑使用 Facade 模式**
5. 在维护一个遗留的大型系统时，可能这个系统已经变得非常难以维护和扩展，此时可以考虑为新系统**开发一个Facade 类，来提供遗留系统的比较清晰简单的接口，让新系统与 Facade 类交互，提高复用性**
6. 不能过多的或者不合理的使用外观模式，使用外观模式好，还是直接调用模块好。要以让系统有层次，利于维护为目的。



### 享元模式

#### 展示网站项目需求

小型的外包项目，给客户 A 做一个产品展示网站，客户 A 的朋友感觉效果不错，也希望做这样的产品展示网站，但是要求都有些不同：

1. 有客户要求以新闻的形式发布

2. 有客户人要求以博客的形式发布

3. 有客户希望以微信公众号的形式发布

 

#### 传统方案解决网站展现项目

1. 直接复制粘贴一份，然后根据客户不同要求，进行定制修改

2. 给每个网站租用一个空间

<center><img src="https://img-blog.csdnimg.cn/20210203155842274.png" /></center>



#### 传统方案解决网站展现项目-问题分析

1. 需要的网站结构相似度很高，而且都不是高访问量网站，如果分成多个虚拟空间来处理，相当于一个相同网站的实例对象很多，造成服务器的资源浪费

2. 解决思路：整合到一个网站中，共享其相关的代码和数据，对于硬盘、内存、CPU、数据库空间等服务器资源都可以达成共享，减少服务器资源

3. 对于代码来说，由于是一份实例，维护和扩展都更加容易

4. 上面的解决思路就可以使用 享元模式 来解决



#### 享元模式基本介绍

1. 享元模式（Flyweight Pattern） 也叫 **蝇量模式**: 运用共享技术有效地支持大量细粒度的对象

2. 常用于系统底层开发，解决系统的性能问题。像数据库连接池，里面都是创建好的连接对象，在这些连接对象中有我们需要的则直接拿来用，避免重新创建，如果没有我们需要的，则创建一个

3. **享元模式能够解决重复对象的内存浪费的问题**，当系统中有大量相似对象，需要缓冲池时。**不需总是创建新对象，可以从缓冲池里拿**。这样**可以降低系统内存，同时提高效率**

4. 享元模式经典的应用场景就是池技术了，**String 常量池、数据库连接池、缓冲池**等等都是享元模式的应用，享元模式是池技术的重要实现方式

<center><img src="https://img-blog.csdnimg.cn/20210203155907372.png" /></center>



#### 享元模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203155934438.png" /></center>

1) **FlyWeight** 是抽象的享元角色, 他是产品的抽象类, 同时定义出对象的外部状态和内部状态(后面介绍)  的接口或实现

2) **ConcreteFlyWeight** 是具体的享元角色，是具体的产品类，实现抽象角色定义相关业务

3) **UnSharedConcreteFlyWeight** 是不可共享的角色，一般不会出现在享元工厂。

4) **FlyWeightFactory** 享元工厂类，用于构建一个池容器(集合)， 同时提供从池中获取对象方法

 

#### 内部状态和外部状态

比如围棋、五子棋、跳棋，它们都有大量的棋子对象，围棋和五子棋只有黑白两色，跳棋颜色多一点，所以棋子颜色就是棋子的内部状态；而各个棋子之间的差别就是位置的不同，当我们落子后，落子颜色是定的，但位置是变化的，所以棋子坐标就是棋子的外部状态	

1. 享元模式提出了两个要求：**细粒度**和**共享对象**。这里就涉及到内部状态和外部状态了，即将对象的信息分为两个部分：**内部状态**和**外部状态**

2. 内部状态指对象共享出来的信息，存储在享元对象内部且不会随环境的改变而改变

3. 外部状态指对象得以依赖的一个标记，是随环境改变而改变的、不可共享的状态。

举个例子：围棋理论上有 361 个空位可以放棋子，每盘棋都有可能有两三百个棋子对象产生，因为内存空间有限，一台服务器很难支持更多的玩家玩围棋游戏，如果用享元模式来处理棋子，那么棋子对象就可以减少到只有两个实例，这样就很好的解决了对象的开销问题

 

#### 享元模式解决网站展现项目

1. 应用实例要求：使用享元模式完成，前面提出的网站外包问题

2. 思路分析和图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203160000896.png" /></center>

```java
public abstract class WebSite {
    public abstract void use(User user);//抽象方法
}
```

```java
//具体网站
public class ConcreteWebSite extends WebSite {
    //共享的部分，内部状态
    private String type = ""; //网站发布的形式(类型)
    //构造器
    public ConcreteWebSite(String type) {
        this.type = type;
    }
    //User是外部状态
    @Override
    public void use(User user) {
        System.out.println("网站的发布形式为:" + type + " 在使用中 .. 使用者是" + user.getName());
    }
}
```

```java
public class User {
   private String name;
   .....省略构造器和set,get方法
}
```

```java
// 网站工厂类，根据需要返回压一个网站
public class WebSiteFactory {
    //集合， 充当池的作用
    private HashMap<String, ConcreteWebSite> pool = new HashMap<>();
    //根据网站的类型，返回一个网站, 如果没有就创建一个网站，并放入到池中,并返回
    public WebSite getWebSiteCategory(String type) {
        if(!pool.containsKey(type)) {
            //就创建一个网站，并放入到池中
            pool.put(type, new ConcreteWebSite(type));
        }
        return (WebSite)pool.get(type);
    }
    //获取网站分类的总数 (池中有多少个网站类型)
    public int getWebSiteCount() {
        return pool.size();
    }
}
```





#### 享元模式在 JDK-Interger 的应用源码分析

1. Integer 中的享元模式

2. 代码分析+Debug 源码+说明

<center><img src="https://img-blog.csdnimg.cn/20210203160537734.png" /></center>

valueOf 方法，就使用到享元模式

在 valueOf 方法中，先判断值是否在 IntegerCache 中，如果不在，就创建新的 Integer(new),  否则，就直接从 缓存池返回

如果使用 valueOf 方法得到一个 Integer 实例，范围在 -128 - 127  ，执行速度比 new 快



#### 享元模式的注意事项和细节 

1. 在享元模式这样理解，“享”就表示共享，“元”表示对象

2. **系统中有大量对象，这些对象消耗大量内存，并且对象的状态大部分可以外部化时**，我们就可以考虑选用享元模式

3. 用唯一标识码判断，如果在内存中有，则返回这个唯一标识码所标识的对象，**用 HashMap/HashTable 存储**

4. **享元模式大大减少了对象的创建，降低了程序内存的占用，提高效率**

5. **享元模式提高了系统的复杂度。需要分离出内部状态和外部状态，而外部状态具有固化特性**，不应该随着内部状态的改变而改变，这是我们使用享元模式需要注意的地方.

6. 使用享元模式时，注意划分内部状态和外部状态，并且需要有一个工厂类加以控制。

7. 享元模式经典的应用场景是需要缓冲池的场景，比如 **String 常量池、数据库连接池**



### 代理模式(Proxy)

代理模式的基本介绍 

代理模式：为一个对象提供一个替身，以控制对这个对象的访问。即通过代理对象访问目标对象.这样做的好处是:可以在目标对象实现的基础上,增强额外的功能操作,即扩展目标对象的功能。

 被代理的对象可以是远程对象、创建开销大的对象或需要安全控制的对象

代理模式有不同的形式, 主要有三种 **静态代理**、**动态代理** (**JDK 代理**(接口代理)， **Cglib 代理**  (可以在内存动态的创建对象，而不需要实现接口， 他是属于动态代理的范畴) ）。

代理模式示意图

<center><img src="https://img-blog.csdnimg.cn/20210203160608663.png" /></center>

 

#### 静态代理

##### 静态代码模式的基本介绍

静态代理在使用时,**需要定义接口或者父类**,被代理对象(即目标对象)与代理对象一起实现相同的接口或者是继承相同父类

##### 应用实例

具体要求

1. 定义一个接口:ITeacherDao

2. 目标对象 TeacherDAO 实现接口 ITeacherDAO

3. 使用静态代理方式,就需要在代理对象 TeacherDAOProxy 中也实现 ITeacherDAO

4.  调用的时候通过调用代理对象的方法来调用目标对象.

5. 特别提醒：代理对象与目标对象要实现相同的接口,然后通过调用相同的方法来调用目标对象的方法

思路分析图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203160636923.png" /></center>

##### 静态代理优缺点 

1. 优点：在不修改目标对象的功能前提下, 能通过代理对象对目标功能扩展

2. 缺点：因为代理对象需要与目标对象实现一样的接口,所以会有很多代理类

3. 一旦接口增加方法,目标对象与代理对象都要维护

 

#### 动态代理

##### 动态代理模式的基本介绍 

1. **代理对象,不需要实现接口，但是目标对象要实现接口**，否则不能用动态代理

2. 代理对象的生成，是利用 JDK 的 API，动态的在内存中构建代理对象

3. 动态代理也叫做：JDK 代理、接口代理

 

##### JDK 中生成代理对象的 API

1. 代理类所在包:**java.lang.reflect.Proxy**

2.  JDK 实现代理只需要使用 **newProxyInstance** 方法,但是该方法需要接收三个参数,完整的写法是:

   ```java
   static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces,InvocationHandler h )
   ```

   

 

##### 动态代理应用实例

应用实例要求

将前面的静态代理改进成动态代理模式(即：JDK 代理模式)

思路图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203160701905.png" /></center>

```java
public class ProxyFactory {
    //维护一个目标对象 , Object
    private Object target;

    //构造器 ， 对target 进行初始
    public ProxyFactory(Object target) {
        this.target = target;
    } 

    //给目标对象 生成一个代理对象(使用匿名内部类的方式))
    public Object getProxyInstance() {
        //说明
        /*
       *  public static Object newProxyInstance(ClassLoader loader,
                                          Class<?>[] interfaces,
                                          InvocationHandler h)

            //1. ClassLoader loader ： 指定当前目标对象使用的类加载器, 获取加载器的方法固定
            //2. Class<?>[] interfaces: 目标对象实现的接口类型，使用泛型方法确认类型
            //3. InvocationHandler h : 事情处理，执行目标对象的方法时，会触发事情处理器方法, 会把当前执行的目标对象方法作为参数传入
       */
        return Proxy.newProxyInstance(target.getClass().getClassLoader(), 
                                      target.getClass().getInterfaces(), 
                                      new InvocationHandler() {
                                          @Override
                                          public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                                              // TODO Auto-generated method stub
                                              System.out.println("JDK代理开始~~");
                                              //反射机制调用目标对象的方法
                                              Object returnVal = method.invoke(target, args);
                                              System.out.println("JDK代理提交");
                                              return returnVal;
                                          }
                                      }); 
    }
}
```



#### Cglib 代理

##### Cglib 代理模式的基本介绍

1. 静态代理和 JDK 代理模式都要求目标对象是实现一个接口,但是有时候目标对象只是一个单独的对象,并没有实现任何的接口,这个时候可使用目标对象子类来实现代理-这就是 Cglib 代理

2. Cglib 代理也叫作子类代理,它是在内存中构建一个子类对象从而实现对目标对象功能扩展, 有些书也将Cglib 代理归属到动态代理。

3. Cglib 是一个强大的高性能的代码生成包,它可以在运行期扩展 java 类与实现 java 接口.**它广泛的被许多 AOP 的框架使用**,例如 Spring AOP，实现方法拦截

4. 在 AOP 编程中如何选择代理模式：
   - **目标对象需要实现接口，用 JDK 代理**
   - **目标对象不需要实现接口，用 Cglib 代理**

5. **Cglib 包的底层是通过使用字节码处理框架 ASM 来转换字节码并生成新的类**



##### Cglib 代理模式实现步骤

1. 需要引入 cglib 的 jar 文件

2. 在内存中动态构建子类，**注意代理的类不能为 final**，否则报错		

   ```java
   java.lang.IllegalArgumentException:
   ```

3. 目标对象的方法如果为 **final/static**,那么就不会被拦截,即不会执行目标对象额外的业务方法.

 

##### Cglib 代理模式应用实例

应用实例要求

将前面的案例用 Cglib 代理模式实现

思路图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203160724908.png" /></center>

```java
public class ProxyFactory implements MethodInterceptor {
    //维护一个目标对象
    private Object target;

    //构造器，传入一个被代理的对象
    public ProxyFactory(Object target) {
        this.target = target;
    }

    //返回一个代理对象:  是 target 对象的代理对象
    public Object getProxyInstance() {
        System.setProperty(DebuggingClassWriter.DEBUG_LOCATION_PROPERTY, "D:\\workspace\\DesignPattern\\out\\production\\DesignPattern\\com\\proxy");
        //1. 创建一个工具类
        Enhancer enhancer = new Enhancer();
        //2. 设置父类
        enhancer.setSuperclass(target.getClass());
        //3. 设置回调函数
        enhancer.setCallback(this);
        //4. 创建子类对象，即代理对象
        return enhancer.create();  
    }
    //重写  intercept 方法，会调用目标对象的方法
    @Override
    public Object intercept(Object arg0, Method method, Object[] args, MethodProxy arg3) throws Throwable {
        // TODO Auto-generated method stub
        System.out.println("Cglib代理模式 ~~ 开始");
        Object returnVal = method.invoke(target, args);
        System.out.println("Cglib代理模式 ~~ 提交");
        return returnVal;
    }
}
```



#### 几种常见的代理模式介绍— 几种变体

1. 防火墙代理

   内网通过代理穿透防火墙，实现对公网的访问。

2.  缓存代理

   比如：当请求图片文件等资源时，先到缓存代理取，如果取到资源则 ok,如果取不到资源，再到公网或者数据库取，然后缓存。

3. 远程代理

   远程对象的本地代表，通过它可以把远程对象当本地对象来调用。远程代理通过网络和真正的远程对象沟通信息。

4. 同步代理：

   主要使用在多线程编程中，完成多线程间同步工作同步代理：主要使用在多线程编程中，完成多线程间同步工作



## 行为型模式

### 模板方法模式

#### 豆浆制作问题

编写制作豆浆的程序，说明如下: 

1. 制作豆浆的流程 选材--->添加配料--->浸泡--->放到豆浆机打碎

2. 通过添加不同的配料，可以制作出不同口味的豆浆

3. 选材、浸泡和放到豆浆机打碎这几个步骤对于制作每种口味的豆浆都是一样的

4. 请使用  模板方法模式  完成 (说明：因为模板方法模式，比较简单，很容易就想到这个方案，因此就直接使用， 不再使用传统的方案来引出模板方法模式 )

 

#### 模板方法模式基本介绍

1.  模板方法模式（Template Method Pattern），又叫模板模式(Template Pattern)，z在一个抽象类公开定义了执行它的方法的模板。它的子类可以按需要重写方法实现，但调用将以抽象类中定义的方式进行。

2.  简单说，**模板方法模式 定义一个操作中的算法的骨架，而将一些步骤延迟到子类中，使得子类可以不改变一个算法的结构，就可以重定义该算法的某些特定步骤,注意使用钩子方法**

3. **这种类型的设计模式属于行为型模式。**

 

#### 模板方法模式原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203160751489.png" /></center>

对原理类图的说明-即(模板方法模式的角色及职责)

1. AbstractClass 抽象类， 类中实现了模板方法(template)，定义了算法的骨架，具体子类需要去实现 其它的抽象方法 operationr2,3,4

2. ConcreteClass 实现抽象方法 operationr2,3,4,  以完成算法中特点子类的步骤

 

#### 模板方法模式解决豆浆制作问题

1. 应用实例要求

   制作豆浆的流程 选材--->添加配料--->浸泡--->放到豆浆机打碎通过添加不同的配料，可以制作出不同口味的豆浆。选材、浸泡和放到豆浆机打碎这几个步骤对于制作每种口味的豆浆都是一样的(红豆、花生豆浆。。。)

2. 思路分析和图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203160817180.png" /></center>



#### 模板方法模式的钩子方法

1. 在模板方法模式的父类中，我们可以定义一个方法，它默认不做任何事，**子类可以视情况要不要覆盖它，该方法称为“钩子”。**

2. 还是用上面做豆浆的例子来讲解，比如，我们还希望制作纯豆浆，不添加任何的配料，请使用钩子方法对前面的模板方法进行改造

```java
public abstract class SoyaMilk {

    //模板方法, make , 模板方法可以做成final , 不让子类去覆盖.
    final void make() {
        select(); 
        if(customerWantCondiments()) {
            addCondiments();
        }
        soak();
        beat();
    }

    //选材料
    void select() {
        System.out.println("第一步：选择好的新鲜黄豆  ");
    }

    //添加不同的配料， 抽象方法, 子类具体实现
    abstract void addCondiments();

    //浸泡
    void soak() {
        System.out.println("第三步， 黄豆和配料开始浸泡， 需要3小时 ");
    }

    void beat() {
        System.out.println("第四步：黄豆和配料放到豆浆机去打碎  ");
    }

    //钩子方法，决定是否需要添加配料
    boolean customerWantCondiments() {
        return true;
    }
}
```

```java
public class PureSoyaMilk extends SoyaMilk{
    @Override
    void addCondiments() {
        // TODO Auto-generated method stub
        //空实现
    }

    @Override
    boolean customerWantCondiments() {
        // TODO Auto-generated method stub
        return false;
    }
}
```



#### 模板方法模式在 Spring 框架应用的源码分析 

1. Spring IOC 容器初始化时运用到的模板方法模式

2. 代码分析+角色分析+说明类图

<center><img src="https://img-blog.csdnimg.cn/20210203160842676.png" /></center>

3. 针对源码的类图(说明层次关系)

<center><img src="https://img-blog.csdnimg.cn/20210203160904342.png" /></center>

#### 模板方法模式的注意事项和细节 

1. **基本思想**是：算法只存在于一个地方，也就是在父类中，容易修改。需要修改算法时，只要修改父类的模板方法或者已经实现的某些步骤，子类就会继承这些修改

2. 实现了**最大化代码复用**。父类的模板方法和已实现的某些步骤会被子类继承而直接使用。

3. 既统一了算法，也提供了很大的灵活性。父类的模板方法确保了算法的结构保持不变，同时由子类提供部分步骤的实现。

4. 该模式的不足之处：**每一个不同的实现都需要一个子类实现，导致类的个数增加，使得系统更加庞大**

5. **一般模板方法都加上 final 关键字， 防止子类重写模板方法.**

6. 模板方法模式使用场景：**当要完成在某个过程，该过程要执行一系列步骤 ，这一系列的步骤基本相同，但其个别步骤在实现时 可能不同，通常考虑用模板方法模式来处理**



### 命令模式

#### 智能生活项目需求

看一个具体的需求

<center><img src="https://img-blog.csdnimg.cn/2021020316092733.png" /></center>

1. 我们买了一套智能家电，有照明灯、风扇、冰箱、洗衣机，我们只要在手机上安装 app 就可以控制对这些家电工作。

2. 这些智能家电来自不同的厂家，我们不想针对每一种家电都安装一个 App，分别控制，我们希望只要一个 app就可以控制全部智能家电。

3. 要实现一个 app 控制所有智能家电的需要，则每个智能家电厂家都要提供一个统一的接口给 app 调用，这时 就可以考虑使用命令模式。

4. 命令模式可将“动作的请求者”从“动作的执行者”对象中解耦出来.

5. 在我们的例子中，动作的请求者是手机 app，动作的执行者是每个厂商的一个家电产品

 

#### 命令模式基本介绍

1. 命令模式（Command Pattern）：在软件设计中，我们经常需要向某些对象发送请求，但是并不知道请求的接收者是谁，也不知道被请求的操作是哪个，我们只需在程序运行时指定具体的请求接收者即可，此时，可以使用命令模式来进行设计

2. 命令模式使得**请求发送者与请求接收者消除彼此之间的耦合**，让对象之间的调用关系更加灵活，实现解耦。

3. 在命名模式中，会将一个请求封装为一个对象，以便使用不同参数来表示不同的请求(即命名)，同时命令模式也支持可撤销的操作。

4. 通俗易懂的理解：将军发布命令，士兵去执行。其中有几个角色：将军（命令发布者）、士兵（命令的具体执行者）、命令(连接将军和士兵)。

   Invoker 是调用者（将军），Receiver 是被调用者（士兵），MyCommand 是命令，实现了 Command 接口，持有接收对象

####  命令模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203160949562.png" /></center>

对原理类图的说明-即(命名模式的角色及职责)

1. `Invoker` 是调用者角色

2. `Command`: 是命令角色，需要执行的所有命令都在这里，可以是接口或抽象类

3. `Receiver`: 接受者角色，知道如何实施和执行一个请求相关的操作

4. `ConcreteCommand`: 将一个接受者对象与一个动作绑定，调用接受者相应的操作，实现 execute

 

#### 命令模式解决智能生活项目

1. 编写程序，使用命令模式 完成前面的智能家电项目

2. 思路分析和图解

<center><img src="https://img-blog.csdnimg.cn/20210203161011411.png" /></center>

```java
//创建命令接口
public interface Command {
   //执行动作(操作)
   public void execute();
   //撤销动作(操作)
   public void undo();
}
```



```java
public class LightOnCommand implements Command {
    //聚合LightReceiver

    LightReceiver light;

    //构造器
    public LightOnCommand(LightReceiver light) {
        this.light = light;
    }
    @Override
    public void execute() {
        //调用接收者的方法
        light.on();
    }

    @Override
    public void undo() {
        //调用接收者的方法
        light.off();
    }
}
```

```java
public class LightOffCommand implements Command {省略}
public class NoCommand implements Command {继承的方法不需要写任何内容}
```

```java
public class LightReceiver {
   public void on() {
      System.out.println(" 电灯打开了.. ");
   }
   public void off() {
      System.out.println(" 电灯关闭了.. ");
   }
}
```



```java
public class RemoteController {
   // 开 按钮的命令数组
   Command[] onCommands;
   Command[] offCommands;
   // 执行撤销的命令
   Command undoCommand;

   // 构造器，完成对按钮初始化
   public RemoteController() {
      onCommands = new Command[5];
      offCommands = new Command[5];
      for (int i = 0; i < 5; i++) {
         onCommands[i] = new NoCommand();
         offCommands[i] = new NoCommand();
      }
   }

   // 给我们的按钮设置你需要的命令
   public void setCommand(int no, Command onCommand, Command offCommand) {
      onCommands[no] = onCommand;
      offCommands[no] = offCommand;
   }

   // 按下开按钮
   public void onButtonWasPushed(int no) { // no 0
      // 找到你按下的开的按钮， 并调用对应方法
      onCommands[no].execute();
      // 记录这次的操作，用于撤销
      undoCommand = onCommands[no];
   }

   // 按下开按钮
   public void offButtonWasPushed(int no) { // no 0
      // 找到你按下的关的按钮， 并调用对应方法
      offCommands[no].execute();
      // 记录这次的操作，用于撤销
      undoCommand = offCommands[no];
   }
   
   // 按下撤销按钮
   public void undoButtonWasPushed() {
      undoCommand.undo();
   }
}
```





#### 命令模式在 Spring 框架 JdbcTemplate 应用的源码分析

1. Spring 框架的 JdbcTemplate 就使用到了命令模式

2. 代码分析

<center><img src="https://img-blog.csdnimg.cn/20210203161037873.png" /></center>

模式角色分析说明

StatementCallback 接口 ,类似命令接口(Command)

class QueryStatementCallback implements StatementCallback<T>, SqlProvider , 匿名内部类， 实现了命令接口， 同时也充当命令接收者

命令调用者 是 JdbcTemplate , 其中 execute(StatementCallback<T> action) 方法中，调用 action.doInStatement 方法. 不同的 实现 StatementCallback 接口的对象，对应不同的 doInStatemnt  实现逻辑

l另外实现  StatementCallback 命令接口的子类还有 QueryStatementCallback、

<center><img src="https://img-blog.csdnimg.cn/20210203161104949.png" /></center>

#### 命令模式的注意事项和细节

1. **将发起请求的对象与执行请求的对象解耦**。发起请求的对象是调用者，调用者只要调用命令对象的 execute()方法就可以让接收者工作，而不必知道具体的接收者对象是谁、是如何实现的，命令对象会负责让接收者执行请求的动作，也就是说：”请求发起者”和“请求执行者”之间的解耦是通过命令对象实现的，命令对象起到了纽带桥梁的作用。

2. 容易设计一个命令队列。只要把命令对象放到列队，就可以多线程的执行命令

3. **容易实现对请求的撤销和重做**

4. 命令模式不足：可能导致某些系统有过多的具体命令类，增加了系统的复杂度，这点在在使用的时候要注意

5. **空命令也是一种设计模式**，它为我们省去了判空的操作。在上面的实例中，如果没有用空命令，我们每按下一个按键都要判空，这给我们编码带来一定的麻烦。

6. 命令模式经典的应用场景：**界面的一个按钮都是一条命令、模拟 CMD（DOS 命令）订单的撤销/恢复、触发- 反馈机制**



### 访问者模式

[http://c.biancheng.net/view/1397.html](http://c.biancheng.net/view/1397.html)

在现实生活中，有些集合对象中存在多种不同的元素，且每种元素也存在多种不同的访问者和处理方式。例如，公园中存在多个景点，也存在多个游客，不同的游客对同一个景点的评价可能不同；医院医生开的处方单中包含多种药元素，査看它的划价员和药房工作人员对它的处理方式也不同，划价员根据处方单上面的药品名和数量进行划价，药房工作人员根据处方单的内容进行抓药。

这样的例子还有很多，例如，电影或电视剧中的人物角色，不同的观众对他们的评价也不同；还有顾客在商场购物时放在“购物车”中的商品，顾客主要关心所选商品的性价比，而收银员关心的是商品的价格和数量。

这些被处理的**数据元素相对稳定而访问方式多种多样**的[数据结构](http://c.biancheng.net/data_structure/)，如果用“访问者模式”来处理比较方便。访问者模式能把处理方法从数据结构中分离出来，并可以根据需要增加新的处理方法，且不用修改原来的程序代码与数据结构，这提高了程序的扩展性和灵活性。

#### 模式的定义

访问者（Visitor）模式的定义：**将作用于某种数据结构中的各元素的操作分离出来封装成独立的类，使其在不改变数据结构的前提下可以添加作用于这些元素的新的操作，为数据结构中的每个元素提供多种访问方式。** 它将对数据的操作与数据结构进行分离，是行为类模式中最复杂的一种模式。

访问者（Visitor）模式实现的关键是**如何将作用于元素的操作分离出来封装成独立的类**，其基本结构与实现方法如下。

#### 模式的结构

访问者模式包含以下主要角色。

1. **抽象访问者（Visitor）角色**：定义一个访问具体元素的接口，为每个具体元素类对应一个访问操作 visit() ，该操作中的参数类型标识了被访问的具体元素。
2. **具体访问者（ConcreteVisitor）角色**：实现抽象访问者角色中声明的各个访问操作，确定访问者访问一个元素时该做什么。
3. **抽象元素（Element）角色**：声明一个包含接受操作 accept() 的接口，被接受的访问者对象作为 accept() 方法的参数。
4. **具体元素（ConcreteElement）角色**：实现抽象元素角色提供的 accept() 操作，其方法体通常都是 visitor.visit(this) ，另外具体元素中可能还包含本身业务逻辑的相关操作。
5. **对象结构（Object Structure）角色**：是一个包含元素角色的容器，提供让访问者对象遍历容器中的所有元素的方法，通常由 List、Set、Map 等聚合类实现。

<center><img src="https://img-blog.csdnimg.cn/20210203161127400.png" height=500 /></center>



#### 模式的应用实例(具体代码在代码模块)

利用“访问者（Visitor）模式”模拟艺术公司与造币公司的功能。

分析：艺术公司利用“铜”可以设计出铜像，利用“纸”可以画出图画；造币公司利用“铜”可以印出铜币，利用“纸”可以印出纸币（[点此下载运行该程序后所要显示的图片](http://c.biancheng.net/uploads/soft/181113/3-1Q119103045.zip)）。**对“铜”和“纸”这两种元素，两个公司的处理方法不同，所以该实例用访问者模式来实现比较适合。**

首先，定义一个公司（Company）接口，它是抽象访问者，提供了两个根据纸（Paper）或铜（Cuprum）这两种元素创建作品的方法；再定义艺术公司（ArtCompany）类和造币公司（Mint）类，它们是具体访问者，实现了父接口的方法；然后，定义一个材料（Material）接口，它是抽象元素，提供了 accept（Company visitor）方法来接受访问者（Company）对象访问；再定义纸（Paper）类和铜（Cuprum）类，它们是具体元素类，实现了父接口中的方法；最后，定义一个材料集（SetMaterial）类，它是对象结构角色，拥有保存所有元素的容器 List，并提供让访问者对象遍历容器中的所有元素的 accept（Company visitor）方法；客户类设计成窗体程序，它提供材料集（SetMaterial）对象供访问者（Company）对象访问，实现了 ItemListener 接口，处理用户的事件请求。图 2 所示是其结构图。

<center><img src="https://img-blog.csdnimg.cn/20210203161202363.png" /></center>



```java
//抽象访问者:公司
interface Company
{
    String create(Paper element);
    String create(Cuprum element);
}
//具体访问者：艺术公司
class ArtCompany implements Company
{
    public String create(Paper element)
    {
        return "讲学图";
    }
    public String create(Cuprum element)
    {
        return "朱熹铜像";
    }
}
//具体访问者：造币公司
class Mint implements Company
{
    public String create(Paper element)
    {
        return "纸币";
    }
    public String create(Cuprum element)
    {
        return "铜币";
    }
}
//抽象元素：材料
interface Material
{
    String accept(Company visitor);
}
//具体元素：纸
class Paper implements Material
{
    public String accept(Company visitor)
    {
        return(visitor.create(this));
    }
}
//具体元素：铜
class Cuprum implements Material
{
    public String accept(Company visitor)
    {
        return(visitor.create(this));
    }
}
//对象结构角色:材料集
class SetMaterial
{   
    private List<Material> list=new ArrayList<Material>();   
    public String accept(Company visitor)
    {
        Iterator<Material> i=list.iterator();
        String tmp="";
        while(i.hasNext())
        {
            tmp+=((Material) i.next()).accept(visitor)+" ";
        }
        return tmp; //返回某公司的作品集     
    }
    public void add(Material element)
    {
        list.add(element);
    }
    public void remove(Material element)
    {
        list.remove(element);
    }
}
```



<center><img src="https://img-blog.csdnimg.cn/20210203161247785.png" /></center>

#### 模式的应用场景

通常在以下情况可以考虑使用访问者（Visitor）模式。

1. **对象结构相对稳定，但其操作算法经常变化的程序。**
2. **对象结构中的对象需要提供多种不同且不相关的操作，而且要避免让这些操作的变化影响对象的结构。**
3. **对象结构包含很多类型的对象，希望对这些对象实施一些依赖于其具体类型的操作。**



#### 模式的优缺点

访问者（Visitor）模式是一种对象行为型模式，其主要优点如下。

1. **扩展性好**。能够在不修改对象结构中的元素的情况下，为对象结构中的元素添加新的功能。
2. **复用性好**。可以通过访问者来定义整个对象结构通用的功能，从而提高系统的复用程度。
3. **灵活性好**。访问者模式将数据结构与作用于结构上的操作解耦，使得操作集合可相对自由地演化而不影响系统的数据结构。
4. **符合单一职责原则**。访问者模式把相关的行为封装在一起，构成一个访问者，使每一个访问者的功能都比较单一。

访问者（Visitor）模式的主要缺点如下。

1. **增加新的元素类很困难**。在访问者模式中，每增加一个新的元素类，都要在每一个具体访问者类中增加相应的具体操作，这违背了“开闭原则”。
2. **破坏封装**。访问者模式中具体元素对访问者公布细节，这破坏了对象的封装性。
3. **违反了依赖倒置原则**。访问者模式依赖了具体类，而没有依赖抽象类。



#### 模式的扩展

访问者（Visitor）模式是使用频率较高的一种[设计模式](http://c.biancheng.net/design_pattern/)，它常常同以下两种设计模式联用。

1. **与“[迭代器模式](http://c.biancheng.net/view/1395.html)”联用**。因为访问者模式中的“对象结构”是一个包含元素角色的容器，当访问者遍历容器中的所有元素时，常常要用迭代器。如【例1】中的对象结构是用 List 实现的，它通过 List 对象的 Itemtor() 方法获取迭代器。如果对象结构中的聚合类没有提供迭代器，也可以用迭代器模式自定义一个。

2. **访问者（Visitor）模式同“[组合模式](http://c.biancheng.net/view/1373.html)”联用**。因为访问者（Visitor）模式中的“元素对象”可能是叶子对象或者是容器对象，如果元素对象包含容器对象，就必须用到[组合模式](http://c.biancheng.net/view/1373.html)，其结构图如图 4 所示。

<center><img src="https://img-blog.csdnimg.cn/20210203161320626.png" /></center>



### 迭代器模式

#### 看一个具体的需求

编写程序展示一个学校院系结构：需求是这样，要在一个页面中展示出学校的院系组成，一个学校有多个学院， 一个学院有多个系。如图：

<center><img src="https://img-blog.csdnimg.cn/20210203161345775.png" /></center>

#### 传统的设计方案(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203161406285.png" /></center>

#### 传统的方式的问题分析

1. 将学院看做是学校的子类，系是学院的子类，这样实际上是站在组织大小来进行分层次的

2. 实际上我们的要求是 ：在一个页面中展示出学校的院系组成，一个学校有多个学院，一个学院有多个系， 因此这种方案，不能很好实现的遍历的操作

3. 解决方案：=> 迭代器模式

#### 迭代器模式基本介绍

基本介绍

1. 迭代器模式（Iterator Pattern）是常用的设计模式，属于行为型模式

2. 如果我们的集合元素是用不同的方式实现的，有数组，还有 java 的集合类，或者还有其他方式，当客户端要遍历这些集合元素的时候就要使用多种遍历方式，而且还会暴露元素的内部结构，可以考虑使用迭代器模式解决。

3. 迭代器模式，**提供一种遍历集合元素的统一接口，用一致的方法遍历集合元素，不需要知道集合对象的底层表示，** 即：不暴露其内部的结构。

####  迭代器模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203161428402.png" /></center>

对原理类图的说明-即(迭代器模式的角色及职责)

1. `Iterator` ： 迭代器接口，是系统提供，含义 hasNext, next, remove

2. `ConcreteIterator` :  具体的迭代器类，管理迭代

3. `Aggregate `:一个统一的聚合接口， 将客户端和具体聚合解耦

4. `ConcreteAggreage `: 具体的聚合持有对象集合， 并提供一个方法，返回一个迭代器， 该迭代器可以正确遍历集合

5. `Client` :客户端，  通过 Iterator 和 Aggregate 依赖子类

#### 迭代器模式应用实例

1. 应用实例要求

   编写程序展示一个学校院系结构：需求是这样，要在一个页面中展示出学校的院系组成，一个学校有多个学院， 一个学院有多个系。

2. 设计思路分析

<center><img src="https://img-blog.csdnimg.cn/20210203161451889.png" /></center>

```java
public class ComputerCollegeIterator implements Iterator {
    //这里我们需要Department 是以怎样的方式存放=>数组
    Department[] departments;
    int position = 0; //遍历的位置

    public ComputerCollegeIterator(Department[] departments) {
        this.departments = departments;
    }

    //判断是否还有下一个元素
    @Override
    public boolean hasNext() {
        if(position >= departments.length || departments[position] == null) {
            return false;
        }else {
            return true;
        }
    }

    @Override
    public Object next() {
        // TODO Auto-generated method stub
        Department department = departments[position];
        position += 1;
        return department;
    }

    //删除的方法，默认空实现
    public void remove() {
    }
}
```

```java
public class ComputerCollege implements College {
//部门数组
Department[] departments=null;
@Override
public Iterator createIterator() {
   return new ComputerCollegeIterator(departments);
}
}
```



#### 迭代器模式在 JDK-ArrayList 集合应用的源码分析

1. JDK 的 ArrayList  集合中就使用了迭代器模式

2. 代码分析+类图+说明

<center><img src="https://img-blog.csdnimg.cn/20210203161514152.png" /></center>

<center><img src="https://img-blog.csdnimg.cn/20210203161541191.png" /></center>

对类图的角色分析和说明

内部类 Itr 充当具体实现迭代器 Iterator 的类， 作为 ArrayList  内部类，List 就是充当了聚合接口，含有一个 iterator() 方法，返回一个迭代器对象ArrayList 是实现聚合接口 List  的子类，实现了 iterator()

Iterator 接口系统提供	迭代器模式解决了 不同集合(ArrayList ,LinkedList) 统一遍历问题

 

#### 迭代器模式的注意事项和细节

 **优点：**

1. 提供一个统一的方法遍历对象，客户不用再考虑聚合的类型，使用一种方法就可以遍历对象了。

2. 隐藏了聚合的内部结构，客户端要遍历聚合的时候只能取到迭代器，而不会知道聚合的具体组成。

3. 提供了一种设计思想，就是一个类应该只有一个引起变化的原因（叫做单一责任原则）。在聚合类中，我们把迭代器分开，就是要**把管理对象集合和遍历对象集合的责任分开**，这样一来集合改变的话，只影响到聚合对象。而如果遍历方式改变的话，只影响到了迭代器。

4. 当要展示一组相似对象，或者遍历一组相同对象时使用, 适合使用迭代器模式

**缺点：**

每个聚合对象都要一个迭代器，会生成多个迭代器不好管理类



### 观察者模式

#### 观察者（Observer）模式的定义

指多个对象间存在一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。这种模式有时又称作发布-订阅模式、模型-视图模式，它是对象行为型模式。

#### 天气预报项目需求

具体要求如下：

1. 气象站可以将每天测量到的温度，湿度，气压等等以公告的形式发布出去(比如发布到自己的网站或第三方)。

2. 需要设计开放型 API，便于其他第三方也能接入气象站获取数据。

3. 提供温度、气压和湿度的接口

4. 测量数据更新时，要能实时的通知给第三方

 

#### 天气预报设计方案 1-普通方案

WeatherData 类

传统的设计方案

<center><img src="https://img-blog.csdnimg.cn/20210203161607332.png" /></center>

<center><img src="https://img-blog.csdnimg.cn/20210203161627890.png" /></center>

#### 问题分析

1. 其他第三方接入气象站获取数据的问题

2. 无法在运行时动态的添加第三方 (新浪网站)

3. 违反 ocp 原则=>观察者模式

```java
//在 WeatherData 中，当增加一个第三方，都需要创建一个对应的第三方的公告板对象，并加入到 dataChange, 不利于维护，也不是动态加入
public void dataChange() {
	currentConditions.update(getTemperature(), getPressure(), getHumidity());
}
```



#### 观察者模式原理

1. 观察者模式类似订牛奶业务

2. 奶站/气象局：Subject

3. 用户/第三方网站：Observer

 Subject：登记注册、移除和通知

1. `registerObserver` 注 册

2. `removeObserver` 移 除

3. `notifyObservers()` 通知所有的注册的用户，根据不同需求，可以是更新数据，让用户来取，也可能是实施推送， 看具体需求定

 Observer：接收输入

观察者模式：**对象之间多对一依赖的一种设计方案，并且当一个对象的状态发生变化时，所有依赖于他的对象都想得到通知并更新。** 被依赖的对象为 Subject，依赖的对象为 Observer，Subject通知 Observer 变化,比如这里的奶站是 Subject，是 1 的一方。用户时 Observer，是多的一方。

 

#### 观察者模式解决天气预报需求

类图说明

<center><img src="https://img-blog.csdnimg.cn/20210203161651520.png" /></center>

```java
//接口, 让WeatherData 来实现 
public interface Subject {
    public void registerObserver(Observer o);
    public void removeObserver(Observer o);
    public void notifyObservers();
}


/**
 * 类是核心
 * 1. 包含最新的天气情况信息 
 * 2. 含有 观察者集合，使用ArrayList管理
 * 3. 当数据有更新时，就主动的调用   ArrayList, 通知所有的（接入方）就看到最新的信息
 * @author Administrator
 *
 */
public class WeatherData implements Subject {
    private float temperatrue;
    private float pressure;
    private float humidity;
    //观察者集合
    private ArrayList<Observer> observers;

    //加入新的第三方

    public WeatherData() {
        observers = new ArrayList<Observer>();
    }

    public float getTemperature() {
        return temperatrue;
    }

    public float getPressure() {
        return pressure;
    }

    public float getHumidity() {
        return humidity;
    }

    public void dataChange() {
        //调用 接入方的 update

        notifyObservers();
    }

    //当数据有更新时，就调用 setData
    public void setData(float temperature, float pressure, float humidity) {
        this.temperatrue = temperature;
        this.pressure = pressure;
        this.humidity = humidity;
        //调用dataChange， 将最新的信息 推送给 接入方 currentConditions
        dataChange();
    }

    //注册一个观察者
    @Override
    public void registerObserver(Observer o) {
        // TODO Auto-generated method stub
        observers.add(o);
    }

    //移除一个观察者
    @Override
    public void removeObserver(Observer o) {
        // TODO Auto-generated method stub
        if(observers.contains(o)) {
            observers.remove(o);
        }
    }

    //遍历所有的观察者，并通知
    @Override
    public void notifyObservers() {
        // TODO Auto-generated method stub
        for(int i = 0; i < observers.size(); i++) {
            observers.get(i).update(this.temperatrue, this.pressure, this.humidity);
        }

    }
}
```

```java
//观察者接口，有观察者来实现
public interface Observer {
    public void update(float temperature, float pressure, float humidity);
}


public class CurrentConditions implements Observer {

    // 温度，气压，湿度
    private float temperature;
    private float pressure;
    private float humidity;

    // 更新 天气情况，是由 WeatherData 来调用，我使用推送模式
    public void update(float temperature, float pressure, float humidity) {
        this.temperature = temperature;
        this.pressure = pressure;
        this.humidity = humidity;
        display();
    }

    // 显示
    public void display() {
        System.out.println("***Today mTemperature: " + temperature + "***");
        System.out.println("***Today mPressure: " + pressure + "***");
        System.out.println("***Today mHumidity: " + humidity + "***");
    }
}
```



#### 观察者模式的好处

1. 观察者模式设计后，会以集合的方式来管理用户(Observer)，包括注册，移除和通知。

2. 这样，我们增加观察者(这里可以理解成一个新的公告板)，就不需要去修改核心类 WeatherData 不会修改代码， 遵守了 ocp 原则。



#### 观察者模式在 Jdk 应用的源码分析

1. Jdk 的 Observable 类就使用了观察者模式

2. 代码分析+模式角色分析

<center><img src="https://img-blog.csdnimg.cn/20210203161718708.png" /></center>

模式角色分析：

- Observable 的作用和地位等价于 我们前面讲过 Subject

- Observable 是类，不是接口，类中已经实现了核心的方法 ,即管理 Observer 的方	法 add.. delete .. notify...

- Observer 的作用和地位等价于我们前面讲过的 Observer, 有 update

- Observable 和 Observer 的使用方法和前面讲过的一样，只是 Observable 是类，通过继承来实现观察者模式

观察者模式是一种对象行为型模式，其主要优点如下：

1. **降低了目标与观察者之间的耦合关系，两者之间是抽象耦合关系。**
2. **目标与观察者之间建立了一套触发机制。**

它的主要缺点如下：

1. 目标与观察者之间的依赖关系并没有完全解除，**而且有可能出现循环引用。**
2. 当观察者对象很多时，通知的发布会花费很多时间，**影响程序的效率。**



### 中介者模式

中介者（Mediator）模式的定义：定义一个中介对象来封装一系列对象之间的交互，使原有对象之间的耦合松散，且可以独立地改变它们之间的交互。中介者模式又叫调停模式，它是**迪米特法则**的典型应用。

#### 智能家庭项目

1. 智能家庭包括各种设备，闹钟、咖啡机、电视机、窗帘 等

2.  主人要看电视时，各个设备可以协同工作，自动完成看电视的准备工作，比如流程为：闹铃响起->咖啡机开始做咖啡->窗帘自动落下->电视机开始播放

#### 传统方案解决智能家庭管理问题

<center><img src="https://img-blog.csdnimg.cn/20210203161744599.png" /></center>

 

#### 传统的方式的问题分析 

1. 当各电器对象有多种状态改变时，相互之间的调用关系会比较复杂

2. 各个电器对象彼此联系，你中有我，我中有你，**不利于松耦合.**

3. 各个电器对象之间所传递的消息(参数)，容易混乱

4. 当系统增加一个新的电器对象时，或者执行流程改变时，代码的可维护性、扩展性都不理想 考虑中介者模式



#### 中介者模式基本介绍

1. 中介者模式（Mediator Pattern），用一个中介对象来封装一系列的对象交互。中介者使各个对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互

2. 中介者模式属于行为型模式，使代码易于维护

3. 比如 **MVC 模式**，C（Controller 控制器）是 M（Model 模型）和 V（View 视图）的中介者，在前后端交互时起到了中间人的作用

#### 中介者模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203161810701.png" /></center>

 对原理类图的说明-即(中介者模式的角色及职责)

1. `Mediator` 就是抽象中介者,定义了同事对象到中介者对象的接口

2. `Colleague` 是抽象同事类

3. `ConcreteMediator` 具体的中介者对象, 实现抽象方法, 他需要知道所有的具体的同事类,即以一个集合来管理HashMap,并接受某个同事对象消息，完成相应的任务

4. `ConcreteColleague` 具体的同事类，会有很多, 每个同事只知道自己的行为， 而不了解其他同事类的行为(方法)， 但 是他们都依赖中介者对象



#### 中介者模式应用实例-智能家庭管理

应用实例要求

完成前面的智能家庭的项目，使用中介者模式

<center><img src="https://img-blog.csdnimg.cn/20210203161835476.png" /></center>

（代码看代码文件夹，此处引用另一个列子）

<center><img src="https://img-blog.csdnimg.cn/20210203161855630.png" /></center>

```java
package com.UMediator;

import java.util.*;
public class MediatorPattern
{
    public static void main(String[] args)
    {
        Mediator md=new ConcreteMediator();
        Colleague c1,c2;
        c1=new ConcreteColleague1();
        c2=new ConcreteColleague2();
        c1.setMedium(md);
        c2.setMedium(md);
        c1.send();
        System.out.println("-------------");
        c2.send();
    }
}
//抽象中介者
abstract class Mediator
{
    public abstract void register(Colleague colleague);
    public abstract void relay(Colleague cl); //转发
}
//具体中介者
class ConcreteMediator extends Mediator
{
    private List<Colleague> colleagues=new ArrayList<Colleague>();
    public void register(Colleague colleague)
    {
        if(!colleagues.contains(colleague))
        {
            colleagues.add(colleague);
        }
    }
    public void relay(Colleague cl)
    {
        for(Colleague ob:colleagues)
        {
            if(!ob.equals(cl))
            {
                ((Colleague)ob).receive();
            }
        }
    }
}
//抽象同事类
abstract class Colleague
{
    protected Mediator mediator;
    public void setMedium(Mediator mediator)
    {
        this.mediator=mediator;
        mediator.register(this);
    }
    public abstract void receive();
    public abstract void send();
}
//具体同事类
class ConcreteColleague1 extends Colleague
{
    public void receive()
    {
        System.out.println("具体同事类1收到请求。");
    }
    public void send()
    {
        System.out.println("具体同事类1发出请求。");
        mediator.relay(this); //请中介者转发
    }
}
//具体同事类
class ConcreteColleague2 extends Colleague
{
    public void receive()
    {
        System.out.println("具体同事类2收到请求。");
    }
    public void send()
    {
        System.out.println("具体同事类2发出请求。");
        mediator.relay(this); //请中介者转发
    }
}
```



#### 中介者模式的注意事项和细节

1. 多个类相互耦合，会形成网状结构, 使用中介者模式将网状结构分离为星型结构，进行解耦

2. 减少类间依赖，降低了耦合，符合迪米特原则

3. **中介者承担了较多的责任**，一旦中介者出现了问题，整个系统就会受到影响

4. 如果设计不当，中介者对象本身变得过于复杂，这点在实际使用时，要特别注意



#### 模式的应用场景

前面分析了中介者模式的结构与特点，下面分析其以下应用场景。

1. **当对象之间存在复杂的网状结构关系而导致依赖关系混乱且难以复用时。**

2. **想创建一个运行于多个类之间的对象，又不想生成新的子类时。**



#### 模式的扩展

在实际开发中，通常采用以下两种方法来简化中介者模式，使开发变得更简单。

1. **不定义中介者接口，把具体中介者对象实现成为单例。**
2. **同事对象不持有中介者，而是在需要的时直接获取中介者对象并调用。**



### 备忘录模式

备忘录（Memento）模式的定义：在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态，以便以后当需要时能将该对象恢复到原先保存的状态。该模式又叫快照模式。

#### 游戏角色状态恢复问题

游戏角色有攻击力和防御力，在大战 Boss 前保存自身的状态(攻击力和防御力)，当大战 Boss 后攻击力和防御力下降，从备忘录对象恢复到大战前的状态

#### 传统方案解决游戏角色恢复

<center><img src="https://img-blog.csdnimg.cn/20210203161931739.png" /></center>

#### 传统的方式的问题分析

1. 一个对象，就对应一个保存对象状态的对象， 这样当我们游戏的对象很多时，不利于管理，开销也很大.

2. 传统的方式是简单地做备份，new 出另外一个对象出来，再把需要备份的数据放到这个新对象，但这就暴露了对象内部的细节

3. 解决方案： => 备忘录模式

 

#### 备忘录模式基本介绍

1. 备忘录模式（Memento Pattern）在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态，以便以后当需要时能将该对象恢复到原先保存的状态。该模式又叫**快照模式**。

2. 可以这里理解备忘录模式：现实生活中的备忘录是用来记录某些要去做的事情，或者是记录已经达成的共同意见的事情，以防忘记了。而在软件层面，备忘录模式有着相同的含义，备忘录对象主要用来记录一个对象的某种状态，或者某些数据，当要做回退时，可以从备忘录对象里获取原来的数据进行恢复操作

3. 备忘录模式属于行为型模式

#### 备忘录模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203162049634.png" /></center>

 对原理类图的说明-即(备忘录模式的角色及职责)

1. `originator` :  发起人对象(需要保存状态的对象)

2. `Memento` ： 备忘录对象,负责保存好记录，即 Originator 内部状态

3. `Caretaker`: 守护者对象,负责保存多个备忘录对象， 使用集合管理，提高效率

4. 说明：如果希望保存多个 originator 对象的不同时间的状态，也可以，只需要要 HashMap <String, 集合>

#### 游戏角色恢复状态实例

1. 应用实例要求

   游戏角色有攻击力和防御力，在大战 Boss 前保存自身的状态(攻击力和防御力)，当大战 Boss 后攻击力和防御力下降，从备忘录对象恢复到大战前的状态

2. 思路分析和图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203162112809.png" /></center>

```java
public class GameRole {
    private int vit;
    private int def;

    //创建Memento ,即根据当前的状态得到Memento
    public Memento createMemento() {
        return new Memento(vit, def);
    }

    //从备忘录对象，恢复GameRole的状态
    public void recoverGameRoleFromMemento(Memento memento) {
        this.vit = memento.getVit();
        this.def = memento.getDef();
    }
    .......省略一些set,get方法以及没用方法
}
```

```java
public class Memento {
    //攻击力
    private int vit;
    //防御力
    private int def;
    public Memento(int vit, int def) {
        super();
        this.vit = vit;
        this.def = def;
    }
    ....省略set,get方法
}
```



#### 备忘录模式的注意事项和细节

1. 给用户提供了一种可以恢复状态的机制，可以使用户能够比较方便地回到某个历史的状态

2. 实现了信息的封装，使得用户不需要关心状态的保存细节

3. 如果类的成员变量过多，**势必会占用比较大的资源**，而且每一次保存都会消耗一定的内存, 这个需要注意

4. **适用的应用场景**：1、后悔药。 2、打游戏时的存档。 3、Windows 里的  ctri + z。  4、IE 中的后退。  4、数据库的事务管理

5. 为了节约内存，备忘录模式可以和原型模式配合使用

6. 备忘录模式可以和命令模式配合使用

<br/>



### 解释器模式

#### 四则运算问题

通过解释器模式来实现四则运算，如计算 a+b-c 的值，具体要求

1. 先输入表达式的形式，比如 a+b+c-d+e,  要求表达式的字母不能重复

2. 在分别输入 a ,b, c, d, e 的值

3. 最后求出结果：如图

<center><img src="https://img-blog.csdnimg.cn/20210203162139789.png" /></center>



#### 传统方案解决四则运算问题分析

1. 编写一个方法，接收表达式的形式，然后根据用户输入的数值进行解析，得到结果

2. 问题分析：如果加入新的运算符，比如 * / ( 等等，不利于扩展，另外让一个方法来解析会造成程序结构混乱， 不够清晰.

3. 解决方案：可以考虑使用解释器模式，  即：  表达式  -> 解释器(可以有多种) -> 结果



#### 解释器模式基本介绍

1. 在编译原理中，一个算术表达式通过词法分析器形成词法单元，而后这些词法单元再通过语法分析器构建语法分析树，最终形成一颗抽象的语法分析树。这里的词法分析器和语法分析器都可以看做是解释器

2. 解释器模式（Interpreter Pattern）：**是指给定一个语言(表达式)，定义它的文法的一种表示，并定义一个解释器， 使用该解释器来解释语言中的句子(表达式)**

3. 应用场景
   - 应用可以将一个需要解释执行的语言中的句子表示为一个抽象语法树
   - 一些重复出现的问题可以用一种简单的语言来表达
   - 一个简单语法需要解释的场景

4. 这样的例子还有，比如**编译器**、**运算表达式计算**、**正则表达式**、**机器人**等

 

#### 解释器模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203162202537.png" /></center>

对原理类图的说明-即(解释器模式的角色及职责)

1. `Context:` 是环境角色,含有解释器之外的全局信息.

2. `AbstractExpression: `抽象表达式， 声明一个抽象的解释操作,这个方法为抽象语法树中所有的节点所共享

3. `TerminalExpression: `为终结符表达式, 实现与文法中的终结符相关的解释操作

4. `NonTermialExpression:` 为非终结符表达式，为文法中的非终结符实现解释操作.

5. 说明： 输入 Context he TerminalExpression  信息通过 Client 输入即可

 

#### 解释器模式来实现四则 

1. 应用实例要求

   通过解释器模式来实现四则运算， 如计算 a+b-c 的值

2. 思路分析和图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203162226344.png" /></center>

```java
public abstract class Expression {
    // a + b - c
    // 解释公式和数值, key 就是公式(表达式) 参数[a,b,c], value就是就是具体值
    // HashMap {a=10, b=20}
    public abstract int interpreter(HashMap<String, Integer> var);
}
```

```java
//变量的解释器(终结符表达式,仅仅使用来解释变量)
public class VarExpression extends Expression {
    private String key; // key=a,key=b,key=c
    public VarExpression(String key) {
        this.key = key;
    }

    // var 就是{a=10, b=20}
    // interpreter 根据 变量名称，返回对应值
    @Override
    public int interpreter(HashMap<String, Integer> var) {
        return var.get(this.key);
    }
}
```

```java
//运算解释器，会有具体的操作解释器继承(非终结符表达式)
public class SymbolExpression extends Expression {
    protected Expression left;
    protected Expression right;

    public SymbolExpression(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }

    //因为 SymbolExpression 是让其子类来实现，因此 interpreter 是一个默认实现
    @Override
    public int interpreter(HashMap<String, Integer> var) {
        // TODO Auto-generated method stub
        return 0;
    }
}
```

```java
//加法解释器
public class AddExpression extends SymbolExpression  {
    public AddExpression(Expression left, Expression right) {
        super(left, right);
    }

    //处理相加
    //var 仍然是 {a=10,b=20}..
    //一会我们debug 源码,就ok
    public int interpreter(HashMap<String, Integer> var) {
        //super.left.interpreter(var) ： 返回 left 表达式对应的值 a = 10
        //super.right.interpreter(var): 返回right 表达式对应值 b = 20
        return super.left.interpreter(var) + super.right.interpreter(var);
    }
}
//减法解释器省略
```

```java
public class Calculator {
    // 定义表达式
    private Expression expression;

    // 构造函数传参，并解析
    public Calculator(String expStr) { // expStr = a+b
        // 安排运算先后顺序
        Stack<Expression> stack = new Stack<>();
        // 表达式拆分成字符数组 
        char[] charArray = expStr.toCharArray();// [a, +, b]

        Expression left = null;
        Expression right = null;
        //遍历我们的字符数组， 即遍历  [a, +, b]
        //针对不同的情况，做处理
        for (int i = 0; i < charArray.length; i++) {
            switch (charArray[i]) {
                case '+': //
                    left = stack.pop();// 从stack取出left => "a"
                    right = new VarExpression(String.valueOf(charArray[++i]));// 取出右表达式 "b"
                    stack.push(new AddExpression(left, right));// 然后根据得到left 和 right 构建 AddExpresson加入stack
                    break;
                case '-': // 
                    left = stack.pop();
                    right = new VarExpression(String.valueOf(charArray[++i]));
                    stack.push(new SubExpression(left, right));
                    break;
                default: 
                    //如果是一个 Var 就创建要给 VarExpression 对象，并push到 stack
                    stack.push(new VarExpression(String.valueOf(charArray[i])));
                    break;
            }
        }
        //当遍历完整个 charArray 数组后，stack 就得到最后Expression
        this.expression = stack.pop();
    }

    public int operation(HashMap<String, Integer> var) {
        //最后将表达式a+b和 var = {a=10,b=20}
        //然后传递给expression的interpreter进行解释执行
        //注意此步骤存在递归
        return this.expression.interpreter(var);
    }
}
```



#### 解释器模式在 Spring 框架应用的源码剖析

1. Spring 框架中 SpelExpressionParser 就使用到解释器模式

2. 代码分析+Debug 源码

<center><img src="https://img-blog.csdnimg.cn/20210203162253586.png" /></center>

1) 说明

<center><img src="https://img-blog.csdnimg.cn/20210203162316393.png" /></center>



#### 解释器模式的注意事项和细节

1. 当有一个语言需要解释执行，**可将该语言中的句子表示为一个抽象语法树，** 就可以考虑使用解释器模式，让程序具有良好的扩展性

2. 应用场景：**编译器**、**运算表达式计算**、**正则表达式**、**机器人**等

3. 使用解释器可能带来的问题：解释器模式会引起类膨胀、解释器模式采用递归调用方法，将会导致调试非常复杂、效率可能降低.



### 状态模式

#### APP 抽奖活动问题

请编写程序完成 APP 抽奖活动 具体要求如下:

1. 假如每参加一次这个活动要扣除用户 50 积分，中奖概率是 10%

2. 奖品数量固定，抽完就不能抽奖

3. 活动有四个状态: 可以抽奖、不能抽奖、发放奖品和奖品领完

4. 活动的四个状态转换关系图(右图)

<center><img src="https://img-blog.csdnimg.cn/20210203162344216.png" /></center>

#### 状态模式基本介绍

1. 状态模式（State Pattern）：**它主要用来解决对象在多种状态转换时，需要对外输出不同的行为的问题。** 状态和行为是一一对应的，状态之间可以相互转换。**即不同状态执行不同的固定操作。**

2. 当一个对象的内在状态改变时，允许改变其行为，这个对象看起来像是改变了其类

#### 状态模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203162404824.png" /></center>

 对原理类图的说明-即(状态模式的角色及职责)

1. `Context `类为环境角色,  用于维护 State 实例,这个实例定义当前状态

2. `State `是抽象状态角色,定义一个接口封装与 Context  的一个特点接口相关行为

3. `ConcreteState` 具体的状态角色，每个子类实现一个与 Context 的一个状态相关行为

 

#### 状态模式解决 APP 抽奖问

1. 应用实例要求

   完成 APP 抽奖活动项目，使用状态模式.

2. 思路分析和图解(类图)
   - 定义出一个接口叫状态接口，每个状态都实现它。
   - 接口有扣除积分方法、抽奖方法、发放奖品方法

<center><img src="https://img-blog.csdnimg.cn/20210203162427451.png" /></center>

```java
public abstract class State {
    // 扣除积分 - 50
    public abstract void deductMoney();

    // 是否抽中奖品
    public abstract boolean raffle();

    // 发放奖品
    public abstract  void dispensePrize();
}
```

```java
//不能抽奖状态
public class NoRaffleState extends State {
    // 初始化时传入活动引用，扣除积分后改变其状态
    RaffleActivity activity;

    public NoRaffleState(RaffleActivity activity) {
        this.activity = activity;
    }

    // 当前状态可以扣积分 , 扣除后，将状态设置成可以抽奖状态
    @Override
    public void deductMoney() {
        System.out.println("扣除50积分成功，您可以抽奖了");
        activity.setState(activity.getCanRaffleState());
    }

    // 当前状态不能抽奖
    @Override
    public boolean raffle() {
        System.out.println("扣了积分才能抽奖喔！");
        return false;
    }

    // 当前状态不能发奖品
    @Override
    public void dispensePrize() {
        System.out.println("不能发放奖品");
    }
}
```

```java
public class CanRaffleState extends State {
    RaffleActivity activity;

    public CanRaffleState(RaffleActivity activity) {
        this.activity = activity;
    }

    //已经扣除了积分，不能再扣
    @Override
    public void deductMoney() {
        System.out.println("已经扣取过了积分");
    }

    //可以抽奖, 抽完奖后，根据实际情况，改成新的状态
    @Override
    public boolean raffle() {
        System.out.println("正在抽奖，请稍等！");
        Random r = new Random();
        int num = r.nextInt(10);
        // 10%中奖机会
        if(num == 0){
            // 改变活动状态为发放奖品 context
            activity.setState(activity.getDispenseState());
            return true;
        }else{
            System.out.println("很遗憾没有抽中奖品！");
            // 改变状态为不能抽奖
            activity.setState(activity.getNoRafflleState());
            return false;
        }
    }

    // 不能发放奖品
    @Override
    public void dispensePrize() {
        System.out.println("没中奖，不能发放奖品");
    }
}
```

```java
其他状态省略
```

```java
//抽奖活动(环境)
public class RaffleActivity {
    // state 表示活动当前的状态，是变化
    State state = null;
    // 奖品数量
    int count = 0;

    // 四个属性，表示四种状态
    State noRafflleState = new NoRaffleState(this);
    State canRaffleState = new CanRaffleState(this);

    State dispenseState =   new DispenseState(this);
    State dispensOutState = new DispenseOutState(this);

    //构造器
    //1. 初始化当前的状态为 noRafflleState（即不能抽奖的状态）
    //2. 初始化奖品的数量 
    public RaffleActivity( int count) {
        this.state = getNoRafflleState();
        this.count = count;
    }

    //扣分, 调用当前状态的 deductMoney
    public void debuctMoney(){
        state.deductMoney();
    }

    //抽奖 
    public void raffle(){
        // 如果当前的状态是抽奖成功
        if(state.raffle()){
            //领取奖品
            state.dispensePrize();
        }

    }

    public State getState() {
        return state;
    }

    public void setState(State state) {
        this.state = state;
    }

    //这里请大家注意，每领取一次奖品，count--
    public int getCount() {
        int curCount = count; 
        count--;
        return curCount;
    }

    //省略set，get方法
```







#### 状态模式在实际项目-借贷平台 源码剖析(代码看代码文件夹)

1. 借贷平台的订单，有审核-发布-抢单 等等 步骤，随着操作的不同，会改变订单的状态, 项目中的这个模块实现就会使用到状态模式

2. 通常通过 if/else 判断订单的状态，从而实现不同的逻辑，伪代码如下

<center><img src="https://img-blog.csdnimg.cn/20210203162454743.png" /></center>

<center><img src="https://img-blog.csdnimg.cn/2021020316251845.png" /></center>



#### 状态模式的注意事项和细节

1. 代码有很强的可读性。状态模式将每个状态的行为封装到对应的一个类中

2. 方便维护。将容易产生问题的 if-else 语句删除了，如果把每个状态的行为都放到一个	类中，每次调用方法时都要判断当前是什么状态，不但会产出很多 if-else 语句，而且容易出错

3. 符合“开闭原则”。容易增删状态

4. 会产生很多类。每个状态都要一个对应的类，当状态过多时会产生很多类，加大维护难度

5. 应用场景：当一个事件或者对象有很多种状态，状态之间会相互转换，对不同的状态要求有不同的行为的时候， 可以考虑使用状态模式



### 策略模式

#### 编写鸭子项目

具体要求如下:

1. 有各种鸭子(比如 野鸭、北京鸭、水鸭等， 鸭子有各种行为，比如 叫、飞行等)

2. 显示鸭子的信息



#### 传统方案解决鸭子问题的分析和代码实现

传统的设计方案(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203162744294.png" /></center>

传统的方式实现的问题分析和解决方案

1. 其它鸭子，都继承了 Duck 类，所以 fly 让所有子类都会飞了，这是不正确的

2. 上面说的 1 的问题，其实是继承带来的问题：对类的局部改动，尤其超类的局部改动，会影响其他部分。会有溢出效应

3. 为了改进 1 问题，我们可以通过覆盖 fly  方法来解决 => 覆盖解决

4. 问题又来了，如果我们有一个玩具鸭子 ToyDuck, 这样就需要 ToyDuck 去覆盖 Duck 的所有实现的方法 => 解决思路 -》 策略模式 (strategy pattern)



#### 策略模式基本介绍

1. 策略模式（Strategy Pattern）中，定义算法族（策略组），分别封装起来，让他们之间可以互相替换，此模式**让算法的变化独立于使用算法的客户**

2. 这算法体现了几个设计原则，第一、把变化的代码从不变的代码中分离出来；第二、针对接口编程而不是具体类（定义了策略接口）；第三、多用组合/聚合，少用继承（客户通过组合方式使用策略）。



#### 策略模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203162824376.png" /></center>

1. 策略（`Strategy`）类：定义了一个公共接口，各种不同的算法以不同的方式实现这个接口，环境角色使用这个接口调用不同的算法，一般使用接口或抽象类实现。
2. 具体策略（`Concrete Strategy`）类：实现了抽象策略定义的接口，提供具体的算法实现。
3. 环境（`Context`）类：持有一个策略类的引用，最终给客户端调用。

说明：从上图可以看到，客户 context 有成员变量 strategy 或者其他的策略接口，至于需要使用到哪个策略，我们可以在构造器中指定



####  策略模式解决鸭子问题

1. 应用实例要求

   编写程序完成前面的鸭子项目，要求使用策略模式

2. 思路分析(类图)

   策略模式：分别封装行为接口，实现算法族，超类里放行为接口对象，在子类里具体设定行为对象。原则就是： 分离变化部分，封装接口，基于接口编程各种功能。此模式让行为的变化独立于算法的使用者

<center><img src="https://img-blog.csdnimg.cn/20210203162849815.png" /></center>

```java
public interface FlyBehavior {
   void fly(); // 子类具体实现
}
```

```java
public class NoFlyBehavior implements FlyBehavior{
   @Override
   public void fly() {
      // TODO Auto-generated method stub
      System.out.println(" 不会飞翔  ");
   }
}
```

```java
public class GoodFlyBehavior implements FlyBehavior {
    @Override
    public void fly() {
        // TODO Auto-generated method stub
        System.out.println(" 飞翔技术高超 ~~~");
    }
}
```

```java
public abstract class Duck {
    //属性, 策略接口
    FlyBehavior flyBehavior;
    //其它属性<->策略接口
    QuackBehavior quackBehavior;

    public abstract void display();//显示鸭子信息

    public void quack() {
        System.out.println("鸭子嘎嘎叫~~");
    }

    public void swim() {
        System.out.println("鸭子会游泳~~");
    }

    public void fly() {
        //改进
        if(flyBehavior != null) {
            flyBehavior.fly();
        }
    }

    //动态的选择行为(算法)
    public void setFlyBehavior(FlyBehavior flyBehavior) {
        this.flyBehavior = flyBehavior;
    }

    public void setQuackBehavior(QuackBehavior quackBehavior) {
        this.quackBehavior = quackBehavior;
    }
}
```







#### 策略模式在 JDK-Arrays 应用的源码分析

1. JDK 的 Arrays 的 Comparator 就使用了策略模式

2. 代码分析+Debug 源码+模式角色分析

<center><img src="https://img-blog.csdnimg.cn/20210203162927310.png" /></center>



#### 策略模式的注意事项和细节

1. 策略模式的关键是：**分析项目中变化部分与不变部分**

2. 策略模式的核心思想是：**多用组合/聚合 少用继承；用行为类组合，而不是行为的继承。** 更有弹性

3. 体现了“**对修改关闭，对扩展开放**”原则，客户端增加行为不用修改原有代码，只要添加一种策略（或者行为） 即可，避免了使用多重转移语句（if..else if..else）

4. 提供了可以替换继承关系的办法： 策略模式将算法封装在独立的 Strategy 类中使得你可以独立于其 Context 改变它，使它易于切换、易于理解、易于扩展

5. 需要注意的是：每添加一个策略就要增加一个类，**当策略过多是会导致类数目庞大**

6. 注意思考桥接模式和访问者模式



### 职责链模式

责任链（Chain of Responsibility）模式的定义：为了避免请求发送者与多个请求处理者耦合在一起，将所有请求的处理者通过前一对象记住其下一个对象的引用而连成一条链；当有请求发生时，可将请求沿着这条链传递，直到有对象处理它为止。

#### 学校 OA 系统的采购审批项目：需求是

采购员采购教学器材

1. 如果金额 小于等于 5000,  由教学主任审批 （0<=x<=5000）

2. 如果金额 小于等于 10000,  由院长审批 (5000<x<=10000)

3. 如果金额 小于等于 30000,  由副校长审批 (10000<x<=30000)

4. 如果金额 超过 30000 以上，有校长审批 ( 30000<x)

请设计程序完成采购审批项目

#### 传统方案解决 OA 系统审批，传统的设计方案(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203162953928.png" /></center>

#### 传统方案解决 OA 系统审批问题分析

1. 传统方式是：接收到一个采购请求后，根据采购金额来调用对应的 Approver (审批人)完成审批。

2. 传统方式的问题分析 :  客户端这里会使用到 分支判断(比如  switch)  来对不同的采购请求处理， 这样就存在如下问题 (1) 如果各个级别的人员审批金额发生变化，在客户端的也需要变化 (2) 客户端必须明确的知道  有多少个审批级别和访问

3. 这样 对一个采购请求进行处理 和 Approver (审批人) 就存在强耦合关系，不利于代码的扩展和维护

4. 解决方案 =》 职责链模式

 

#### 职责链模式基本介绍

基本介绍

1. 职责链模式（Chain of Responsibility Pattern）, 又叫 责任链模式，为请求创建了一个接收者对象的链(简单示意图)。这种模式对请求的发送者和接收者进行解耦。

2. 职责链模式通常每个接收者都包含对另一个接收者的引用。如果一个对象不能处理该请求，那么它会把相同的请求传给下一个接收者，依此类推。

3. 这种类型的设计模式属于行为型模式

 

#### 职责链模式的原理类图

<center><img src="https://img-blog.csdnimg.cn/20210203163017162.png" /></center>

 对原理类图的说明-即(职责链模式的角色及职责)

1. `Handler `:  抽象的处理者,  定义了一个处理请求的接口,  同时含义另外 Handler

2. `ConcreteHandlerA` , B  是具体的处理者, 处理它自己负责的请求， 可以访问它的后继者(即下一个处理者),  如果可以处理当前请求，则处理，否则就将该请求交个 后继者去处理，从而形成一个职责链

3. `Request` ， 含义很多属性，表示一个请求



#### 职责链模式解决 OA 系统采购审批

1. 应用实例要求

   编写程序完成学校 OA 系统的采购审批项目：需求采购员采购教学器材

   如果金额 小于等于 5000, 由教学主任审批如果金额 小于等于 10000, 由院长审批

   如果金额 小于等于 30000, 由副校长审批如果金额 超过 30000 以上，有校长审批

2. 思路分析和图解(类图)

<center><img src="https://img-blog.csdnimg.cn/20210203163041613.png" /></center>

```java
//请求类
public class PurchaseRequest {
   private int type = 0; //请求类型
   private float price = 0.0f; //请求金额
   private int id = 0;
   //构造器
   public PurchaseRequest(int type, float price, int id) {
      this.type = type;
      this.price = price;
      this.id = id;
   }
   public int getType() {
      return type;
   }
   public float getPrice() {
      return price;
   }
   public int getId() {
      return id;
   }
}
```

```java
public abstract class Approver {
   Approver approver;  //下一个处理者
   String name; // 名字
   
   public Approver(String name) {
      // TODO Auto-generated constructor stub
      this.name = name;
   }

   //下一个处理者
   public void setApprover(Approver approver) {
      this.approver = approver;
   }
   //处理审批请求的方法，得到一个请求, 处理是子类完成，因此该方法做成抽象
   public abstract void processRequest(PurchaseRequest purchaseRequest);
   
}
```

```java
public class CollegeApprover extends Approver {

    public CollegeApprover(String name) {
        // TODO Auto-generated constructor stub
        super(name);
    }

    @Override
    public void processRequest(PurchaseRequest purchaseRequest) {
        // TODO Auto-generated method stub
        if(purchaseRequest.getPrice() < 5000 && purchaseRequest.getPrice() <= 10000) {
            System.out.println(" 请求编号 id= " + purchaseRequest.getId() + " 被 " + this.name + " 处理");
        }else {
            approver.processRequest(purchaseRequest);
        }
    }
}
public class DepartmentApprover extends Approver {}
public class SchoolMasterApprover extends Approver {}
public class ViceSchoolMasterApprover extends Approver {}
```



#### 职责链模式在 SpringMVC 框架应用的源码分析

1. SpringMVC-HandlerExecutionChain 类就使用到职责链模式

2. SpringMVC 请求流程简图

3. 代码分析+Debug 源码+说明

<center><img src="https://img-blog.csdnimg.cn/20210203163109790.png" /></center>

对源码总结：

- springmvc 请求的流程图中，执行了 拦截器相关方法 interceptor.preHandler 等等

- 在处理 SpringMvc 请求时，使用到职责链模式还使用到适配器模式

- HandlerExecutionChain 主要负责的是请求拦截器的执行和请求处理,但是他本身不处理请求，只是将请求分配给链上注册处理器执行，这是职责链实现方式,减少职责链本身与处理逻辑之间的耦合,规范了处理流程

- HandlerExecutionChain 维护了 HandlerInterceptor 的集合， 可以向其中注册相应的拦截器.



#### 职责链模式的注意事项和细节

1. **将请求和处理分开**，实现解耦，提高系统的灵活性

2. 简化了对象，使对象不需要知道链的结构

3. **性能会受到影响**，特别是在链比较长的时候，因此需控制链中最大节点数量，一般通过在 Handler 中设置一个最大节点数量，在 setNext()方法中判断是否已经超过阀值，超过则不允许该链建立，避免出现超长链无意识地破坏系统性能

4. **调试不方便**。采用了类似递归的方式，调试时逻辑可能比较复杂

5. 最佳应用场景：有多个对象可以处理同一个请求时，比如：**多级请求、请假/加薪等审批流程、Java Web 中 Tomcat对 Encoding 的处理、拦截器**

6. 可以适当用循环链,防止在某一个环节进行处理
