xl

# JAVASE

# 7.17

## 1.错例，java 里变量未附值错误

```
int i;
System.out.println(i);
```



# 7.18

## 1.数据类型转换:

整数的最小类型是int 型(type+short=int),long则为long

错例：

```
short a=1;

type b =2;

[false] short a=a+b;

特殊：[true] a+=b;
```

## 2.i++与++i

i++ : 先运算后加

++i :先加后运算

注意：一小段就结束了，i++ + ++i ; 不是分号结束再全部加。



## 3.逻辑运算符 

| 逻辑运算符     | 功能                                                         |
| -------------- | ------------------------------------------------------------ |
| \|\|（短路或） | 都为false，则false。有一个为true便不再继续判断了             |
| \|（逻辑或）   | 都为false，则false。所有的条件都判断                         |
| &&（短路与）   | 都为true，则true。有一个为false便不再继续判断了；即前有一false，后不执行。 |
| &（逻辑与）    | 都为true，则true。所有的条件都判断                           |
| ！(非)         | 变成相反                                                     |
| ^（异或）      | 相同则为false，不相同则为true                                |

  (1)例： 

```
int a=10,b=20;

boolean r = a<b&&(b=30)>a;

注意：stou b = 20，r=0;前为假后不运算
```

​	(2)  &和&&

单语无短路，双语有短路；

&能使用数值和布尔类型，&&只能使用布尔类型；



## 4.移位运算符 << >>

2<<1 <==> 2*2;

## 5.三目运算符

boolean ? 值1 ：值2  （值可以为任意类型）

boolean = true ---> 值1

false ---> 值2



## 6.随机数

### 6.1	**Math.random()方法** --> [0.0,1.0)

```
公式：(数据类型)(最小值+Math.random()*(最大值-最小值+1))

上述公式为产生的随机数，范围包含最小值与最大值。
```

### 6.2 	**random类**

除了Math类中的random()方法可以获取随机数之外，在Java中还提供了一种可以获取随机数的方式，那就是java.util.Random类。可以通过实例化一个Random对象创建一个随机数生成器。

语法如下：

```
Random r=new Random();

其中，r是指Random对象

import java.util.Random;                         
Random r = new Random();              
r.nextInt(bound);   [0,bound)

```



常用的方法

| 方法                         | 说明                                   |
| ---------------------------- | -------------------------------------- |
| public int nextInt()         | 返回一个随机整数。                     |
| public int nextInt(itn)      | 返回大于等于0且小于n的随机整数。       |
| public long nextLong()       | 返回一个随机长整型值。                 |
| public boolean nextBoolean() | 返回一个随机布尔型值。                 |
| public float nextFloat()     | 返回一个随机浮点型值。                 |
| public double nextDouble()   | 返回一个随机双精度型值。               |
| public double nextGaussian() | 返回一个概率密度为高斯分布的双精度值。 |





# **7.21** 面向对象（OOP）

## 1.类的定义

类：代表一类事物

对象：某个类的个体

```
class 类名{

}//
```

## 2.类中的内容：

（1）属性-->特征

eg:  人： 性别，年龄，姓名，体重....

```
class Person{
    String name;
    int age;
}
```

（2）方法-->行为

​	功能--能干什么

​	参数:

​			有参方法	无参方法

​	返回值:

​			有返回值	无返回值

​	定义：

​		[访问修饰符] 返回类型 方法名称(参数列表.....）{

​	方法体---要做的事情

​	}

## 3.类名命名规则：与变量相同

​       命名规范：首字母大写

​       属性默认值：

​            整型：0	浮点：0.0	字符"\u0000"	布尔：false	其他：null

  

注意：

一个文件内可以定义多个类，只能有一个是public的，并且public修饰的类名与文件名一致

不建议在一个文件中写多个类



## 4.对象的创建方式：

```
 类 名称 = new 类();

eg: Desk desk = new Desk();
```



## 5.对象在内存中的创建过程:**(重点)**

(1)加载类

(2)根据加载的类创建对象

(3)给属性赋默认值

(4)把内存地址赋值给名称



## 6.new: 创建对象，每new 一次都会在堆中开辟新的空间

## 7.对象储存内存

<img src="C:\Users\Starry_z666\AppData\Roaming\Typora\typora-user-images\image-20230721094129668.png" alt="image-20230721094129668" style="zoom: 80%;" />



![image-20230721103528753](C:\Users\Starry_z666\AppData\Roaming\Typora\typora-user-images\image-20230721103528753.png)



## 8.null

栈中的变量找不到堆中对应的内存，空指针



## 9.方法重载（overload) :（重点）

1.同一个类中，方法名称一致；

2.方法参数的个数、类型或者顺序不一致；

3.与返回值、访问修饰符无关。



## 10.变量

​	局部变量：定义在方法内，方法参数 --- 只能在方法内使用

​	成员变量：属性-定义在类中 --- 在类中的任意位置都可使用（main方法除外）

​	如果成员变量和局部变量名称相同，在同一范围内，默认使用局部变量，若想使用成员变量，需要加 this. 指定

另：

实例变量： 定义在类中的变量是类的成员变量，可以不进行初始化， java 会自动进行初始化。（如果是引用类默认初始化为 null, 如果是基本类型，默认初始化为 0 ）

局部变量 ：定义在方法中的变量，必须进行初始化，否则不通过编译。

类变量 ：（也叫作静态变量）是类中独立于方法之外的变量，用 static 修饰。

final 修饰的变量： 也称为常量。



## 11.+用法：

拼接--> 任意类型与字符串+，结果转成字符串

字符串拼接技巧：

## 12.方法栈：

1. 运行完方法数据清空

## 13.静态方法（类方法）：

1. static 静态修饰符 --- 使用类名.直接调用

   使用static关键字修饰一个属性：该属性就是静态属性，也叫全局变量，类名.属性名可以直接访问
   使用static关键字修饰一个方法：该方法就是静态方法，可以不用创建对象，直接类名.方法名调用
   声明为static的方法有以下几条限制： 
    1、静态方法只能调用其他的静态方法，不能调用非静态方法。而在非静态方法中是可以调用静态方法的
    2、静态方法中只能访问静态属性
    3、静态方法不能引用this或super。
    4、不允许用来修饰局部变量

   

## 14.构造器（构造函数、构造方法） -- 创造对象

​	定义：名称与类名相同，并且没有返回的修饰值

​	用法：构造器可以重载 - - 一般情况下，带参数的构造器可以在创建对象时给属性赋值



```
public class Pig{
  String nickname;
    
  public Pig(){
      System.out.println("Pig");
    }
  public Pig(String nickName){
  this.nickName = nickName;
  }
  
  public static void main(String[] args) {
  Pig p = new Pig("ha");
  }
}

```

注：

一个中如果没有定义任何构造器，系统会默认添加一个公有无参构造器；

如果定义了构造器，就不会添加了；

开发时建议把无参构造器写上，很多的框架需要使用这个无参构造器；

## 15.this

区分成员变量和局部变量





# **7.22**

## 1.构造器this：

​	this--构造器调用   this(  ,  ,  ,); 

this--调用同一类中的其它构造器(一般多参调用少参，赋值)

- ​	--必须是第一条语句
- ​	--执行顺序-按顺序
- ​	--执行完成顺序--先进去后完成，后进去先完成-->方法栈



## 2.static

- ​	属性--静态属性--类属性--类名调用
- ​	静态块---在类加载时执行，只会执行一次--资源的初始化
- ​	静态方法---类方法-类名调用--不能调用成员变量



​	声明为static的方法有以下几条限制： 
​		1、静态方法只能调用其他的静态方法，不能调用非静态方法。而在非静态方法中是可以调用静态方法的
​		2、静态方法中只能访问静态属性
​		3、静态方法不能引用this或super。
​		4、不允许用来修饰局部变量

```cobol

```

![image-20230722095127811](C:\Users\Starry_z666\AppData\Roaming\Typora\typora-user-images\image-20230722095127811.png)



## 3.包--package

​	（1）组织代码结构--不同功能的类放在不同的包下

​	（2）解决类的同名问题

​	定义：package 包名；

​		包名：用 . 分割的若干个单词组成 eg: com.tencent ---公司域名的反写，建议小写

​		a.b.c ;	

​		子包：层下在下

​		全限定类名 包+类

import 导入包下的类

		* 导入包内所有类，导入父包*
		* 导入父包不能导入子包下的类



## 4.访问修饰符

- ​		private --- 只能在本类使用
- ​		default默认的[frendly] -- 什么都不加--同包中的类
- ​		public --- 任何类都能用 
- ​        protected --- 受保护的--本类，同包，其他包的子类

![image-20230723104836395](C:\Users\Starry_z666\AppData\Roaming\Typora\typora-user-images\image-20230723104836395.png)





## 5.引用类型数组：

​	eg:

​			Student name age

​			Student[]





# **7.23**

## 1.面向对象特征：

​	 （1）封装

- 把属性私有化,提供一对方法，分别对属性进行赋值和取值
- 赋值方法 void setXxx(参数)
- 取值方法 返回类型

​	（2)继承

- 消除代码冗余的手段

- 父类：被继承的类--基类

  子类：继承的类--派生类

  子类 extends 父类

  能继承的内容：属性，方法

- 限制：私有的不能继承--不能访问的都不能继承

    		 构造器不能继承

- java继承特点：单根性 --- 一个类只能有一个父类

​					       	层次性 --- 父类也可有父类，可以间接继承

​							==>只能有一个直接父类

​			object : 默认继承object,所有类的父类 

- 构造器的调用：子类中调用父类构造器  

​						 子类对象在创建时，要先调用父类构造器，默认调用父类无参构造器

- super:调用父类构造器

  ​			调用

  **注意点：**
  （1）super调用父类的构造方法的语句：`super();`，必须放在构造方法的第一行；
  （2）super必须只能出现在子类的方法或者构造方法中；
  （3）super和this不能同时调用构造方法。



- 构造器链：

  ​		super

  ​		this

- 方法的重写：

​		子类中定义一个与父类同名，参数相同,返回类型相同的方法，子类的访问修饰符不能小于父类---子类重写了父类的方法	--@Override

​		能继承才能重写	      

​								

​	   (3)多态

​	   (4)抽象





# **7.25**

## 1.继承的原则： is-a原则    子类 is a kind of 父类

## 2.**static**

​	(1)	static方法 静态能继承不能重写	

​		static属性--如果子类进行覆盖，子类将不再使用父类属性

(2)执行顺序	

***无继承关系时的执行顺序****

：

- 静态代码块先执行，且只执行一次，在类加载阶段执行
- 当有对象创建时，才会执行实例代码块，实例代码块执行完后，再执行构造方法

 **有继承关系时的执行顺序：**

：

- 父类静态代码块优先子类静态代码块执行，都是最早执行的
- **·** 父类实例代码块和父类构造方法紧接着执行
- **·** 子类的实例代码块和子类构造方法在接着执行
- **·** 第二次实例化对象时，父类和子类的静态代码块都不会在执行  



## 3.**final** -- 常量  值不能改   初始化-->定义赋值或（每个s）构造器赋值

  final关键字可以用来修饰变量，成员方法以及类。

（1）属性，修饰变量或字段，表示常量（即不能修改）

```
final int a = 10;
a = 20;//编译报错
```

（2）修饰类，表示类不能继承

```
final public class Person{
     
}
public class Student extends Person{
     
}//编译报错
```

（3）修饰方法，表示方法不能被重写，但能继承



初始化：

final修饰的变量可以分为两类，**局部变量**和**全局变量**。

当final修饰的变量是局部变量时，只需在用到这个变量之前进行初始化就可以了。

但是**，当final修饰的变量是全局变量时，必须在变量所属类的对象创建完成之前进行初始化。**

## 4.**抽象类**

​		abstract ---不能实例化 new

​			有构造器--给属性赋值，但不能实例化

​			可以写实例方法和抽象方法

​			抽象方法-- 必须写在抽象类里 ，没有方法体(),需要子类重写

- ​	如果一个类继承了抽象类，对于抽象方法

  ​		1、如果子类是可实例化的 ，必须重写

​			   2、子类也是抽象的 -- 可以不重写、可以重写

```
特点总:
1、用abstract声明
2、可以有构造器，但是不能实例化，给属性赋值
3、可以有实例方法和抽象方法
4、子类如果是可实例化的，必须重写抽象方法，否则，这子类必须是抽象的
```



```
public void eat(){

}
public abstract void show();
```



**抽象方法：**

```
1、从上面的例子中我们可以看到抽象方法跟普通方法是有区别的，它没有自己的主体（没有{}包起来的
业务逻辑），跟接口中的方法有点类似。所以我们没法直接调用抽象方法

2、抽象方法不能用private修饰，因为抽象方法必须被子类实现（覆写），而private权限对于子类来
说是不能访问的，所以就会产生矛盾

3、抽象方法也不能用static修饰，试想一下，如果用static修饰了，那么我们可以直接通过类名调
用，而抽象方法压根就没有主体，没有任何业务逻辑，这样就毫无意义了。
```


**抽象类：**

```
1、用abstract关键字来表达的类，其表达形式为：（public）abstract class 类名{}

2、抽象类不能被实例化，也就是说我们没法直接new 一个抽象类。抽象类本身就代表了一个类型，无法
确定为一个具体的对象，所以不能实例化就合乎情理了，只能有它的继承类实例化。

3、抽象类虽然不能被实例化，但有自己的构造方法

4、抽象类与接口（interface）有很大的不同之处，接口中不能有实例方法去实现业务逻辑，而抽象类
中可以有实例方法，并实现业务逻辑，比如我们可以在抽象类中创建和销毁一个线程池。

5、抽象类不能使用final关键字修饰，因为final修饰的类是无法被继承，而对于抽象类来说就是
需要通过继承去实现抽象方法，这又会产生矛盾。（后面将写一篇关于finally的文章详细讨论）
```

**抽象类与抽象方法的关联：**

```
1、如果一个类中至少有一个抽象方法，那么这个类一定是抽象类，但反之则不然。也就是说一个抽象类中可以没有抽象方法。这样做的目的是为了此类不能被实例化。

2、如果一个类继承了一个抽象类，那么它必须全部覆写抽象类中的抽象方法，当然也可以不全部覆写，如果不覆写全部抽象方法则这个子类也必须是抽象类（这样做就无意义了）	
```





## 5.**包裹类（包装类）**

对于*基本数据类型*，Java提供了对应的包裹(wrap)类型。这些包裹类型将一个基本数据类型的数据转换成对象的形式，从而使得它们可以像对象一样参与运算和传递。

储存在堆里

| 基本类型 | 包裹类型  |
| -------- | --------- |
| boolean  | Boolean   |
| char     | Character |
| byte     | Byte      |
| short    | Short     |
| int      | Integer   |
| long     | Long      |
| float    | Float     |
| double   | Double    |



## 6.**接口**

​	interface--没有构造器的	方法是抽象的（jdk1.8前）--方法可以省略public abstact，属性都是公有静态常量

(jdk1.8后)可以有默认方法

作业：解耦合

接口必须被类实现 才能使用，需要重写抽象方法，否则这个类也必须是抽象的

类与类:继承extends，只能继承一个类

类与接口:实现 implements，可以实现多个接口

接口与接口：继承 extendss  可以多继承



## 7.**接口与抽象类区别与联系**：

​	

```
1.声明方式：抽象类 abstract class  接口	interface

​	2.构造器-- 接口中没有构造器

​	3.属性 -- 接口重点属性都是public static final

​	4.方法 -- 抽象类中可以有实例方法和抽象方法，接口中的方法都是抽象的（jdk1.8可以有默认方法）

​	5.抽象类必须有子类继承，需要重写抽象方法；接口必须有实现类，要实现抽象方法	无论是子类 还是实现类，如果是抽象的可以不重写抽象方法

​	6.抽象类	倾向属性的相同（同一种类型）；接口--功能相同（有相同的方法）
```





一.抽象类

```
	抽象类是用abstract修饰的类,在抽象类中可以拥有抽象方法和普通方法,也可以只有普通方法但是没有意义.
	当我们抽取事物的共性组成父类时,如果在父类中并不能够具体的实现某个方法时.可以将这个方法定义为抽象方法,这个类为抽象类.
```

二.接口

```
接口是用interface修饰的, 用来扩充具体类的功能.
```

三.抽象类与接口的区别

```
1.成员不同:
	构造方法:
		接口中没有构造方法,抽象类有构造方法但是不能直接创建对象
	成员方法:
		接口中成员方法默认添加 public abstract 修饰,只能存在抽象方法;
		抽象类中既有抽象方法也有普通方法
	成员变量:
		接口中的成员变量默认添加static final 修饰,只有公开静态常量.
		抽象类中的变量没有这个限制
2.关系不同:
	类与类之间的关系是继承:extends;
	接口与接口之间的关系是继承:extends;
	类与接口之间的关系是实现:implements;子类称为子实现类
3.设计思想不同:
	抽象类是让子类继承的,体现的是一种"is a"的理念,并且子类只能继承一个父类;
	是为了子类扩充功能,体现的是"like a"的理念,一个子实现类可以同时实现多个接口 .
```

四.抽象类与接口的联系

```
1.都可以拥有抽象方法;
2.都不可以直接创建对象;
3.都依靠于子类存在才有意义,子类必须实现其所有的抽象方法
4.都可以实现多态
```



## 8.面向接口编程：

依赖接口不依赖实现



## 9.多态

​	一个对象的多种表现形式

​	编译期 

​	运行时

​	语法: 父类名称= new 子类()			 接口名称 = new 实现类()

属性向上转型原则：eg:声明为什么即为什么，父类覆盖子类，父类子类只输出父类

```
实现多态的条件：
1.继承：必须要有子类继承父类的继承关系。
2.重写：子类需要对父类中的一些方法进行重写，然后调用方法时就会调用子类重写的方法而不是原本父类的方法。
3.向上转型：在多态中需要将子类的引用赋给父类对象，只有这样该引用才能够具备技能调用父类的方法和子类的方法。
```

分析：子类win1重载了tostring()方法，重写了Tostring()方法，当我们调用a.tostring()方法时，因为向上转型的原则，先会调用父类中的tostring()方法（子类中的tostring()重载后丢失），在调用子类中的Tostring()方法。



应用场景：

里氏代换法则--lsp : 父类对象出现的地方都可以使用子类对象替换多态参数 

-- instanceof 判断对象的类型

```
if(pet instanceof Dog){

Dog d = (Dog)pet;//下型转型d.s();
```





# **7.26** 

## 1.**jdk：API**

​		-- 应用程序接口--别人写好的功能



### 1.1Math类：

| 方法名                                      | 说明                                |
| ------------------------------------------- | ----------------------------------- |
| public static int abs(int a)                | 获取参数a的绝对值                   |
| public static double ceil(double a) [ce’l]  | 向上取整                            |
| public static double floor(double a)        | 向下取整                            |
| public static long round(double a)          | 四舍五入取整                        |
| public static int max(int a,int b)          | 返回两个数中较大值                  |
| public static int min(int a,int b)          | 返回两个数中较小值                  |
| public static double pow(double a,double b) | 获取a的b次幂                        |
| public static double random()               | 返回值为double类型随机数 [0.0~1.0） |
| Math.sqrt(4)                                | 开平方                              |
| Math.E                                      | 常数e                               |
| Math.PI                                     | 常数Π                               |



### 1.2 **日期类**

#### 1.2.1**Date类**

- **构造方法**

| 方法名                 | 说明                           |
| ---------------------- | ------------------------------ |
| public Date()          | 创建当前系统的此刻日期时间对象 |
| public Date(long time) | 把时间毫秒值转换成日期对象     |



- **常用方法**

| 方法名                         | 说明                                                |
| ------------------------------ | --------------------------------------------------- |
| public long getTime()          | 获取日期对象从1970年1月1日00：00：00 到现在的毫秒值 |
| public void setTime(long time) | 设置时间，给的是毫秒值                              |

##### 1.2.1.1 SimpleDateFormat类 [ˈsɪmpl]

- 可以对日期格式化和解析

- 日期和时间格式由日期和时间模式字符串指定，在日期和时间模式字符串中,从 ‘A’ 到 ‘Z’ 以及从 ‘a’ 到’z’ 

- 引号的字母被解释为表示日期或时间字符串的组件的模式字母

- 常用的模式字母对应： y—年；M—月；d—日；H—时；m—分；s—秒；E—星期几；a—上午 / 下午

- **构造方法**：

| 方法名                                  | 说明                                 |
| --------------------------------------- | ------------------------------------ |
| public SimpleDateFormat()               | 使用默认模式和日期模式               |
| public SimpleDateFormat(String pattern) | 指定时间的格式创建简单日期格式化对象 |



- **格式化和解析日期方法**

| 方法名                                  | 说明                                |
| --------------------------------------- | ----------------------------------- |
| public String format(Date date)         | 将日期格式化为日期 / 时间字符串     |
| public String format(Object time)       | 将时间毫秒格式化为日期 / 时间字符串 |
| public Date parse(String source) [pɑːz] | 从给定的字符串开始解析文本生成日期  |



eg:

```
public class TestDate {
    public static void main(String[] args) throws ParseException {

        Date d = new Date();
        System.out.println(d);//Wed Jul 26 10:18:25 CST 2023

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss E a");
        String s = sdf.format(d);
        System.out.println(s); //2023年07月26日 10:18:25 星期三 上午

        SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        Date d1 = sdf1.parse(s); //parse报错了，选中按下Alt+enter，默认选第一个
        System.out.println(d1); //Wed Jul 26 10:18:25 CST 2023

    }
}
```



#### 12.2 **Calender类**

- Calendar 代表了系统此刻日期对应的日历对象
- Calendar 是一个抽象类，不能直接创建对象
- **常用方法**

| 方法名                                             | 说明                                                   |
| -------------------------------------------------- | ------------------------------------------------------ |
| public static Calendar getInstance()               | 返回一个日历类的对象                                   |
| public int get(int field)                          | 返回给定日历的值                                       |
| public void set(int field,int value)               | 修改日历的某个字段信息                                 |
| public abstract void add(int field,int amount)     | 根据日历的规则，将指定的时间量添加或减去给定的日历字段 |
| public final void set(int year,int month,int date) | 设置当前日历年月日                                     |



```
Calendar c = Calendar.getInstance();
c.set(2021,10,5);
int year = c.get(Calendar.YEAR);
int month = c.get(Calendar.MONTH)+1;
int day = c.get(Calendar.DATE);
int week = c.getWeeksInWeekYear();// int week = c.get(Calendar.WEEK_OF_YEAR);
System.out.println("year:"+year+"\tmonth:"+month+"\tday:"+day+"\tweek:"+week);

 //Calendar 转换为 Date
        Date d =  c.getTime();
        System.out.println(d);
```



### 1.3 **Object类**

​	toString :对象转字符串

```
@Override
public String toString() {
    return "TestObject{" +
            "name='" + name + '\'' +
            ", age=" + age +
            '}';
}
```

​	equals:比较两个对象是否相等--默认情况下比较-->是否是同一块内存

- ​	默认是比较两个对象的地址是否相同，相同返回true

- 直接比较两个对象的地址是否完全相同，可以用"=="替代equals
- 所以 equals 存在的意义是为了被子类**重写**

​	hashcode: 	jvm--同一个对象的hash应该是相同的      --> 重写equals 必重写hashcode

- == 和 equals 区别

​	== ： 可以比较基本类型和引用类型

​				基本类型：值是否相等

​				引用类型：地址是否相等

 equals : 只能比较引用类型

​			默认：比较是否是同一个对象

​			重写：按照重写逻辑比较

另： == 为true equals 一定为true

​		equals 为true ==不一定为true(未重写)



### 1.4 **String**

```
（1）常见String类的获取功能

length：获取字符串长度；
charAt(int index)：获取指定索引位置的字符；
indexOf(int ch)：返回指定字符在此字符串中第一次出现处的索引；
// System.out.println(s.lastIndexOf("f")); 倒数
substring(int start)：从指定位置开始截取字符串,默认到末尾；
substring(int start,int end)：从指定位置开始到指定位置结束截取字符串；

（2）常见String类的判断功能

equals(Object obj)： 比较字符串的内容是否相同,区分大小写；
//System.out.println( s.equalsIgnoreCase("saffF"));忽略大小写
contains(String str): 判断字符串中是否包含传递进来的字符串；
startsWith(String str): 判断字符串是否以传递进来的字符串开头；
endsWith(String str): 判断字符串是否以传递进来的字符串结尾；
isEmpty(): 判断字符串的内容是否为空串""；

（3）常见String类的转换功能

byte[] getBytes(): 把字符串转换为字节数组；
char[] toCharArray(): 把字符串转换为字符数组；
String valueOf(char[] chs): 把字符数组转成字符串。valueOf可以将任意类型转为字符串；
toLowerCase(): 把字符串转成小写；
toUpperCase(): 把字符串转成大写；
concat(String str): 把字符串拼接；

（4）常见String类的其他常用功能

replace(char old,char new) 将指定字符进行互换
replace(String old,String new) 将指定字符串进行互换
trim() 去除两端空格
int compareTo(String str) 会对照ASCII 码表 从第一个字母进行减法运算 返回的就是这个减法的结果，如果前面几个字母一样会根据两个字符串的长度进行减法运算返回的就是这个减法的结果，如果连个字符串一摸一样 返回的就是0。

String[] split(String regex)
		根据给定正则表达式的匹配拆分此字符串；
//	 String ss = "aaa#ddd#ccc";
        String[] arr = ss.split("#");
        for(String s1:arr){
            System.out.println(s1);
        }
```



#### --深入理解string

##### 1、String类的特性

- String是被final修饰的类，不能被继承；
- String实现了Serializable和Comparable接口，表示String支持序列化和可以比较大小；
- String底层是通过char类型的数据实现的，并且被final修饰，所以字符串的值创建之后就不可以被修改，具有不可变性。

##### 2、深入理解String的不可变性

- 总结1：String字符串具有不可变性，当字符串重新赋值时，不会在原来的内存地址进行修改，而是重新分配新的内存地址进行赋值。
- 总结2：当字符串进行拼接时，也不会在原来的内存地址进行修改，而是重新分配新的内存地址进行赋值。
- 总结3：当调用String的replace方法修改指定的字符或字符串时，也不会在原来的内存地址进行修改，也是重新分配新的内存地址进行赋值。

##### 3、String实例化的两种方式

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071210484861.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yX3d4Yw==,size_16,color_FFFFFF,t_70)

```
//1.通过字面量方式为字符串赋值时，此时的字符串存储在方法区的字符串常量池中
String s1="hello";
String s2="hello";

//2.通过new+构造器方式实例化字符串时，字符串对象存储在堆中
String s3=new String("hello");
String s4=new String("hello");

System.out.println(s1==s2);//true
System.out.println(s1==s3);//false
System.out.println(s1==s4);//false
System.out.println(s3==s4);//false
```

- **面试题**：使用String str=new String(“hello”)方式创建对象，一共创建了几个对象？

  一共会创建两个对象，一个是使用new创建的对象，存储在堆中；另一个是常量对象"hello"，存储在字符串常量池中。

##### 4、String不同拼接方式的对比

     public static void main(String[] args) {
        String s1="Hello";
        String s2="World";
    
        String s3="HelloWorld";
        String s4="Hello"+"World";
        String s5=s1+"World";
        String s6="Hello"+s2;
        String s7=s1+s2;
    
        System.out.println(s3==s4); //true
        System.out.println(s3==s5); //false
        System.out.println(s3==s6); //false
        System.out.println(s3==s7); //false
        System.out.println(s5==s6); //false
        System.out.println(s5==s7); //false
        System.out.println(s6==s7); //false
    
        String s8=s5.intern();
        System.out.println(s3==s8); //true
    }



(1)Java中有常量优化机制，“Hello"和"World"本身就是字符串常量，所以在编译时，会直接把"Hello"和"World"合并成"HelloWorld"字符串，又因为在执行s3的时候已经在常量池中创建了"HelloWorld”，所以s3==s4。
(2)当变量与字面量或变量与变量进行拼接时，会在堆中创建一个StringBuilde对象，然后使用StringBuilder的append()方法将变量与字面量或变量与变量进行拼接，最后调用toString()方法转成String对象。所以s5、s6、s7指向的都是堆内存中String对象的地址值。
(3)使用intern()这个方法时，首先会检查字符串常量池中是否有对应的字符串，如果存在则返回这个字符串的引用；否则会先将字符串添加到字符串常量池中，然后再返回这个字符串的引用。所以s3==s8。

# 7.27

## 1.异常

### 1.1分类：

​	运行时异常：非检查的异常（unchecked exceptions）

​	编译时异常：检查异常（checked exceptions  --  必须在编译时处理，否则不能编译

运行时异常: RuntimeException及其子类，编译阶段不会出现异常提醒。运行时出现的异常(如:数组索引越界异常)

编译时异常:编译阶段就会出现异常提醒的。 (如:日期解析异常)

### 1.2异常和错误区别：

​	错误：通过编写代码能够改正的

​	异常：不能通过编写代码控制



异常作用：

异常作用一:异常是用来查询bug的关键参考信息

异常作用二:异常可以作为方法内部的一种特殊返回值，以便通知调用者底层的执行情况





### 1.3体系结构：

​	Exception: 异常

​	Error: 错误

![img](https://img-blog.csdnimg.cn/721cce36b3f741a388d0a3b61fc6da07.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oiR5piv5rOi5ZOp5Liq5rOi,size_16,color_FFFFFF,t_70,g_se,x_16)



### 1.4常见异常：



| 异常提示                          | 解释                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| ArithmeticException:              | 算术运算异常，除数为0，抛出该异常；                          |
| java.lang.RuntimeException:       | 运行时异常                                                   |
| ClassCastException:               | 类类型转换异常，当试图将对象强制转换为不是实例的子类时，抛出该异常； |
| NullPointerException:             | 空指针异常，通过null进行方法和属性调用会抛出该异常；         |
| ArrayIndexOutOfBoundsException:   | 数组下标越界异常，当你使用不合法的索引访问数组时会抛出该异常； |
| NumberFormatException:            | 数字转换异常，当试图将一个String转换为指定的数字类型，而该字符串确不满足数字类型要求的格式时，抛出该异常； |
| InputMismatchException:           | 输入不匹配异常，输入的值数据类型与设置的值数据类型不能匹配。 |
| java.io.IOExeption:               | 输入输出异常                                                 |
| FileNotFoundException:            | 文件找不到异常，通常是两种情况：1、系统找不到指定的路径 2、拒绝访问（指定的是目录时，就会报拒绝访问异常） |
| EOFException:                     | 文件已结束异常，抛出EOFException一定是因为连接断了还在继续read； |
| java.lang.ClassNotFoundException: | 类找不到异常，当我们通过配置文件去查找一个类的时候，如果配置路径写错，就会抛出该异常，比如：web.xml文件中根本就不存在该类的配置或者配置的路径写错；（比较常见） |
| java.sql.SQLException:            | SQL异常，数据库的各种信息的异常；                            |






### 1.5异常处理机制：

​	针对checked异常

#### 1.5.1异常处理机制一：	try-catch-finally           

语法格式：

```
        try{
​            ...... //捕获异常，可能产生异常的代码 --  发生异常 跳到catch中，异常代码后的代码都不执行
​        }// try中发生的异常和catch中处理的异常yihzh
​        catch( ExceptionName1 e ){
​            ...... //当产生ExceptionName1型异常时的处置措施
​        }
​        catch( ExceptionName2 e ){
​            ...... //当产生ExceptionName2型异常时的处置措施
​        }
​        [ finally{
​            ...... //无论是否发生异常，都无条件执行的语句
​        } ]  //可选，finally主要做一些清理工作，如流的关闭，数据库连接的关闭等。


```



```
public class Test_Input_01 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        /*
		 * 当我们只写一个try{}的时候,会报错:
		 * 	Syntax error, insert "Finally" to complete TryStatement
		 * 	语法错误，插入“Finally”来完成Try块
		 * 
		 * 总结: try不能单独存在,必须结合catch或finally来使用
		 * 	try块中没有异常,会执行finally(如果有)
		 *  try块中有异常,会执行对应的catch块(如果有),try中异常发生点之后的代码将不会执行
		 */
        try{
            //try块中放可能发生异常的代码。
            //如果执行完try且不发生异常，则接着去执行finally块和finally后面的代码（如果有的话）。
            //如果发生异常，则尝试去匹配catch块。异常点之后的代码不会运行

            //这行代码有可能出错
            int num1 = sc.nextInt(); //这行代码如果出现异常,那么后面的输出语句就不执行
     
            int num2 = sc.nextInt();
     
            System.out.println(num1+"\t"+num2);
     
            System.out.println(num1/num2);
            
                    String str = null;
        System.out.println(str.charAt(0));
 
    }catch(InputMismatchException | NullPointerException e) { 
        // catch(异常对象)	当异常发生了,catch就会捕获对应的异常
        // 每一个catch块用于捕获并处理一个特定的异常，或者这异常类型的子类。Java7中可以将多个异常声明在一个catch中。 catch(Exception1 | Exception2 | Exception3 e)
        // catch后面的括号定义了异常类型和异常参数。如果异常与之匹配且是最先匹配到的，则虚拟机将使用这个catch块来处理异常。
        // 在catch块中可以使用这个块的异常参数来获取异常的相关信息。异常参数是这个catch块中的局部变量，其它块不能访问。
        // 如果当前try块中发生的异常在后续的所有catch中都没捕获到，则先去执行finally，然后到这个函数的外部caller中去匹配异常处理器。
        // 如果try中没有发生异常，则所有的catch块将被忽略。
        System.out.println("catch块 - try里面发生了异常 - 空指针和输入不匹配异常都走这个Catch");
    }catch(java.lang.ArithmeticException e){
        e.getMessage();
        System.out.println("算数异常:除数不能为0");
 
    }catch(Exception e){
        System.out.println("程序发生未知异常");
    }finally {
        // finally块通常是可选的。
        // 无论异常是否发生，异常是否匹配被处理，finally都会执行。
        // 一个try至少要有一个catch块，否则， 至少要有1个finally块。但是finally不是用来处理异常的，finally不会捕获异常。
        // finally主要做一些清理工作，如流的关闭，数据库连接的关闭等。 
        System.out.println("finally块");
    }
 
    System.out.println("异常捕获之后的代码");
}
}	


```

##### 1.5.1.1finally块和return

（1）一个不容易理解的事实：在 try块中即便有return，break，continue等改变执行流的语句，finally也会执行。

（2）finally中的return 会覆盖 try 或者catch中的返回值。

另： 如果 try 中有return finally也要执行，在return 前执行，把值暂存起来



#### 1.5.2异常处理机制二： throw 

声明异常
	在方法上throws异常--调用方法时 需要处理

​	调用者处理--- (否) ---jvm 

抛出异常:

​	在方法内 手动抛出 throw ----自定义异常

​	如果抛出的是RuntimeException 方法上不需要声明，如果抛出Checked异常，方法上需要声明

​	可以有多个catch--每个catch处理不同的异常，父异常要写在下边



匿名内部类：

​	必须有接口或抽象类



# 2.集合

---- 能够储存多个数据



![在这里插入图片描述](https://img-blog.csdnimg.cn/adf66ce8c546460ebe17a6add26956a8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfNTE3NTE0NTI=,size_18,color_FFFFFF,t_70,g_se,x_16)

## 2.1与数组区别

![这里写图片描述](https://img-blog.csdn.net/20180803193134355?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaXlhbmFmZmVjdGlvbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

​	Collection&&Map

## 2.2Collection	

### 2.2.1Collection集合的方法

![这里写图片描述](https://img-blog.csdn.net/20180803193423722?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaXlhbmFmZmVjdGlvbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

```
ArrayList list = new ArrayList();
list.add(123);
list.add("asd");
list.add("asd");
list.add(true);
System.out.println(list);
list.add(1,"ttt");//指定位置插入
System.out.println(list);

ArrayList lst = new ArrayList();
        lst.add(345);
        lst.add(567);
        list.add(lst);//将lst整体作为一个元素加入到list后
        list.addAll(lst);//将lst元素逐个补充到list后
        System.out.println(list);
```



```
List list = new ArrayList();
list .add(1);
list.add(2);
list.add(3);

list.remove(1);//默认为index 索引
System.out.println(list);

list.remove(new Integer(1));//按值移除
System.out.println(list);
```



### 2.2.2常用集合的分类：

Collection 接口的接口 对象的集合（单列集合）
├——-List 接口：元素按进入先后有序保存，可重复
│—————-├ LinkedList 接口实现类， 链表， 插入删除， 没有同步， 线程不安全
│—————-├ ArrayList 接口实现类， 数组， 随机访问， 没有同步， 线程不安全
│—————-└ Vector 接口实现类 数组， 同步， 线程安全
│ ———————-└ Stack 是Vector类的实现类
└——-Set 接口： 仅接收一次，不可重复，并做内部排序
├—————-└HashSet 使用hash表（数组）存储元素
│————————└ LinkedHashSet 链表维护元素的插入次序
└ —————-TreeSet 底层实现为二叉树，元素排好序



**list -- 有序可重复集合**	

![这里写图片描述](https://img-blog.csdn.net/20180803201736883?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaXlhbmFmZmVjdGlvbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

#### 2.2.2.1 ArrayList： 

​		

##### **1、底层原理（面试常考）： **

Object数组 --> 查询快

​			  （1）三种方式创建ArrayList

```
1、new ArrayList() 初始化数组长度为10

2、new ArrayList(len) -- 直接以len作为长度 初始化数组

3、new ArrayList(集合) -- 直接把集合转成数组赋值给存储对象
```

​				（2）add方法

```
是否需要扩容 -- 默认扩容1.5，但需要根据minCapacity判断 
如果minCapacity > 扩容1.5倍后的值，就以minCapacity新容量，
且新容量不能超出整数范围 
```

​				增加元素

#### 2.2.2.2 LinkedList -- 

1. 底层原理：双向链表 --> 插入和删除快

​		

set -- 无序不可重复集合





# 7.29

#### 2.2.2.3 vector



```
Vector v = new Vector();
        v.add(13);
        v.add(456);
        v.add("abc");
        System.out.println(v.size());
        System.out.println(v.get(1));
        int cap = v.capacity();

        System.out.println(cap);

        v.addElement("def");
        Object obj = v.elementAt(2);//get
        System.out.println(obj);

        Object f = v.firstElement();//返回第一个元素
        System.out.println(f);

        Enumeration enums = v.elements();//返回集合中的所有元素，返回的是Enumeration
        while(enums.hasMoreElements()){//判断末尾是否为空
            System.out.println(enums.nextElement());
```



##### 1、底层源码

​	数组 -- 默认创建10个长度的数组

​	扩容 ： capacityIncrement >0 ? old +capacityIncrement : old*2



​	线程安全的

总结：
(01) Vector实际上是通过一个**数组**去保存数据的。当我们构造Vecotr时；若使用默认构造函数，则Vector的默认容量大小是10。
(02) 当Vector容量不足以容纳全部元素时，Vector的容量会增加。若容量增加系数 >0，则将容量的值增加“容量增加系数”；否则，将容量大小增加一倍。
(03) Vector的克隆函数，即是将全部元素克隆到一个数组中。

#### 2.2.4 Set

无序不可重复集合 -- 如何判断重复（qeuals--hashmap)

##### 1、底层

HashSet 底层： HashMap --> 以存储元素作为HashMap的key，值是个固定的对象



```
HashSet set = new HashSet();
    set.add("123");
    set.add("456");
    set.add("abc");
    set.add("abc");
    System.out.println(set.size());
    System.out.println(set);

//两种遍历方法
    Iterator iterator = set.iterator();
    while(iterator.hasNext()){
        System.out.println(iterator.next());
    }

    System.out.println("---");
    for(Object obj : set){
        System.out.println(obj);
    }
}
```



## 2.3Map

​	键值对 	key -- value

​	HashMap

​	

```
Map map= new HashMap();

map.put("name","z3");
map.put("age",21);
map.put(new Date(),123);
map.put("sname","z4");

System.out.println(map.size());
System.out.println(map);

System.out.println(map.get("age"));

System.out.println(map.containsKey("age"));
System.out.println(map.containsValue(123));

Map m = new HashMap();
m.put("sex","male");

map.putAll(m);
System.out.println(map.size());
System.out.println(map);

//------------------------------------------------

//遍历

//1.通过键找值的方法；
Set keys = map.keySet();//返回key的集合Set
for(Object key : keys){
    System.out.println(key+"--"+map.get(key));
}
System.out.println("------");
//2.获取所有的value
Collection vs = map.values();//获取所有的value
for(Iterator it = vs.iterator(); it.hasNext();){
    System.out.println(it.next());

    System.out.println("----");
    //3.使用entry对象,利用set遍历
    //Map.Entry<K,V>,在Map接口中有一个内部接口Entry（内部类）
    //作用：当集合一创建，就会在Map集合中创建一个Entry对象，用来记录键与值（键值对对象，键值的映射关系）
    Set entries = map.entrySet();
    for(Object obj : entries){
        Map.Entry entry = (Map.Entry)obj;
        System.out.println(entry.getKey()+"---"+entry.getValue());
    }
}
```



### 2.3.1 HashMap

【1】.特点：

1.HashMap底是哈希表，查询速度非常快（jdk1.8之前是数组+单向链表，1.8之后是数组+单向链表/红黑树 ，链表长度超过8时，换成红黑树）

2.HashMap是无序的集合，存储元素和取出元素的顺序有可能不一致

3.集合是不同步的，也就是说是多线程的，速度快

**【2】**.HashMap存储自定义类型键值

HashMap存储自定义类型键值，Map集合保证key是唯一的：作为key的元素，必须重写hashCode方法和equals方法，以保证key唯一



对key取哈希



#### 1、底层源码（面试常考）

- 默认初始化16长度Node数组，put -- 计算key 的 hash(找到数组中的储存元素)，
- 如果这个位置没有元素--直接放这，
- 如果有元素，判断是链表还是红黑树，
- 链表--深度是否超过8，没有超过，直接放到链表尾部，如果超过，转成红黑树，再储存这个节点
- 红黑树--深度超过6 -- 扩容 没超过直接添加

#### 2.3.1.1 例：map三种遍历方法

```
Map map= new HashMap();

map.put("name","z3");
map.put("age",21);
map.put(new Date(),123);
map.put("sname","z4");

System.out.println(map.size());
System.out.println(map);

System.out.println(map.get("age"));

System.out.println(map.containsKey("age"));
System.out.println(map.containsValue(123));

Map m = new HashMap();
m.put("sex","male");

map.putAll(m);
System.out.println(map.size());
System.out.println(map);

//1.通过键找值的方法；
Set keys = map.keySet();//返回key的集合Set
for(Object key : keys){
    System.out.println(key+"--"+map.get(key));
}
System.out.println("------");
//2.获取所有的value
Collection vs = map.values();//获取所有的value
for(Iterator it = vs.iterator(); it.hasNext();){
    System.out.println(it.next());

    System.out.println("----");
   // 3.使用entry对象,利用set遍历
    //Map.Entry<K,V>,在Map接口中有一个内部接口Entry（内部类）
    //作用：当集合一创建，就会在Map集合中创建一个Entry对象，用来记录键与值（键值对对象，键值的映射关系）
    Set entries = map.entrySet();
    for(Object obj : entries){
        Map.Entry entry = (Map.Entry)obj;
        System.out.println(entry.getKey()+"---"+entry.getValue());
    }
}
```



### 2.3.2 Hashtable

#### 2.3.2.1 与 HashMap 对比

| Hashtable                                                    | HashMap                                                    |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| 底层也是哈希表，是同步的，是一个单线程结合，是线程安全的集合，速度慢 | 底层也是哈希表，但是线程不安全的集合，是多线程集合，速度快 |
| 不能存储null键，null值                                       | （还有之前学的所有集合）：都可以存储null键，null值         |


#### 2.3.2.2 例1：嵌套

```
 List<Map<String,String>> market = new ArrayList<>();

        Map<String,String> m1 = new HashMap<>();
        m1.put("纸","z1");
        m1.put("盆","p1");

        Map<String,String> m2 = new HashMap<>();
        m1.put("足球","f");
        m1.put("篮球","b");
11
        Map<String,String> m3 = new HashMap<>();
        m1.put("啤酒","bear");
        m1.put("白酒","drink");

        market.add(m1);
        market.add(m2);
        market.add(m3);

        for(Map<String,String> map : market){
            for(Map.Entry<String,String> entry : map.entrySet()){
                System.out.println(entry.getKey()+"---"+entry.getValue());
            }
        }
```





#### 2.3.2.3 例2：给对象排序方法

```
Person[] ps = new Person[3];
Person p1 = new Person(32);
Person p2 = new Person(23);
Person p3 = new Person(28);

ps[0] = p1;
ps[1] = p2;
ps[2] = p3;

//1.给对象排序方式
Arrays.sort(ps, new Comparator<Person>() {
    @Override
    public int compare(Person o1, Person o2) {
        return o1.age-o2.age;
       // return -(o1.age-o2.age);//逆序括号前加-
    }
});

for(Person p :ps){
    System.out.println(p);
}
//---------------------------------------------
//2.接口
ublic class Person implements Comparable<Person>{
...

  @Override
    public int compareTo(Person o) {
        return this.age-o.age;
    }

}
...
 Arrays.sort(ps);
        for(Person p :ps){
            System.out.println(p);
        }

```



## StringBuffer



例：

```
//可变字符串，再原有基础上操作
StringBuffer sb1 = new StringBuffer();//多线程时

//StringBuilder sb2 = new StringBuilder("123");//API一样，单线程快
sb1.append("abc");

//不为String型，强转

sb1.delete(1,3);  //[1,3)
sb1.insert(4,"123");

String s = sb1.toString();
System.out.println(s);
```



## Collections

例：



```
  Collections.sort(）
 
 List l1 =new ArrayList();
 l1.add(1);
 l1.add(2);
l1.add(5);

 List l2 =new ArrayList();
 l2.add(3);
 l2.add(4);
 //l2.add(6);

 Collections.copy(l1,l2);//要求l1.size()>=l2.size()

 for(Object o1 : l1){
     System.out.println(o1);
 }
 System.out.println("-----");

 for(Object o2 : l2){
     System.out.println(o2);
 }


 Collections.reverse(l1); //颠倒
 for(Object o1 : l1){
     System.out.println(o1);
 }

 Collections.shuffle(l1); //打乱
 System.out.println(l1.toString());
 
 Collections.swap(l1,0,2);//交换位置
 System.out.println(l1.toString());
```





# 7.30

## 1.File

### 1.1 什么是File类
​        Java文件类以抽象的方式代表文件名和目录路径名。该类主要用于文件和目录的创建、文件的查找和文件的删除等。File类在java.io包里。
​        说的通俗易懂就是，file就是指一个文件或文件夹，文件及文件夹的创建、删除需要用到它，可以通过他获取文件的各种信息，但是不能获取文件的内容！！要获取文件的内容需要用到其他的类。

### 1.2 File类的常用操作

#### 1.2.1创建一个File实例

```
f = new File("text3.txt");
File f = new File("D:\\soft\\IDE JAVA\\demo")
```

在括号内直接输入文件目录的路径，

第一行的路径为相对路径，可以直接写文件名，但是文件要放在该项目的文件夹下，否则是无法找到该文件的；

第二行为绝对路径，即无论文件放在何处，都能找到。而此时的f或者f1指的就是路径对应下的文件。

注意：在Java中‘\’是转义符，用\\或/表示文件的分隔符


#### 1.2.2 File中常用方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210616175436943.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg4NDIzNA==,size_16,color_FFFFFF,t_70)



#### 1.2.3 判断文件是否存在：

```
if(!f.exists()){
   try {
       f.createNewFile();
   }catch (IOException e){
       e.printStackTrace();
   }
```



#### 1.2.4遍历（递归）

例：遍历目录下的文件名称，包含子目录

```
static  void print(File file){
    if(file.isFile()){
        System.out.println(file.getName());
    }else{
        for(File f : file.listFiles()){
            print(f);
        }
    }
}
```



## 2.IO

### 一、概念：
#### 1.1. 什么是I/O
操作系统中，内存与外部存储设备之间交换数据，即IO。
Java通过输入流和输出流完成IO功能，从而实现和外设的数据交互。

#### 1.2. I/O流
处理JVM内存和外设之间的数据传输。
Java通过流（stream）的方式完成数据传输.

#### 1.3. 流模型：
在外设和JVM内存之间建立一个数据传输通道（数据传输通道是在创建流对象时创建的）。
让数据在通道上流动起来。



### 二、流的分类

​	流--

​		传输数据类型：

​			字节流 --按字节传输---非文本--图片 音视频

​			字符流 -- 按字符传输

​		数据的流向:

​			输入流---InputStream()   Reader（）

​			输出流---OutputStream Writer

​		是否与节点相连：

​			节点流---直接操作节点

​			处理流 ---关联其它流  InputStreamReader



### 三、例

#### 3.1例，字节流：

```
public class Test3 {
    public static void main(String[] args) {
        InputStream is = null;
        OutputStream os = null;
        try {
            //法一：一个字节一个字节，了解
          /*   is = new FileInputStream("t.txt");
             os = new FileOutputStream("b.txt");
            int c = is.read();
            while (c != -1){
                os.write(c);
                c=is.read();
                //System.out.println(c);
            }
*/
            //法二：存缓冲区
            is = new FileInputStream("t.txt");
            os = new FileOutputStream("b.txt");
            byte[] buffer = new byte[64];//缓冲区
            int c = is.read(buffer);//把读取的字节放入buffer中
            while (c != -1){
                os.write(buffer,0, buffer.length);
                c=is.read(buffer);
                System.out.println(c);
            }

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if(os!=null){
                try {
                    os.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }

            }
            if(is!=null){
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```



#### 3.2例，字符流：



```
public class Test4 {
    public static void main(String[] args) {
        Reader reader = null;
        Writer writer = null;
        try {
            reader = new FileReader("t.txt");
            writer = new FileWriter("b.txt");
            char[] buffer = new char[4];
            int c = reader.read(buffer);
            while(c!=-1){
                writer.write(buffer,0, buffer.length);
                c = reader.read(buffer);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            if(writer!=null){
                try {
                    writer.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(reader!=null){
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
```



#### 3.3例，处理流：

```
public class Test5 {
    public static void main(String[] args) {
        InputStream is =null;
        InputStreamReader isr = null;
        Writer writer = null;
        try {
            is = new FileInputStream("t.txt");
            writer = new FileWriter("b.txt");
            isr = new InputStreamReader(is);
            char[] buffer = new char[4];
            int len;
            while((len=isr.read(buffer))!=-1){
                writer.write(buffer,0, len);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            if(writer!=null){
                try {
                    writer.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(is!=null){
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
```



#### 3.4整行读

```
public class Test {
    public static void main(String[] args) {

        Reader reader = null;
        Writer writer = null;
        BufferedReader br =null;
        BufferedWriter bw =null;

        try {
            reader = new FileReader("t.txt");//节点流
            writer = new FileWriter("b.txt");
            br = new BufferedReader(reader);//处理流
            bw = new BufferedWriter(writer);

            String line = br.readLine();//按行读

            while(line!=null){
                bw.write(line,0,line.length());
                bw.newLine();//换行
                line = br.readLine();
                System.out.println(line);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            if(br!=null){
                try {
                    br.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(bw!=null){
                try {
                    bw.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

        }
    }
```



### 四、序列化与反序列化（暂先了解）

序列化 --反序列化

对象--存在磁盘

当对象的创建开销较大，使用不频繁--适用于序列化



#### 4.1 理解Java序列化和反序列化
Serialization(序列化)：将java对象以一连串的字节保存在磁盘文件中的过程，也可以说是保存java对象状态的过程。序列化可以将数据永久保存在磁盘上(通常保存在文件中)。

deserialization(反序列化)：将保存在磁盘文件中的java字节码重新转换成java对象称为反序列化。

#### 4.2序列化和反序列化的应用
​	两个进程在远程通信时，可以发送多种数据，包括文本、图片、音频、视频等，这些数据都是以二进制序列的形式在网络上传输。

​	java是面向对象的开发方式，一切都是java对象，想要在网络中传输java对象，可以使用序列化和反序列化去实现，发送发需要将java对象转换为字节序列，然后在网络上传送，接收方收到字符序列后，会通过反序列化将字节序列恢复成java对象。

java序列化的优点：
	实现了数据的持久化，通过序列化可以把数据持久地保存在硬盘上(磁盘文件)。
利用序列化实现远程通信，在网络上传输字节序列。

#### 4.3序列化和反序列化地实现
1.JDK类库提供的序列化API:

- java.io.ObjectOutputStream    

  表示对象输出流，其中writeObject(Object obj)方法可以将给定参数的obj对象进行序列化，将转换的一连串的字节序列写到指定的目标输出流中。

- java.io.ObjectInputStream

  该类表示对象输入流，该类下的readObject(Object obj)方法会从源输入流中读取字节序列，并将它反序列化为一个java对象并返回。

序列化要求：

实现序列化的类对象必须实现了Serializable类或Externalizable类才能被序列化，否则会抛出异常。属性--transientl修饰的属性不能序列化，不保存此类的值



# 7.31

## 一、线程（初识）

### 1.并发和并行

并发:在同一时刻，有多个指令在单个CPU上**交替**执行

并行:在同一时刻，有多个指令在多个CPU上**同时**执行

### 2.实现方式：

​	（1）继承Thread类--重写run-线程启动时 自动执行的方法

​	（2）实现Runnable接口

​	启动线程的方式start()

​	priority:优先级1--10 --> 优先级越高，被执行的几率越大，不代表一定





### +12102.线程的生命周期

1. 新建状态
2. 就绪状态
3. 运行状态
4. 阻塞状态
5. 死亡状态

新建状态（New）：至今尚未启动的线程的状态。线程刚被创建，但尚未启动。如：Thread t = new MyThread();

就绪状态（Runnable）：当调用线程对象的start()方法（t.start();），线程即进入就绪状态。处于就绪状态的线程，只是说明此线程已经做好了准备，随时等待CPU调度执行，并不是说执行了t.start()此线程立即就会执行；

运行状态（Running）：当CPU开始调度处于就绪状态的线程时，此时线程才得以真正执行，即进入到运行状态。注：就 绪状态是进入到运行状态的唯一入口，也就是说，线程要想进入运行状态执行，首先必须处于就绪状态中；

阻塞状态（Blocked）：处于运行状态中的线程由于某种原因，暂时放弃对CPU的使用权，停止执行，此时进入阻塞状态，直到其进入到就绪状态，才有机会再次被CPU调用以进入到运行状态。根据阻塞产生的原因不同，阻塞状态又可以分为三种：

1）等待阻塞—位于对象等待池中的阻塞状态（Blocked in object’s wait pool）：当线程处于运行状态时，如果执行了某个对象的wait()方法，Java虚拟机就会把线程放到这个对象的等待池中，这涉及到“线程通信”的内容。

2）同步阻塞 --位于对象锁池中的阻塞状态（Blocked in object’s lock pool）：当线程处于运行状态时，试图获得某个对象的同步锁时，如果该对象的同步锁已经被其他线程占用，Java虚拟机就会把这个线程放到这个对象的锁池中，这涉及到“线程同步”的内容。【线程在获取synchronized同步锁失败(因为锁被其它线程所占用)】

3）其他阻塞状态（Otherwise Blocked）：当前线程执行了sleep()方法，或者调用了其他线程的join()方法，或者发出了I/O请求时，就会进入这个状态。线程会进入到阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入就绪状态。

死亡状态（Dead）：线程执行完了或者因异常退出了run()方法，该线程结束生命周期。




![线程生命周期](https://img-blog.csdnimg.cn/20210512173109590.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzE1OTQz,size_16,color_FFFFFF,t_70)
