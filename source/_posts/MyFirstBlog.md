---
title: MyFirstBlog
date: 2020-01-19 14:18:20
tags:
---

# Java基础知识面试复习

### 1. 面向对象和面向过程的区别

- **面向过程性能高，因为类调用时需要实例化，开销比较大，比较消耗资源**
- **面向过程没有面向对象易维护、易复用、易扩展(封装、继承、多态)**

<!--more-->

### 2. JVM

- Java虚拟机（JVM）是运行 Java 字节码的虚拟机。**JVM有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果**。字节码和不同系统的 JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在。

### 3. 构造器Constructor 是否可被 override?

- 继承的时候我们就知道父类的私有属性和构造方法并不能被继承，所以 Constructor 也就**不能被 override（重写）**,但是**可以 overload（重载）**,所以你可以看到一个类中有多个构造函数的情况。

### 4. Java面向对象三大特性：封装、继承、多态

- 封装：封装把一**个对象的属性私有化**，同时**提供一些可以被外界访问的属性的方法**，如果属性不想被外界访问，我们大可不必提供方法给外界访问。但是如果一个类没有提供给外界访问的方法，那么这个类也没有什么意义了。

### 5. String StringBuffer 和 StringBuilder 的区别是什么? String 为什么是不可变的?

- String类中：private **final** char value[]  --->不可变
- StringBuilder 与 StringBuffer 的构造方法都是**调用父类构造方法也就是 AbstractStringBuilder 实现**的
- StringBuffer 对方法**加了同步锁或者对调用的方法加了同步锁(synchronized)**，所以是线程安全的。StringBuilder 并没有对方法进行加同步锁，所以是非线程安全的

### 6. 接口和抽象类区别

- 接口的方法**默认是 public**，所有方法在接口中不能有实现(Java 8 开始接口方法可以有默认实现），**而抽象类可以有非抽象的方法。**
- 接口中**除了static、final变量，不能有其他变量**，而抽象类中则不一定。
- 一个类可以实现多个接口，**但只能实现一个抽象类**。接口自己本身可以通过extends关键字扩展多个接口。
- 在JDK8中，接口也可以定义静态方法，可以直接用接口名调用。实现类和实现是不可以调用的。如果同时实现两个接口，接口中定义了一样的默认方法，则必须重写，不然会报错。

### 7. 对象实体和对象引用有何区别？

- new创建对象实例（**对象实例在堆内存中**），**对象引用指向对象实例**（对象引用存放在栈内存中）。一个对象引用可以指向0个或1个对象（一根绳子可以不系气球，也可以系一个气球）;**一个对象可以有n个引用指向它**（可以用n条绳子系住一个气球）。

### 8. 实例方法和静态方法有何不同？

- 浅层次：在外部调用**静态方法时，可以使用"类名.方法名"的方式**，**也可以使用"对象名.方法名"的方式**。而实例方法只有后面这种方式。也就是说，**调用静态方法可以无需创建对象。（静态方法的调用不依赖于对象）**
- JVM深层次：类的静态方法，静态变量是在**类装载的时候装载的**，这时候还没有产生对象**。静态变量 存放在 Java 内存区域的方法区**
- static关键字使用场景
  1. **修饰成员变量和成员方法:** 被 static 修饰的成员属于类，不属于单个这个类的某个对象，被类中所有对象共享，可以并且建议通过类名调用。被static 声明的成员变量属于静态成员变量，静态变量 存放在 Java 内存区域的方法区。调用格式：`类名.静态变量名` `类名.静态方法名()`
  2. **静态代码块:** 静态代码块定义在类中方法外, **静态代码块在非静态代码块之前执行(静态代码块—>非静态代码块—>构造方法)。 该类不管创建多少对象，静态代码块只执行一次.**
  3. **静态内部类（static修饰类的话只能修饰内部类）：** 静态内部类与非静态内部类之间存在一个最大的区别: 非静态内部类在编译完成之后会隐含地保存着一个引用，该引用是指向创建它的外围类，但是静态内部类却没有。没有这个引用就意味着：1. 它的创建是不需要依赖外围类的创建。2. 它不能使用任何外围类的非static成员变量和方法。
  4. **静态导包(用来导入类中的静态资源，1.5之后的新特性):** 格式为：`import static` 这两个关键字连用可以指定导入某个类中的指定静态资源，并且不需要使用类名调用类中静态成员，可以直接使用类中静态成员变量和成员方法。

### 9. 线程、程序、进程

- 进程

  ```
  - 定义：
  	1、一个正在执行的程序
  	2、系统运行程序的基本单位
  	3、一个进程可由进程控制块(PCB包含：标识符、状态、优先级、程序计数器、内存指针、上下文数据、IO信息等)的数据结构来控制
  	
  ```

  进程状态

  ![image-20191217155307260](https://tva1.sinaimg.cn/large/006tNbRwly1g9zrtw49tuj30s40bm0y5.jpg)

  - 新建态：线程被创建，PCB被创建出来但还未加载到内存

  - 就绪态：进程已经加载到内存，已经做好了准备，等待CPU进行调度

  - 运行态：得到CPU的调度，进程正在执行

  - 阻塞态：进程因为某些事件需要停止执行(IO操作等)

  - 退出态：操作系统从可执行进程组中释放该进程，要么自己停止，要么因为某种原因被取消运行

    Java中

    <img src="https://tva1.sinaimg.cn/large/006tNbRwly1g9zscph8rfj31ba0u0dzc.jpg" alt="image-20191217161118329" style="zoom:80%;" />

- 线程:一个进程在其执行的过程中可以产生多个线程。与进程**不同的是同类的多个线程共享同一块内存空间和一组系统资源**系统在产生一个线程，或是在**各个线程之间作切换工作时，负担要比进程小得多**，也正因为如此，线程也被称为轻量级进程

  操作系统隐藏 Java虚拟机（JVM）中的 READY 和 RUNNING 状态，它只能看到 RUNNABLE 状态



### 10. final关键字

- 可作用在变量、方法、类

- final作用在基本数据类型上：数值一旦初始化便不能随意更改；final作用在引用型变量：初始化之后不能再指向其他的对象

- final作用在类上-->该类不能被继承，所有的成员方法默认为final

- final作用在方法上：

  - 把方法锁定，防止任何继承类修改它的含义

- 类中的private修饰的方法默认添加有final关键字

  

### 11. Java中异常

- 层次图

  ![image-20191217165252832](https://tva1.sinaimg.cn/large/006tNbRwly1g9ztjy5yx9j31a20py7nz.jpg)

- **Error（错误）:是程序无法处理的错误**，表示运行应用程序中较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时 JVM（Java 虚拟机）出现的问题。

- **Exception（异常）:是程序本身可以处理的异常**。Exception 类有一个重要的子类 **RuntimeException**。RuntimeException 异常由Java虚拟机抛出。**NullPointerException**（要访问的变量没有引用任何对象时，抛出该异常）、**ArithmeticException**（算术运算异常，一个整数除以0时，抛出该异常）和 **ArrayIndexOutOfBoundsException** （下标越界异常）。

- **异常和错误的区别：异常能被程序本身处理，错误是无法处理。**

#### try/catch/fianlly

- **try 块：** 用于捕获异常。其后可接零个或多个catch块，如果没有catch块，则必须跟一个finally块。
- **catch 块：** 用于处理try捕获到的异常。
- **finally 块：** 无论是否捕获或处理异常，finally块里的语句都会被执行。**当在try块或catch块中遇到return 语句时，finally语句块将在方法返回之前被执行。**
- finally语句块不会被执行的情况：
  1. 在finally语句块第一行发生了异常。 因为在其他行，finally块还是会得到执行
  2. 在前面的代码中用了System.exit(int)已退出程序。 exit是带参函数 ；若该语句在异常语句之后，finally会执行
  3. 程序所在的线程死亡。
  4. 关闭CPU。

### 12.深拷贝/浅拷贝

1. **浅拷贝**：对基本数据类型进行值传递，引用类型的属性复制，复制栈中的变量 和 变量指向堆内存中的对象的指针，不复制堆内存中的对象。

   <img src="https://tva1.sinaimg.cn/large/006tNbRwly1g9ztvk9ybgj30u00uyack.jpg" alt="image-20191217170403217" style="zoom:50%;" />

2. **深拷贝**：对基本数据类型进行值传递，引用类型的属性复制，复制栈中的变量 和 变量指向堆内存中的对象的指针和堆内存中的对象。（在堆中创建了新的对象）

   <img src="https://tva1.sinaimg.cn/large/006tNbRwly1g9ztxcys4pj30u00v5gnt.jpg" alt="image-20191217170540653" style="zoom:50%;" />

### 13. sleep()和wait()方法的区别和共同点

- 最主要的区别在于：**sleep 方法没有释放锁，而 wait 方法释放了锁** 。

- Wait 通常被用于线程间交互/通信，sleep 通常被用于暂停执行。

- wait() 方法被调用后，线程不会自动苏醒，需要别的线程调用同一个对象上的 notify() 或者 notifyAll() 方法。sleep() 方法执行完成后，线程会自动苏醒。或者可以使用 wait(long timeout)超时后线程会自动苏醒。

- 共同点：**都可以暂停线程的执行**

  

### 14. 为什么我们调用 start() 方法时会执行 run() 方法，为什么我们不能直接调用 run() 方法？

- new 一个 Thread，线程进入了新建状态;**调用 start() 方法，会启动一个线程并使线程进入了就绪状态**，当分配到时间片后就可以开始运行了。 **start() 会执行线程的相应准备工作，然后自动执行 run() 方法**的内容
- 直接执行 run() 方法，会把 run 方法**当成一个 main 线程下的普通方法去执行，并不会在某个线程中执行它**

### 15. 反射

1. 对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。--->**反射就是把java类中的各种成分映射成一个个的Java对象**

   ![image-20191217172633390](https://tva1.sinaimg.cn/large/006tNbRwly1g9zuj06enpj31gm0lkn56.jpg)

2. 反射优势：运行期类型的判断，动态加载类，提高代码灵活度。

3. 应用：

   - JDBC 连接数据库时使用 `Class.forName()`通过反射加载数据库的驱动程序
   - Spring XML配置方法进行装在Bean

### 16. Java线程内存模型

#### 多线程运行下内存模型

<img src="https://tva1.sinaimg.cn/large/006tNbRwly1g9zv84vidnj30wd0u0dqz.jpg" alt="image-20191217175041005" style="zoom:50%;" />

- 线程私有

  1. 程序计数器--->**为了线程切换后能恢复到正确的执行位置，每条线程都需要有一个独立的程序计数器，各线程之间计数器互不影响，独立存储，我们称这类内存区域为“线程私有”的内存。**程序计数器是唯一一个不会出现OutOfMemoryError的内存区域，它的生命周期随着线程的创建而创建，随着线程的结束而死亡。
  2. 虚拟机栈--->**其中栈就是现在说的虚拟机栈，或者说是虚拟机栈中局部变量表部分。** （实际上，Java虚拟机栈是由一个个栈帧组成，而每个栈帧中都拥有：局部变量表、操作数栈、动态链接、方法出口信息。）
  3. 本地方法栈--->和虚拟机栈所发挥的作用非常相似，区别是： **虚拟机栈为虚拟机执行 Java 方法 （也就是字节码）服务，而本地方法栈则为虚拟机使用到的 Native 方法服务**

- 线程共有：

  1. 堆：Java 堆是所有线程共享的一块内存区域，在虚拟机启动时创建。**此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例以及数组都在这里分配内存。**

     - 新生代(1/3)
       - Eden(8/10)
       - From Survivor(1/10)
       - To Survivor(1/10)
     - 老年代(2/3)
     - 永久代--->JDK1.8**移除整个永久代，取而代之的是一个叫元空间（Metaspace）的区域（永久代使用的是JVM的堆内存空间，而元空间使用的是物理内存，直接受到本机的物理内存限制）**

  2. 方法区

     **方法区与 Java 堆一样，是各个线程共享的内存区域，它用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。**

     - 运行时常量池：**运行时常量池是方法区的一部分**。Class 文件中除了有类的版本、字段、方法、接口等描述信息外，还有常量池信息（用于存放编译期生成的各种字面量和符号引用）

  3. 直接内存

#### 常见垃圾回收算法

[https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/jvm/JVM%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6.md](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/jvm/JVM垃圾回收.md)



- **如何判断对象已经死亡**

  - 引用计数法---->**不能解决循环引用问题**

    ​		给对象中添加一个引用计数器，每当有一个地方引用它，计数器就加 1；当引用失效，计数器就减 1；任何时候计数器为 0 的对象就是不可能再被使用的。**实现简单，效率高**

  - GC Roots(可达性分析算法)

    ​	<img src="https://tva1.sinaimg.cn/large/006tNbRwly1ga6jh9u01jj30s60jmafy.jpg" alt="image-20191223122314902" style="zoom:50%;" />

    从这些节点开始向下搜索，节点所走过的路径称为引用链，当一个对象到 GC Roots 没有任何引用链相连的话，**则证明此对象是不可用的**。

    可作为GC Roots的：**线程栈变量、静态变量、常量池、JNI指针**

    

- 常见垃圾回收算法

  

  - **标记清除(Mark and sweep)**

    <img src="https://tva1.sinaimg.cn/large/006tNbRwly1ga6jopo2u0j30vy0oyae1.jpg" alt="image-20191223123026324" style="zoom: 50%;" />

    首先标记出所有需要回收的对象，**在标记完成后统一回收所有被标记的对象**---->问题：位置不连续产生碎片

  

  

  - **拷贝算法**

    <img src="https://tva1.sinaimg.cn/large/006tNbRwly1ga6jq7761fj30vs0p0q7r.jpg" alt="image-20191223123151261" style="zoom:50%;" />

    它可以将**内存分为大小相同的两块，每次使用其中的一块**。当这一块的内存使用完后，就将还存活的对象复制到另一块去，**然后再把使用的空间一次清理掉**。这样就使每次的内存回收都是对内存区间的一半进行回收。**没有碎片，效率高，连续**------>**问题：浪费内存**

  

  

  - **标记-压缩(标记整理)**

    <img src="https://tva1.sinaimg.cn/large/006tNbRwly1ga6jtlfwr9j313e0lygqa.jpg" alt="image-20191223123507134" style="zoom:50%;" />

    标记过程仍然与“标记-清除”算法一样，**但后续步骤不是直接对可回收对象回收，而是让所有存活的对象向一端移动**，然后直接清理掉端边界以外的内存。**没有碎片**--->**问题：浪费内存**

  

  

  - **分代收集**

    这种算法没有什么新的思想，**只是根据对象存活周期的不同将内存分为几块**。一般将 java 堆分为**新生代和老年代**，这样我们就可以根据各个年代的特点选择合适的垃圾收集算法。

    **比如在新生代中，每次收集都会有大量对象死去，所以可以选择复制算法，只需要付出少量对象的复制成本就可以完成每次垃圾收集。而老年代的对象存活几率是比较高的，而且没有额外的空间对它进行分配担保，所以我们必须选择“标记-清除”或“标记-整理”算法进行垃圾收集。**

### 17. HotSpot虚拟机对象揭秘



#### 	对象创建过程

- 类加载检查

  ```
  虚拟机遇到一条 new 指令时，首先将去检查这个指令的参数是否能在常量池中定位到这个类的符号引用，并且检查这个符号引用代表的类是否已被加载过、解析和初始化过。如果没有，那必须先执行相应的类加载过程。
  ```

- 申请内存

  - 指针碰撞

    用于堆内存比较规整

  - 空闲列表

    用于堆内存比较零散

    ![image-20191217195035011](https://tva1.sinaimg.cn/large/006tNbRwly1g9zyoumlhkj31nk0eiq6w.jpg)

- 成员变量赋予默认值

- 调用初始化方法

  - 成员变量按顺序调用

  - 初始化成员变量

  - 构造方法调用

    

#### 对象内存布局

和虚拟机有关

以HotSpot为例

- 对象头markWord

  - **存储对象自身的自身运行时数据(哈希码、GC分代年龄、锁状态标志等等)**
  - 类型指针---->指向它的类元数据的指针，虚拟机通过这个指针来确定这个对象是那个类的实例。

- 实例数据(对象的成员变量)

- 补齐(因为Hotspot虚拟机的自动内存管理系统要求对象**起始地址必须是8字节的整数倍**)

  

#### 对象的访问定位

1. 使用句柄：Java堆中将会划分出一块内存来作为句柄池

   ![image-20191218134522761](https://tva1.sinaimg.cn/large/006tNbRwly1ga0tr5oz9tj314i0jo46h.jpg)

2. 直接指针： Java 堆对象的布局中就必须考虑如何放置访问类型数据的相关信息

   ![image-20191218134627510](https://tva1.sinaimg.cn/large/006tNbRwly1ga0tsb9nsdj315i0k8jyq.jpg)

**使用句柄来访问的最大好处是 reference 中存储的是稳定的句柄地址，在对象被移动时只会改变句柄中的实例数据指针，而 reference 本身不需要修改。使用直接指针访问方式最大的好处就是速度快，它节省了一次指针定位的时间开销。**



#### String类和常量池

1. String对象的两种创建方式

   ``` Java
        String str1 = "abcd";
        String str2 = new String("abcd");
        System.out.println(str1==str2);//false
   ```

   第一种方式是在常量池中拿对象，第二种方式是直接在堆内存空间创建一个新的对象。（只要使用了new方法，则一定会在堆内存区域创建新的对象）

   ![image-20191218135354038](https://tva1.sinaimg.cn/large/006tNbRwly1ga0u00la52j312q0hyq4p.jpg)

2. String类型的常量池

   - 直接使用双引号声明出来的 String 对象会直接存储在常量池中。

   - 如果不是用双引号声明的 String 对象，可以使用 String 提供的 intern 方法。String.intern() 是一个 Native 方法，它的作用是：**如果运行时常量池中已经包含一个等于此 String 对象内容的字符串，则返回常量池中该字符串的引用**；如果没有，**则在常量池中创建与此 String 内容相同的字符串，并返回常量池中创建的字符串的引用。**

     ``` java
     	String s1 = new String("计算机");
     	String s2 = s1.intern();
     	String s3 = "计算机";
     	System.out.println(s2);//计算机
     	System.out.println(s1 == s2);//false，因为一个是堆内存中的String对象一个是常量池中的String对象，
     	System.out.println(s3 == s2);//true，因为两个都是常量池中的String对象
     ```

     

   - 字符串拼接

     ``` java
     			String str1 = "str";
     		  String str2 = "ing";
     		  
     		  String str3 = "str" + "ing";//常量池中的对象
     		  String str4 = str1 + str2; //在堆上创建的新的对象	  
     		  String str5 = "string";//常量池中的对象
     		  System.out.println(str3 == str4);//false
     		  System.out.println(str3 == str5);//true
     		  System.out.println(str4 == str5);//false
     ```

     <img src="https://tva1.sinaimg.cn/large/006tNbRwly1ga0u4luznqj30u00v9djq.jpg" alt="image-20191218135818700" style="zoom:50%;" />

3. String str = new String("abc"); 这句话创建了几个对象？

   **2个**  先有**字符串"abc"放入常量池**，然后 **new 了一份字符串"abc"放入Java堆**(字符串常量"abc"在编译期就已经确定放入常量池，而 Java 堆上的"abc"是在运行期初始化阶段才确定)，然后 Java 栈的 str1 指向Java堆上的"abc"。

   验证：

   ``` java
   		String s1 = new String("abc");// 堆内存的地址值
   		String s2 = "abc";
   		System.out.println(s1 == s2);// 输出false,因为一个是堆内存，一个是常量池的内存，故两者是不同的。
   		System.out.println(s1.equals(s2));// 输出true
   ```

   

#### 8种基本类型的包装类和常量池

- **Java 基本类型的包装类的大部分都实现了常量池技术，即Byte,Short,Integer,Long,Character,Boolean；这5种包装类默认创建了数值[-128，127]的相应类型的缓存数据，但是超出此范围仍然会去创建新的对象。**

- **两种浮点数类型的包装类 Float,Double 并没有实现常量池技术。**

验证：

``` java
		Integer i1 = 33;
		Integer i2 = 33;
		System.out.println(i1 == i2);// 输出true
		Integer i11 = 333;
		Integer i22 = 333;
		System.out.println(i11 == i22);// 输出false
		Double i3 = 1.2;
		Double i4 = 1.2;
		System.out.println(i3 == i4);// 输出false
```

- 深入理解包装类的装箱拆箱

``` java
	Integer i1 = 40;
  Integer i2 = 40;
  Integer i3 = 0;
  Integer i4 = new Integer(40);
  Integer i5 = new Integer(40);
  Integer i6 = new Integer(0);
  
  System.out.println("i1=i2   " + (i1 == i2));
  System.out.println("i1=i2+i3   " + (i1 == i2 + i3));
  System.out.println("i1=i4   " + (i1 == i4));
  System.out.println("i4=i5   " + (i4 == i5));
  System.out.println("i4=i5+i6   " + (i4 == i5 + i6));   
  System.out.println("40=i5+i6   " + (40 == i5 + i6));    
```

输出结果：

```
i1=i2   true
i1=i2+i3   true
i1=i4   false
i4=i5   false
i4=i5+i6   true
40=i5+i6   true
```

1. Integer i1=40；Java 在编译的时候会直接将代码封装成Integer i1=Integer.valueOf(40);，从而**使用常量池中的对象**。

2. Integer i4 = new Integer(40);这种情况下**会创建新的对象**。

3. 语句i4 == i5 + i6，**因为+这个操作符不适用于Integer对象，首先i5和i6进行自动拆箱操作，进行数值相加**，即i4 == 40。**然后Integer对象无法与数值进行直接比较，所以i4自动拆箱转为int值40**，最终这条语句转为40 == 40进行数值比较。

    

### 18. 什么是上下文切换？

​		多线程编程中一般**线程的个数都大于 CPU 核心的个数**，而**一个 CPU 核心在任意时刻只能被一个线程使用**，为了让这些线程都能得到有效执行，CPU 采取的策略是为**每个线程分配时间片并轮转的形式**。当一个线程的时间片用完的时候就会**重新处于就绪状态让给其他线程使用**，这个过程就属于一次上下文切换。

​		总结说：当前任务在执行完 CPU 时间片切换到另一个任务之前会先保存自己的状态，以便下次再切换回这个任务时，可以再加载这个任务的状态。**任务从保存到再加载的过程就是一次上下文切换**。



### 19. 线程死锁？避免死锁？

​		多个线程同时被阻塞，它们中的一个或者全部都在等待某个资源被释放。由于线程被无限期地阻塞，因此程序不可能正常终止。



#### 产生死锁的必要条件

- **互斥条件**：该资源任意一个时刻只由一个线程占用。
- **请求与保持条件**：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
- **不剥夺条件**:线程已获得的资源在末使用完之前不能被其他线程强行剥夺，只有自己使用完毕后才释放资源。
- **循环等待条件**:若干进程之间形成一种头尾相接的循环等待资源关系。



#### 如何避免死锁

- 破坏互斥条件：**没有办法破坏**，因为我们用锁本来就是想让他们互斥的（临界资源需要互斥访问）

- 破坏请求和保持条件：一次性申请所有的资源（银行家算法）

- 破坏不剥夺条件：占用部分资源的线程进一步申请其他资源时，如果申请不到，可以主动释放它占有的资源。

- 破坏循环等待条件：靠按序申请资源来预防。按某一顺序申请资源，释放资源则反序释放。破坏循环等待条件。

  

#### 写一产生死锁的程序



``` java
public class DeadLockDemo {
    private static Object resource1 = new Object();//资源 1
    private static Object resource2 = new Object();//资源 2

    public static void main(String[] args) {
        new Thread(() -> {
            synchronized (resource1) {
                System.out.println(Thread.currentThread() + "get resource1");
                try {
                    Thread.sleep(1000);  //
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread() + "waiting get resource2");
                synchronized (resource2) {
                    System.out.println(Thread.currentThread() + "get resource2");
                }
            }
        }, "线程 1").start();

        new Thread(() -> {
            synchronized (resource2) {
                System.out.println(Thread.currentThread() + "get resource2");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread() + "waiting get resource1");
                synchronized (resource1) {
                    System.out.println(Thread.currentThread() + "get resource1");
                }
            }
        }, "线程 2").start();
    }
}
```

输出：

```
Thread[线程 1,5,main]get resource1
Thread[线程 2,5,main]get resource2
Thread[线程 1,5,main]waiting get resource2
Thread[线程 2,5,main]waiting get resource1
```

线程 A 通过 `synchronized (resource1) `获得 resource1 的监视器锁，然后通过`Thread.sleep(1000);`让线程 A 休眠 1s 为的是让**线程 B 得到执行然后获取到 resource2 的监视器锁**。线程 A 和线程 B 休眠结束了都开始企图请求获取对方的资源，然后这**两个线程就会陷入互相等待的状态**，这也就产生了死锁。



- 如何破坏这段代码的死锁？---->靠**按序申请资源来预防。按某一顺序申请资源**，释放资源则反序释放。破坏循环等待条件。

  ``` java
  new Thread(() -> {
              synchronized (resource1) {
                  System.out.println(Thread.currentThread() + "get resource1");
                  try {
                      Thread.sleep(1000);
                  } catch (InterruptedException e) {
                      e.printStackTrace();
                  }
                  System.out.println(Thread.currentThread() + "waiting get resource2");
                  synchronized (resource2) {
                      System.out.println(Thread.currentThread() + "get resource2");
                  }
              }
          }, "线程 2").start();
  ```

  **线程 1 首先获得到 resource1 的监视器锁,这时候线程 2 就获取不到了**。然后线程 1 再去获取 resource2 的监视器锁，可以获取到。**然后线程 1 释放了对 resource1、resource2 的监视器锁的占用，线程 2 获取到就可以执行了**。这样就破坏了破坏循环等待条件，因此避免了死锁。

  

### 20. 乐观锁和悲观锁



#### 何为乐观锁、悲观锁

- 乐观锁

  总是**假设最好**的情况，每次去拿数据的时候都**认为别人不会修改**，所以**不会上锁**，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，**乐观锁适用于多读的应用类型，这样可以提高吞吐量**

- 悲观锁

  总是**假设最坏**的情况，每次去拿数据的时候都**认为别人会修改**，所以每次在拿数据的时候都**会上锁**，这样别人想拿这个数据就会阻塞直到它拿到锁（**共享资源每次只给一个线程使用，其它线程阻塞，用完后再把资源转让给其它线程**）。**一般多写的场景下用悲观锁就比较合适。**---->synchronized ReentrantLock就是悲观锁的思想，传统的关系型数据库里边就用到了很多这种锁机制，比如**行锁，表锁等，读锁，写锁**等

  

#### 乐观锁实现方式

- 版本号控制

  ​		一般是在数据表中**加上一个数据版本号version字段**，**表示数据被修改的次数**，当数据被修改时，version值会加一。当线程**A要更新数据值时，在读取数据的同时也会读取version值**，在**提交更新时，若刚才读取到的version值为当前数据库中的version值相等时才更新**，否则重试更新操作，直到更新成功。

![image-20191219124054387](https://tva1.sinaimg.cn/large/006tNbRwly1ga1xidusg9j31h00hmgu1.jpg)

- CAS算法

  即**compare and swap（比较与交换）**，是一种有名的**无锁算法**。无锁编程，即不使用锁的情况下实现多线程之间的变量同步，也就是在没有线程被阻塞的情况下实现变量的同步，所以也叫非阻塞同步（Non-blocking Synchronization）。**CAS算法**涉及到三个操作数

  ​		需要读写的内存值V

  ​		进行比较的值A

  ​		拟写入的新值B

  当且仅当 V 的值等于 A时，CAS通过原子方式用新值B来更新V的值，否则不会执行任何操作（比较和替换是一个原子操作）。一般情况下是一个**自旋操作**，即**不断的重试**。



#### 乐观锁缺点

- **ABA问题**：如果一个变量V初次读取的时候是A值，并且在准备赋值的时候检查到它仍然是A值，那我们就能说明它的值没有被其他线程修改过了吗？很明显是不能的，因为在这段时间它的值可能被改为其他值，然后又改回A，那CAS操作就会误认为它从来没有被修改过。这个问题被称为CAS操作的 **"ABA"问题。**

  解决ABA问题办法---->引入版本号控制

- 循环时间长CPU开销大：**自旋CAS（也就是不成功就一直循环执行直到成功）如果长时间不成功，会给CPU带来非常大的执行开销。** 

- **只能保证一个共享变量的原子操作**：CAS机制所保证的只是一个变量的原子性操作，而不能保证整个代码块的原子性。但是从 JDK 1.5开始，提供了`AtomicReference类`来保证引用对象之间的原子性，你可以把多个变量放在一个对象里来进行 CAS 操作.所以我们可以使用锁或者利用`AtomicReference类`把多个共享变量合并成一个共享变量来操作。



#### CAS和Synchronized的使用场景

**简单的来说CAS适用于写比较少的情况下（多读场景，冲突一般较少），synchronized适用于写比较多的情况下（多写场景，冲突一般较多）**

​		对于资源竞争较少（线程冲突较轻）的情况，**使用synchronized同步锁进行线程阻塞和唤醒切换以及用户态内核态间的切换操作额外浪费消耗cpu资源**；而**CAS基于硬件实现，不需要进入内核**，不需要切换线程，操作自旋几率较少，因此可以获得更高的性能。

​		Java并发编程这个领域中synchronized关键字一直都是元老级的角色，很久之前很多人都会称它为 **“重量级锁”** 。但是，在JavaSE 1.6之后进行了主要包括为了减少获得锁和释放锁带来的性能消耗而引入的 **偏向锁** 和 **轻量级锁** 以及其它**各种优化**之后变得在某些情况下并不是那么重了。synchronized的底层实现主要依靠 **Lock-Free** 的队列，基本思路是 **自旋后阻塞**，**竞争切换后继续竞争锁**，**稍微牺牲了公平性，但获得了高吞吐量**。在线程冲突较少的情况下，可以获得和CAS类似的性能；而线程冲突严重的情况下，性能远高于CAS。



### 21.Synchronized,ReentrantLock,Lock



#### synchronized关键字用法

1. **修饰一个代码块**，被修饰的代码块称为同步语句块，其作用的范围是大括号{}括起来的代码，**作用的对象是调用这个代码块的对象**



​		**Demo1 --->理解synchronized关键字锁的是对象**

``` java
class SyncThread implements Runnable {
   private static int count;

   public SyncThread() {
      count = 0;
   }

   public  void run() {
      synchronized(this) {
         for (int i = 0; i < 5; i++) {
            try {
               System.out.println(Thread.currentThread().getName() + ":" + (count++));
               Thread.sleep(100);
            } catch (InterruptedException e) {
               e.printStackTrace();
            }
         }
      }
   }

   public int getCount() {
      return count;
   }
}




```

调用结果1：

``` java
// main方法调用---->一个对象
SyncThread syncThread = new SyncThread();
Thread thread1 = new Thread(syncThread, "SyncThread1");
Thread thread2 = new Thread(syncThread, "SyncThread2");
thread1.start();
thread2.start();

结果：
SyncThread1:0
SyncThread1:1
SyncThread1:2
SyncThread1:3
SyncThread1:4
SyncThread2:5
SyncThread2:6
SyncThread2:7
SyncThread2:8
SyncThread2:9

```

调用结果2：

``` java
// main方法调用---->两个对象的时候
SyncThread syncThread1 = new SyncThread();
SyncThread syncThread2 = new SyncThread();
Thread thread1 = new Thread(syncThread1, "SyncThread1");
Thread thread2 = new Thread(syncThread2, "SyncThread2");
thread1.start();
thread2.start();


SyncThread1:0
SyncThread2:1
SyncThread1:2
SyncThread2:3
SyncThread1:4
SyncThread2:5
SyncThread2:6
SyncThread1:7
SyncThread1:8
SyncThread2:9

```

这时创建了**两个SyncThread的对象syncThread1和syncThread2，线程thread1执行的是syncThread1对象中的synchronized代码(run)，而线程thread2执行的是syncThread2对象中的synchronized代码(run)**；我们知道synchronized锁定的是对象，这时会有**两把锁**分别锁定syncThread1对象和syncThread2对象，而这两把锁是互不干扰的，不形成互斥，所以两个线程可以同时执行。

**一个线程访问一个对象的synchronized代码块时，别的线程可以访问该对象的非synchronized代码块而不受阻塞**



​		**Demo2--->指定某个对象加锁**

``` java
/**
 * 银行账户类
 */
class Account {
   String name;
   float amount;

   public Account(String name, float amount) {
      this.name = name;
      this.amount = amount;
   }
   //存钱
   public  void deposit(float amt) {
      amount += amt;
      try {
         Thread.sleep(100);
      } catch (InterruptedException e) {
         e.printStackTrace();
      }
   }
   //取钱
   public  void withdraw(float amt) {
      amount -= amt;
      try {
         Thread.sleep(100);
      } catch (InterruptedException e) {
         e.printStackTrace();
      }
   }

   public float getBalance() {
      return amount;
   }
}

/**
 * 账户操作类
 */
class AccountOperator implements Runnable{
   private Account account;
   public AccountOperator(Account account) {
      this.account = account;
   }

   public void run() {
      synchronized (account) {
         account.deposit(500);
         account.withdraw(500);
         System.out.println(Thread.currentThread().getName() + ":" + account.getBalance());
      }
   }
}

// main方法进行调用
Account account = new Account("zhang san", 10000.0f);
AccountOperator accountOperator = new AccountOperator(account);

final int THREAD_NUM = 5;
Thread threads[] = new Thread[THREAD_NUM];
for (int i = 0; i < THREAD_NUM; i ++) {
   threads[i] = new Thread(accountOperator, "Thread" + i);
   threads[i].start();
}

```

调用结果：

```
Thread3:10000.0
Thread2:10000.0
Thread1:10000.0
Thread4:10000.0
Thread0:10000.0
```





2. **修饰一个方法**，被修饰的方法称为同步方法，其作用的范围是整个方法，作用的对象是调用这个方法的对象

Synchronized修饰一个方法很简单，就是在方法的前面加synchronized，public synchronized void method(){//todo}; synchronized修饰方法和修饰一个代码块类似，**只是作用范围不一样，修饰代码块是大括号括起来的范围，而修饰方法范围是整个函数。**


<img src="https://tva1.sinaimg.cn/large/006tNbRwly1ga5k9ll02vj30x80u0430.jpg" alt="image-20191222160453297" style="zoom:50%;" />

虽然可以使用synchronized来定义方法，但synchronized并不属于方法定义的一部分，因此，synchronized关键字不能被继承。**如果在父类中的某个方法使用了synchronized关键字，而在子类中覆盖了这个方法，在子类中的这个方法默认情况下并不是同步的**，而必须显式地在**子类的这个方法中加上synchronized关键字才可以**。

<img src="https://tva1.sinaimg.cn/large/006tNbRwly1ga5kcdlrp3j30tg0l476y.jpg" alt="image-20191222160736255" style="zoom:50%;" />





3. **修饰一个静态的方法**，其作用的范围是整个静态方法，作用的对象是这个类的所有对象

   Demo：synchronized关键字修饰静态方法

``` java
/**
 * 同步线程
 */
class SyncThread implements Runnable {
   private static int count;

   public SyncThread() {
      count = 0;
   }

   public synchronized static void method() {
      for (int i = 0; i < 5; i ++) {
         try {
            System.out.println(Thread.currentThread().getName() + ":" + (count++));
            Thread.sleep(100);
         } catch (InterruptedException e) {
            e.printStackTrace();
         }
      }
   }

   public synchronized void run() {
      method();
   }
}

// main方法中的调用
SyncThread syncThread1 = new SyncThread();
SyncThread syncThread2 = new SyncThread();
Thread thread1 = new Thread(syncThread1, "SyncThread1");
Thread thread2 = new Thread(syncThread2, "SyncThread2");
thread1.start();
thread2.start();

```



调用结果：

```
SyncThread1:0
SyncThread1:1
SyncThread1:2
SyncThread1:3
SyncThread1:4
SyncThread2:5
SyncThread2:6
SyncThread2:7
SyncThread2:8
SyncThread2:9
```

syncThread1和syncThread2是SyncThread的两个对象，但在thread1和thread2并发执行时却保持了线程同步。这是因为run中调用了静态方法method，**而静态方法是属于类的，所以syncThread1和syncThread2相当于用了同一把锁。**



4. **修饰一个类**其作用的范围是synchronized后面括号括起来的部分，作用主的对象是这个类的所有对象。


``` java
class ClassName {
   public void method() {
      synchronized(ClassName.class) {
         // todo
      }
   }
}
```

**synchronized作用于一个类T时，是给这个类T加锁，T的所有对象用的是同一把锁**



#### synchronized底层实现

- 进入执行synchronized代码块： monitorenter：count++
- 释放：monitorexit： count--；
- 线程判断计数器是否是0，如果是0表示当前锁空闲，可以进行占用，反之就等待

#### synchronized的性能优化问题

参考：http://www.pianshen.com/article/13827882/

- JDK1.6之前---->重量级锁

  ​		**Synchronized是通过对象内部的一个叫做监视器锁（monitor）来实现的**。但是监视器锁本质又是依赖于底层的操作系统的Mutex Lock来实现的。而**操作系统实现线程之间的切换这就需要从用户态转换到核心态，这个成本非常高，状态之间的转换需要相对比较长的时间，这就是为什么Synchronized效率低的原因。**因此，这种依赖于操作系统Mutex Lock所实现的锁我们称之为“重量级锁”。JDK中对Synchronized做的种种优化，其核心都是为了减少这种重量级锁的使用

- JDK1.6之后--->进行了优化

  ​		锁的升级过程如下：***\*锁的状态总共有四种：无锁状态、偏向锁、轻量级锁和重量级锁\****。(对象头中锁的状态是2个字节)随着锁的竞争，锁可以从**偏向锁升级到轻量级锁，再升级的重量级锁**（但是锁的升级是单向的，也就是说只能从低到高升级，不会出现锁的降级

  

  - **自旋锁优化---->自适应自旋锁**

    ​		**频繁的阻塞和唤醒对CPU来说是一件负担很重的工作,所谓自旋锁，就是让该线程等待一段时间，不会被立即挂起，看持有锁的线程是否会很快释放锁。**怎么等待呢？执行一段无意义的循环即可（自旋),如果持有锁的线程很快就释放了锁，那么自旋的效率就非常好

    ​		JDK 1.6引入了更加聪明的自旋锁，即***自适应自旋锁***。所谓自适应就意味着自旋的次数不再是固定的，它是由前一次在同一个锁上的自旋时间及锁的拥有者的状态来决定。它怎么做呢？**线程如果自旋成功了，那么下次自旋的次数会更加多，因为虚拟机认为既然上次成功了，那么此次自旋也很有可能会再次成功，那么它就会允许自旋等待持续的次数更多。**反之，**如果对于某个锁，很少有自旋能够成功的，那么在以后要或者这个锁的时候自旋的次数会减少甚至省略掉自旋过程，以免浪费处理器资源。**

    

  - **锁消除**

    ​		锁消除**是Java虚拟机在JIT编译时**，通过对运行上下文的扫描，**去除不可能存在共享资源竞争的锁，通过锁消除，可以节省毫无意义的请求锁时间**。就是JVM会检测到不可能存在共享数据竞争，JVM会进行锁的消除(StringBuffer,Vector,HashTable)

    

  - **锁粗化**

    ​		将连续的加锁 精简到只加一次锁。

    ``` java
    public class StringBufferTest {
        StringBuffer stringBuffer = new StringBuffer();
     
        public void append(){
            stringBuffer.append("a");
            stringBuffer.append("b");
            stringBuffer.append("c");
        }
    }
    ```

    ​		这里**每次调用stringBuffer.append方法都需要加锁和解锁**，如果虚拟机检测到有一系列连串的对同一个对象加锁和解锁操作，就会将其合并成一次范围更大的加锁和解锁操作，**即在第一次append方法时进行加锁，最后一次append方法结束后进行解锁。** 

    

  - **轻量级锁**

    **无竞争的条件下，通过CAS消除同步互斥**多个线程交替同步执行的情况，没有竞争

    

  - **偏向锁**

    无竞争条件下，消除整个互斥同步，**连CAS都不做(只有一个线程执行同步)**

    ​		引入偏向锁是为了在**无多线程竞争的情况下尽量减少不必要的轻量级锁执行路径**，因为轻量级锁的获取及释放**依赖多次CAS原子指令，而偏向锁只需要在置换ThreadID的时候依赖一次CAS原子指令**（由于一旦出现**多线程竞争的情况就必须撤销偏向锁**，所以偏向锁的撤销操作的性能损耗必须小于节省下来的CAS原子指令的性能消耗）。

    ​		偏向锁只有**遇到其他线程尝试竞争偏向锁时**，持有偏向锁的线程才会释放锁，线程不会主动去释放偏向锁。

    

    ![image-20191222170850243](https://tva1.sinaimg.cn/large/006tNbRwly1ga5m43mnzij316c0e80vr.jpg)

    

#### Lock

![image-20191222171301152](https://tva1.sinaimg.cn/large/006tNbRwly1ga5m8g1y7bj31ik0mi78d.jpg)

​		Lock实现和synchronized不一样，**后者是一种悲观锁，它胆子很小，它很怕有人和它抢吃的，所以它每次吃东西前都把自己关起来**。而**Lock呢底层其实是CAS乐观锁的体现，它无所谓，别人抢了它吃的，它重新去拿吃的就好啦，所以它很乐观**。



Lock接口的源码：



``` java
public interface Lock {

    /**
     * Acquires the lock.
     */
    void lock();

    /**
     * Acquires the lock unless the current thread is
     * {@linkplain Thread#interrupt interrupted}.
     */
    void lockInterruptibly() throws InterruptedException;

    /**
     * Acquires the lock only if it is free at the time of invocation.
     */
    boolean tryLock();

    /**
     * Acquires the lock if it is free within the given waiting time and the
     * current thread has not been {@linkplain Thread#interrupt interrupted}.
     */
    boolean tryLock(long time, TimeUnit unit) throws InterruptedException;

    /**
     * Releases the lock.
     */
    void unlock();
	
}

```







#### ReentrantLock

**ReentrantLock是Lock的一个具体实现类**

``` java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class LockTest {
	private Lock lock = new ReentrantLock();

	//需要参与同步的方法
	private void method(Thread thread){
		lock.lock();
		try {
			System.out.println("线程名"+thread.getName() + "获得了锁");
		}catch(Exception e){
			e.printStackTrace();
		} finally {
			System.out.println("线程名"+thread.getName() + "释放了锁");
			lock.unlock();
		}
	}
	
	public static void main(String[] args) {
		LockTest lockTest = new LockTest();
		
		//线程1
		Thread t1 = new Thread(new Runnable() {
			
			@Override
			public void run() {
				lockTest.method(Thread.currentThread());
			}
		}, "t1");
		
		Thread t2 = new Thread(new Runnable() {
			
			@Override
			public void run() {
				lockTest.method(Thread.currentThread());
			}
		}, "t2");
		
		t1.start();
		t2.start();
	}
}
//执行情况： 线程名t1获得了锁
//         线程名t1释放了锁
//         线程名t2获得了锁
//         线程名t2释放了锁

```



#### ReentrantLock和synchronized用法区别

- 用ReentrantlLock保护代码块一定要在finally块里面释放锁，synchronized不需要，JVM自动帮助我们释放

``` java
Lock lock = new ReentrantLock();
lock.lock();
try { 
  // update object state
}
finally {
  lock.unlock(); 
}
```

- 性能区别

  在Synchronized优化以前，synchronized的性能是比ReenTrantLock差很多的，但是自从Synchronized引入了偏向锁，轻量级锁（自旋锁）后，两者的性能就差不多了，在两种方法都可用的情况下，官方甚至建议使用synchronized，其实synchronized的优化我感觉就借鉴了ReenTrantLock中的CAS技术。都是试图在用户态就把加锁问题解决，避免进入内核态的线程阻塞。

- 功能区别

  便利性：很明显**Synchronized的使用比较方便简洁**，并且**由编译器去保证锁的加锁和释放，而ReenTrantLock需要手工声明来加锁和释放锁**，为了避免忘记手工释放锁造成死锁，所以最好在finally中声明释放锁。

  锁的细粒度和灵活度：很明显ReenTrantLock优于Synchronized

- 相关使用场景

  - 竞争资源不是很激烈，偶有同步--->synchronized
  - 同步激烈，synchronized性能急剧下降--->ReentrantLock

- 我们什么时候才应该使用 `ReentrantLock` 呢？

  ​		**在确实需要一些 synchronized 所没有的特性的时候**，比如**时间锁等候、可中断锁等候、无块结构锁、多个条件变量或者锁投票(ReentrantLock的独有魅力)**。 `ReentrantLock` 还具有可伸缩性的好处，应当在高度争用的情况下使用它，但是请记住，大多数 synchronized 块几乎从来没有出现过争用，所以可以把高度争用放在一边。我建议用 synchronized 开发，直到确实证明 synchronized 不合适，而不要仅仅是假设如果使用 `ReentrantLock` “性能会更好”。





### 23.Java多线程3中实现方式



#### 继承Thread类实现多线程

继承Thread类的方法尽管被我列为一种多线程实现方式，但Thread本质上也是实现了Runnable接口的一个实例，它代表一个线程的实例，并且，启动线程的唯一方法就是通过Thread类的start()实例方法。start()方法是一个native方法，它将启动一个新线程，并执行run()方法。这种方式实现多线程很简单，通过自己的类直接extend Thread，并复写run()方法，就可以启动新线程并执行自己定义的run()方法。

``` java
public class MyThread extends Thread {
　　public void run() {
　　 System.out.println("MyThread.run()");
　　}
}
```

在合适的地方启动线程

``` java
MyThread myThread1 = new MyThread();
MyThread myThread2 = new MyThread();
myThread1.start();
myThread2.start();
```



#### 实现Runnable接口实现多线程

如果自己的类已经extends另一个类，就无法直接extends Thread，此时，必须实现一个Runnable接口，如下：

``` java
public class MyThread extends OtherClass implements Runnable {
　　public void run() {
　　 System.out.println("MyThread.run()");
　　}
}
```

启动MyThread

``` java
MyThread myThread = new MyThread();
Thread thread = new Thread(myThread);
thread.start();
```

事实上，当传入一个Runnable target参数给Thread后，Thread的run()方法就会调用target.run()，参考JDK源代码：

``` java
public void run() {
　　if (target != null) {
　　 target.run();
　　}
}
```



#### 使用ExecutorService、Callable、Future实现有返回结果的多线程



Executor框架是指java 5中引入的一系列并发库中与executor相关的一些功能类，其中包括线程池，Executor，Executors，ExecutorService，CompletionService，Future，Callable等。他们的关系为： 

并发编程的一种编程方式是把任务拆分为一些列的小任务，即Runnable，然后在提交给一个Executor执行，**Executor.execute(Runnalbe)** 。Executor在执行时使用内部的线程池完成操作。



- **创建线程池**



Executors类，提供了**一系列工厂方法用于创先线程池**，返回的线程池都实现了ExecutorService接口。

**public static ExecutorService newFixedThreadPool(int nThreads)**

创建固定数目线程的线程池。

**public static ExecutorService newCachedThreadPool()**

创建一个可缓存的线程池，调用`execute` 将重用以前构造的线程（如果线程可用）。如果现有线程没有可用的，则创建一个新线程并添加到池中。终止并从缓存中移除那些已有 60 秒钟未被使用的线程。

**public static ExecutorService newSingleThreadExecutor()**

创建一个单线程化的Executor。

**public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize)**

创建一个支持定时及周期性的任务执行的线程池，多数情况下可用来替代Timer类。



``` java
Executor executor = Executors.newFixedThreadPool(10);  
Runnable task = new Runnable() {  
    @Override  
    public void run() {  
        System.out.println("task over");  
    }  
};  
executor.execute(task);  
  
executor = Executors.newScheduledThreadPool(10);  
ScheduledExecutorService scheduler = (ScheduledExecutorService) executor;  
scheduler.scheduleAtFixedRate(task, 10, 10, TimeUnit.SECONDS);
```



- **ExecutorService生命周期**



ExecutorService**扩展了Executor并添加了一些生命周期管理的方法**。一个Executor的生命周期有三种状态，**运行** ，**关闭** ，**终止** 。Executor创建时处于运行状态。**当调用ExecutorService.shutdown()后，处于关闭状态，isShutdown()方法返回true**。这时，不应该再想Executor中添加任务，所有已添加的任务执行完毕后，Executor处于终止状态，isTerminated()返回true。

如果Executor处于关闭状态，往Executor提交任务会抛出unchecked exception RejectedExecutionException。

``` java
ExecutorService executorService = (ExecutorService) executor;  
while (!executorService.isShutdown()) {  
    try {  
        executorService.execute(task);  
    } catch (RejectedExecutionException ignored) {  
          
    }  
}  
executorService.shutdown();  
```



- 使用Callable，Future返回结果

Future<V>代表一个异步执行的操作，通过get()方法可以获得操作的结果，如果异步操作还没有完成，则，get()会使当前线程阻塞。**FutureTask<V>实现了Future<V>和Runable<V>。Callable代表一个有返回值的操作**。



``` java
Callable<Integer> func = new Callable<Integer>(){  
    public Integer call() throws Exception {  
        System.out.println("inside callable");  
        Thread.sleep(1000);  
        return new Integer(8);  
    }         
};        
FutureTask<Integer> futureTask  = new FutureTask<Integer>(func);  
Thread newThread = new Thread(futureTask);  
newThread.start();  
  
try {  
    System.out.println("blocking here");  
    Integer result = futureTask.get();  
    System.out.println(result);  
} catch (InterruptedException ignored) {  
} catch (ExecutionException ignored) {  
}
```



