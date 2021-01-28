#### 目录
[一、JDK和JRE和JVM的作用和区别](#one)
    
[二、JAVA环境变量](#two)
  
[三、基础数据类型](#three)
  
[四、重载](#four)

[五、内存分析](#five)

[六、垃圾回收机制](#six)

[七、类](#seven)

[八、包](#eight)

[九、继承](#nine)

[十、重写](#ten)

[十一、高内聚、低耦合](#eleven)

[十二、访问修饰符](#twelve)

[十三、JavaBean](#thirteen)

[十四、多态](#fourteen)

[十五、JAVA数组](#fifteen)

[十六、抽象类、抽象方法](#sixteen)

[十七、接口和实现](#seventeen)

[十八、类、抽象类、接口和实现之间的联系](#eightteen)

[十九、内部类](#nineteen)

[二十、常用类](#twenty)

[二十一、数据类型转化](#twenty-one)

[二十二、容器](#twenty-two)

[二十三、泛型](#twenty-three)

[二十四、io](#twenty-four)

[二十五、多线程](#twenty-five)

[二十六、网络编程](#twenty-six)

[二十七、手写webserver](#twenty-seven)

[二十八、注解](#twenty-eight)

[二十九、反射机制](#twenty-nine)

[三十、动态编译](#thirty)

[三十一、脚本引擎执行javascript代码](#thirty-one)

[三十二、字节码操作](#thirty-two)

[三十三、JVM核心机制](#thirty-three)

[三十四、设计模式](#thirty-four)

[三十五、正则表达式](#thirty-five)

#### <h3 id="one">一、JDK和JRE和JVM的作用和区别</h3>
```
    1.JavaSE、JavaEE、JavaME
    JavaSE: 标准版，用于开发个人桌面应用程序
    JavaEE: 企业版，用于开发服务器端的应用
    JavaME: 微型版，用于开发消费性电子产品的应用(物联网)
    
    2.JAVA应用程序的运行机制：
    源文件(*.java) -> java编译器 -> 字节码文件
    -> JRE(->类装载器 -> 字节码校验器 -> 解释器 ->) 
    -> 系统平台

    3.JVM、JRE、JDK
    JVM：java虚拟机
    JRE：java运行时环境
    JDK：java开发工具包
    JDK = JRE + (javac、jar、debugging.tools、javap)
    JRE = JVM + (java、javaw、libraries、rt.jar) 

    不同的JVM虚拟机用于在不同的操作系统上解释并执行字节码文件(*.class)

    Java目录：
    bin 二进制文件
    lib 类库
    src.zip JDK源代码
    
```

#### <h3 id="two">二、JAVA环境变量</h3>

```
    JAVA_HOME: JDK的安装路径，这是给其他工具使用的
    %JAVA_HOME%/bin: java的可执行二进制文件目录
    classpath: JDK1.5以下才需要设置的类路径
    java的变量：
        1.局部变量
        2.静态变量
        3.成员变量
    常量：final
```

#### <h3 id="three">三、基础数据类型</h3>

```
    java的3类8种基本数据类型：
    数值型：byte、short、int、long、float、double
    字符型(文本型)：char
    布尔型：boolean
    引用数据类型：类class、接口interface、数组
```

#### <h3 id="four">四、重载</h3>

```
    重载：重载的方法，实际是完全不同的方法，只是名称相同而已
    触发重载：
    1.形参类型不同
    2.形参顺序不同
    3.形参个数不同

    构造方法的重载：用于(同一个类)创建不同类型的对象
```

#### <h3 id="five">五、内存分析</h3>

```
    java虚拟机的内存可以分为三个区域：
    栈(stack)
        方法执行的内存模型
        每个方法被调用都会创建一个栈帧，存储局部变量、操作数、方法出口等
        先入后出，后入先出
    堆(heap)
        用于存储创建好的对象
        无序
    方法区(method area)
        实际也是堆，只是用于存储类信息(代码)、静态变量(静态方法)、常量等

```

#### <h3 id="six">六、垃圾回收机制</h3>

```
    垃圾回收机制：
        相关算法：1.引用计数法  2.引用可达法(根搜索算法)
```

#### <h3 id="seven">七、类</h3>

```
    static修饰的成员变量和方法属于类
    普通成员变量和方法属于对象
```

#### <h3 id="eight">八、包</h3>

```
    包对于类 -> 相当于文件夹对于文件
    JDK中的主要包:
        java.lang: 语言核心类、常用功能(不用导入可以直接使用)
        java.awt: GUI图形用户界面
        java.net: 网络相关
        java.io: 输入\输出
        java.util: 实用工具类

    import: 
        1.导入不同包下的类
        2.同包下的类无需导入
        3.导入包下所有的类: import cn.com.*，会导致编译变慢，不会导致运行变慢
        4.同包名：java.util.Date date = new java.util.Date();

```

#### <h3 id="nine">九、继承</h3>

```
    继承：
        java中只能扩展(继承)一个类
        java中的接口可以多继承
        extends 继承
        instanceof 判断是否继承
```

#### <h3 id="ten">十、重写</h3>

```
    重写：
        子类重写父类的方法(override)
        1.方法名、形参列表相同
        2.返回值类型和异常声明类型、子类小于等于父类(返回值如果是一个类，必须为父类返回值的子孙类)
        3.访问权限，子类大于等于父类
```

#### <h3 id="eleven">十一、高内聚、低耦合</h3>

```
    高内聚：
        封装细节、类的内部自己完成细节，不允许外部干涉
    低耦合：
        仅暴露少量方法给外部使用，便于扩展和协作
```

#### <h3 id="twelve">十二、访问修饰符</h3>

```
    访问修饰符      同一个类    同一个包    子类    所有类      使用范围
    private          可以                                    给自己用
    default          可以        可以                        给自己和同包用
    protected        可以        可以     可以                给自己、同包、不同包的子类用
    public           可以        可以     可以      可以       公用
```

#### <h3 id="thirteen">十三、JavaBean</h3>

```
    JavaBean: 没有复杂的属性方法的类
```

#### <h3 id="fourteen">十四、多态</h3>

```
    多态(方法多态)：指同一个方法调用、由于对象不同可能会有不同的行为
    必要条件：继承、方法重写、父类引用指向子类对象
    描述：同一个父类造出不同功能的子类(多种形态)
```

#### <h3 id="fiveteen">十五、JAVA数组</h3>

```
    java数组：
        1.长度确定
        2.元素类型相同
        3.数组类型可以是任何类型
        初始化方式：
            1.静态初始化 
            int[] a = {2,3,4};
            2.动态初始化 
            int[] b = new int[1];
            b[0] = 1;
            3.默认初始化
            int[] = new int[3];
    for-each: 循环
    用于读取数组或集合中的数据，不能修改元素的值
    String[] str = {"1","2","3"};
    for(String m:str) {
        System.out.println(m);
    }
```

#### <h3 id="sixteen">十六、抽象类、抽象方法</h3>

```
    抽象类(abstract)、抽象方法:
    抽象方法必须在抽象类中定义
    特点：
    1.没有实现
    2.子类必须实现，否则报错
    3.不能new、只能被继承
    作用：给子类提供严格的规范
```

#### <h3 id="seventeen">十七、接口和实现</h3>

```
    接口(interface)：比抽象类还要抽象的抽象类
    接口里的方法都是抽象方法
    实现了规范和具体实现的分离

    实现(inplements):用于实现接口
```

#### <h3 id="eightteen">十八、类、抽象类、接口和实现之间的联系</h3>

```
    类class - 抽象类abstract - 接口interface - 实现implements
    抽象类是类的规范
    接口 = 抽象类 + 实现
    类只能继承一个父类
    接口可以实现多个父类、且可以多继承
    1.单继承 
        class a extends b
    2.多实现
        class d implements a,b,c
    3.多继承
        interface a extends b,c

    面向接口编程：
        千变万变接口不变、实现类变

    类(单继承)，抽象类，接口(多继承，实现)
	1. 抽象类是类的抽象，接口是抽象类的抽象
	2. 包含内容
	   类：普通方法，属性
	   抽象类：普通方法，属性，抽象方法(只有方法名，没有实现)
	   接口：只有抽象方法
	3. 
	   类：可以new生成对象，可以被继承
	   抽象类：不能new，只能被继承(不能多继承)，由子类new生成对象.抽象方法必须被子类实现
	   接口：不能new，只能被继承(可以多继承)，方法必须被子类实现，由子类new生成对象
	4. java中类只能单继承，接口可以多继承
```

#### <h3 id="nineteen">十九、内部类</h3>

```
    内部类：成员内部类(静态、非静态)、匿名内部类、局部内部类(x)
```


#### <h3 id="twenty">二十、常用类</h3>

```
    
```

#### <h3 id="twenty-one">二十一、数据类型转化</h3>

```
    
```

#### <h3 id="twenty-two">二十二、容器</h3>

```
    容器就是集合 collction
    数组: 优点、速度快，缺点、不灵活，容量不能随需求改变。
    所以有了容器

    有哪些容器：
    0.数组(array)		 {}
    1.有序，可重复(List)   []
    2.无序，不可重复(Set)  {}
    3.键值对(Map)	        {}

    collection<interface> -> Set<interface> -> HashSet
    特点：

    collection<interface> -> List<interface> -> ArrayList
    特点：数组实现，查询效率高，增删效率低，线程不安全

    collection<interface> -> List<interface> -> LinkedList
    特点：链表实现，查询效率低，增删效率高，线程不安全

    collection<interface> -> List<interface> -> Vector
    特点：数组实现，线程安全、效率低

    Set: 无序、不可重复
    List: 有序、可重复

    Map<interface> -> HashMap
    特点：哈希表实现，键值对，线程不安全、效率高、允许key或value为null

    Map<interface> -> HashTable
    特点：线程安全、效率低，不允许key或value为null

    Map<interface> -> TreeMap
    特点：红黑二叉树实现，效率低，排序用


    迭代器(Iterator):
    迭代器其实就是一个集合
    有hasNext方法检查下个节点是否存在
    有next方法将游标指向下一个节点，并返回该节点
    用来遍历容器(List/Set/Map)

    Collections工具类

    使用容器存储表格：
        ORM思想：对象关系映射

    遍历Map的思维：
        1.直接获取Map中所有对象存到Set中遍历
        2.获取Map所有key的Set集合，遍历key来实现(map.keySet)

```

#### <h3 id="twenty-three">二十三、泛型</h3>

```
    泛型就是(参数的)类型检测 
    <T><E><D><T.E.D>
    <>相当于()，里面可能放形参和实参

    在编译的时候，确定好参数类型，这样可以统一严格规范参数的传入和返回的类型

```

#### <h3 id="twenty-four">二十四、io</h3>

```
	输入：读
	输出：写

	1.字节流和字符流使用情况:
	字符流和字节流的使用范围：字节流一般用来处理图像，视频，以及PPT，Word类型的文件。字符流一般用于处理纯文本类型的文件，如TXT文件等，字节流可以用来处理纯文本文件，但是字符流不能用于处理图像视频等非文本类型的文件。
	
	2.字节流和字符流的区别:
	字节流没有缓冲区，是直接输出的，而字符流是输出到缓冲区的。因此在输出时，字节流不调用colse()方法时，信息已经输出了，而字符流只有在调用close()方法关闭缓冲区时，信息才输出。要想字符流在未关闭时输出信息，则需要手动调用flush()方法。
	读写单位不同：字节流以字节（8bit）为单位，字符流以字符为单位，根据码表映射字符，一次可能读多个字节。
	处理对象不同：字节流能处理所有类型的数据（如图片、avi等），而字符流只能处理字符类型的数据。
	
	结论：只要是处理纯文本数据，就优先考虑使用字符流。除此之外都使用字节流。
	
	3.序列化和反序列化
	序列化：将保存在内存中的对象数据转化为二进制数据流进行传输(对象转二进制)
	反序列化：将二进制数据换回原对象(二进制转对象)
	
	4.处理流BufferedReader，BufferedWriter,BufferedInputStream
	BufferedOutputsStream，都要包上一层节点流。也就是说处理流是在节点流的基础之上进行的，带有Buffered的流又称为缓冲流，缓冲流处理文件的输入输出的速度是最快的。所以一般缓冲流的使用比较多。
	
	5.总结
	inputStream类的功能不足被Scanner解决了

	OutputStream类的功能不足被PrintStream解决了

	Reader类功能不足被BufferReader解决了

	Writer类的功能不足被PrintWriter解决了

	输出数据用printStream，printwriter读取数据用Scanner其次是bufferReader
	
	
```

#### <h3 id="twenty-five">二十五、多线程</h3>
```
	1.操作系统 -> 任务(程序) -> 进程(在内存运行中的程序，Process) -> 线程(进程中的顺序执行流)
	2.进程特征
	    1.独立性
	      进程拥有自己的私有的地址空间，相互独立禁止访问，除非设置允许
	    2.动态性
	      进程加入了时间概念，比程序多了生命周期和各种不同的状态
	    3.并发性
	      多个进程可以在单个处理器上切换并发执行
	3.并发和并行
	    并发：单个处理器上切换执行多个进程指令
	    并行：多个处理器上同时执行多个进程指令
	4.多线程
	    几乎同时执行多个线程
	5.多线程优点
	    1.进程之间不能共享内存，线程可以
	    2.系统创建进程需要重新分配系统资源，但创建线程代价小的多
	    3.Java语言内置了多线程功能支持，而不是单纯地作为底层操作系统的调度方式，从而简化了Java的多线程编程
	6.使用多线程
	    1.多线程的创建
	      a.继承Thread类
	      b.实现Runnable接口
	      c.使用Callable和Future创建线程
	    2.线程的生命周期
	      新建 -> 就绪 -> 运行 -> 死亡
	      新建 -> 就绪 -> 运行 -> 阻塞 -> 就绪 -> 运行 -> 死亡
	    3.控制线程
	      join线程
	        特点：让当前join的线程执行完再继续执行
	      后台线程
	        特点：如果所有的前台线程都死亡，后台线程会自动死亡
	      线程睡眠
	      改变线程优先级
	    4.线程安全问题
	      多个线程修改同一个共享数据，可能发生线程安全问题
	    5.解决线程安全问题
	      1.同步代码块
	      2.同步方法
	      3.同步锁
	      
	      死锁：
	        当两个线程相互等待对方释放同步监视器时就会发生死锁，Java虚拟机没有监测，也没有采取措施来处理死锁情况，所以多线程编程时应该采取措施避免死锁岀现。一旦岀现死锁，整个程序既不会发生任何异常，也不会给出任何提示，只是所有线程处于阻塞状态，无法继续。
		
	    6.线程池
	      系统启动一个新线程的成本是比较高的，因为它涉及与操作系统交互。在这种情形下，使用线程池可以很好地提高性能，尤其是当程序中需要创建大量生存期很短暂的线程时，更应该考虑使用线程池。
	    创建线程池的几个常用方法：
	    1.newSingleThreadExecutor    创建一个单线程的线程池
	    2.newFixedThreadPool         创建固定大小的线程池
	    3.newCachedThreadPool        创建一个可缓存的线程池
	    4.newScheduledThreadPool     创建一个大小无限的线程池
```

